# scrum-ticket-lifecycle

Azure DevOps + Scrum 工單生命週期規範 Skill，適用於雄獅旅遊 IT 多 Squad 矩陣組織。

## 用途

輔助 Scrum 流程運作的**流程檢查工具**，協助團隊在以下場景建立共同語言：

- 確認開單前提條件是否備妥
- 判斷卡片應在哪個狀態（To Do / In Progress / Pending / Done / Blocked）
- 定義各狀態的關單條件（DoD）
- 處理跨 Squad 工單邊界
- 管理 Sprint 插單、衍生任務、carry-over

> **決策權在 TPO**：要開哪些 Epic / Story、優先度判斷由 Squad TPO 負責。本 skill 只做流程條件檢查。

---

## 檔案結構

```
scrum-ticket-lifecycle/
├── SKILL.md                        # 主規範（Claude Code / Copilot 載入點）
└── references/
    ├── ac-guide.md                 # AC 定義規範與範例
    ├── block-handling.md           # Block 判斷樹與允收流程
    ├── card-states.md              # 卡片狀態定義與判斷引導
    └── ado-fields.md               # ADO 欄位對應表
```

---

## 安裝方式

### Claude Code

將 `scrum-ticket-lifecycle/` 資料夾複製到你的 Claude Code skills 目錄：

```bash
# 預設 skills 路徑（依實際環境調整）
cp -r scrum-ticket-lifecycle/ ~/.claude/skills/
```

或在 `CLAUDE.md` 中直接引用本 skill：

```markdown
## Skills
- path: ./scrum-ticket-lifecycle/SKILL.md
```

### GitHub Copilot

本 repo 的 `.github/copilot-instructions.md` 已預先設定，Clone 後即可使用。

---

## 觸發範例

直接在 Claude Code 或 Copilot Chat 說：

- 「這張卡可以關了嗎？」
- 「AC 怎麼寫？」
- 「這個需求可以進 backlog 嗎？」
- 「Sprint 內跑出新東西怎麼辦？」
- 「這張卡現在該在哪個狀態？」
- 「跨 Squad 工單誰主責？」

---

## 貢獻方式

1. Fork 本 repo
2. 建立 feature branch（`git checkout -b feat/your-change`）
3. 修改規範內容
4. Push 後開 PR，等待 maintainer review 後 merge

PR 說明請包含：修改原因、影響的規則範圍、是否需要同步更新 references。

---

## License

MIT
