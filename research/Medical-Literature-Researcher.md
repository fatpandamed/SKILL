# 增加連線容忍時間與請求間隔
options(rentrez.curl_timeout_ms = 60000) 
# 設定 API 請求間隔為 1.0 秒以避開 NCBI 限制
Sys.sleep(1.0)

library(rentrez)
library(tidyverse)
library(googledrive)

run_agent_to_cloud <- function(keyword, years = "2006:2026") {
  query <- paste0(keyword, " AND ", years, "[pdat]")
  search_res <- entrez_search(db = "pubmed", term = query, use_history = TRUE)
  # ... (完整抓取與 Google Drive 同步邏輯)
}