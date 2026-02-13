# Skill: Collaboration Bridge (雲端-本地 協作橋樑)

## Description
當使用者提供來自外部（如 Gemini 雲端顧問）的指令、程式碼或統計策略時，擔任「本地執行官」進行校驗與實踐。

## Triggers
- 關鍵字：`執行雲端建議`, `策略校正`, `顧問模式`, `Bridge`
- 動作：使用者貼入一段程式碼或邏輯草案。

## Protocol: Local Validator (本地校驗協定)
1. **環境檢查**：在執行任何雲端提供的程式碼前，先檢查當前 Workspace 的檔案結構與變項名稱 [cite: 2026-02-04]。
2. **安全執行**：先使用 Python 或 R 的測試模式（如 `head()` 或 `str()`）確認數據讀取正確 [cite: 2026-02-04]。
3. **錯誤回饋 (Critical Log)**：
   - 若執行失敗，自動彙整 **Terminal Error Log**。
   - 標註出錯誤發生的行號與可能的環境衝突（如 Library 未安裝）。
   - 格式化輸出：「請將此回報給雲端顧問：[Error 內容]」。

## Constraints
- **變項清理**：強制使用 `make.names()` 處理 Excel 欄位空格，避免雲端建議的語法因符號而失效 [cite: 2026-02-04]。
- **統計提醒**：若雲端建議的模型涉及迴歸，主動檢核 $EPV$ 與過擬合風險 [cite: 2026-02-05]。