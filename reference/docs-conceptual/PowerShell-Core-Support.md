---
title: PowerShell Core 支援週期
description: 控管 PowerShell Core 支援的原則
ms.date: 08/06/2018
ms.openlocfilehash: 2e0ca1b9c133e6f316a40aff13365d0489059165
ms.sourcegitcommit: 01ac77cd0b00e4e5e964504563a9212e8002e5e0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2018
ms.locfileid: "39587154"
---
# <a name="powershell-core-support-lifecycle"></a>PowerShell Core 支援週期

PowerShell Core 是一組可以與 Windows PowerShell 分開出貨、安裝和設定的不同工具和元件。
因此，Windows 7/8.1/10 或 Windows Server 授權合約不包含 PowerShell Core。

不過，傳統 Microsoft 支援合約支援 PowerShell Core，包含 [Premier][]、[Microsoft 企業授權][enterprise-agreement]和[軟體保證權益][assurance]。
您也可以提出您問題的支援要求，付費獲得 PowerShell Core 的[輔助支援][]。

我們也會在您可提出問題、Bug 或功能要求的 GitHub 上提供[社群支援][]。
或者，您可能會在一般 [Microsoft Community][] 或 Microsoft [PowerShell Tech Community][] 上找到其他社群成員的協助。
我們不保證在該處會及時處理或解決您的問題。
如果您有需要立即注意的問題，則應該使用傳統付費支援選項。

## <a name="lifecycle-of-powershell-core"></a>PowerShell Core 生命週期

PowerShell Core 會採用 [Microsoft 現代化生命週期原則 ][modern]。
此支援生命週期是要保持客戶的最新版本最新資訊。

大約每六個月更新 PowerShell Core 6.x 版分支一次 (例如 6.0、6.1、6.2 等等)。

> [!IMPORTANT]
> 您必須在每個新次要版本發行之後的六個月內進行更新，才能持續接收支援。

例如，如果 PowerShell Core 6.1 是在 2018 年 7 月1 日發行，則必須在 2019 年 1 月 1 日之前更新至 PowerShell Core 6.1 以維護支援。

![PowerShell Core 分支生命週期][lifecycle-chart]

Modern 生命週期原則也需要 Microsoft 在中斷產品 (即 PowerShell Core) 支援之前的 12 個月通知客戶。

最後，我們預期 PowerShell Core 會採用僅需要服務和安全性更新的「長期服務」方式，保持特定 6.x 的分支/版本支援。

## <a name="supported-platforms"></a>支援的平台

請參閱下表，以了解您使用的 PowerShell Core 版本所正式支援的平台。

我們的社群也針對部分平台貢獻了套件，但這些套件未受正式支援。
這些套件在表格中標示為 `Community`。

列為 `Experimental` 的平台為非正式支援，但可用於實驗和提供意見反應。

|                                                   | 6.0         | 6.1         |
|---------------------------------------------------|:-----------:|:-----------:|
| Windows 7、8.1 和 10                            | 支援   | 支援   |
| Windows Server 2008 R2、2012 R2、2016             | 支援   | 支援   |
| [Windows Server 半年通道][semi-annual] | 支援   | 支援   |
| Ubuntu 14.04 和 16.04                           | 支援   | 支援   |
| Ubuntu 18.04                                      |             | 支援   |
| Ubuntu 18.10 (透過 Snap 套件)                   |             | 群體   |
| Debian 8.7+ 和 9                                | 支援   | 支援   |
| CentOS 7                                          | 支援   | 支援   |
| Red Hat Enterprise Linux 7                        | 支援   | 支援   |
| OpenSUSE 42.3                                     | 支援   | 支援   |
| Fedora 27                                         | 支援   | 支援   |
| Fedora 28                                         |             | 支援   |
| macOS 10.12+                                      | 支援   | 支援   |
| Arch                                              | 群體   | 群體   |
| Raspbian                                          | Experimental| 群體   |
| Kali                                              | 群體   | 群體   |
| AppImage (作用於多個 Linux 平台)     | 群體   | 群體   |
| [Snap 套件](https://snapcraft.io/powershell)   | 請參閱備註    | 請參閱備註    |

> [!NOTE]
> Snap 套件會有一段時間處於實驗階段。  之後，我們相信 Snap 就不會帶來新的支援問題，而支援會跟隨於您執行套件的發佈。

## <a name="platform-which-are-out-of-support"></a>支援終止的平台

當平台版本到達平台擁有者所定義的生命週期結束時，PowerShell Core 也會停止對該平台版本提供支援。 先前推出的套件仍然可供需要存取的客戶取得，但將不再提供任何類型的正式支援和更新。

因此，以下版本的支援已經由發行版本擁有者終止，且不受支援。

| 作業系統       | 版本 | 生命週期結束                                                                                 |
|----------|---------|---------------------------------------------------------------------------------------------|
| Fedora   | 24      | [2017 年 8 月](https://fedoramagazine.org/fedora-24-eol/)                                    |
| Fedora   | 25      | [2017 年 12 月](https://fedoramagazine.org/fedora-25-end-life/)                             |
| Fedora   | 26      | [2018 年 5 月](https://fedoramagazine.org/fedora-26-end-life/)                                  |
| openSUSE | 42.1    | [2017 年 5 月](https://lists.opensuse.org/opensuse-security-announce/2017-05/msg00053.html)     |
| openSUSE | 42.2    | [2018 年 1 月](https://lists.opensuse.org/opensuse-security-announce/2017-11/msg00066.html) |
| Ubuntu   | 16.10   | [2017 年 7 月](https://lists.ubuntu.com/archives/ubuntu-announce/2017-July/000223.html)        |
| Ubuntu   | 17.04   | [2018 年 1 月](https://lists.ubuntu.com/archives/ubuntu-announce/2018-January.txt)          |
| Ubuntu   | 17.10   | [2018 年 7 月](https://lists.ubuntu.com/archives/ubuntu-announce/2018-July/000232.html)        |

## <a name="notes-on-licensing"></a>授權附註

PowerShell Core 是透過 [MIT 授權][]所發行。
透過此授權，而且沒有付費支援合約，則使用者就只有[社群支援][]。
運用社群支援，Microsoft 不保證會回應或修正。

## <a name="windows-powershell-module"></a>Windows PowerShell 模組

除非其他產品模組明確支援 PowerShell Core，否則 PowerShell Core 支援不會延伸到這些模組。
例如，使用隨附為 Windows Server 一部分的 `ActiveDirectory` 模組，就是不支援的案例。

不過，在某些情況下，未明確支援 PowerShell Core 的模組可能會相容。
安裝 [`WindowsPSModulePath`][] 模組，即可將 Windows PowerShell `PSModulePath` 附加至 PowerShell Core `PSModulePath`。

首先，從 PowerShell 資源庫安裝 `WindowsPSModulePath` 模組：

```powershell
# Add `-Scope CurrentUser` if you're installing as non-admin
Install-Module WindowsPSModulePath -Force
```

安裝此模組之後，請執行 `Add-WindowsPSModulePath` Cmdlet，以將 Windows PowerShell `PSModulePath` 新增至 PowerShell Core：

```powershell
# Add this line to your profile if you always want Windows PowerShell PSModulePath
Add-WindowsPSModulePath
```

[Premier]: https://www.microsoft.com/en-us/microsoftservices/support.aspx
[enterprise-agreement]: https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx
[assurance]: https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx
[社群支援]: https://github.com/powershell/powershell/issues
[Microsoft Community]: https://answers.microsoft.com/
[PowerShell Tech Community]: https://techcommunity.microsoft.com/t5/PowerShell/ct-p/WindowsPowerShell
[輔助支援]: https://support.microsoft.com/assistedsupportproducts
[modern]: https://support.microsoft.com/help/30881/modern-lifecycle-policy
[lifecycle-chart]: ./images/modern-lifecycle.png
[semi-annual]: https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview
[MIT 授權]: https://github.com/PowerShell/PowerShell/blob/master/LICENSE.txt
[`WindowsPSModulePath`]: https://www.powershellgallery.com/packages/WindowsPSModulePath/
