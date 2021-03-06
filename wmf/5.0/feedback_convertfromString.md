---
ms.date: 06/12/2017
keywords: wmf,powershell,設定
ms.openlocfilehash: fcf2adf67f36edb534df3e2a849459fb20e1c2de
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892346"
---
# <a name="extract-and-parse-structured-objects-out-of-string"></a>從字串擷取和剖析結構化物件

本主題也將介紹 `ConvertFrom-String` Cmdlet 的一些額外功能：

- 預設情況下會移除範圍文字屬性， 您可以使用 IncludeExtent 參數將此屬性加入。

- 許多 MVP 和社群意見反應的學習演算法 Bug 修正。

- 新的 -UpdateTemplate 參數，可將學習演算法的結果儲存成範本檔案中的註解， 使得學習程序 (最慢的階段) 成為單次成本。 現在使用包含已編碼學習演算法的範本，幾乎可以瞬間執行 Convert-String。

## <a name="extract-and-parse-structured-objects-out-of-string-content"></a>從字串內容擷取和剖析結構化物件

在與 [Microsoft Research](https://www.microsoft.com/en-us/research/?from=http%3A%2F%2Fresearch.microsoft.com%2F) 合作之下，已新增 `ConvertFrom-String` Cmdlet。

這個 Cmdlet 支援兩種模式︰基本的分隔剖析和自動產生的範例驅動剖析。

根據預設，分隔的剖析將輸入從空白字元位置分割，並將屬性名稱指派給產生的群組。 您可以自訂分隔符號︰

```powershell
"Hello World" | ConvertFrom-String | Format-Table -Auto
```

```output
P1     P2
--     --
Hello  World
```

此 Cmdlet 也會根據 [Microsoft Research](https://www.microsoft.com/en-us/research/?from=http%3A%2F%2Fresearch.microsoft.com%2F) 中的 [FlashExtract](https://www.microsoft.com/en-us/research/publication/flashextract-framework-data-extraction-examples/?from=http%3A%2F%2Fresearch.microsoft.com%2Fen-us%2Fum%2Fpeople%2Fsumitg%2Fflashextract.html) 研究工作，支援自動產生範例驅動剖析。

若要開始，請考慮使用以文字為基礎的通訊錄︰

```
    Ana Trujillo

    Redmond, WA

    Antonio Moreno

    Renton, WA

    Thomas Hardy

    Seattle, WA

    Christina Berglund

    Redmond, WA

    Hanna Moos

    Puyallup, WA
```

將幾個範例複製到要作為範本使用的檔案中︰

```
    Ana Trujillo

    Redmond, WA

    Antonio Moreno

    Renton, WA
```

以大括號括住您想要擷取的資料，在這麼做的時候，提供一個名稱。 因為 **Name** 屬性 (和與其相關聯的其他屬性) 可以出現多次，所以請使用星號 (\*)，表示這會產生多筆記錄 (而非將一大堆內容擷取成一個記錄)︰

```
    {Name\*:Ana Trujillo}

    {City:Redmond}, {State:WA}

    {Name\*:Antonio Moreno}

    {City:Renton}, {State:WA}
```

在這組範例中，`ConvertFrom-String` 現在可以自動從輸入檔擷取具類似結構且以物件為基礎的輸出。

```powershell
Get-Content .\addresses.output.txt | ConvertFrom-String -TemplateFile .\addresses.template.txt | Format-Table -Auto
```

```output
ExtentText                     Name               City     State
----------                     ----               ----     -----
Ana Trujillo...                Ana Trujillo       Redmond  WA
Antonio Moreno...              Antonio Moreno     Renton   WA
Thomas Hardy...                Thomas Hardy       Seattle  WA
Christina Berglund...          Christina Berglund Redmond  WA
Hanna Moos...                  Hanna Moos         Puyallup WA
```

若要在擷取的文字上執行其他資料操作，**ExtentText** 屬性可從擷取記錄中擷取未經處理的文字。 若要提供這項功能的意見反應，或共用您在撰寫時遇到困難的範例內容，請寄電子郵件至 <psdmfb@microsoft.com>。