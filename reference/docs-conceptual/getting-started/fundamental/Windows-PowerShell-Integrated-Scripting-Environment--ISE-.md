---
ms.date: 06/05/2017
keywords: powershell,cmdlet
title: Windows PowerShell 整合式指令碼環境 ISE
ms.assetid: f156b92d-0203-46d2-89c7-b4989d32e3d2
ms.openlocfilehash: d116ec107c2d07e9fd55ee974008b3636b4ab049
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2018
ms.locfileid: "30952064"
---
# <a name="windows-powershell-integrated-scripting-environment-ise"></a>Windows PowerShell 整合式指令碼環境 (ISE)

Windows PowerShell 整合式指令碼環境 (ISE) 是 Windows PowerShell 引擎和語言之兩部主機的其中一部。 您可以使用它，透過 Windows PowerShell 主控台中無法使用的方式來撰寫、執行和測試指令碼。 ISE 新增語法著色、Tab 鍵自動完成、IntelliSense、視覺化偵錯和即時線上說明。

ISE 可讓您在主控台窗格中執行命令，但也支援數個窗格，可用來同時檢視您的指令碼和可插入 ISE 之其他工具的原始碼。 您甚至可以同時開啟多個指令碼視窗，這在所偵錯的指令碼使用其他指令碼或模組中所定義的函式時特別有用。

## <a name="whats-new"></a>新功能

以下是一些已在最新版的 PowerShell ISE 中新增的功能。

### <a name="added-in-powershell-30-windows-server-2012-windows-8"></a>PowerShell 3.0 的新功能 (Windows Server 2012、Windows 8)

在您輸入文字時，**IntelliSense** 透過顯示與輸入文字相符的 Cmdlet、參數、參數值、檔案或資料夾的功能表，來自動完成命令。

**程式碼片段**是可輕鬆地插入所撰寫指令碼的簡短程式碼區段。 有用程式碼片段的集合包含在方塊中，而且使用 **New-Snippet** Cmdlet 可以有更多的程式碼片段。

**附加元件工具**可將功能新增至 ISE，藉由撰寫與 [Windows PowerShell ISE 指令碼物件模型](../../core-powershell/ise/The-ISE-Object-Model-Hierarchy.md)互動的程式碼即可建立。

這些工具可以在索引標籤式窗格中顯示控制項，或在背景無形地工作。 **命令**附加元件是不錯的範例，並包含 3.0 版和更新版本，會顯示可用命令的清單和其說明。

**重新啟動管理員和自動儲存**每兩分鐘會自動儲存您的指令碼，協助您避免在當機或意外重新啟動時遺失工作。

**[最近使用的清單]** 現在是 [開啟舊檔] 功能表的一部分，讓您更輕鬆地取得您最常使用的檔案。

**合併的主控台窗格**。 在舊版的 ISE 中，具有個別的 [命令] 和 [輸出] 窗格。 它們現在合併成單一窗格，更直接與您在 Windows Powershell 主控台中看到的內容相似。

**命令列參數**。 數個新的命令列參數可讓您更充分掌控 ISE 的運作方式。 -NoProfile 會啟動 ISE，但不執行設定檔指令碼。 -Help 會開啟含 ISE 的說明視窗。 -mta 會使用「多執行緒 Apartment 模式」啟動 ISE。 預設值是單一執行緒。

**新編輯器功能**可輕鬆地建立和讀取您的程式碼︰

- **XML 語法著色**。 ISE 編輯器現在將 XML 語法著色，方法與將 Windows PowerShell 程式碼語法著色相同。

- **括號對稱**。 Windows PowerShell ISE 會反白顯示對稱的括號，協助您確保左右括號數目相符。 使用 CTRL- \[ 找出與游標所在左括號對稱的右括號。

- **大綱檢視**。 您可以按一下左邊界的加號和減號，來摺疊或展開程式碼區段。 這可讓您更輕鬆地找到您要在長指令碼中尋找的程式碼。

- **拖放文字編輯**。 您可以選取某區塊的文字，並將它拖曳至另一個位置來移動它。 如果您在按住 Ctrl 鍵時拖曳選取的文字，則會進行複製，而不是移動。

- **剖析錯誤顯示**。 當您輸入時，Windows PowerShell 會檢查您的指令碼。 如果它偵測到錯誤，則會在違規程式碼下顯示紅色曲線。 暫留於指示的錯誤時，工具提示會顯示發現的問題。

- **縮放**。 您可以使用 ISE 視窗右下角的滑桿來放大文字以輕鬆地讀取，或縮小來查看較大的圖片。

- **RTF 複製與貼上**。 從 ISE 複製到剪貼簿時，會包括所選取文字的字型、大小和色彩資訊。

- **區塊選擇**。 在使用滑鼠選取指令碼窗格中的文字時按住 ALT 鍵或按 **Alt+Shift+方向鍵**，就可以選取一個區塊形狀的文字區塊。

### <a name="added-in-powershell-20-windows-server-2008-r2-windows-7"></a>PowerShell 2.0 的新功能 (Windows Server 2008 R2、Windows 7)

ISE 是在 PowerShell 2.0 版引進。

## <a name="requirements-for-running-the-windows-powershell-ise"></a>Windows PowerShell ISE 的執行需求

ISE 可以在任何可執行 Windows PowerShell 2.0 版或更新版本的 Windows 電腦上使用。 每個版本的 Windows 和 Windows Server 都包括某個版本的 Windows PowerShell 和 ISE，但您可以安裝 Windows Management Framework (WMF) 來升級到最新可用版本。 如需詳細資訊，請參閱 [WMF](/powershell/wmf/readme) 文件。

> [!NOTE]
> 因為 Windows PowerShell ISE 需要圖形化使用者介面，所以無法在 Windows Server 的 Server Core 選項上執行它。

## <a name="see-also"></a>另請參閱

[Windows PowerShell ISE 指令碼物件模型的用途](../../core-powershell/ise/Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)