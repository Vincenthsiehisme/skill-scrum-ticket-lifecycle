---
name: scrum-ticket-lifecycle
description: >
  Azure DevOps + Scrum 工單生命週期規範顧問。定義開單、關單、分工的條件與時機，幫助團隊建立共同語言。

  觸發關鍵字：「什麼時候開單」「什麼時候關單」「什麼時候分工」「DoD」「Definition of Done」「工單邊界」「工單規範」「怎麼拆工單」「誰來認領」「這張單可以關了嗎」「這個需求要開幾張單」「跨 Squad 工單誰主責」「工單流程」「ADO 規範」「Sprint 工單」「AC 怎麼寫」「插單」「carry-over」「block」「refinement」「planning」「許願清單」「backlog 入口」「衍生任務」「subtask」「extra point」「短解」「next action」。

  使用者貼上工單描述並問「這樣對嗎」「可以關了嗎」「誰來開單」「這個需求可以進 backlog 嗎」「Sprint 內跑出新東西怎麼辦」時也應主動觸發。
---

# Scrum Ticket Lifecycle — 工單生命週期規範

## 定位

輔助 Scrum 流程運作的**流程檢查工具**，不是需求決策工具。

**決策權在 TPO，skill 負責流程：**
- 要開哪些 Epic / Story、優先度高中低 → **Squad TPO 判斷**，skill 不介入
- TPO 決定要做之後 → skill 協助確認流程條件是否備妥、卡片狀態是否正確

- **工單工具**：Azure DevOps（Epic → Feature → User Story → Task 四層）
- **開發框架**：Scrum（Sprint Planning / Refinement / Retro）
- **團隊結構**：多 Squad 矩陣組織（雄獅旅遊 IT 部門）

---

## 核心規則摘要

### 🟢 開單條件（流程前提檢查）

TPO 決定要做某個需求後，開單前確認以下條件已備妥：

| 層級 | 開單時機 | 開單前必須確認 |
|------|---------|-------------|
| **Epic** | TPO 確認要做這個方向 | 有 business goal、有負責的 Squad |
| **Feature** | Sprint Planning 前的 Refinement | 範圍可以在 1–2 個 Sprint 內交付 |
| **User Story** | Refinement 完成後 | AC 已寫清楚、有 Squad owner |
| **Task** | Sprint Planning 當下 | 指派到人、預估 hours |

**硬規則：User Story 沒有 AC，不進 Sprint。**

先不開單的情況：需求還在討論、跨 Squad 主責未定、描述模糊到無法驗收。

> AC 寫法詳見 `references/ac-guide.md`（使用者問「AC 怎麼寫」或「AC 範例」時載入）

---

### 🔴 關單條件（DoD）

**User Story 關單需全部勾選：**
- [ ] 功能符合 AC，由 PM 或 PO 驗收確認
- [ ] 程式碼已 merge 到主線（PR approved）
- [ ] 測試案例通過（需有紀錄）
- [ ] 若涉跨 Squad 介面，對方 Squad TPO 已確認

**部署與關單分離**：測試通過即可關 Story，上版另開 Task 追蹤。

**AC 未達成**：不自動關單，需 Story Owner 明確允收並留 Discussion 紀錄；不允收則 carry-over 至下一 Sprint。

> Block 判斷樹詳見 `references/block-handling.md`（使用者問 Sprint 結束前怎麼處理 block 時載入）

**Task 關單**：產出物已存放、認領人自行標記 Done。

**跨 Squad Feature 關單**：雙方 Task 全 Done + 測試環境驗證 + 主責 TPO 確認。

---

### 🟣 卡片狀態規範

Sprint Board 使用四個狀態：**To Do → In Progress → Pending → Done**，加上任何階段可標記的 **Blocked**。

| 狀態 | 意義 | 卡太久的警戒線 |
|------|------|-------------|
| **To Do** | 已排入 Sprint，尚未開始 | Sprint 前半段結束仍未動 → TPO 評估 |
| **In Progress** | 實作或測試進行中 | 超過 3 天無更新 → Daily 提出 |
| **Pending** | 開發完成，等外部（驗收/審核/上版） | 超過 3 工作天無進展 → 通知 TPO |
| **Done** | DoD 全勾，完全交付 | — |
| **Blocked** | 有外部依賴卡住，無法自行推進 | 超過 2 工作天無進展 → 升報 TPO |

> 狀態判斷引導、各狀態進入條件、Pending 追蹤規範、Carry-over 處理詳見 `references/card-states.md`

---

### 🔵 分工規則

**Squad 內部**：Task 在 Planning 時才拆分指派，一張 Task 一個 Assignee。同一人認領超過 3 張 Task 應在 Planning 提出討論。

**跨 Squad**：先定主責 Squad 再開單。主責開 Feature，依賴 Squad 的 Task 掛在同一 Feature 下，不要各自開 Feature 靠口頭協調。

---

### 🟡 Backlog 入口規範

BO 許願清單（Teams / Email / Excel 等圖外工具）與 ADO backlog 是兩個不同的東西。

```
BO 許願清單（圖外工具）
       │
       ▼ TPO 判斷值不值得做
       ▼ 能被 Refinement 寫出 AC？
       │
       ▼
   ADO Backlog（才能被 Refinement 估點）
```

**進 backlog 的唯一門檻：這個需求能被描述成可驗收的 AC。**
描述模糊、範圍不清、無法定義完成條件的需求，停在許願清單，不進 backlog。

---

### 🟡 Refinement 規則

- 估點單位：人天，最小 **0.25 天**，整個 Squad 共同估
- **超過 3 人天強制拆卡**
- Velocity 追蹤：每 Sprint 記錄實際完成點數供下次 Planning 參考
- **Refinement 完 ≠ 排進 Sprint**，實際排入由 Planning 決定

---

### 🟡 Planning 規則

- 依 backlog 優先度揀卡，參考 velocity 決定點數上限
- 各 Squad 可自行定義高/中/低優先卡的比例，skill 不強制
- **至少預排 2 個 Sprint**

---

### 🟡 Sprint 插單規則

| 等級 | 定義 | 處理方式 |
|------|------|---------|
| 🔴 Urgent | 影響線上營運、客戶交易、資安 | 插入當前 Sprint，評估排擠哪張既有卡 |
| 🟡 High | 重要但不影響線上 | 評估空間，告知 BO 排擠狀況 |
| 🟢 Normal | 無時間壓力 | 列入下一 Sprint，走 Refinement 流程 |

**插單一律需要估點**，不估點就無法評估對本 Sprint 容量的實際影響。

**插單必須在 ADO Discussion 欄留紀錄**，說明原因與影響的既有工項，口頭告知不算。

---

### 🟡 Sprint 內衍生任務規則

Sprint 進行中若發現原始 Story 衍生出額外工作，依可完成性判斷處理方式：

**可隨手完成（當下就能做完）：**
- 在原 Story 下開 Subtask
- 若團隊啟用 Extra Point 自訂欄位，填入額外工作量（人天）
- Extra Point 僅用於記錄意外溢出的工作量，**不計入 velocity**
- ⚠️ Extra Point 欄位為選用規則，非所有 Squad 必須採用

**無法隨手完成：**

```
AC 有定義這個場景的短解（最小可行解）？
│
├─ 有短解
│   └─ 本 Sprint 按短解執行
│       └─ 另開 next action Task，記錄完整優化方向（掛關聯）
│
└─ 沒有短解（AC 未涵蓋此場景）
    └─ 先對齊 TPO
        ├─ 確認本 Sprint 能做到哪個程度
        ├─ 評估能否在 2 個 Sprint 內完成
        │   ├─ 能 → 開 next action Story，排入下一 Sprint
        │   └─ 不能 → TPO + BO 重新對焦範圍與優先度
        └─ 對齊完成前，不開單
```

---

## 執行流程

### Step 0：判斷觸發模式

| 輸入性質 | 執行模式 |
|---------|---------|
| 使用者貼上工單描述問「這樣對嗎」 | **Spot Check** |
| 使用者問「流程該怎麼定」 | **Full Output** |
| 使用者問跨 Squad 工單邊界 | **Boundary Check** |
| 使用者問「這張卡該在哪個狀態」「卡了很久怎麼辦」 | 載入 `references/card-states.md`，執行狀態判斷引導 |

---

### Spot Check（針對單張工單）

依序確認：開單層級是否正確 → AC 是否可驗收 → DoD 哪些已勾未勾 → 分工是否唯一明確。

輸出格式：
```
**層級判斷**：[Epic / Feature / Story / Task]
**開單條件**：✅ 滿足 / ⚠️ 缺少 [XXX] / ❌ 不應開單，原因：[...]
**AC 狀態**：✅ 清楚可驗證 / ⚠️ 模糊，建議改寫為 [...]
**DoD 進度**：[x] 已完成 / [ ] 未完成
**分工狀態**：✅ 明確 / ⚠️ [問題描述]
**建議**：[一句話結論]
```

---

### Boundary Check（跨 Squad 工單）

確認：主責 Squad → 依賴 Squad → Task 是否掛同一 Feature → 關單條件是否含對方 TPO 確認。

輸出格式：
```
**主責 Squad**：[名稱]（理由：[...]）
**依賴 Squad**：[名稱]（提供：[...]）
**建議工單結構**：
  Feature（主責 Squad 開）
  └─ Task A（主責）／Task B（依賴，掛同一 Feature）
**關單額外條件**：雙方 Task Done + TPO [姓名] 確認
⚠️ 風險提示：[跨系統時序、狀態同步等已知風險]
```

---

### Stop-and-Align

每次輸出後停下來等使用者確認，不自動繼續。

---

## Gotchas

- **AC 未達成不能靜默關單**：必須有 Owner 允收的明確 ADO 紀錄
- **插單溝通不能只靠口頭**：必須留 ADO Discussion 紀錄
- **Refinement 完 ≠ 排進去了**：不要對 BO 承諾「Refinement 完就會做」
- **部署不是關單條件**：測試通過即可關 Story
- **跨 Squad 主責不要猜**：不確定時標 `[待確認]`
- **Task 不需要 AC**：Task 只需清楚的產出描述
- **DoD 不超過 5 條**：條件太多導致關單困難

---

## Reference Files

| 檔案 | 載入時機 |
|------|---------|
| `references/ac-guide.md` | 使用者問 AC 怎麼寫、AC 範例、AC 格式 |
| `references/block-handling.md` | 使用者問 Sprint 結束前 block 怎麼處理、允收流程 |
| `references/ado-fields.md` | 使用者問 ADO 欄位對應、Tags 格式、Discussion 欄怎麼用 |
| `references/card-states.md` | 使用者問卡片該在哪個狀態、卡太久怎麼辦、Pending 怎麼追、Carry-over 怎麼處理 |
