# 安全政策

## 🔒 安全承諾

環友科技股份有限公司致力於為我們的開源專案和使用者提供安全的軟體環境。我們認真對待安全問題，並感謝安全研究人員和社群成員協助我們保持軟體的安全性。

## 🛡️ 支援的版本

以下是目前接受安全更新的軟體版本：

| 版本 | 支援狀態 |
| --- | --- |
| 2.x.x | ✅ 完整支援 |
| 1.8.x | ✅ 安全修復 |
| 1.7.x | ⚠️ 有限支援 |
| < 1.7 | ❌ 不再支援 |

## 🚨 回報安全漏洞

### 🔐 負責任的揭露

如果您發現安全漏洞，請**不要**在公開的 Issue 追蹤器中回報。相反，請透過以下安全管道回報：

### 📧 安全聯絡方式

**主要聯絡方式:**
- 電子郵件: sen@utk.com.tw
- 緊急聯絡: sen@utk.com.tw

**回報時請包含:**
- 漏洞的詳細描述
- 受影響的版本
- 重現步驟（如果可能）
- 潛在的影響評估
- 建議的修復方案（如果有）

### 🕐 回應時間表

我們承諾在以下時間內回應安全回報：

- **確認收到**: 24 小時內
- **初始評估**: 72 小時內
- **詳細分析**: 7 天內
- **修復計劃**: 14 天內（視嚴重程度而定）

## 🎯 安全漏洞類型

我們特別關注以下類型的安全問題：

### 高嚴重性漏洞
- 遠端程式碼執行 (RCE)
- SQL 注入攻擊
- 驗證繞過
- 權限提升
- 敏感資料外洩

### 中嚴重性漏洞
- 跨站腳本攻擊 (XSS)
- 跨站請求偽造 (CSRF)
- 資訊揭露
- 拒絕服務攻擊 (DoS)
- 不安全的直接物件參考

### 低嚴重性漏洞
- 安全設定問題
- 密碼政策問題
- 記錄敏感資訊
- 缺乏速率限制

## 🛠️ 安全開發實踐

### 程式碼安全檢查

我們的開發流程包含以下安全措施：

```csharp
// 輸入驗證範例
public class UserController : ControllerBase
{
    [HttpPost]
    public async Task<IActionResult> CreateUser([FromBody] CreateUserRequest request)
    {
        // 輸入驗證
        if (!ModelState.IsValid)
            return BadRequest(ModelState);
            
        // 清理輸入資料
        var sanitizedRequest = _sanitizer.Sanitize(request);
        
        // 使用參數化查詢
        var user = await _userService.CreateUserAsync(sanitizedRequest);
        
        return Ok(user);
    }
}
```

### 安全設定

#### ASP.NET Core 安全標頭
```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    // 安全標頭
    app.UseHsts();
    app.UseHttpsRedirection();
    
    // CSP 設定
    app.Use(async (context, next) =>
    {
        context.Response.Headers.Add("Content-Security-Policy", 
            "default-src 'self'; script-src 'self' 'unsafe-inline'");
        context.Response.Headers.Add("X-Frame-Options", "DENY");
        context.Response.Headers.Add("X-Content-Type-Options", "nosniff");
        await next();
    });
}
```

#### 資料庫安全
```csharp
// 使用 Entity Framework 參數化查詢
public async Task<User> GetUserAsync(int id)
{
    return await _context.Users
        .Where(u => u.Id == id)
        .FirstOrDefaultAsync(); // 自動參數化
}

// 避免原始 SQL（如果必須使用，請使用參數）
public async Task<List<User>> SearchUsersAsync(string searchTerm)
{
    return await _context.Users
        .FromSqlRaw("SELECT * FROM Users WHERE Name LIKE {0}", $"%{searchTerm}%")
        .ToListAsync();
}
```

### 敏感資料處理

```csharp
// 設定檔加密
public class EncryptedConfigurationProvider : IConfigurationProvider
{
    public void Set(string key, string value)
    {
        if (IsSensitiveKey(key))
        {
            value = _encryptionService.Encrypt(value);
        }
        // 儲存設定...
    }
}

// 密碼雜湊
public class PasswordService
{
    public string HashPassword(string password)
    {
        return BCrypt.Net.BCrypt.HashPassword(password, 12);
    }
    
    public bool VerifyPassword(string password, string hash)
    {
        return BCrypt.Net.BCrypt.Verify(password, hash);
    }
}
```

## 🔍 安全測試

### 自動化安全掃描

我們使用以下工具進行安全掃描：

- **SAST (靜態分析)**: SonarQube, CodeQL
- **DAST (動態分析)**: OWASP ZAP
- **相依性掃描**: OWASP Dependency Check, Snyk
- **容器掃描**: Trivy, Clair

### 安全測試檢查清單

#### 開發階段安全檢查
- [ ] **輸入驗證**: 所有用戶輸入都經過驗證和清理
- [ ] **輸出編碼**: 防止 XSS 攻擊的輸出編碼
- [ ] **參數化查詢**: 使用 ORM 或參數化查詢防止 SQL 注入
- [ ] **認證機制**: 強密碼政策和多因素認證
- [ ] **授權檢查**: 適當的角色和權限控制
- [ ] **敏感資料**: 密碼雜湊和敏感資料加密
- [ ] **錯誤處理**: 避免洩露敏感系統資訊
- [ ] **記錄和監控**: 安全事件的完整記錄

#### 部署階段安全檢查
- [ ] **HTTPS 強制**: 所有通訊使用 TLS/SSL
- [ ] **安全標頭**: CSP、HSTS、X-Frame-Options 等
- [ ] **相依性掃描**: 檢查已知漏洞的套件
- [ ] **容器安全**: 最小化映像和非 root 用戶
- [ ] **網路安全**: 防火牆規則和網路分段
- [ ] **存取控制**: 最小權限原則
- [ ] **備份安全**: 加密備份和安全存取
- [ ] **監控設置**: 入侵檢測和異常監控

#### 自動化安全工具整合
```bash
# 靜態程式碼分析
dotnet sonarscanner begin /k:"project-key"
dotnet build
dotnet sonarscanner end

# 相依性漏洞掃描
dotnet list package --vulnerable
snyk test

# 程式碼品質和安全檢查
dotnet format --verify-no-changes
dotnet security-scan
```

## 📋 安全更新流程

### 發現漏洞後的處理流程

1. **確認和分類** (1-2 天)
   - 驗證漏洞真實性
   - 評估嚴重程度
   - 確定影響範圍

2. **開發修復** (3-14 天，視嚴重程度)
   - 設計安全修復
   - 實作修復程式碼
   - 進行安全測試

3. **發佈準備** (1-3 天)
   - 準備安全公告
   - 建立修復版本
   - 準備升級指南

4. **公開發佈**
   - 發佈修復版本
   - 公佈安全公告
   - 通知使用者升級

### 緊急安全修復

對於嚴重安全漏洞：

- **回應時間**: 24 小時內確認
- **修復時間**: 72 小時內發佈修復
- **通知機制**: 電子郵件、GitHub Security Advisory
- **向下相容**: 提供多版本修復

## 🏆 安全研究人員致謝

我們感謝以下安全研究人員的貢獻：

<!-- 當有安全研究人員提交有效的安全回報時，我們會在此列出 -->

### 致謝政策

對於負責任揭露安全漏洞的研究人員，我們提供：

- 公開致謝（如果研究人員同意）
- 詳細的回饋和後續追蹤
- 優先處理未來的安全回報

## 📊 安全指標

我們定期發佈安全指標報告：

- 平均修復時間
- 漏洞嚴重程度分佈
- 安全測試覆蓋率
- 相依性安全狀態

## 📚 安全資源

### 🏢 企業安全治理

#### 安全政策框架
- **資訊安全政策**: 組織層級的安全政策和程序
- **資料分類標準**: 敏感資料的分類和處理規範
- **存取控制政策**: 用戶權限和存取管理
- **事件回應計劃**: 安全事件的標準處理流程

#### 合規性和稽核
- **ISO 27001**: 資訊安全管理系統標準
- **SOC 2**: 服務組織控制報告
- **GDPR**: 歐盟一般資料保護規範
- **定期安全稽核**: 第三方安全評估

### 📖 內部安全文件

- [安全開發指南](docs/security-development.md) - 完整的安全開發生命週期
- [部署安全檢查清單](docs/deployment-security.md) - 生產環境安全配置
- [事件回應計劃](docs/incident-response.md) - 安全事件處理程序
- [威脅建模指南](docs/threat-modeling.md) - 系統威脅分析方法
- [安全程式碼審查](docs/security-code-review.md) - 程式碼安全審查標準

### 🌐 外部資源

#### 安全框架和標準
- [OWASP Top 10](https://owasp.org/www-project-top-ten/) - Web 應用程式安全風險
- [OWASP ASVS](https://owasp.org/www-project-application-security-verification-standard/) - 應用程式安全驗證標準
- [Microsoft 安全開發生命週期](https://www.microsoft.com/en-us/securityengineering/sdl)
- [.NET 安全指南](https://docs.microsoft.com/en-us/dotnet/standard/security/)

#### 威脅情報和研究
- [MITRE ATT&CK](https://attack.mitre.org/) - 威脅行為框架
- [CVE Database](https://cve.mitre.org/) - 已知漏洞資料庫
- [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework) - 網路安全框架

## 🔄 政策更新

此安全政策會定期審查和更新。重大變更將：

- 透過 GitHub 通知
- 在官方網站公佈
- 透過電子郵件通知註冊使用者

## 📞 聯絡資訊

**安全團隊:**
- 電子郵件: sen@utk.com.tw
- 緊急聯絡: sen@utk.com.tw
- 官方網站: [https://www.utk.com.tw/security](https://www.utk.com.tw/security)

**一般聯絡:**
- 一般查詢: sen@utk.com.tw
- GitHub: [@UTK-TW](https://github.com/UTK-TW)

---

**最後更新**: 2025年8月18日

感謝您協助保持我們軟體的安全性！🔒