# 實作計畫：新增 Firefox 版本資訊頁（.shtml）

### 來源

- 官方 {xxx.x} Release Notes（英文）[link](https://www.firefox.com/en-US/firefox/{xxx.x}/releasenotes/)

### 要做的事

- 在 `firefox/releases/{xxx.x}/` 新增 `index.shtml`，不用建立 `index.html`。
- 依過去版本 `./index.shtml` 的結構與標籤樣式撰寫，包含：`fx_head-sandstone.shtml`/`fx_tail-sandstone.shtml` 引入、`<article id="whatsnew">`、兩個 `<ul class="tags">` 區段、結尾完整變更清單與前一版本連結區塊、社群貢獻者清單。
- 社群貢獻者清單中的 bug 編號需加上可點擊的 Bugzilla 連結（`https://bugzilla.mozilla.org/<bug>`）。
- 若官方段落包含示意圖：請下載圖片至 `firefox/releases/{xxx.x}/`，沿用清楚且可辨識的檔名（例如：`{xxx}_<slug>.png`），並在對應的 `<li>` 描述文字之後加入：`<p><img src="/firefox/releases/{xxx.x}/{filename}" alt="{圖說（繁中）}"></p>`。
 - 若官方標示為逐步釋出（progressive roll out），請在該 `<li>` 下加入一段 `p.progressive-roll` 說明，並移除原文括號註記。
- 置頂變數：
  - `release_date` 設為新版釋出日期
  - `version` 設為新版版本號
  - `previous_version` 設為前一版版本號
- 內容以繁體中文整理以下段落與重點，沿用 `tag-new/tag-fixed/tag-changed/tag-enterprise/tag-developer/tag-html5` 等樣式：
  - 全新功能：
  - 修正：
  - 企業版：
    - 連結至 Firefox for Enterprise xxx 版本資訊：`https://support.mozilla.org/kb/firefox-enterprise-{xxx}-release-notes`
  - 開發者：
    - 連結 MDN Releases {xxx}：`https://developer.mozilla.org/docs/Mozilla/Firefox/Releases/{xxx}`。
  - 網路平台：
  - 社群貢獻者：
    - 依來源頁所列完整名單與 Bug 編號呈現，並將編號連到 Bugzilla。
- 結尾區塊「完整變更清單」：
  - Bugzilla 查詢更新為 {xxx}：`v3=Firefox {xxx}` / `v1=mozilla{xxx}`，並維持 `cf_status_firefox{xxx}` 與 `fixed,verified` 條件。
  - 「前一個版本」連到 `/firefox/releases/{previous_version}/`。

### 重要片段（示意）

- 置頂變數與引入：
```2:8:firefox/releases/{xxx.x}/index.shtml
<!--#set var="release_date" value="{release_date}" -->
<!--#set var="version" value="{xxx.x}" -->
<!--#set var="previous_version" value="{previous_version}" -->

<!--#include virtual="/firefox/inc/fx_head-sandstone.shtml" -->
```

- 結尾查詢與上一版：
```1:6:firefox/releases/{xxx.x}/index.shtml
<ul class="tags">
  <li class="complete">
    請參考此版本的<a target="_blank" href="https://bugzilla.mozilla.org/buglist.cgi?j_top=OR&f1=target_milestone&o3=equals&v3=Firefox%20{xxx}&o1=equals&resolution=FIXED&o2=anyexact&query_format=advanced&f3=target_milestone&f2=cf_status_firefox{xxx}&bug_status=RESOLVED&bug_status=VERIFIED&bug_status=CLOSED&v1=mozilla{xxx}&v2=fixed%2Cverified&limit=0">完整變更清單</a>。
    你可能也想瞭解<a target="_blank" href='/firefox/releases/<!--#echo var="previous_version" -->/'>前一個版本的更新</a>。
  </li>
</ul>
```

### To-dos

- [ ] 建立 `firefox/releases/{xxx.x}/index.shtml` 檔案（無 index.html）
- [ ] 設定 release_date={release_date}, version={xxx.x}, previous_version={previous_version}
- [ ] 撰寫全新功能/修正/企業版/開發者/網路平台段落（繁中）
- [ ] 加入社群貢獻者名單（依來源頁）
- [ ] 社群貢獻者 bug 編號加上 Bugzilla 連結
- [ ] 若段落含示意圖：下載圖片到該版本目錄並插入 `<img>` 標記
- [ ] 加入 Bugzilla 完整變更清單與前一版連結，收尾 include
