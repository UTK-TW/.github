---
created: 2025-09-02T18:49:02Z
last_updated: 2025-09-02T18:49:02Z
version: 1.0
author: Claude Code PM System
---

# 專案結構文件

## 根目錄結構
```
.
├── .claude/                    # Claude Code SuperClaude 配置目錄
├── .git/                      # Git 版本控制
├── .github/                   # GitHub 組織設定
├── CLAUDE.md                  # Claude 工作指引 (主要)
├── CONTRIBUTING.md            # 貢獻指南
├── LICENSE                    # 專有授權條款
├── README.md                  # 專案說明文件
├── SECURITY.md                # 安全政策
├── SUPPORT.md                 # 技術支援說明
└── profile/                   # GitHub 組織簡介頁面
```

## .claude/ 目錄架構
SuperClaude 框架的核心配置區域：

```
.claude/
├── agents/                    # 專業化子代理程式
│   ├── code-analyzer.md      # 程式碼分析專家
│   ├── file-analyzer.md      # 檔案分析專家
│   ├── parallel-worker.md    # 平行處理協調器
│   └── test-runner.md        # 測試執行專家
├── commands/                 # 自訂指令系統
│   ├── code-rabbit.md        # CodeRabbit 評論處理器
│   ├── context/              # 專案上下文管理
│   ├── pm/                   # 專案管理指令
│   ├── prompt.md             # 提示詞管理
│   ├── re-init.md           # 重新初始化指令
│   └── testing/              # 測試工作流程
├── context/                  # 專案上下文文件 (本目錄)
├── epics/                    # 功能史詩管理
├── prds/                     # 產品需求文件
├── rules/                    # 系統規則集合
├── scripts/                  # 自動化腳本
├── CLAUDE.md                 # 開發指引 (詳細版)
└── settings.local.json       # 本地權限設定
```

## .github/ 目錄結構
GitHub 組織標準化設定：

```
.github/
├── ISSUE_TEMPLATE/           # Issue 模板集合
│   ├── bug_report.yml       # 錯誤回報模板
│   ├── config.yml           # 模板設定
│   ├── documentation.yml    # 文件改進模板
│   ├── feature_request.yml  # 功能請求模板
│   └── question.yml         # 問題諮詢模板
├── PULL_REQUEST_TEMPLATE/   # Pull Request 模板
├── workflows/               # GitHub Actions 工作流程
│   └── sync-labels-to-all-repos-fixed.yml
└── labels.yml              # 組織標準標籤定義
```

## 檔案命名模式

### Markdown 文件
- **英文檔案**: kebab-case (例如: `project-structure.md`)
- **中文內容**: 使用繁體中文
- **模板檔案**: 明確的用途描述 (例如: `bug_report.yml`)

### 設定檔案
- **YAML 檔案**: kebab-case 或 snake_case
- **JSON 檔案**: camelCase 或 kebab-case
- **Shell 腳本**: kebab-case.sh

### 目錄結構
- **功能目錄**: 單數形式 (例如: `agent/`, `command/`)
- **資料目錄**: 複數形式 (例如: `epics/`, `prds/`)
- **隱藏目錄**: 點前綴 (例如: `.claude/`, `.github/`)

## 模組組織

### SuperClaude 框架層次
1. **核心配置層** - 主要框架設定和規則
2. **代理程式層** - 專業化子代理程式
3. **指令層** - 使用者介面和工作流程
4. **腳本層** - 自動化和實用工具

### GitHub 組織層次
1. **模板層** - 標準化 Issue 和 PR 流程
2. **工作流程層** - 自動化標籤管理和品質檢查
3. **政策層** - 安全、貢獻和支援政策
4. **品牌層** - 組織形象和簡介頁面

## 關鍵檔案說明

### 重要設定檔
- **`.claude/settings.local.json`** - Claude Code 權限設定
- **`.github/labels.yml`** - 統一標籤系統定義
- **`LICENSE`** - Proprietary 專有授權條款

### 主要文件檔案
- **`README.md`** - 專案概述和使用說明 (繁體中文)
- **`CLAUDE.md`** - Claude 工作指引 (雙語)
- **`CONTRIBUTING.md`** - 貢獻流程和開發規範

### 自動化腳本
- **`.claude/scripts/pm/`** - 專案管理自動化腳本
- **`.claude/scripts/test-and-log.sh`** - 測試執行和日誌記錄

## 檔案存取模式

### 公開檔案
- 所有 `.md` 檔案
- `LICENSE` 檔案
- `.github/` 下的模板和設定

### 內部使用檔案
- `.claude/` 目錄下的所有檔案
- 本地設定和快取檔案

### 自動生成檔案
- Git 版本控制檔案
- 臨時日誌檔案
- 快取和狀態檔案

## 新增檔案時的最佳實務
1. **確認目錄位置** - 根據功能選擇正確的目錄
2. **遵循命名慣例** - 使用一致的命名模式
3. **新增前導資料** - YAML frontmatter 和元資料
4. **文件說明** - 適當的註解和說明
5. **權限檢查** - 確認檔案存取權限正確設定