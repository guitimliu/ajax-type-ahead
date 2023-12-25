<script setup>
// 引入外部套件
import axios from 'axios';
import { onMounted, ref, watch } from 'vue';

// 變數
const noDataText = ref('資料載入中，請稍後...');
const haveCache = ref(false);
const data = ref([]);
const filterData = ref([]);
const keyword = ref('');
const error = ref(false);

// 生命週期
onMounted(() => {
  if (localStorage.getItem('keyword') === null || localStorage.getItem('searchResult') === null) {
    getInitData();
  } else {
    haveCache.value = true;
    keyword.value = localStorage.getItem('keyword');
    filterData.value = JSON.parse(localStorage.getItem('searchResult'));
    noDataText.value = '目前沒有符合條件的資料';
  }
})

// 取得 API 資料
async function getInitData() {
  try {
    const apiUrl = '/ajax-type-ahead/cities.json';
    const getData = await axios.get(apiUrl);
    data.value = getData.data;
    noDataText.value = '目前沒有符合條件的資料';
    getFilterData();
  } catch {
    error.value = true;
  }
}

// 判斷關鍵字變更
watch(keyword, () => {
  haveCache.value ? haveCache.value = false : getInitData();
})

// 篩選資料
function getFilterData() {
  if (keyword.value.length > 0) {
    filterData.value = [];
    data.value.forEach((item) => {
      if (comparisonFilter(item.city) || comparisonFilter(item.state)) {
        filterData.value.push({
          city: item.city,
          state: item.state,
          population: item.population,
          name: `${showKeyword(item.city)}, ${showKeyword(item.state)}`
        });
      }
    })
  } else {
    filterData.value = data.value;
  }
  localStorage.setItem('keyword', keyword.value);
  localStorage.setItem('searchResult', JSON.stringify(filterData.value))
}

// 判斷關鍵字是否符合資料的正則表達式
function comparisonFilter(value) {
  return new RegExp(keyword.value, 'gi').test(value);
}

// 將符合關鍵字的文字醒目顯示
function showKeyword(value) {
  return value.replace(
    new RegExp(keyword.value, 'gi'),
    `<span class="hl">${keyword.value}</span>`,
  );
}

// 刪除 call 紀錄，並重新呼叫 API
function callApi() {
  if (keyword.value === 'call') {
    localStorage.removeItem('keyword');
    localStorage.removeItem('searchResult');
    keyword.value = '';
    getInitData();
  }
}
</script>

<template>
  <div v-if="!error">
    <form class="search-form">
      <input
        v-model.debounce="keyword"
        @keydown.enter="callApi"
        type="text"
        class="search"
        placeholder="搜尋城市名稱"
      >
      <ul class="suggestions">
        <li v-if="filterData.length === 0">
          {{ noDataText }}
        </li>
        <li v-for="item in filterData" :key="item.city + Math.random()">
          <span v-if="keyword.length === 0" class="name">
            {{ item.city }}, {{ item.state }}
          </span>
          <span class="name" v-else v-html="item.name" />
          <span class="population">
            {{ item.population?.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',') }}
          </span>
        </li>
      </ul>
    </form>
  </div>
  <div class="maintain" v-else>
    <p>本網站維護中，請於稍後再度嘗試。</p>
  </div>
</template>
