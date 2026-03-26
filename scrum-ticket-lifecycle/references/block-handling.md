# Block 處理判斷樹

## 測試階段跨 Sprint 的 Block

```
測試中，Sprint 快結束
│
├─ Block 來源是 Squad 內部？
│   ├─ 能在本 Sprint 內解決 → 繼續，不動單
│   └─ 無法在本 Sprint 解決 → 拆 Task 列入下一 Sprint
│
└─ Block 來源是跨 Squad（外部依賴）？
    ├─ 本張單的工作已完成（AC 已滿足）？
    │   └─ 是 → 關 Story，開 next action Task，掛關聯
    └─ 本張單的 AC 尚未達成？
        ├─ 討論 Story Owner 是否允收
        │   ├─ 允收 → 關單，記錄允收原因（ADO Discussion 欄）
        │   └─ 不允收 → 標 Blocked，通知對方 Squad TPO，移入下一 Sprint
        └─ 對方 Squad 是主責 → 由對方 Squad TPO 決定先關單掛關聯，還是繼續 block
```

---

## 允收紀錄格式（貼入 ADO Discussion 欄）

```
[允收紀錄]
允收人：[Owner 姓名]
日期：[YYYY-MM-DD]
原因：[說明為何允收，AC 哪一條未達成]
後續行動：[next action Task 連結或描述]
```
