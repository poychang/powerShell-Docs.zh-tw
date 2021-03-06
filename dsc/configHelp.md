---
ms.date: 06/12/2017
keywords: dsc,powershell,設定,安裝
title: 撰寫 DSC 設定的說明
ms.openlocfilehash: a4b5e688744b9a4519ce06d920ad8f11efeb99ad
ms.sourcegitcommit: e76665315fd928bf85210778f1fea2be15264fea
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/30/2018
ms.locfileid: "50225687"
---
# <a name="writing-help-for-dsc-configurations"></a>撰寫 DSC 設定的說明

>適用於：Windows PowerShell 5.0

您可以在 DSC 設定中，以註解方式呈現說明。 使用者可以呼叫設定函數加上 `-?`，或使用 [Get-Help](https://technet.microsoft.com/library/hh849696.aspx) Cmdlet 存取說明。 如需如何在 PowerShell 中，以註解方式呈現說明的詳細資訊，請參閱 [about_Comment_Based_Help](https://technet.microsoft.com/library/hh847834.aspx)。

下列範例顯示包含設定的指令碼及其註解說明︰

```powershell
<#
.SYNOPSIS
A brief description of the function or script. This keyword can be used only once for each configuration.


.DESCRIPTION
A detailed description of the function or script. This keyword can be used only once for each configuration.


.PARAMETER ComputerName
The description of a parameter. Add a .PARAMETER keyword for each parameter in the function or script syntax.

Type the parameter name on the same line as the .PARAMETER keyword. Type the parameter description on the lines following the .PARAMETER keyword.
Windows PowerShell interprets all text between the .PARAMETER line and the next keyword or the end of the comment block as part of the parameter description.
The description can include paragraph breaks.

The Parameter keywords can appear in any order in the comment block, but the function or script syntax determines the order in which the parameters
(and their descriptions) appear in help topic. To change the order, change the syntax.

.PARAMETER FilePath
Provide a PARAMETER section for each parameter that your script or function accepts.

.EXAMPLE
A sample command that uses the function or script, optionally followed by sample output and a description. Repeat this keyword for each example. If you have multiple examples,
there is no need to number them. PowerShell will number the examples in help text.

.EXAMPLE
This example will be labeled "EXAMPLE 2" when help is displayed to the user.
#>

configuration HelpSample1
{
    param([string]$ComputerName,[string]$FilePath)
    File f
    {
        Contents="Hello World"
        DestinationPath = "c:\Destination.txt"
    }
}
```

## <a name="viewing-configuration-help"></a>檢視設定說明

若要檢視設定的說明，請使用 **Get-help** Cmdlet 加上函數名稱，或輸入函數名稱加上 `-?`。 以下是將前一個函數傳遞給 **Get-help** 後的輸出：

```powershell
PS C:\> Get-Help HelpSample1

NAME
    HelpSample1

SYNOPSIS
    A brief description of the function or script. This keyword can be used only once for each configuration.


SYNTAX
    HelpSample1 [[-InstanceName] <String>] [[-DependsOn] <String[]>] [[-OutputPath] <String>] [[-ConfigurationData] <Hashtable>] [[-ComputerName]
    <String>] [[-FilePath] <String>] [<CommonParameters>]


DESCRIPTION
    A detailed description of the function or script. This keyword can be used only once for each configuration.


RELATED LINKS

REMARKS
    To see the examples, type: "get-help HelpSample1 -examples".
    For more information, type: "get-help HelpSample1 -detailed".
    For technical information, type: "get-help HelpSample1 -full".
```

## <a name="see-also"></a>另請參閱
* [DSC 設定](configurations.md)