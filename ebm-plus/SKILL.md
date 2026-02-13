# Skill: EBM+ 2.0 (Clinical Evidence Deep Dive)

## Description
針對醫學文獻進行深度全景分析與數據核對，結合 Python 執行環境確保 100% 數據精確度，嚴禁憑記憶回答。

## Triggers
- 關鍵字：`EBM+`, `啟動 EBM+`, `文獻深度分析`, `EBM 2.0`
- 動作：使用者上傳醫學論文 PDF 或提供文獻連結。

## Protocol: Python-First Verification (🛡️ 結構化核對協定)
當此技能啟動時，Agent 必須優先執行以下 Python 邏輯：

1. **定位文字 (Anchor Text)**：
   - 使用 `pdfplumber` 或 `PyMuPDF` 檢索主題在 PDF 中的具體頁碼。
2. **提取標記 (Citation Extraction)**：
   - 精確抓取段落後方的 Reference 編號（如 [9], [10]）。
3. **清單映射 (Reference Mapping)**：
   - 讀取文獻末尾的 Reference List，將編號對應至完整試驗名稱（如 TTM-2, ECLS-SHOCK）。
4. **數據比對 (Data Verification)**：
   - 讀取該試驗對應的具體 $N$、$P$ 值與 $OR/HR$ 數據，確保與摘要描述 100% 同步。

## Output Structure

### 第一部分：全景導讀 (The Big Picture)
- **Landmark Data 核心數據表**：包含 $N$、$P$ 值、主要結論（需標註 PDF 頁碼）。
- **全球準則接軌分析**：該研究如何與國際準則（如 ACLS, ESC, AHA）對接。
- **臨床珍珠 (Pearl)**：針對特定次族群（如多管 PCI、休克患者）的隱藏風險警告。

### 第二部分：段落深度解析 (Deep Dive Analysis)
- **Introduction 分析**：指出作者如何佈局研究缺口 (The Gap) 以及如何挑戰現有禁忌。
- **Method 解析**：
    - **Inclusion/Exclusion**：逐段拆解並與 Results 的 Baseline Table 進行核對。
    - **Statistics 選用動機**：分析非參數檢定、樣本數估算、Overfitting 處理。
    - **Selection Bias**：分析數據庫選擇偏誤的處理邏輯。

## Constraints
- **嚴禁憑記憶**：所有統計數據（$P < 0.05$ 等）必須經由 Python 提取原始文字核對。
- **反幻想機制**：若文獻結果為「中性 (Neutral)」或「無顯著差異」，必須直接摘錄原文。
- **Latex 規範**：所有數學符號與變項（如 $MAP$, $AUC$）需使用 Latex 格式。

"自動化行為：分析結束後，必須主動詢問是否將結果存為 {日期}_EBM_Report.md。"

**數值語意規範**：在提取統計數據時，必須明確區分「基準值 (Baseline)」、「改善幅度 (Improvement)」與「盛行率 (Prevalence)」，嚴禁簡化語意導致歧義。