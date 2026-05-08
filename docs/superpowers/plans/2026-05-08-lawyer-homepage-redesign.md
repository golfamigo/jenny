# Lawyer-Oriented Homepage Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 將 `docs/index.html` 從證據閱讀首頁改造成律師導向案件總控台，同時保留原本證據閱讀功能為第二層頁面。

**Architecture:** 先把現有證據閱讀頁完整抽離到新的 `docs/evidence-reader.html`，確保證據內容不遺失；再重寫 `docs/index.html` 的首頁資訊架構為 `程序 / 文書現況 → 核心爭點 → 待辦 → 第二層入口`。最後統一所有子頁的返回與入口連結，避免首頁與證據頁角色混亂。

**Tech Stack:** 靜態 HTML、內嵌 CSS、GitHub Pages、本機瀏覽器驗證

---

### Task 1: 抽離證據閱讀頁為獨立第二層頁面

**Files:**
- Create: `docs/evidence-reader.html`
- Modify: `docs/index.html`
- Test: 本機瀏覽器開啟 `docs/evidence-reader.html`

- [ ] **Step 1: 以現有首頁為底建立新的證據閱讀頁**

從目前的 `docs/index.html` 複製出 `docs/evidence-reader.html`，保留原本證據卡、圖片、影片與來源連結結構。

新頁的基本頭部要改成：

```html
<title>Jenny案 證據閱讀版</title>
...
<span class="eyebrow">Jenny Case / Reader View</span>
<h1>證據閱讀版</h1>
<p>
  這一頁專門用來直接看圖、看影片與逐項讀證據卡。
  首頁已改為案件總控台；若要先看程序與待辦，請回首頁。
</p>
<div class="action-row">
  <a class="action-link" href="./index.html">回案件首頁</a>
  <a class="action-link" href="./timeline.html">看時間軸 + 爭點清單</a>
  <a class="action-link" href="./claim-expansion.html">看訴之擴張討論頁</a>
</div>
```

- [ ] **Step 2: 確認證據閱讀頁的側欄與來源連結仍可用**

保留原證據頁的側欄導航，但將頂部說明調整為第二層頁面定位：

```html
<div class="sidebar-head">
  <span class="eyebrow">Evidence Reader</span>
  <h2>Jenny案</h2>
  <div class="side-note">
    這一頁只負責讀證據，不再承擔案件首頁功能。<br />
    若要先看程序現況與待辦，請回案件首頁。
  </div>
</div>
```

- [ ] **Step 3: 本機開啟新頁確認證據內容完整**

Run:

```powershell
Start-Process "file:///C:/Users/88698/Downloads/jenny案/docs/evidence-reader.html"
```

Expected:
- 可看到原本證據閱讀頁的所有證據卡
- 影片與圖片連結不壞
- 頁首已改成「回案件首頁」

- [ ] **Step 4: Commit**

```bash
git add docs/evidence-reader.html
git commit -m "Create standalone evidence reader page"
```

### Task 2: 將 index.html 重寫為律師導向案件總控台

**Files:**
- Modify: `docs/index.html`
- Test: 本機瀏覽器開啟 `docs/index.html`

- [ ] **Step 1: 重寫首頁 hero 為案件總覽而非證據閱讀器**

將目前首頁 hero 改成程序優先版本，核心內容如下：

```html
<span class="eyebrow">Lawyer Dashboard</span>
<h1>Jenny 案件總控台</h1>
<p>
  本頁作為律師與原告共同使用的案件首頁。先看程序 / 文書現況、
  核心爭點與目前待辦，再依需要進入時間軸、證據、對話、
  書狀與訴之擴張頁面。
</p>
<div class="hero-grid">
  <div class="metric"><span class="label">案號</span><span class="value">114年度建字第109號</span></div>
  <div class="metric"><span class="label">程序階段</span><span class="value">建字審理中</span></div>
  <div class="metric"><span class="label">主路徑</span><span class="value">修復 + 鑑定 + 擴張</span></div>
  <div class="metric"><span class="label">首頁定位</span><span class="value">律師工作首頁</span></div>
</div>
```

- [ ] **Step 2: 以程序 / 文書現況取代首頁第一個主要內容區**

在首頁主內容第一區塊放入裁定、聲請調查證據狀與程序焦點：

```html
<section class="card panel" id="status">
  <div class="card-head">
    <div class="card-title">
      <small>第一優先區塊</small>
      <h2>程序 / 文書現況</h2>
    </div>
  </div>
  <div class="entry-grid">
    <div class="note-box">
      <h3>114年度補字第632號民事裁定</h3>
      <ul>
        <li>訴訟標的價額 523,898 元。</li>
        <li>補繳第一審裁判費 5,730 元。</li>
      </ul>
    </div>
    <div class="note-box">
      <h3>民事準備(一)暨聲請調查證據狀</h3>
      <ul>
        <li>已主張前手施工範圍與後手重作 / 保固責任。</li>
        <li>已聲請鑑定位置、原因、修復費用、修復期間與可居住性。</li>
      </ul>
    </div>
    <div class="note-box">
      <h3>目前程序焦點</h3>
      <ul>
        <li>共同被告結構。</li>
        <li>補充鑑定題目。</li>
        <li>訴之擴張項目與金額路徑。</li>
      </ul>
    </div>
  </div>
</section>
```

- [ ] **Step 3: 新增核心爭點與雙 Todo 區塊**

首頁中段加入「核心爭點摘要」與兩欄待辦：

```html
<section class="card panel" id="issues">
  <h2>核心爭點摘要</h2>
  <ul class="flat-list">
    <li>前手本體施工責任。</li>
    <li>後手重作、防水、保固責任。</li>
    <li>漏水因果需落到窗框、門檻、地坪與異材質交界。</li>
    <li>入住與付款不等於驗收完成。</li>
  </ul>
</section>

<section class="card panel" id="todo">
  <div class="two-col">
    <article class="note-box">
      <h3>待律師討論 / 決策</h3>
      <ul>
        <li>是否改列共同被告。</li>
        <li>訴之擴張主軸是否先鎖定修繕、鑑定、木地板、附帶裝修。</li>
        <li>遷居 / 住宿 / 搬運 / 倉儲先列事實還是先列金額。</li>
      </ul>
    </article>
    <article class="note-box">
      <h3>待原告補件 / 提供證據</h3>
      <ul>
        <li>最新修繕估價單。</li>
        <li>木地板拆除 / 重鋪 / 材料 / 工資單據。</li>
        <li>法院鑑定費與必要檢測費收據。</li>
      </ul>
    </article>
  </div>
</section>
```

- [ ] **Step 4: 移除首頁中的證據縮圖與大量證據卡，改成入口卡**

原本首頁中的證據卡區塊不再直接展開。首頁底部改為五張文字入口卡：

```html
<section class="card panel" id="entry-points">
  <div class="card-head">
    <div class="card-title">
      <small>第三優先區塊</small>
      <h2>重要入口卡</h2>
    </div>
  </div>
  <div class="summary-grid">
    <article class="summary-card"><h3>時間軸 + 爭點</h3><p>先看案情脈絡與責任線。</p></article>
    <article class="summary-card"><h3>證據閱讀版</h3><p>需要看圖再進，不在首頁展開。</p></article>
    <article class="summary-card"><h3>對話整理</h3><p>補強未驗收、催款、保固脈絡。</p></article>
    <article class="summary-card"><h3>書狀重點</h3><p>先看已寫進程序文件的主張。</p></article>
    <article class="summary-card"><h3>訴之擴張</h3><p>看求償項目、法條與待補件。</p></article>
  </div>
</section>
```

- [ ] **Step 5: 本機開啟首頁確認閱讀順序**

Run:

```powershell
Start-Process "file:///C:/Users/88698/Downloads/jenny案/docs/index.html"
```

Expected:
- 第一屏先看到程序 / 文書現況，不是證據卡
- 首頁沒有大面積證據縮圖
- 證據閱讀版只以入口卡存在

- [ ] **Step 6: Commit**

```bash
git add docs/index.html
git commit -m "Redesign homepage as lawyer dashboard"
```

### Task 3: 更新所有第二層頁面的返回與入口連結

**Files:**
- Modify: `docs/timeline.html`
- Modify: `docs/conversation.html`
- Modify: `docs/pleading-summary.html`
- Modify: `docs/claim-expansion.html`
- Test: 四個頁面的 action links 與側欄連結

- [ ] **Step 1: 把原本指向 index 的「證據閱讀版」連結改成 evidence-reader**

在子頁中，凡是原本代表「回證據閱讀版」的按鈕或文字連結，改成：

```html
<a class="action-link" href="./evidence-reader.html" target="_blank" rel="noopener noreferrer">證據閱讀版</a>
<a class="action-link" href="./index.html" target="_blank" rel="noopener noreferrer">案件首頁</a>
```

至少要補在各頁 hero 區，讓使用者可以清楚分辨：

- `index.html` = 案件首頁
- `evidence-reader.html` = 證據閱讀版

- [ ] **Step 2: 在四個第二層頁面加入一致的首頁返回入口**

每個頁面都要在首頁區加入兩個入口：

```html
<div class="action-row">
  <a class="action-link" href="./index.html" target="_blank" rel="noopener noreferrer">回案件首頁</a>
  <a class="action-link" href="./evidence-reader.html" target="_blank" rel="noopener noreferrer">證據閱讀版</a>
</div>
```

- [ ] **Step 3: 以文字搜尋驗證各頁連結沒有混淆**

Run:

```powershell
Select-String -Path `
  'C:\Users\88698\Downloads\jenny案\docs\timeline.html',`
  'C:\Users\88698\Downloads\jenny案\docs\conversation.html',`
  'C:\Users\88698\Downloads\jenny案\docs\pleading-summary.html',`
  'C:\Users\88698\Downloads\jenny案\docs\claim-expansion.html' `
  -Pattern 'evidence-reader.html|回案件首頁'
```

Expected:
- 四個頁面都至少有 `evidence-reader.html`
- 四個頁面都至少有 `回案件首頁`

- [ ] **Step 4: Commit**

```bash
git add docs/timeline.html docs/conversation.html docs/pleading-summary.html docs/claim-expansion.html
git commit -m "Clarify homepage and evidence page navigation"
```

### Task 4: 整體驗證與發布前檢查

**Files:**
- Modify: none
- Test: `docs/index.html`, `docs/evidence-reader.html`, 第二層頁面入口

- [ ] **Step 1: 本機逐頁驗證首頁與第二層頁面角色**

Run:

```powershell
Start-Process "file:///C:/Users/88698/Downloads/jenny案/docs/index.html"
Start-Process "file:///C:/Users/88698/Downloads/jenny案/docs/evidence-reader.html"
```

Expected:
- `index.html` 像案件總控台，不像證據牆
- `evidence-reader.html` 保留原本讀圖功能

- [ ] **Step 2: 驗證第二層頁面能回首頁也能回證據閱讀版**

人工檢查：
- `timeline.html`
- `conversation.html`
- `pleading-summary.html`
- `claim-expansion.html`

Expected:
- 四頁都有 `回案件首頁`
- 四頁都有 `證據閱讀版`
- 不再出現把首頁誤當證據頁的情況

- [ ] **Step 3: 檢查工作樹只包含預期變更**

Run:

```bash
git status --short
```

Expected:
- 只出現首頁改版與連結調整相關檔案
- 不包含使用者原有的 `[LINE]...txt` 或未追蹤 PDF

- [ ] **Step 4: Final Commit**

```bash
git add docs/index.html docs/evidence-reader.html docs/timeline.html docs/conversation.html docs/pleading-summary.html docs/claim-expansion.html
git commit -m "Promote lawyer dashboard homepage and demote evidence reader"
```
