# Jenny Timeline Balance Update Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 將 1290 行後新增的對話內容整理進案件 HTML，明確標示 `前手 / 後手 / 程序`，並以中性語氣補入「未驗收催尾款」與「後手誠信輔助評價點」。

**Architecture:** 以 `docs/timeline.html` 為主修改檔，新增事件標籤、後手履約段落、爭點卡與輔助評價區塊；`docs/index.html` 僅在版面合理時補一張輔助證據卡。所有新增內容都與漏水主因分流，避免把尾款爭議寫成漏水原因本體。

**Tech Stack:** 靜態 HTML、內嵌 CSS、GitHub Pages

---

### Task 1: 更新時間軸事件標籤與分流

**Files:**
- Modify: `C:\Users\88698\Downloads\jenny案\docs\timeline.html`

- [ ] **Step 1: 在 CSS 新增事件標籤樣式**

```html
.event-tag {
  display: inline-flex;
  align-items: center;
  min-height: 28px;
  padding: 4px 10px;
  border-radius: 999px;
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 0.04em;
}

.event-tag.front {
  background: rgba(146, 64, 14, 0.12);
  color: var(--warn);
  border: 1px solid rgba(146, 64, 14, 0.18);
}

.event-tag.back {
  background: rgba(29, 78, 216, 0.1);
  color: var(--info);
  border: 1px solid rgba(29, 78, 216, 0.16);
}

.event-tag.procedure {
  background: rgba(49, 87, 44, 0.1);
  color: var(--good);
  border: 1px solid rgba(49, 87, 44, 0.16);
}
```

- [ ] **Step 2: 在既有時間軸事件中加入 `前手 / 後手 / 程序` 標籤**

```html
<div class="event-head">
  <div>
    <span class="event-tag back">後手</span>
    <h3>2023-03-11 與睿創簽約，並出具防水保固</h3>
  </div>
  <span class="event-date">書狀載明：112年3月11日</span>
</div>
```

- [ ] **Step 3: 對既有事件做分流校正**

```html
<span class="event-tag front">前手</span>
<h3>2024-01-28 發現壁癌 / 漏水</h3>
```

```html
<span class="event-tag procedure">程序</span>
<h3>2026-05-19 預定法院系爭鑑定</h3>
```

- [ ] **Step 4: 用文字校正前手 / 後手交錯關係**

```html
<div class="sub">意義：此節點在頁面上歸為前手漏水發現脈絡，避免與後手的未驗收、催尾款爭議混寫。</div>
```

- [ ] **Step 5: 檢查 `timeline.html` 內是否都已標籤**

Run: `Select-String -Path 'docs\timeline.html' -Pattern 'event-tag front|event-tag back|event-tag procedure'`
Expected: 至少出現 `front`、`back`、`procedure` 三種類型

- [ ] **Step 6: Commit**

```bash
git add "C:\Users\88698\Downloads\jenny案\docs\timeline.html"
git commit -m "feat: label timeline events by actor"
```

### Task 2: 新增後手未驗收催尾款段落

**Files:**
- Modify: `C:\Users\88698\Downloads\jenny案\docs\timeline.html`

- [ ] **Step 1: 在時間軸中新增「後手：入住、未驗收與尾款壓力」段落**

```html
<article class="event">
  <div class="event-head">
    <div>
      <span class="event-tag back">後手</span>
      <h3>2023-08-01 因房租壓力先搬入，但非正式驗收</h3>
    </div>
    <span class="event-date">依 1290 行後新增對話整理</span>
  </div>
  <p>原告表示當時很多工程仍未完成，搬入原因是為節省房租先搬回居住，並非正式驗收完成之表示。</p>
  <div class="sub">意義：入住事實不能直接等同工程已完工、驗收合格或瑕疵不存在。</div>
</article>
```

- [ ] **Step 2: 補入「2023-10 前後仍未完工卻催尾款」事件**

```html
<article class="event">
  <div class="event-head">
    <div>
      <span class="event-tag back">後手</span>
      <h3>2023-10 前後工程未完，卻已催付尾款</h3>
    </div>
    <span class="event-date">依 1290 行後新增對話整理</span>
  </div>
  <p>新增對話指出，至 10 月前後工程仍未全部完成，但被告法代已以入住事實為由催付尾款。</p>
  <div class="sub">意義：此節點主要用來反駁「入住 = 驗收完成」的推論。</div>
</article>
```

- [ ] **Step 3: 補入「2023-12-01 付款不等於驗收」事件**

```html
<article class="event">
  <div class="event-head">
    <div>
      <span class="event-tag back">後手</span>
      <h3>2023-12-01 在未正式驗收下支付尾款</h3>
    </div>
    <span class="event-date">依新增對話自述日期</span>
  </div>
  <p>原告表示尾款支付時，工程尚未經正式驗收，且木地板等瑕疵處理仍與付款條件相互連結。</p>
  <div class="sub">意義：付款背景不足以直接推論原告已承認工程完成、品質無瑕疵或放棄後續權利。</div>
</article>
```

- [ ] **Step 4: 補入「2024-08 被告仍提及驗收程序」事件**

```html
<article class="event">
  <div class="event-head">
    <div>
      <span class="event-tag back">後手</span>
      <h3>2024-08 被告仍稱「工務還沒跟你驗收嗎」</h3>
    </div>
    <span class="event-date">依新增對話整理</span>
  </div>
  <p>原告表示其事後詢問是否存在驗收程序時，被告法代回稱「工務還沒跟你驗收嗎」。</p>
  <div class="sub">意義：反向顯示被告自己也知道工程本應另有正式驗收程序。</div>
</article>
```

- [ ] **Step 5: 用關鍵字檢查新事件是否都已落入**

Run: `Select-String -Path 'docs\timeline.html' -Pattern '2023-08-01|2023-10|2023-12-01|2024-08|工務還沒跟你驗收嗎'`
Expected: 五個關鍵字都能在 `docs\timeline.html` 中找到

- [ ] **Step 6: Commit**

```bash
git add "C:\Users\88698\Downloads\jenny案\docs\timeline.html"
git commit -m "feat: add backhand acceptance and payment timeline"
```

### Task 3: 新增爭點卡與誠信輔助評價區

**Files:**
- Modify: `C:\Users\88698\Downloads\jenny案\docs\timeline.html`

- [ ] **Step 1: 在爭點區新增「入住及付款不等於驗收完成」卡片**

```html
<article class="issue-card">
  <h3>爭點 6：入住及付款是否可推定驗收完成</h3>
  <p>新增對話顯示，原告搬入係因房租壓力，付款則發生於工程未正式驗收、瑕疵未完全排除且催款壓力仍在的脈絡下，因此不能僅因入住與付款即推定原告已承認工程完成、品質無瑕疵或放棄後續權利。</p>
  <ul class="flat-list">
    <li>有利材料：2023-08-01 搬入、2023-10 前後催款、2023-12-01 付款、2024-08 驗收對話。</li>
    <li>用途：反駁後手若主張「入住 + 尾款 = 驗收完成」。</li>
  </ul>
</article>
```

- [ ] **Step 2: 在爭點區後方新增中性輔助評價區塊**

```html
<section class="card panel" id="credibility">
  <div class="card-head">
    <div class="card-title">
      <small>Supplement</small>
      <h2>後手履約誠信爭議（輔助評價點）</h2>
    </div>
    <div class="chip-row">
      <span class="chip warn">輔助點打</span>
      <span class="chip">不直接證明漏水主因</span>
    </div>
  </div>
  <div class="two-col">
    <div class="note-box">
      <h3>頁面用途</h3>
      <p>此部分不直接證明漏水原因，但可作為評價後手履約誠信及抗辯可信度的輔助資料。</p>
    </div>
    <div class="note-box">
      <h3>整理重點</h3>
      <p>包含未驗收催尾款、將瑕疵修繕與付款連結、對處理方案前後反覆，以及事後仍自承存在驗收程序。</p>
    </div>
  </div>
</section>
```

- [ ] **Step 3: 在輔助區塊中濃縮寫入後手誠信評價句**

```html
<div class="note-box">
  <h3>中性補述</h3>
  <p>現有對話脈絡顯示，被告於工程尚未正式驗收、瑕疵尚未完全排除時，即反覆以入住事實催付尾款，並曾將木地板等瑕疵處理與付款條件連結。此情形雖不直接證明漏水原因，但可作為評價後手履約誠信及其抗辯可信度的輔助資料。</p>
</div>
```

- [ ] **Step 4: 補入民法第148條但避免寫成書狀口吻**

```html
<div class="note-box">
  <h3>法律定位</h3>
  <p>若後續需要進一步轉為書狀主張，可由律師再評估是否結合誠信原則論述，作為反駁後手將入住與付款逕自包裝為驗收完成的補充依據。</p>
</div>
```

- [ ] **Step 5: 檢查輔助區塊沒有誤寫成漏水主因**

Run: `Select-String -Path 'docs\timeline.html' -Pattern '不直接證明漏水原因|抗辯可信度|未驗收催尾款'`
Expected: 三個關鍵語句皆存在

- [ ] **Step 6: Commit**

```bash
git add "C:\Users\88698\Downloads\jenny案\docs\timeline.html"
git commit -m "feat: add credibility support section for backhand conduct"
```

### Task 4: 視版面補入未完工 / 未驗收輔助證據卡

**Files:**
- Modify: `C:\Users\88698\Downloads\jenny案\docs\index.html`
- Reference: `C:\Users\88698\Pictures\截圖\Image 1703.png`

- [ ] **Step 1: 在證據閱讀版判斷是否新增輔助證據卡**

```html
<a href="#e13">E13 未完工 / 未驗收爭議</a>
```

- [ ] **Step 2: 若加入，新增中性定位卡片**

```html
<section class="card panel" id="e13">
  <div class="card-head">
    <div class="card-title">
      <small>E13 / 後手履約脈絡補充</small>
      <h2>未完工 / 未驗收爭議</h2>
    </div>
    <div class="chip-row">
      <span class="chip warn">輔助證據</span>
      <span class="chip">不直接證明漏水主因</span>
    </div>
  </div>
  <div class="meta">
    <div class="meta-block"><span class="meta-label">證據用途</span><div class="meta-text">支撐原告搬入時仍有未完成事項、未正式驗收，以及付款不等於驗收完成。</div></div>
    <div class="meta-block"><span class="meta-label">對應爭點</span><div class="meta-text">反駁後手若主張入住及付款即代表驗收或承認無瑕疵。</div></div>
  </div>
</section>
```

- [ ] **Step 3: 若加入圖片，使用使用者提供的檔案路徑**

```html
<figure class="media"><img src="C:/Users/88698/Pictures/截圖/Image 1703.png" alt="E13-1" /><figcaption class="caption">工務手寫未完工事項輔助圖</figcaption></figure>
```

- [ ] **Step 4: 若圖片採用本機絕對路徑，改為複製到 `docs/assets/` 後再引用**

```bash
Copy-Item "C:\Users\88698\Pictures\截圖\Image 1703.png" "C:\Users\88698\Downloads\jenny案\docs\assets\Image-1703.png"
```

```html
<figure class="media"><img src="./assets/Image-1703.png" alt="E13-1" /><figcaption class="caption">工務手寫未完工事項輔助圖</figcaption></figure>
```

- [ ] **Step 5: 檢查 `index.html` 與圖片路徑**

Run: `Select-String -Path 'docs\index.html' -Pattern 'E13|Image-1703.png|未完工 / 未驗收爭議'`
Expected: 若採納此卡，三個關鍵字皆存在

- [ ] **Step 6: Commit**

```bash
git add "C:\Users\88698\Downloads\jenny案\docs\index.html" "C:\Users\88698\Downloads\jenny案\docs\assets\Image-1703.png"
git commit -m "feat: add unfinished acceptance support evidence card"
```

### Task 5: 最終檢查與發布

**Files:**
- Modify: `C:\Users\88698\Downloads\jenny案\docs\timeline.html`
- Modify: `C:\Users\88698\Downloads\jenny案\docs\index.html`
- Modify: `C:\Users\88698\Downloads\jenny案\README.md` (僅在需要補入口時)

- [ ] **Step 1: 全面檢查新頁關鍵字**

Run: `Select-String -Path 'docs\timeline.html','docs\index.html' -Pattern '前手|後手|程序|未驗收|尾款|抗辯可信度'`
Expected: 關鍵字能在預期頁面出現，且 `index.html` 不必全部都有

- [ ] **Step 2: 檢查相對連結與資產存在**

Run: `$files = 'docs/index.html','docs/timeline.html'; foreach ($file in $files) { $content = Get-Content -Raw $file; $matches = [regex]::Matches($content, '(?:href|src)=\"(\\./[^\"]+)\"'); foreach ($m in $matches) { $rel = $m.Groups[1].Value; if ($rel -like './index.html*' -or $rel -like './timeline.html*' -or $rel -like '#*') { continue }; $path = Join-Path (Split-Path $file) ($rel -replace '^\\./',''); if (-not (Test-Path $path)) { Write-Output (\"MISSING `\"{0}`\" in {1}\" -f $rel, $file) } } }`
Expected: 無輸出

- [ ] **Step 3: 檢查 git 狀態**

Run: `git status --short --branch`
Expected: 僅顯示本次 HTML / 資產相關變更，不包含使用者正在編輯的其他檔案以外的意外修改

- [ ] **Step 4: 推送**

```bash
git add "C:\Users\88698\Downloads\jenny案\docs\timeline.html" "C:\Users\88698\Downloads\jenny案\docs\index.html" "C:\Users\88698\Downloads\jenny案\docs\assets\Image-1703.png" "C:\Users\88698\Downloads\jenny案\README.md"
git commit -m "feat: add balanced acceptance and credibility updates"
git push origin master
```

- [ ] **Step 5: 確認 GitHub Pages**

Run: `try { (Invoke-WebRequest 'https://golfamigo.github.io/jenny/timeline.html' -UseBasicParsing -Method Head).StatusCode } catch { $_.Exception.Response.StatusCode.value__ }`
Expected: `200`
