---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "dsc,powershell,設定,安裝"
title: "巢狀設定"
ms.openlocfilehash: 4de53b94056df46d74923dda56e02841cfac2cd1
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2017
---
# <a name="nesting-dsc-configurations"></a><span data-ttu-id="1773c-103">巢狀 DSC 設定</span><span class="sxs-lookup"><span data-stu-id="1773c-103">Nesting DSC configurations</span></span>

<span data-ttu-id="1773c-104">巢狀設定 (也稱為複合設定) 是在另一個設定中將它當成資源般呼叫的設定。</span><span class="sxs-lookup"><span data-stu-id="1773c-104">A nested configuration (also called composite configuration) is a configuration that is called within another configuration as if it were a resource.</span></span>
<span data-ttu-id="1773c-105">這兩個設定必須定義在同一個檔案中。</span><span class="sxs-lookup"><span data-stu-id="1773c-105">Both configurations must be defined in the same file.</span></span>

<span data-ttu-id="1773c-106">讓我們看一個簡單範例：</span><span class="sxs-lookup"><span data-stu-id="1773c-106">Let's look at a simple example:</span></span>

```powershell
Configuration FileConfig 
{
    param (
        [Parameter(Mandatory = $true)]
        [String] $CopyFrom,

        [Parameter(Mandatory = $true)]
        [String] $CopyTo
    )

    Import-DscResource -ModuleName PSDesiredStateConfiguration

    File FileTest
       {
           SourcePath = $CopyFrom
           DestinationPath = $CopyTo
           Ensure = 'Present'
       }
    
}

Configuration NestedFileConfig
{
    Node localhost
    {
        FileConfig NestedConfig
        {
            CopyFrom = 'C:\Test\TestFile.txt'
            CopyTo = 'C:\Test2'
        }
    }
}
```

<span data-ttu-id="1773c-107">在此範例中，`FileConfig` 採用兩個必要參數 **CopyFrom** 和 **CopyTo**，這兩個參數是用來做為 `File` 資源區塊中**SourcePath** 和 **DestinationPath** 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="1773c-107">In this example, `FileConfig` takes two mandatory parameters,  **CopyFrom** and **CopyTo**, which are used as the values for the **SourcePath** and **DestinationPath** properties in the `File` resource block.</span></span> <span data-ttu-id="1773c-108">`NestedConfig` 設定會將 `FileConfig` 當成資源般來呼叫。</span><span class="sxs-lookup"><span data-stu-id="1773c-108">The `NestedConfig` configuration calls `FileConfig` as if it were a resource.</span></span>
<span data-ttu-id="1773c-109">`NestedConfig` 資源區塊中的屬性 (**CopyFrom** 和 **CopyTo**) 是 `FileConfig` 設定的參數。</span><span class="sxs-lookup"><span data-stu-id="1773c-109">The properties in the `NestedConfig` resource block (**CopyFrom** and **CopyTo**) are the parameters of the `FileConfig` configuration.</span></span>

## <a name="see-also"></a><span data-ttu-id="1773c-110">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1773c-110">See Also</span></span>

- [<span data-ttu-id="1773c-111">複合資源 -- 把 DSC 設定當做資源使用</span><span class="sxs-lookup"><span data-stu-id="1773c-111">Composite resources--Using a DSC configuration as a resource</span></span>](authoringResourceComposite.md)
