---
ms.date: 06/12/2017
keywords: dsc,powershell,設定,安裝
title: 設定 DSC 提取用戶端
ms.openlocfilehash: 7f8758bd7145518e30e9c28b74d0db5d74dfaab3
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2018
ms.locfileid: "34186655"
---
# <a name="setting-up-a-dsc-pull-client"></a>設定 DSC 提取用戶端

> 適用於：Windows PowerShell 4.0、Windows PowerShell 5.0

> [!IMPORTANT]
> 提取伺服器 (Windows 功能「DSC 服務」) 是支援的 Windows Server 元件，但未計劃提供新特性或功能。 建議開始將受控用戶端轉換為 [Azure 自動化 DSC](/azure/automation/automation-dsc-getting-started) (包括 Windows Server 上提取伺服器以外的功能)，或[此處](pullserver.md#community-solutions-for-pull-service)列出的其中一個社群解決方案。

必須告知每個目標節點使用提取模式和指定的 URL 或檔案位置，它可從中連絡提取伺服器以取得設定和資源，以及傳送報表資料。

下列主題說明如何設定提取用戶端：

* [使用設定名稱設定提取用戶端](pullClientConfigNames.md)
* [使用設定識別碼設定提取用戶端](pullClientConfigID.md)

> **注意**：這些主題適用於 PowerShell 5.0。 若要設定 PowerShell 4.0 中的提取用戶端，請參閱[使用 PowerShell 4.0 中的設定識別碼設定提取用戶端](pullClientConfigID4.md)。