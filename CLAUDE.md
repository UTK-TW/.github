# CLAUDE.md

此檔案為 Claude Code (claude.ai/code) 在此儲存庫中工作時的指引文件。

## 儲存庫目的

這是環友科技股份有限公司 (UTK Technology Co., Ltd.) 的 GitHub 組織預設儲存庫 (`.github`)。包含組織層級的範本、政策和自動化功能，會自動套用至 UTK-TW 組織中的所有儲存庫。

## 主要架構

### 組織結構
- **組織檔案**: `/profile/README.md` 作為 github.com/UTK-TW 的公開組織頁面
- **範本**: `.github/ISSUE_TEMPLATE/` 包含標準化問題表單，涵蓋錯誤回報、功能請求、問題諮詢和文件需求
- **工作流程**: `.github/workflows/` 包含 GitHub Actions，用於在所有組織儲存庫間自動同步標籤
- **標準**: `.github/labels.yml` 定義所有 UTK 專案使用的標準標籤系統

### 技術堆疊環境
組織主要使用：
- .NET 8.0 / .NET Core 與 ASP.NET Core MVC/API
- Entity Framework Core 進行資料存取
- Azure 雲端服務和 Azure SQL
- Windows Server/IIS 部署
- 工作排程器進行自動化

## 常用指令

### 標籤管理
```bash
# 觸發跨所有組織儲存庫的標籤同步
# 透過 GitHub UI: Actions 頁籤 > "同步標籤到所有組織儲存庫" > Run workflow

# 預覽模式 (試執行):
gh workflow run sync-labels-to-all-repos-fixed.yml --field dry_run=true

# 強制同步而不修改 labels.yml:
gh workflow run sync-labels-to-all-repos-fixed.yml
```

### 驗證與測試
```bash
# 驗證工作流程和設定檔的 YAML 語法
yamllint .github/workflows/
yamllint .github/labels.yml

# 檢查工作流程語法
gh workflow list
gh workflow view sync-labels-to-all-repos-fixed.yml
```

## 重要檔案及其影響

### 自動套用檔案
這些檔案會自動套用至 UTK-TW 組織中所有沒有自訂版本的儲存庫：
- `CONTRIBUTING.md` - 開發和貢獻標準
- `SECURITY.md` - 安全政策和漏洞回報
- `SUPPORT.md` - 技術支援流程和聯絡資訊
- `LICENSE` - 專有授權條款
- `.github/ISSUE_TEMPLATE/` 中的問題範本

### 工作流程相依性
- **標籤同步工作流程**: 需要具有 `repo` 和 `read:org` 權限的 `ORG_PAT_TOKEN` 密鑰
- **目標儲存庫**: 自動發現組織中所有非分支、非封存的儲存庫
- **並行執行**: 同時處理最多 3 個儲存庫以避免 API 速率限制

## 語言與在地化

所有文件主要使用繁體中文，針對台灣/香港市場。進行修改時請：
- 保持中文作為主要語言
- 使用適合台灣科技業的商業術語
- 遵循既有的正式語調和結構
- 考量繁體中文字符的使用

## 安全與合規

### 權杖管理
- `ORG_PAT_TOKEN` 必須保持安全並定期輪換
- 工作流程在執行前會驗證權杖權限
- 驗證失敗會停止執行並提供明確錯誤訊息

### 文件標準
- 安全政策包含完整的 OWASP 合規指導原則
- 所有程式碼範例都展示安全編碼實踐（參數化查詢、輸入驗證、HTTPS 強制執行）
- 漏洞揭露程序遵循業界最佳實踐

## 工作流程行為

### 標籤同步
主要自動化功能會將 `.github/labels.yml` 的標籤同步至所有組織儲存庫：
- **觸發條件**: 推送到主分支影響 `labels.yml` 或手動觸發工作流程
- **範圍**: 所有活動中的（非分支、非封存）組織儲存庫
- **安全機制**: 包含試執行模式和完整錯誤處理
- **衝突解決**: 更新既有標籤，建立缺失標籤

修改 labels.yml 時：
1. 變更會自動觸發同步
2. 工作流程提供詳細操作摘要
3. 個別儲存庫失敗不會停止整個程序
4. 結果會記錄每個儲存庫的成功/失敗狀態