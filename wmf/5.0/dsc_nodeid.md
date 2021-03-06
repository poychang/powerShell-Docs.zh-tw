---
ms.date: 06/12/2017
keywords: wmf,powershell,設定
ms.openlocfilehash: 6c036c2d8f97e559d20dd3ac40133fa06f5dab08
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2018
ms.locfileid: "34188280"
---
# <a name="separation-of-node-and-configuration-ids"></a>隔離節點和設定識別碼

## <a name="overview"></a>概觀

為了在 Pull 模式中使用 DSC 時提供更有彈性且有效率的體驗，我們在此版本中加入了多種功能。 這些功能可讓您更有彈性地輕鬆設定及部署跨多個節點的設定，同時仍然可以個別追蹤每個節點的狀態及報告資訊。
這些功能如下所示︰

* 用來識別電腦設定的設定名稱。 此名稱可由多個目標節點共用
* 可唯一識別單一節點的代理程式識別碼
* 只在目標節點第一次連線到提取伺服器時發生的註冊步驟

**注意︰** 這些功能已經加入，而且不會取代現有的提取功能和概念。 您可以使用這些新功能或具有此版本中發送之新提取伺服器的舊功能。

如需詳細資訊，請參閱[使用設定名稱設定提取用戶端](https://msdn.microsoft.com/powershell/dsc/pullclientconfignames)。
