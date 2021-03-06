---
ms.date: 06/12/2017
contributor: JKeithB
keywords: gallery,powershell,cmdlet,psgallery
title: 具有相容 PowerShell 版本的套件
ms.openlocfilehash: e16cfb0ee30e344c9399bec2985baafc5a252fd7
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2018
ms.locfileid: "50003707"
---
# <a name="packages-with-compatible-powershell-editions"></a>具有相容 PowerShell 版本的套件

從 5.1 版開始，PowerShell 提供代表各種功能集及平台相容性的不同版本。

- **Desktop Edition︰** 建置在 .NET Framework 上，與在完整使用量的 Windows 版本 (如 Server Core 和 Windows Desktop) 上執行之 PowerShell 版本的指令碼和模組相容。
- **Core Edition︰** 建置在 .NET Core 上，與在降低使用量的 Windows 版本 (如 Nano Server 和 Windows IoT) 上執行之 PowerShell 版本的指令碼和模組相容。

## <a name="powershell-gallery-extracts-supported-pseditions-metadata-and-allows-you-to-filters-the-packages-compatible-for-specific-powershell-editions"></a>PowerShell Gallery 會擷取支援的 PSEditions 中繼資料，並可讓您篩選與特定 PowerShell 版本相容的套件

如果套件已指定相容的 PSEditions，則 PSEditions 會列為套件顯示頁面和套件結果中「PowerShell 版本」的一部分。

![含有 PSEditions 的項目顯示網頁](../../Images/manual_package_download.png)

## <a name="search-for-packages-in-the-gallery-ui-which-works-on-powershellcore"></a>搜尋組件庫 UI 中適用於 PowerShellCore 的套件

使用 Tags:"PSEdition_Desktop" 和 Tags:"PSEdition_Core" 篩選 PowerShell Gallery 上的套件。

### <a name="use-tagspseditioncore-to-search-items-compatible-with-powershell-core-edition"></a>使用 Tags:"PSEdition_Core" 搜尋與 PowerShell Core 版本相容的項目。

![與 Core PSEdition 相容之項目的搜尋結果](../../Images/SearchResultsWithPSEditions.PNG)

### <a name="use-tagspseditiondesktop-to-search-items-compatible-with-powershell-desktop-edition"></a>使用 Tags:"PSEdition_Desktop" 搜尋與 PowerShell Desktop 版本相容的項目。

![與 Desktop PSEdition 相容之項目的搜尋結果](../../Images/SearchResultsWithPSEdition-Desktop.PNG)

## <a name="more-details-on-authoring-and-finding-the-packages-with-compatible-powershell-editions"></a>撰寫和尋找與 PowerShell 版本相容之套件的詳細資訊

- [PSEditions 的模組](../../concepts/module-psedition-support.md)
- [搭配 PSEditions 的指令碼](../../concepts/script-psedition-support.md)
