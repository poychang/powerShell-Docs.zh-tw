---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,設定
title: WMF 5.1 的新案例和功能
ms.openlocfilehash: b00069aad7422f86d1462a62a6c4bc8a91e46705
ms.sourcegitcommit: 50b66cada6943784b8d3c103cebc3c1e3e286a16
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090358"
---
# <a name="new-scenarios-and-features-in-wmf-51"></a>WMF 5.1 的新案例和功能

> 注意：本資訊尚屬初始版本，後續有可能變更。

## <a name="powershell-editions"></a>PowerShell 版本

從 5.1 版開始，PowerShell 提供代表各種功能集和平台相容性的不同版本。

- **Desktop Edition︰** 建置在 .NET Framework 上，與在完整使用量的 Windows 版本 (如 Server Core 和 Windows Desktop) 上執行之 PowerShell 版本的指令碼和模組相容。
- **Core Edition︰** 建置在 .NET Core 上，與在降低使用量的 Windows 版本 (如 Nano Server 和 Windows IoT) 上執行之 PowerShell 版本的指令碼和模組相容。

**深入了解使用 PowerShell 版本**

- [使用 PSVersionTable 來判斷執行的 PowerShell 版本](/powershell/module/microsoft.powershell.core/about/about_automatic_variables)
- [使用 PSEdition 參數並依據 CompatiblePSEditions 篩選 Get-Module 結果](/powershell/module/microsoft.powershell.core/get-module)
- [只有在相容的 PowerShell 版本上執行才會執行指令碼](/powershell/gallery/concepts/script-psedition-support)
- [宣告特定 PowerShell 版本的模組相容性](/powershell/gallery/concepts/module-psedition-support)

## <a name="catalog-cmdlets"></a>類別目錄 Cmdlet

[Microsoft.PowerShell.Security](/powershell/module/microsoft.powershell.security) 模組中新增了兩個新的 Cmdlet，它們會產生和驗證 Windows 類別目錄檔案。

### <a name="new-filecatalog"></a>New-FileCatalog
--------------------------------

New-FileCatalog 會建立 Windows 類別目錄檔案，供資料夾和檔案集合使用。
此類別目錄檔案包含指定路徑中的所有檔案雜湊。
使用者可以散發資料夾集合以及代表這些資料夾的對應類別目錄檔案。
這項資訊對驗證資料夾在類別目錄建立後是否有任何變更，非常有用。

```powershell
New-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-CatalogVersion <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

支援類別目錄第 1 版和第 2 版。
第 1 版使用 SHA1 雜湊演算法建立檔案雜湊，第 2 版使用 SHA256。
*Windows Server 2008 R2* 或 *Windows 7* 不支援第 2 版的類別目錄。
*Windows 8*、*Windows Server 2012* 和更新版本的作業系統，應該使用類別目錄第 2 版。

![](../images/NewFileCatalog.jpg)

這會建立類別目錄檔案。

![](../images/CatalogFile1.jpg)

![](../images/CatalogFile2.jpg)

若要驗證類別目錄檔案 (上例中為 Pester.cat) 的完整性，請使用 [Set-AuthenticodeSignature](/powershell/module/Microsoft.PowerShell.Security/Set-AuthenticodeSignature) Cmdlet 來加以簽署。

### <a name="test-filecatalog"></a>Test-FileCatalog
--------------------------------

Test-FileCatalog 會驗證代表資料夾集合的類別目錄。

```powershell
Test-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-Detailed] [-FilesToSkip <string[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

![](../images/TestFileCatalog.jpg)

此 Cmdlet 會比較所有的檔案雜湊及在 *catalog* 和 *disk* 中找到的相對路徑。
如果檔案雜湊和路徑中偵測到任何不相符的項目，就會傳回 *ValidationFailed* 狀態。
使用者可以使用 *-Detailed* 參數來擷取此資訊的完整內容。
它也會在 *Signature* 屬性中顯示類別目錄的簽署狀態，和呼叫 [Get-AuthenticodeSignature](/powershell/module/Microsoft.PowerShell.Security/Get-AuthenticodeSignature) Cmdlet 一模一樣。
使用者也可以使用 *-FilesToSkip* 參數，在驗證期間略過任何檔案。

## <a name="module-analysis-cache"></a>模組分析快取

從 WMF 5.1 開始，PowerShell 可以控制快取模組資料所用的檔案，例如匯出的命令。

此快取預設儲存在 `${env:LOCALAPPDATA}\Microsoft\Windows\PowerShell\ModuleAnalysisCache` 檔案中。
快取一般在啟動同時搜尋命令時讀取，並在模組匯入一段時間後寫入背景執行緒。

若要變更快取的預設位置，請先設定環境變數 `$env:PSModuleAnalysisCachePath` 再啟動 PowerShell。
此環境變數的變更只會影響子處理程序。
該值應該命名 PowerShell 有權建立和寫入檔案的完整路徑 (包括檔名)。
若要停用檔案快取，請將此值設定於無效的位置，例如︰

```powershell
$env:PSModuleAnalysisCachePath = 'nul'
```

這會將路徑設定到無效的裝置。
如果 PowerShell 無法寫入該路徑，就不會傳回任何錯誤，但您可以藉由使用追蹤查看錯誤報告︰

```powershell
Trace-Command -PSHost -Name Modules -Expression { Import-Module Microsoft.PowerShell.Management -Force }
```

寫出快取時，PowerShell 會檢查確認模組已不存在，避免不必要的大型快取。
有時候不需要這些檢查，在此情況下，您可以透過設定下列項目關閉這些檢查：

```powershell
$env:PSDisableModuleAnalysisCacheCleanup = 1
```

此環境變數設定會立即在目前的程序中生效。

## <a name="specifying-module-version"></a>指定模組版本

在 WMF 5.1 中，`using module` 與 PowerShell 中其他模組相關的語法結構表現一致。
以往，您無法指定特定的模組版本；如果有多個版本存在，這會導致錯誤。

在 WMF 5.1 中：

- 您可以使用 [ModuleSpecification 建構函式 (雜湊表)](/dotnet/api/microsoft.powershell.commands.modulespecification.-ctor?view=powershellsdk-1.1.0#Microsoft_PowerShell_Commands_ModuleSpecification__ctor_System_Collections_Hashtable_)。
此雜湊表與 `Get-Module -FullyQualifiedName` 的格式相同。

**範例：**`using module @{ModuleName = 'PSReadLine'; RequiredVersion = '1.1'}`

- 如果模組有多個版本，PowerShell 會使用與 `Import-Module` **相同的解析邏輯**，不傳回錯誤，和 `Import-Module` 及 `Import-DscResource` 的行為一樣。

## <a name="improvements-to-pester"></a>Pester 的改善

在 WMF 5.1 中，PowerShell 隨附的 Pester 版本已從 3.3.5 更新至 3.4.0 並附帶認可 https://github.com/pester/Pester/pull/484/commits/3854ae8a1f215b39697ac6c2607baf42257b102e，讓 Pester 在 Nano 伺服器上有更好的表現。

您可以調查 ChangeLog.md 檔案來檢視 3.3.5 版到 3.4.0 版之間的變更，位置在：https://github.com/pester/Pester/blob/master/CHANGELOG.md
