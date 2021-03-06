---
ms.date: 06/12/2017
keywords: dsc,powershell,設定,安裝
title: DSC WindowsProcess 資源
ms.openlocfilehash: cee93ab283ded407d6e032161125aa6d6ac98827
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/26/2018
ms.locfileid: "39267952"
---
# <a name="dsc-windowsprocess-resource"></a>DSC WindowsProcess 資源

_適用於：Windows PowerShell 4.0、Windows PowerShell 5.0_

Windows PowerShell 預期狀態設定 (DSC) 的 **WindowsProcess** 資源提供了在目標節點設定程序的機制。

## <a name="syntax"></a>語法

```
WindowsProcess [string] #ResourceName
{
    Arguments = [string]
    Path = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ DependsOn = [string[]] ]
    [ StandardErrorPath = [string] ]
    [ StandardInputPath = [string] ]
    [ StandardOutputPath = [string] ]
    [ WorkingDirectory = [string] ]
}
```

## <a name="properties"></a>Properties

| 屬性 | 描述 |
| --- | --- |
| 引數| 表示要保持原狀傳遞至處理程序的引數字串。 如果需要傳遞數個引數，請將它們都放在這個字串裡。|
| 路徑| 處理程序可執行檔的路徑。 如果這是可執行檔的名稱 (不是完整路徑)，則 DSC 資源會搜尋環境 **Path** 變數 (`$env:Path`) 來尋找可執行檔。 如果這個屬性的值是完整路徑，DSC 不會使用 **Path** 環境變數尋找檔案，但若路徑不存在則會擲回錯誤。 不允許相對路徑。|
| 認證| 表示啟動處理程序的認證。|
| Ensure| 表示處理程序是否存在。 將這個屬性設定為 "Present" 以確保處理程序存在。 否則，請設定為 "Absent"。 預設值是 "Present"。|
| DependsOn | 表示必須先執行另一個資源的設定，再設定這個資源。 例如，如果第一個想要執行的資源設定指令碼區塊的識別碼是 **ResourceName**，而它的類型是 **ResourceType**，則使用這個屬性的語法就是 `DependsOn = "[ResourceType]ResourceName"`。|
| StandardErrorPath| 表示寫入標準錯誤的目錄路徑。 此處的所有檔案都會被覆寫。|
| StandardInputPath| 表示標準輸入的位置。|
| StandardOutputPath| 表示寫入標準輸出的位置。 此處的所有檔案都會被覆寫。|
| WorkingDirectory| 表示會用為處理程序目前工作目錄的位置。|