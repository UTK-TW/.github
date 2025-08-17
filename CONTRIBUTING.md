# 貢獻指南

感謝您對環友科技開源專案的興趣！我們歡迎所有形式的貢獻，包括程式碼、文件、錯誤回報、功能建議等。

## 📋 目錄

- [行為準則](#行為準則)
- [如何貢獻](#如何貢獻)
- [開發環境設置](#開發環境設置)
- [程式碼風格指南](#程式碼風格指南)
- [提交流程](#提交流程)
- [Issue 和 Pull Request 指南](#issue-和-pull-request-指南)
- [發佈流程](#發佈流程)

## 🤝 行為準則

### 我們的承諾

為了營造開放且友善的環境，我們作為貢獻者和維護者承諾，無論年齡、體型、身心健康、民族、性別認同和表達、經驗水平、教育程度、社會經濟地位、國籍、個人形象、種族、宗教或性取向，參與我們專案和社群的每個人都能享有無騷擾的體驗。

### 我們的標準

有助於創造正面環境的行為範例包括：

- 使用友善且包容的語言
- 尊重不同的觀點和經驗
- 優雅地接受建設性批評
- 專注於對社群最有利的事情
- 對其他社群成員表示同理心

### 執行

如果您遇到不當行為，請聯絡專案團隊：sen@utk.com.tw

## 🚀 如何貢獻

### 回報錯誤

如果您發現錯誤，請：

1. 檢查 [現有 Issues](https://github.com/UTK-TW/.github/issues) 確認問題尚未被回報
2. 使用 [錯誤回報模板](https://github.com/UTK-TW/.github/issues/new?template=bug_report.md) 建立新的 Issue
3. 提供詳細的重現步驟和環境資訊

### 建議功能

如果您有新功能的想法：

1. 檢查 [現有 Issues](https://github.com/UTK-TW/.github/issues) 確認功能尚未被建議
2. 使用 [功能請求模板](https://github.com/UTK-TW/.github/issues/new?template=feature_request.md) 建立新的 Issue
3. 詳細描述功能的用途和預期效果

### 改善文件

文件改善總是被歡迎的：

- 修正錯字或語法錯誤
- 改善說明的清晰度
- 新增缺失的資訊
- 提供更多範例

## 🛠️ 開發環境設置

### 必要條件

- **作業系統**: Windows 10/11 (建議)
- **.NET SDK**: .NET 8.0 或更新版本
- **IDE**: Visual Studio 2022 或 Visual Studio Code
- **資料庫**: SQL Server 2019+ 或 Azure SQL
- **Git**: 最新版本

### 環境設置步驟

1. **Clone 儲存庫**
   ```bash
   git clone https://github.com/UTK-TW/[repository-name].git
   cd [repository-name]
   ```

2. **安裝相依性**
   ```bash
   dotnet restore
   ```

3. **設定資料庫**
   ```bash
   dotnet ef database update
   ```

4. **執行專案**
   ```bash
   dotnet run
   ```

### 開發工具建議

- **Visual Studio Extensions**:
  - ReSharper 或 CodeMaid (程式碼整理)
  - SonarLint (程式碼品質檢查)
  - GitLens (Git 增強功能)

- **VS Code Extensions**:
  - C# for Visual Studio Code
  - .NET Install Tool
  - Azure Tools

### 🔧 疑難排解指南

#### 常見開發環境問題

**1. 建置錯誤**
```bash
# 清理並重新建置
dotnet clean
dotnet restore
dotnet build

# 檢查 .NET 版本
dotnet --version

# 清除 NuGet 快取
dotnet nuget locals all --clear
```

**2. 資料庫連線問題**
```bash
# 檢查連線字串
dotnet ef dbcontext info

# 重置資料庫
dotnet ef database drop
dotnet ef database update

# 檢查 Migration 狀態
dotnet ef migrations list
```

**3. 套件版本衝突**
```bash
# 檢查過期套件
dotnet list package --outdated

# 檢查套件參考
dotnet list package --include-transitive

# 強制套件還原
dotnet restore --force
```

#### 除錯最佳實務

**設定開發環境日誌**
```json
// appsettings.Development.json
{
  "Logging": {
    "LogLevel": {
      "Default": "Debug",
      "Microsoft.AspNetCore": "Warning",
      "Microsoft.EntityFrameworkCore.Database.Command": "Information"
    }
  }
}
```

**使用結構化日誌**
```csharp
// 推薦的日誌記錄方式
_logger.LogInformation("User {UserId} created successfully", user.Id);

// 避免字串插值
// _logger.LogInformation($"User {user.Id} created successfully"); // ❌
```

**效能分析工具**
- **dotMemory** - 記憶體分析
- **dotTrace** - 效能分析
- **Application Insights** - 生產環境監控
- **MiniProfiler** - Web 請求分析

## 📝 程式碼風格指南

### C# 編碼標準

我們遵循 [Microsoft C# 編碼慣例](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/inside-a-program/coding-conventions)：

#### 命名慣例

```csharp
// 類別和方法使用 PascalCase
public class UserService
{
    public void CreateUser() { }
}

// 欄位使用 camelCase，私有欄位以底線開頭
private readonly string _connectionString;
public string UserName { get; set; }

// 常數使用 PascalCase
public const int MaxRetryCount = 3;

// 區域變數使用 camelCase
var userList = new List<User>();
```

#### 程式碼組織

```csharp
// 檔案結構順序
using System;
using System.Collections.Generic;
using Microsoft.Extensions.DependencyInjection;

namespace UTK.ProjectName.Services
{
    /// <summary>
    /// 使用者服務類別
    /// </summary>
    public class UserService : IUserService
    {
        // 私有欄位
        private readonly IUserRepository _userRepository;
        
        // 建構子
        public UserService(IUserRepository userRepository)
        {
            _userRepository = userRepository;
        }
        
        // 公開屬性
        public int TotalUsers { get; private set; }
        
        // 公開方法
        public async Task<User> GetUserAsync(int id)
        {
            // 實作
        }
        
        // 私有方法
        private void ValidateUser(User user)
        {
            // 實作
        }
    }
}
```

### 資料庫慣例

- 資料表名稱使用複數形式 (Users, Orders)
- 欄位名稱使用 PascalCase
- 主鍵命名為 Id
- 外鍵命名為 [TableName]Id

### API 設計慣例

```csharp
[ApiController]
[Route("api/[controller]")]
public class UsersController : ControllerBase
{
    // GET api/users
    [HttpGet]
    public async Task<ActionResult<IEnumerable<UserDto>>> GetUsers(
        [FromQuery] int page = 1,
        [FromQuery] int pageSize = 10)
    {
        // 驗證輸入參數
        if (page < 1 || pageSize < 1 || pageSize > 100)
            return BadRequest("Invalid pagination parameters");
            
        // 實作分頁查詢
    }
    
    // GET api/users/5
    [HttpGet("{id}")]
    public async Task<ActionResult<UserDto>> GetUser(int id)
    {
        // 驗證輸入
        if (id <= 0)
            return BadRequest("Invalid user ID");
            
        // 實作查詢邏輯
    }
    
    // POST api/users
    [HttpPost]
    public async Task<ActionResult<UserDto>> CreateUser(CreateUserDto createUserDto)
    {
        // 模型驗證
        if (!ModelState.IsValid)
            return BadRequest(ModelState);
            
        // 實作建立邏輯
    }
    
    // PUT api/users/5
    [HttpPut("{id}")]
    public async Task<IActionResult> UpdateUser(int id, UpdateUserDto updateUserDto)
    
    // DELETE api/users/5
    [HttpDelete("{id}")]
    public async Task<IActionResult> DeleteUser(int id)
}
```

### 安全開發實務

#### 輸入驗證
```csharp
// 總是驗證用戶輸入
public async Task<IActionResult> UpdateUser(int id, UpdateUserRequest request)
{
    // 驗證 ID 格式
    if (id <= 0)
        return BadRequest("Invalid user ID");
    
    // 驗證模型
    if (!ModelState.IsValid)
        return BadRequest(ModelState);
    
    // 業務邏輯驗證
    if (string.IsNullOrWhiteSpace(request.Email) || !IsValidEmail(request.Email))
        return BadRequest("Invalid email format");
    
    // 清理輸入
    request.Name = request.Name?.Trim();
    
    // 繼續處理...
}
```

#### 安全的資料存取
```csharp
// 使用參數化查詢防止 SQL 注入
public async Task<List<User>> SearchUsersAsync(string searchTerm)
{
    return await _context.Users
        .Where(u => u.Name.Contains(searchTerm))  // EF Core 自動參數化
        .Select(u => new User { Id = u.Id, Name = u.Name })  // 只選擇需要的欄位
        .ToListAsync();
}

// 避免敏感資訊洩露
public class UserDto
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
    // 不包含密碼、內部 ID 等敏感資訊
}
```

## 🔄 提交流程

### Git 工作流程

我們使用 **Git Flow** 分支策略：

- `main` - 生產版本分支
- `develop` - 開發分支
- `feature/*` - 功能開發分支
- `release/*` - 發佈準備分支
- `hotfix/*` - 緊急修復分支

### 分支命名慣例

```bash
feature/user-authentication
feature/order-management
bugfix/login-error
hotfix/security-patch
release/v1.2.0
```

### 提交訊息格式

使用 [Conventional Commits](https://www.conventionalcommits.org/) 格式：

```
<type>(<scope>): <description>

[optional body]

[optional footer(s)]
```

#### 類型 (Type)

- `feat`: 新功能
- `fix`: 錯誤修復
- `docs`: 文件變更
- `style`: 格式調整（不影響程式碼意義）
- `refactor`: 重構（既不修復錯誤也不新增功能）
- `perf`: 效能改善
- `test`: 新增或修改測試
- `build`: 建置系統或外部相依性變更
- `ci`: CI 設定檔案和腳本變更
- `chore`: 其他不修改 src 或 test 檔案的變更

#### 範例

```bash
feat(auth): add user login functionality
fix(api): resolve null reference exception in user service
docs(readme): update installation instructions
style(user): format code according to style guide
refactor(order): simplify order calculation logic
test(user): add unit tests for user service
```

## 📋 Issue 和 Pull Request 指南

### 建立 Issue

1. 使用適當的 Issue 模板
2. 提供清楚的標題和描述
3. 新增相關標籤
4. 如果是錯誤，提供重現步驟
5. 如果是功能請求，說明使用案例

### 建立 Pull Request

1. **建立分支**
   ```bash
   git checkout develop
   git pull origin develop
   git checkout -b feature/your-feature-name
   ```

2. **開發並測試**
   - 撰寫程式碼
   - 新增或更新測試
   - 確保所有測試通過
   - 遵循程式碼風格指南

3. **提交變更**
   ```bash
   git add .
   git commit -m "feat(scope): add new feature"
   git push origin feature/your-feature-name
   ```

4. **建立 Pull Request**
   - 使用 PR 模板
   - 提供清楚的描述
   - 連結相關 Issue
   - 新增適當的標籤
   - 請求程式碼審查

### 程式碼審查準則

#### 審查者應檢查：

**程式碼品質**
- ✅ 程式碼是否符合風格指南
- ✅ 是否遵循 SOLID 原則
- ✅ 程式碼是否易於理解和維護
- ✅ 是否有適當的註解和文件

**測試與品質保證**
- ✅ 是否有足夠的測試覆蓋率 (目標 > 80%)
- ✅ 單元測試是否測試了邊界條件
- ✅ 整合測試是否涵蓋關鍵路徑
- ✅ 是否有適當的錯誤處理和邊界檢查

**效能與安全性**
- ✅ 效能是否可接受（無明顯的性能瓶頸）
- ✅ 是否考慮了資料庫查詢效率
- ✅ 安全性是否考慮周全（輸入驗證、授權檢查）
- ✅ 是否避免了常見的安全漏洞（SQL 注入、XSS 等）

**架構與設計**
- ✅ 是否符合現有的架構模式
- ✅ 依賴注入是否正確使用
- ✅ 是否有適當的抽象和介面設計
- ✅ 資料庫遷移是否向下相容

**文件與維護性**
- ✅ API 文件是否已更新
- ✅ README 或相關文件是否反映變更
- ✅ 變更日誌是否已更新（如適用）

#### 作者應確保：

**提交前檢查清單**
- [ ] 所有測試都通過（單元測試、整合測試）
- [ ] 程式碼已經自我審查
- [ ] 遵循程式碼風格指南
- [ ] 新增了適當的測試覆蓋
- [ ] 文件已更新（API 文件、README 等）
- [ ] 沒有調試代碼殘留（console.log、斷點等）
- [ ] 沒有敏感資訊（密鑰、密碼、內部 URL）
- [ ] 變更日誌已更新（重大變更）

**測試驗證**
```bash
# 執行完整測試套件
dotnet test

# 檢查程式碼覆蓋率
dotnet test --collect:"XPlat Code Coverage"

# 執行程式碼品質檢查
dotnet format --verify-no-changes
```

**效能基準測試**（如適用）
```bash
# 效能測試
dotnet run --configuration Release --project PerformanceTests

# 記憶體分析
dotnet-dump ps
```

## 🚀 發佈流程

### 版本命名

我們使用 [語義化版本控制](https://semver.org/)：

- `MAJOR.MINOR.PATCH` (例如 1.2.3)
- `MAJOR`: 不相容的 API 變更
- `MINOR`: 新增功能但保持向下相容
- `PATCH`: 錯誤修復

### 發佈步驟

1. **準備發佈**
   ```bash
   git checkout develop
   git pull origin develop
   git checkout -b release/v1.2.0
   ```

2. **更新版本資訊**
   - 更新 `*.csproj` 檔案中的版本號
   - 更新 `CHANGELOG.md`
   - 更新文件中的版本參考

3. **測試發佈**
   ```bash
   dotnet build --configuration Release
   dotnet test
   ```

4. **合併到 main**
   ```bash
   git checkout main
   git merge release/v1.2.0
   git tag v1.2.0
   git push origin main --tags
   ```

5. **合併回 develop**
   ```bash
   git checkout develop
   git merge main
   git push origin develop
   ```

## 🆘 需要協助？

如果您在貢獻過程中遇到任何問題：

- 查看我們的 [支援指南](SUPPORT.md)
- 在 [Discussions](https://github.com/UTK-TW/.github/discussions) 中提問
- 傳送電子郵件至 sen@utk.com.tw
- 瀏覽我們的 [官方網站](https://www.utk.com.tw/)

## 📄 授權

透過貢獻，您同意您的貢獻將在與專案相同的授權條款下授權。

---

再次感謝您的貢獻！🎉

*最後更新: 2025年8月*