---
ms.date: 06/12/2017
keywords: dsc,powershell,設定,安裝
title: MSFT_DSCLocalConfigurationManager 類別的 ResourceGet 方法
ms.openlocfilehash: 1b74adf2327af2e0f9416f1d00eac4e3b75e9013
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893200"
---
# <a name="resourceget-method-of-the-msftdsclocalconfigurationmanager-class"></a>MSFT_DSCLocalConfigurationManager 類別的 ResourceGet 方法

直接呼叫 DSC 資源的 **Get** 方法。

## <a name="syntax"></a>語法

```mof
uint32 ResourceGet(
  [in]  string           ResourceType,
  [in]  string           ModuleName,
  [in]  uint8            resourceProperty[],
  [out] OMI_BaseResource configurations
);
```

## <a name="parameters"></a>參數

*ResourceType* \[in\] 要呼叫的資源名稱。

*ModuleName* \[in\] 包含要呼叫之資源的模組名稱。

*resourceProperty* \[in\] 在雜湊表中指定資源的屬性名稱與其值，分別作為索引鍵和值。 使用 [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) Cmdlet，探索資源的屬性和其類型。

*configurations* \[out\] 傳回時，包含設定的內嵌執行個體。

## <a name="return-value"></a>傳回值

若成功即傳回零；否則傳回錯誤碼。

## <a name="remarks"></a>備註

此為靜態方法。

## <a name="requirements"></a>需求

**MOF：** DscCore.mof

**Namespace**：Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>另請參閱

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)