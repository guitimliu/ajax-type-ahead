# JavaScript 30 Day 6 Ajax Type Ahead

## 數據整合

* 使用基於 Ajax 的 Axios 串接 API。
* 使用 async 與 await 處理非同步。
* 使用 try 與 catch 處理錯誤狀況，並且在出現錯誤時呈現維護訊息。

## 搜尋功能 & 顯示結果

* 能夠在進行輸入文字時即時透過關鍵字過濾資料。
* 在尚未載入資料前，會顯示資料載入中。
* 資料載入成功後但如果仍偵測資料陣列為 0，則顯示沒有符合條件的資料。

## 使用者介面

* 利用 CodePen 範例的樣式，進行調整與增加 RWD 置適應。
* 在呈現 `/* 以下為我自行撰寫之樣式 */` 與 `/* 自行撰寫之樣式 Start */ /* 自行撰寫之樣式 end */` 間的樣式為我撰寫的樣式。（已經寫到一半才想到可以先將語法引入至此後先 commit 做到區別，但已經做到一半想說就算了）

## 程式碼組織

* HTML 與 Vue 邏輯撰寫在 App.vue，樣式撰寫在 style.css。
* 原本有想過進行元件化，但因為僅單頁且架構少，評估過後認為是不需要元件化，僅將正則表達式的部分 Function 化。

## 額外挑戰

* 有使用 localStorage 快取關鍵字與搜尋結果，另外如果要清除快取，可在搜尋欄上輸入 call 後點擊 Enter，即可刪除快取、清除關鍵字與呼叫 API，方便清除快取使用。
* 搜尋欄使用 v-model.debounce 來做到防抖動效果。
* 當 API 錯誤而導致無資料時，能夠透過 try catch 跳轉到維護中訊息。
* 有實作當關鍵字清空時，就會顯示所有結果。
* 使用 Vite 使 Mac 與 Windows 都能方便進行開發，並且方便部署至 GitHub Pages。
* 關於 API 是從另一 repo 取得這一點，因為不太確定做法，所以只有將 json 檔案下載到跟本專案目錄。

## 其它說明

其實應該在過程中就不斷討論相關問題，如是否應該元件化（或許您本來就想看我如何規劃元件）、從另一 repo 取得 API 的方式（是否只是將 json 下載回來或是需要能持續同步更新），但由於前幾天有事情，所以延遲現在才進行完成開發，就先將功能以個人認知來做完成，感到很不好意思～

因爲專案一次撰寫完成，所以開發部分就只有一筆 commit，在此說明一下～

## 遺珠之憾

另外在串接 API 與整理資料那一塊，原本有想說取得資料後就先將所有資料做整理成 name 那樣的形式，filter 的時候就不用還要繼續整理，但是後來發現可能跟 v-html 渲染的關係有關，實作出上述那樣的方式後輸入搜尋欄時會有一些卡，所以就以目前相對不卡的方式來呈現。

## 有使用到的參考資料與資源

* https://codepen.io/tariso/pen/LyoaRM
* https://gist.githubusercontent.com/Miserlou/c5cd8364bf9b2420bb29/raw/2bf258763cdddd704f8ffd3ea9a3e81d25e2c6f6/cities.json
* https://davefollett.io/2018/11/02/a-new-vue-on-javascript30-06-type-ahead/
* https://a498390344.medium.com/localstorage%E5%AF%A6%E4%BD%9C%E4%B9%8Bto-do-list-8e8a996121c3
* Chat GPT

---

## Vue 3 + Vite

This template should help get you started developing with Vue 3 in Vite. The template uses Vue 3 `<script setup>` SFCs, check out the [script setup docs](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to learn more.

## Recommended IDE Setup

- [VS Code](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).
