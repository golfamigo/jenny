# Jenny Claim Expansion Discussion Page Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 新增一頁可公開閱讀的 `claim-expansion.html`，供原告與律師討論訴之擴張時盤點所有可能求償項目、保本主軸、策略擴張項、現有證據與缺失候補。

**Architecture:** 以現有 `docs/index.html` 與 `docs/timeline.html` 的靜態 HTML 風格為基底，新建獨立頁面 `docs/claim-expansion.html`。頁面主體分為策略定位、求償項目總表、證據缺失候補清單與律師決策點四段；首頁與時間軸頁只新增入口，不改動既有證據主結構。

**Tech Stack:** 靜態 HTML、內嵌 CSS、GitHub Pages、PowerShell 驗證

---

### Task 1: 建立 `claim-expansion.html` 頁面骨架與導覽

**Files:**
- Create: `C:\Users\88698\Downloads\jenny案\docs\claim-expansion.html`
- Reference: `C:\Users\88698\Downloads\jenny案\docs\index.html`
- Reference: `C:\Users\88698\Downloads\jenny案\docs\timeline.html`

- [ ] **Step 1: 以現有頁面樣式為基底建立新頁外殼**

```html
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Jenny案 訴之擴張討論版</title>
  <style>
    :root {
      --bg: #f5efe8;
      --paper: #fffaf3;
      --ink: #201814;
      --muted: #6e6259;
      --line: #dccdbe;
      --accent: #9a3412;
      --accent-2: #7c2d12;
      --soft: #f2e5d6;
      --chip: #efe1d0;
      --good: #31572c;
      --warn: #92400e;
      --info: #1d4ed8;
      --shadow: 0 14px 34px rgba(75, 52, 37, 0.08);
    }
  </style>
</head>
```

- [ ] **Step 2: 新增側欄導覽與頁首定位**

```html
<aside class="sidebar panel">
  <div class="sidebar-head">
    <span class="eyebrow">Claim Expansion</span>
    <h2>訴之擴張討論版</h2>
    <div class="side-note">
      這一頁是供律師討論的策略工作版，目的是盤點保本主軸、策略擴張項與目前證據缺口。
    </div>
  </div>
  <nav class="nav">
    <div class="nav-group">
      <div class="nav-title">總覽</div>
      <a href="#overview">頁面說明</a>
      <a href="#positioning">策略定位</a>
    </div>
    <div class="nav-group">
      <div class="nav-title">主體</div>
      <a href="#matrix">求償項目總表</a>
      <a href="#gaps">證據缺失候補</a>
      <a href="#decision-points">律師決策點</a>
    </div>
    <div class="nav-group">
      <div class="nav-title">回其他頁面</div>
      <a href="./timeline.html" target="_blank" rel="noopener noreferrer">回時間軸頁</a>
      <a href="./index.html" target="_blank" rel="noopener noreferrer">回證據閱讀版</a>
    </div>
  </nav>
</aside>
```

- [ ] **Step 3: 建立頁首摘要區塊**

```html
<section class="hero panel" id="overview">
  <span class="eyebrow">Jenny Case / Claim Expansion</span>
  <h1>訴之擴張討論版</h1>
  <p>
    本頁不是正式書狀，而是供原告與律師盤點所有可能求償項目、法律基礎、現有證據與缺失候補的工作頁。
    重點是先確保修繕金、鑑定費、木地板與附帶裝修損害足額回復，再評估其他擴張項目。
  </p>
</section>
```

- [ ] **Step 4: 檢查頁面標題與主要錨點是否存在**

Run: `Select-String -Path 'docs\claim-expansion.html' -Pattern '訴之擴張討論版|id=\"positioning\"|id=\"matrix\"|id=\"gaps\"|id=\"decision-points\"'`
Expected: 五個關鍵字都能找到

- [ ] **Step 5: Commit**

```bash
git add "C:\Users\88698\Downloads\jenny案\docs\claim-expansion.html"
git commit -m "feat: scaffold claim expansion discussion page"
```

### Task 2: 寫入策略定位與分類原則

**Files:**
- Modify: `C:\Users\88698\Downloads\jenny案\docs\claim-expansion.html`

- [ ] **Step 1: 在頁面加入策略定位卡**

```html
<section class="card panel" id="positioning">
  <div class="card-head">
    <div class="card-title">
      <small>Strategy Positioning</small>
      <h2>策略定位</h2>
    </div>
    <div class="chip-row">
      <span class="chip good">保本主軸</span>
      <span class="chip warn">策略擴張項</span>
      <span class="chip info">全列給律師判斷</span>
    </div>
  </div>
  <div class="two-col">
    <div class="note-box">
      <h3>保本主軸</h3>
      <p>保本主軸的目標是使原告回復原有應得之居住品質，不因漏水、發霉、木地板受損或必要修復而自行負擔成本。</p>
    </div>
    <div class="note-box">
      <h3>策略擴張項</h3>
      <p>其餘項目不先刪除，全部列入討論範圍，由律師依證據成熟度、鑑定結果與程序策略判斷是否納入訴之擴張。</p>
    </div>
  </div>
</section>
```

- [ ] **Step 2: 明文列出保本主軸分類**

```html
<ul class="flat-list">
  <li>漏水本體修復費。</li>
  <li>鑑定費與必要檢測費。</li>
  <li>木地板損害。</li>
  <li>附帶裝修復原。</li>
  <li>恢復原有居住品質所必要的直接支出。</li>
</ul>
```

- [ ] **Step 3: 明文列出策略擴張項分類**

```html
<ul class="flat-list">
  <li>修復期間遷居費、住宿費、搬運費、倉儲費。</li>
  <li>除霉、除蟲、清潔與其他暫時處置支出。</li>
  <li>居住空間縮減或部分失能損害。</li>
  <li>健康損害與精神慰撫金。</li>
</ul>
```

- [ ] **Step 4: 檢查木地板與附帶裝修是否明確放在保本主軸**

Run: `Select-String -Path 'docs\claim-expansion.html' -Pattern '木地板損害|附帶裝修復原|保本主軸'`
Expected: 三個關鍵字都存在，且出現在同一區段附近

- [ ] **Step 5: Commit**

```bash
git add "C:\Users\88698\Downloads\jenny案\docs\claim-expansion.html"
git commit -m "feat: add claim expansion strategy positioning"
```

### Task 3: 建立求償項目總表

**Files:**
- Modify: `C:\Users\88698\Downloads\jenny案\docs\claim-expansion.html`
- Reference: `C:\Users\88698\Downloads\jenny案\docs\timeline.html`
- Reference: `C:\Users\88698\Downloads\jenny案\docs\pleading-summary.html`

- [ ] **Step 1: 建立總表欄位標頭**

```html
<section class="card panel" id="matrix">
  <div class="card-head">
    <div class="card-title">
      <small>Matrix</small>
      <h2>求償項目總表</h2>
    </div>
  </div>
  <div class="table-wrap">
    <table class="claim-table">
      <thead>
        <tr>
          <th>分類</th>
          <th>項目</th>
          <th>法律基礎</th>
          <th>可主張理由</th>
          <th>目前已有證據</th>
          <th>缺失候補</th>
          <th>可量化方式</th>
          <th>與律師討論重點</th>
        </tr>
      </thead>
      <tbody>
      </tbody>
    </table>
  </div>
</section>
```

- [ ] **Step 2: 先寫入保本主軸列**

```html
<tr>
  <td><span class="tag good">保本主軸</span></td>
  <td>漏水本體修復費</td>
  <td>民法第493條、第495條、第213條</td>
  <td>屬修復滲漏水及回復原狀之必要費用，應優先足額回復。</td>
  <td>現有起訴附件修繕方法與既有修繕費 368,898 元、原證11、鑑定事項第3、4點。</td>
  <td>最新估價單、若工法與範圍變動則需更新總價。</td>
  <td>既有估價 + 新估價 + 鑑定確認範圍。</td>
  <td>是否以最新估價取代舊估價，或保留舊估價作最低基準。</td>
</tr>
<tr>
  <td><span class="tag good">保本主軸</span></td>
  <td>木地板損害</td>
  <td>民法第495條、第216條、第227條</td>
  <td>木地板膨脹、發黑、發霉若與漏水路徑有因果關係，屬直接財產損害，不應由原告自負。</td>
  <td>木地板拆除後發黑發霉之對話、照片、後手願處理木地板之對話脈絡。</td>
  <td>重鋪估價、拆除費、材料單據、與漏水因果的鑑定承接。</td>
  <td>拆除費 + 材料費 + 重鋪工資；未定則標待估。</td>
  <td>是否將木地板列為保本主軸明示項目，而非僅列在損害事實中。</td>
</tr>
```

- [ ] **Step 3: 補入策略擴張項列**

```html
<tr>
  <td><span class="tag warn">策略擴張項</span></td>
  <td>修復期間遷居 / 住宿 / 搬運 / 倉儲</td>
  <td>民法第213條、第216條、第227條</td>
  <td>若鑑定認為修復期間不能正常居住，另覓住處與搬運倉儲屬必要衍生支出。</td>
  <td>現有鑑定事項已問到修復期間是否可正常居住。</td>
  <td>住宿、短租、搬運、倉儲單據；修復期間長度；不可居住之鑑定意見。</td>
  <td>依實際支出單據計算；未發生者標待單據 / 待鑑定。</td>
  <td>是否先把原因事實與項目列入，待鑑定後再補金額。</td>
</tr>
<tr>
  <td><span class="tag warn">策略擴張項</span></td>
  <td>精神慰撫金</td>
  <td>民法第195條、第227-1條</td>
  <td>若能證明人格法益、健康或生活安寧受實質侵害，可作非財產上損害補充請求。</td>
  <td>現有對話僅能反映長期困擾、房間不能使用、霉菌與生活品質受影響。</td>
  <td>醫療紀錄、診斷證明、長期失眠或過敏就醫資料。</td>
  <td>難以精準量化，金額通常由法院酌定。</td>
  <td>是否保留作策略項，或暫以事實鋪陳先不寫死金額。</td>
</tr>
```

- [ ] **Step 4: 檢查總表至少包含保本主軸與策略擴張項**

Run: `Select-String -Path 'docs\claim-expansion.html' -Pattern '保本主軸|策略擴張項|木地板損害|精神慰撫金|修復期間遷居'`
Expected: 五個關鍵字都能找到

- [ ] **Step 5: Commit**

```bash
git add "C:\Users\88698\Downloads\jenny案\docs\claim-expansion.html"
git commit -m "feat: add claim expansion matrix"
```

### Task 4: 補入證據缺失候補與律師決策點

**Files:**
- Modify: `C:\Users\88698\Downloads\jenny案\docs\claim-expansion.html`

- [ ] **Step 1: 建立證據缺失候補區**

```html
<section class="card panel" id="gaps">
  <div class="card-head">
    <div class="card-title">
      <small>Evidence Gaps</small>
      <h2>證據缺失候補清單</h2>
    </div>
  </div>
  <div class="grid two-col">
    <div class="note-box">
      <h3>單據類</h3>
      <ul class="flat-list">
        <li>最新修繕估價單。</li>
        <li>木地板拆除 / 重鋪 / 材料 / 工資單據。</li>
        <li>除霉、除蟲、清潔、暫時處置單據。</li>
        <li>住宿、搬運、倉儲單據。</li>
      </ul>
    </div>
    <div class="note-box">
      <h3>因果與鑑定承接</h3>
      <ul class="flat-list">
        <li>木地板與漏水路徑之因果關係。</li>
        <li>修復期間是否不可居住。</li>
        <li>健康受損與霉菌暴露之醫療連結。</li>
      </ul>
    </div>
  </div>
</section>
```

- [ ] **Step 2: 建立與律師討論的決策點**

```html
<section class="card panel" id="decision-points">
  <div class="card-head">
    <div class="card-title">
      <small>Decision Points</small>
      <h2>與律師討論時應直接確認的決策點</h2>
    </div>
  </div>
  <ul class="flat-list">
    <li>是否以最新修繕估價與木地板復原費作為本次擴張主金額。</li>
    <li>是否把木地板與附帶裝修損害明確列為保本主軸。</li>
    <li>遷居與住宿費是否先列項目、待鑑定後補金額。</li>
    <li>精神慰撫金與健康損害是本次主張，還是保留到下一次補充。</li>
    <li>是否需補強不可居住期間與居住空間縮減的量化基礎。</li>
  </ul>
</section>
```

- [ ] **Step 3: 檢查缺失候補與決策點段落存在**

Run: `Select-String -Path 'docs\claim-expansion.html' -Pattern '證據缺失候補清單|與律師討論時應直接確認的決策點|最新修繕估價單|精神慰撫金'`
Expected: 四個關鍵字都能找到

- [ ] **Step 4: Commit**

```bash
git add "C:\Users\88698\Downloads\jenny案\docs\claim-expansion.html"
git commit -m "feat: add claim expansion evidence gaps and lawyer decisions"
```

### Task 5: 補首頁與時間軸頁入口

**Files:**
- Modify: `C:\Users\88698\Downloads\jenny案\docs\index.html`
- Modify: `C:\Users\88698\Downloads\jenny案\docs\timeline.html`

- [ ] **Step 1: 在首頁 action row 加入入口**

```html
<a class="action-link" href="./claim-expansion.html" target="_blank" rel="noopener noreferrer">
  訴之擴張討論版
</a>
```

- [ ] **Step 2: 在時間軸頁來源或損害相關區加入入口**

```html
<a class="action-link" href="./claim-expansion.html" target="_blank" rel="noopener noreferrer">
  開啟訴之擴張討論版
</a>
```

- [ ] **Step 3: 視側欄結構補上導覽連結**

```html
<a href="./claim-expansion.html" target="_blank" rel="noopener noreferrer">訴之擴張討論版</a>
```

- [ ] **Step 4: 檢查兩頁都已有新入口**

Run: `Select-String -Path 'docs\index.html','docs\timeline.html' -Pattern 'claim-expansion.html|訴之擴張討論版'`
Expected: `index.html`、`timeline.html` 都至少各出現一次

- [ ] **Step 5: Commit**

```bash
git add "C:\Users\88698\Downloads\jenny案\docs\index.html" "C:\Users\88698\Downloads\jenny案\docs\timeline.html"
git commit -m "feat: link claim expansion discussion page"
```

### Task 6: 手動驗證與發布

**Files:**
- Verify: `C:\Users\88698\Downloads\jenny案\docs\claim-expansion.html`
- Verify: `C:\Users\88698\Downloads\jenny案\docs\index.html`
- Verify: `C:\Users\88698\Downloads\jenny案\docs\timeline.html`

- [ ] **Step 1: 檢查頁面中不應出現的詞**

Run: `Select-String -Path 'docs\claim-expansion.html' -Pattern '分成|提高律師積極度|談判'`
Expected: 無輸出

- [ ] **Step 2: 檢查公開頁面保留必要策略但無內部措辭**

Run: `Select-String -Path 'docs\claim-expansion.html' -Pattern '保本主軸|策略擴張項|缺失候補|與律師討論重點'`
Expected: 四個關鍵字都存在

- [ ] **Step 3: 用本機瀏覽或當前預覽頁檢查版面**

Run: `Get-Item 'C:\Users\88698\Downloads\jenny案\docs\claim-expansion.html' | Select-Object FullName,Length`
Expected: 顯示新頁檔案存在且大小非 0；再以 in-app browser 開啟頁面確認表格可讀、導覽可跳轉、入口可點擊

- [ ] **Step 4: 推送前確認只修改預期檔案**

Run: `git status --short`
Expected: 新增或修改應只包含 `docs\claim-expansion.html`、`docs\index.html`、`docs\timeline.html`；若同時看到既有的 `[LINE]請勿直接電話聯繫🍣♨️Jenny.txt` 與兩份 PDF，應保持原狀且不得納入 commit

- [ ] **Step 5: Commit**

```bash
git add "C:\Users\88698\Downloads\jenny案\docs\claim-expansion.html" "C:\Users\88698\Downloads\jenny案\docs\index.html" "C:\Users\88698\Downloads\jenny案\docs\timeline.html"
git commit -m "feat: publish claim expansion discussion page"
```
