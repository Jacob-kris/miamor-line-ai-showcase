# AI / Agent Workflow

## 設計重點

這個專案中的 AI 並不是單獨存在的聊天模型，而是 workflow 的一部分。

AI 的任務：

- 回答課程與服務相關問題。
- 協助引導使用者完成資訊收集。
- 在產品規則內提供自然語言回覆。

AI 不負責：

- 直接決定資料庫最終狀態。
- 處理 admin 權限。
- 保存 secret。
- 執行付款、排程或敏感資料寫入。

## 簡化流程

1. LINE webhook 收到訊息。
2. 後端讀取使用者狀態。
3. Workflow engine 判斷訊息屬於哪個流程。
4. 若適合 AI 回覆，才把必要 context 傳給 AI。
5. 若是結構化問卷或 follow-up 任務，使用 server-side workflow 處理。
6. 重要狀態寫入 Supabase。
7. Admin UI 顯示可操作的結果。

## 避免 AI 亂回答的方式

- 使用 prompt boundary 限制回覆範圍。
- 讓流程狀態由 backend 和 database 控制。
- 不讓 AI 直接改寫關鍵資料。
- 遇到不確定、超出範圍或需要人工判斷的情境，回到人工確認。

## Agent 設計能力展現

這個專案展示的不是「把 prompt 丟給模型」，而是：

- 需求拆解。
- Workflow design。
- API integration。
- Database state design。
- Human-in-the-loop admin workflow。
- AI-assisted development 與文件整理。
