---
ms.date: 06/05/2017
keywords: powershell,cmdlet
title: 使用登錄機碼
ms.assetid: 91bfaecd-8684-48b4-ad86-065dfe6dc90a
ms.openlocfilehash: a9d08f2f6b5803980dec45a4e266ad66879c8c8d
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2018
ms.locfileid: "30951693"
---
# <a name="working-with-registry-keys"></a>使用登錄機碼

因為登錄機碼是 Windows PowerShell 磁碟機上的項目，所以使用它們很像是使用檔案和資料夾。 最大的差別是登錄式 Windows PowerShell 磁碟機上的每個項目都是容器，就像檔案系統磁碟機上的資料夾。 不過，登錄項目及其相關值都是項目的屬性，而非不同的項目。

### <a name="listing-all-subkeys-of-a-registry-key"></a>列出登錄機碼所有的子機碼

您可以使用 **Get-ChildItem** 直接顯示登錄機碼內的所有項目。 加入選用的 **Force** 參數，以顯示隱藏或系統項目。 例如，這個命令會直接顯示 Windows PowerShell 磁碟機 HKCU: 內的項目，與 HKEY_CURRENT_USER 登錄區相對應︰

```
PS> Get-ChildItem -Path hkcu:\

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_CURRENT_USER

SKC  VC Name                           Property
---  -- ----                           --------
  2   0 AppEvents                      {}
  7  33 Console                        {ColorTable00, ColorTable01, ColorTab...
 25   1 Control Panel                  {Opened}
  0   5 Environment                    {APR_ICONV_PATH, INCLUDE, LIB, TEMP...}
  1   7 Identities                     {Last Username, Last User ...
  4   0 Keyboard Layout                {}
...
```

這些是在登錄編輯程式 (Regedit.exe) 中可看到的 HKEY_CURRENT_USER 的最上層機碼。

您也可以指定登錄提供者的名稱，後面加上 "**::**"，來指定這個登錄路徑。 登錄提供者的完整名稱是 **Microsoft.PowerShell.Core\\Registry**，但可以縮短到 **Registry**。 下列任一命令都會直接列出 HKCU 下的內容︰

```powershell
Get-ChildItem -Path Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Registry::HKCU
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKCU
Get-ChildItem HKCU:
```

這些命令只會列出直接包含的項目，很像使用 Cmd.exe 的 **DIR** 命令或 UNIX 殼層的 **ls**。 若要顯示包含的項目，您必須指定 **Recurse** 參數。 若要列出 HKCU 的所有登錄機碼，請使用下列命令 (這項作業可能耗費很長時間)︰

```powershell
Get-ChildItem -Path hkcu:\ -Recurse
```

**Get-ChildItem** 可以透過其 **Path**、**Filter**、**Include** 和 **Exclude** 參數執行複雜的篩選功能，但這些參數通常只以名稱為基礎。 您可以使用 **Where-Object** Cmdlet 根據項目的其他屬性來執行複雜的篩選。 下列命令會尋找 HKCU:\\Software 內，只有一個子機碼且僅有四個值的所有機碼︰

```powershell
Get-ChildItem -Path HKCU:\Software -Recurse | Where-Object -FilterScript {($_.SubKeyCount -le 1) -and ($_.ValueCount -eq 4) }
```

### <a name="copying-keys"></a>複製機碼

以 **Copy-Item** 完成複製。 下列命令會將 HKLM:\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion 及其所有屬性複製到 HKCU:\\，建立名為 "CurrentVersion" 的新機碼︰

```powershell
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu:
```

如果您使用登錄編輯程式或 **Get-ChildItem** 檢查這個新機碼，您會發現新位置沒有所包含子機碼的複本。 若要複製容器的所有內容，您必須指定 **Recurse** 參數。 若要讓上述的複製命令遞迴，您可以使用這個命令︰

```powershell
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu: -Recurse
```

您仍然可以使用現有的其他工具執行檔案系統複製作業。 您可以在 Windows PowerShell 中使用任何登錄編輯工具，包括 reg.exe、regini.exe、regedit.exe 和支援登錄編輯的 COM 物件 (如 WScript.Shell 和 WMI 的 StdRegProv 類別)。

### <a name="creating-keys"></a>建立機碼

在登錄中建立新機碼比在檔案系統中建立新項目簡單。 因為所有的登錄機碼都是容器，所以不需要指定項目類型，只要提供明確的路徑，例如︰

```powershell
New-Item -Path hkcu:\software_DeleteMe
```

您也可以使用提供者路徑來指定機碼︰

```powershell
New-Item -Path Registry::HKCU_DeleteMe
```

### <a name="deleting-keys"></a>刪除機碼

所有提供者的項目刪除作業本質上是相同的。 下列命令會以無訊息模式移除項目︰

```powershell
Remove-Item -Path hkcu:\Software_DeleteMe
Remove-Item -Path 'hkcu:\key with spaces in the name'
```

### <a name="removing-all-keys-under-a-specific-key"></a>移除特定機碼下的所有機碼

您可以使用 **Remove-Item** 移除包含的項目，但如果項目包含任何其他項目，系統會提示您確認移除。 例如，如果我們嘗試刪除之前建立的 HKCU:\\CurrentVersion 子機碼，我們會看到︰

```
Remove-Item -Path hkcu:\CurrentVersion

Confirm
The item at HKCU:\CurrentVersion\AdminDebug has children and the -recurse
parameter was not specified. If you continue, all children will be removed with
 the item. Are you sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

若要刪除包含的項目但不顯示提示，請指定 **-Recurse** 參數︰

```powershell
Remove-Item -Path HKCU:\CurrentVersion -Recurse
```

如果想要移除 HKCU:\\CurrentVersion 內的所有項目但保留 HKCU:\\CurrentVersion 本身，您可以改用︰

```powershell
Remove-Item -Path HKCU:\CurrentVersion\* -Recurse
```