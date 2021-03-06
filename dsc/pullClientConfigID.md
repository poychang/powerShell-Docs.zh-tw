---
ms.date: 06/12/2017
keywords: dsc,powershell,設定,安裝
title: 使用設定識別碼設定提取用戶端
ms.openlocfilehash: b4a45c4d014b3c4fc0140ad492f81474b260065a
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2018
ms.locfileid: "34187488"
---
# <a name="setting-up-a-pull-client-using-configuration-id"></a>使用設定識別碼設定提取用戶端

> 適用於：Windows PowerShell 5.0

> [!IMPORTANT]
> 提取伺服器 (Windows 功能「DSC 服務」) 是支援的 Windows Server 元件，但未計劃提供新特性或功能。 建議開始將受控用戶端轉換為 [Azure 自動化 DSC](/azure/automation/automation-dsc-getting-started) (包括 Windows Server 上提取伺服器以外的功能)，或[此處](pullserver.md#community-solutions-for-pull-service)列出的其中一個社群解決方案。

必須告知每個目標節點使用提取模式和指定的 URL，其中它可連絡提取伺服器以取得設定。 若要這樣做，您必須使用必要的資訊來設定本機設定管理員 (LCM)。 若要設定 LCM，必須先建立一種特殊設定，再加上 **DSCLocalConfigurationManager** 屬性裝飾。 如需設定 LCM 的詳細資訊，請參閱[設定本機設定管理員](metaConfig.md)。

> **注意**：本主題適用於 PowerShell 5.0。 如需設定 PowerShell 4.0 中提取用戶端的資訊，請參閱[在 PowerShell 4.0 中使用設定識別碼設定提取用戶端](pullClientConfigID4.md)。

下列指令碼會設定 LCM 從名為 "CONTOSO-PullSrv" 的伺服器提取設定。

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'

        }
    }
}
PullClientConfigID
```

在此指令碼中，**ConfigurationRepositoryWeb** 區塊會定義提取伺服器。 **ServerURL**

執行這個指令碼之後，它會建立新的輸出資料夾，名為 **PullClientConfigID**，並在該處放入中繼設定 MOF 檔案。 在此情況下，中繼設定 MOF 檔案將名為 `localhost.meta.mof`。

若要套用設定，請呼叫 **Set-DscLocalConfigurationManager** Cmdlet，其中 **Path** 設為中繼設定 MOF 檔案的位置。 例如：`Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigID –Verbose.`

## <a name="configuration-id"></a>設定識別碼

此指令碼將 LCM 的 **ConfigurationID** 屬性設為先前針對這個用途建立的 GUID (您可以透過 **New-Guid** Cmdlet 建立 GUID)。 **ConfigurationID** 供 LCM 用來在提取伺服器上尋找適當設定。 提取伺服器上的設定 MOF 檔案必須命名為 _ConfigurationID_.mof，其中 _ConfigurationID_ 是目標節點 LCM 的 **ConfigurationID** 屬性值。

## <a name="smb-pull-server"></a>SMB 提取伺服器

若要設定用戶端從 SMB 伺服器提取設定，請使用 **ConfigurationRepositoryShare** 區塊。 在 **ConfigurationRepositoryShare** 區塊中，您可以設定 **SourcePath** 屬性指定伺服器的路徑。 下列中繼設定會設定目標節點從名為 **SMBPullServer** 的 SMB 提取伺服器提取。

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryShare SMBPullServer
        {
            SourcePath = '\\SMBPullServer\PullSource'

        }
    }
}
PullClientConfigID
```

## <a name="resource-and-report-servers"></a>資源和報表伺服器

如果在 LCM 設定中只指定了 **ConfigurationRepositoryWeb** 或 **ConfigurationRepositoryShare** 區塊 (如上述範例所示)，提取用戶端將會從指定的伺服器提取資源，但不會將報表傳送給伺服器。 您可以針對設定、資源和報告使用單一提取伺服器，但必須建立 **ReportRepositoryWeb** 區塊才可設定報告功能。

下列範例示範中繼設定，該中繼設定會設定用戶端以提取設定和資源，並將報告資料傳送至單一提取伺服器。

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'

        }


        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
        }
    }
}
PullClientConfigID
```

您也可以對資源和報告指定不同的提取伺服器。 若要指定資源伺服器，您可使用 **ResourceRepositoryWeb** (適用於 Web 提取伺服器) 或 **ResourceRepositoryShare** 區塊 (適用於 SMB 提取伺服器)。
若要指定報表伺服器，您可使用 **ReportRepositoryWeb** 區塊。 報表伺服器不得為 SMB 伺服器。
下列中繼設定會設定提取用戶端從 **CONTOSO-PullSrv** 取得其設定，並從 **CONTOSO-ResourceSrv** 取得其資源，然後傳送狀態報表給 **CONTOSO-ReportSrv**：

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'

        }

        ResourceRepositoryWeb CONTOSO-ResourceSrv
        {
            ServerURL = 'https://CONTOSO-REsourceSrv:8080/PSDSCPullServer.svc'
        }

        ReportServerWeb CONTOSO-ReportSrv
        {
            ServerURL = 'https://CONTOSO-REsourceSrv:8080/PSDSCPullServer.svc'
        }
    }
}
PullClientConfigID
```

## <a name="see-also"></a>另請參閱

* [以設定名稱設定提取用戶端](pullClientConfigNames.md)