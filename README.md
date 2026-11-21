# 型態雷達（Pattern Radar）

台股蔡森十二招＋CIS 型態掃描、類股雷達、回測與盤後警示。網站：https://nightknight01.github.io/pattern-radar/

本工具只做型態偵測與歷史驗證，不構成投資建議，也不會代為下單。

## 這個 repo 怎麼運作
- 每個交易日台北 17:30（20:30 補跑）GitHub Actions 自動執行 `.github/workflows/radar.yml`：
  抓證交所／櫃買中心官方資料 → 掃描 13 個型態 → 回測 → 產生盤後警示 → 更新網站。
- 網站是純靜態頁（GitHub Pages），只讀批次算好的 JSON。
- 資料狀態存在 Release「radar-state」的附檔（每天一份，保留最近 7 份）；第一次執行用 repo 裡的 `seed_*` 檔。

## 檔案
| 檔案 | 用途 |
|---|---|
| `app.zip` | 程式（pipeline/ Python 批次＋web/ 網頁外殼）。更新程式時只要重傳這個檔 |
| `params.json` | 型態與回測參數，可直接在 GitHub 網頁上編輯，下一次執行生效 |
| `seed_*` | 2024-01-02～2026-11-19 的初始資料（只在第一次執行用到） |
| `.github/workflows/radar.yml` | 每日排程 |

## Secrets（Settings → Secrets and variables → Actions）
`SMTP_USER`（寄件 Gmail）、`SMTP_PASS`（Gmail 應用程式密碼）、`ALERT_TO`（收件人）。沒設就只產生預覽、不寄信。
