# 卡片狀態規範

## 狀態流轉總覽

```
Backlog
  │
  ▼
To Do ──────────────────────────────────┐
  │                                     │
  ▼                                     │
In Progress ──► Blocked（任何階段可標記）│
  │                                     │
  ▼                                     │
Pending                                 │
  │                                     │
  ▼                                     │
Done ◄──────────────────────────────────┘
                              （Carry-over 退回 To Do）
```

---

## 各狀態定義

### 🔲 To Do
**意義**：已排入本 Sprint，尚未開始。

**進入條件：**
- Story 已有 AC
- 已在 Sprint Planning 中被揀入
- Assignee 已指定

**負責推動**：Assignee 自行認領開始，移入 In Progress。

**卡太久警戒**：Sprint 前半段結束（約第 5 天）仍在 To Do → Assignee 主動說明原因，TPO 評估是否調整優先度或移出 Sprint。

---

### 🔵 In Progress
**意義**：Assignee 已開始實作或測試中。

**進入條件：**
- Assignee 實際開始動工
- 一張卡同一時間只能一個人 In Progress（不能掛著不動）

**負責推動**：Assignee 每日更新進度；有卡關立即標 Blocked，不要讓卡片靜止。

**卡太久警戒**：同一張卡 In Progress 超過 3 天無任何更新 → Daily Standup 主動提出，SM / TPO 協助排除。

---

### 🟡 Pending
**意義**：開發完成，等待外部動作才能繼續（驗收、BO 審核、跨 Squad 確認、上版等）。

**進入條件：**
- 開發 / 測試工作本身已完成
- 剩餘的 blocking 因素在外部（非 Assignee 可自行推進）

**負責推動**：Assignee 負責追蹤外部進度，**不是等別人來找你**。

**常見 Pending 情境：**

| 情境 | 等待對象 | 建議追蹤頻率 |
|------|---------|------------|
| 等 PM / PO 驗收 AC | PM / PO | 每天追一次 |
| 等 BO 審核或簽核 | BO | 每天追一次，並在 ADO Discussion 留紀錄 |
| 等跨 Squad 介面就緒 | 對方 Squad TPO | 每兩天同步一次 |
| 等上版窗口 | Release 負責人 | 確認窗口時間，不需每天追 |

**卡太久警戒**：Pending 超過 **3 個工作天** 無進展 → Assignee 主動通知 TPO，評估是否先關單開 next action 或升報。

---

### ✅ Done
**意義**：DoD 全部勾選，本張卡完全交付。

**進入條件（Story）：**
- AC 由 PM / PO 驗收確認
- 程式碼已 merge
- 測試通過並有紀錄
- 跨 Squad 介面已確認（若有）

**進入條件（Task）：**
- 產出物已存放指定位置
- Assignee 自行確認完成

**誰來移**：Story 由 PM / PO 確認後移入；Task 由 Assignee 自行移入。

---

### 🚫 Blocked
**意義**：有明確的外部依賴卡住，Assignee 無法自行推進。

**可在任何階段標記**（To Do / In Progress / Pending 皆適用）。

**標記時必須在 ADO Discussion 欄說明：**
```
[Blocked]
原因：[具體是什麼卡住，不要只寫「等對方」]
等待對象：[人名 或 Squad]
預計解除時間：[若有]
```

**負責推動**：標記者負責追蹤，並通知對方 Squad TPO（跨 Squad 時）。

**卡太久警戒**：Blocked 超過 **2 個工作天** 無進展 → 升報 TPO，由 TPO 決定是否先關單掛關聯或調整 Sprint 範圍。

---

## 狀態判斷引導

當使用者說「這張卡現在該在哪個狀態」，依以下問題依序判斷：

```
1. 這張卡排進 Sprint 了嗎？
   否 → Backlog（不在 Board 上）
   是 → 繼續往下

2. Assignee 開始動工了嗎？
   否 → To Do
   是 → 繼續往下

3. 開發 / 測試工作本身完成了嗎？
   否，且有卡關 → Blocked（標記原因）
   否，正在進行 → In Progress
   是 → 繼續往下

4. DoD 全部勾選了嗎？
   否，在等外部（驗收 / 審核 / 上版）→ Pending
   是 → Done
```

---

## Carry-over 處理

Sprint 結束時仍未 Done 的卡：

- **Story Owner 允收** → 關單，開 next action Task 掛關聯
- **Story Owner 不允收** → 退回 To Do，加 `carry-over` Tag，移入下一 Sprint
- **Blocked 狀態** → TPO 判斷先關單掛關聯，或整張帶入下一 Sprint
