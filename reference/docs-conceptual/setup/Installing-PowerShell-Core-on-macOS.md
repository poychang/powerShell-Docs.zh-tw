---
title: 在 macOS 上安裝 PowerShell Core
description: 在 macOS 上安裝 PowerShell Core 的相關資訊
ms.date: 11/02/2018
ms.openlocfilehash: 162e841bf71d708e9db84ea1bb2dbef13924783b
ms.sourcegitcommit: f4247d3f91d06ec392c4cd66921ce7d0456a2bd9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2018
ms.locfileid: "50998498"
---
# <a name="installing-powershell-core-on-macos"></a>在 macOS 上安裝 PowerShell Core

PowerShell Core 支援 macOS 10.12 和更版本。
GitHub [版本][]頁面上提供所有套件。
安裝套件之後，請從終端機執行 `pwsh`。

## <a name="about-brew"></a>關於 Brew

[Homebrew][ brew] 是 macOS 首選的套件管理員。
如果找不到 `brew` 命令，您需要遵循[指示][brew]安裝 Homebrew。

## <a name="installation-of-latest-stable-release-via-homebrew-on-macos-1012-or-higher"></a>在 macOS 10.12 或更高版本上透過 Homebrew 安裝最新的穩定版本

如需 Brew 的相關資訊，請參閱[關於 Brew](#about-brew)。

現在，您可以安裝 PowerShell：

```sh
brew cask install powershell
```

最後，確認您的安裝可以正常執行：

```sh
pwsh
```

發行新的 PowerShell 版本時，只要更新 Homebrew 的公式並升級 PowerShell 即可：

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> 您可從 PowerShell (pwsh) 主機內呼叫上命令，但必須結束並重新啟動 PowerShell 殼層，才能完成升級並重新整理 $PSVersionTable 中顯示的值。

[brew]: http://brew.sh/

## <a name="installation-of-latest-preview-release-via-homebrew-on-macos-1012-or-higher"></a>在 macOS 10.12 或更高版本上透過 Homebrew 安裝最新的預覽版本

如需 Brew 的相關資訊，請參閱[關於 Brew](#about-brew)。

安裝好 Homebrew 之後，安裝 PowerShell 就很容易。
首先，安裝 [Cask 版本][cask-versions]，這可讓您安裝 Cask 套件的替代版本：

```sh
brew tap homebrew/cask-versions
```

現在，您可以安裝 PowerShell：

```sh
brew cask install powershell-preview
```

最後，確認您的安裝可以正常執行：

```sh
pwsh-preview
```

發行新的 PowerShell 版本時，只要更新 Homebrew 的公式並升級 PowerShell 即可：

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> 上述命令可從 PowerShell (pwsh) 主機內呼叫，但 PowerShell 殼層必須結束並重新啟動，才能完成升級。
> 並重新整理 $PSVersionTable 中顯示的值。

## <a name="installation-via-direct-download"></a>透過直接下載來安裝

將 PKG 套件 `powershell-6.1.0-osx-x64.pkg`
從[版本][]頁面下載到您的 macOS 電腦。

您可以按兩下檔案並依照提示執行作業，或從終端機安裝：

```sh
sudo installer -pkg powershell-6.1.0-osx-x64.pkg -target /
```

安裝 [OpenSSL](#install-openssl)，因為 PowerShell 遠端執行功能與 CIM 作業需要它。

## <a name="binary-archives"></a>二進位封存

macOS 平台有 PowerShell 二進位 `tar.gz` 封存，以啟用進階的部署案例。

### <a name="installing-binary-archives-on-macos"></a>解除安裝 macOS 上的二進位封存

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-osx-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /usr/local/microsoft/powershell/6.1.0

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /usr/local/microsoft/powershell/6.1.0

# Set execute permissions
sudo chmod +x /usr/local/microsoft/powershell/6.1.0/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /usr/local/microsoft/powershell/6.1.0/pwsh /usr/local/bin/pwsh
```

安裝 [OpenSSL](#install-openssl)，因為 PowerShell 遠端執行功能與 CIM 作業需要它。

## <a name="installing-dependencies"></a>安裝相依性

### <a name="install-xcode-command-line-tools"></a>安裝 XCode 命令列工具

```shell
xcode-select -install
```

### <a name="install-openssl"></a>安裝 OpenSSL

PowerShell 遠端執行功能與 CIM 作業需要 OpenSSL。  您可以透過 MacPorts 或 Brew 來安裝。

#### <a name="install-openssl-via-brew"></a>透過 Brew 安裝 OpenSSL

如需 Brew 的相關資訊，請參閱[關於 Brew](#about-brew)。

執行 `brew install openssl` 以安裝 OpenSSL。

#### <a name="install-openssl-via-macports"></a>透過 MacPorts 安裝 OpenSSL

1. 安裝 [XCode 命令列工具](#install-xcode-command-line-tools)
1. 安裝 MacPorts。
   若需要指示，請參閱[安裝指南](https://guide.macports.org/chunked/installing.macports.html)。
1. 透過執行 `sudo port selfupdate` 以更新 MacPorts
1. 透過執行 `sudo port upgrade outdated` 以升級 MacPorts 套件
1. 透過執行 `sudo port instal openssl` 以安裝 OpenSSL
1. 連結到程式庫，以便 PowerShell 可以使用它。

```shell
sudo mkdir -p /usr/local/opt/openssl
sudo ln -s /opt/local/lib /usr/local/opt/openssl/lib
```

## <a name="uninstalling-powershell-core"></a>解除安裝 PowerShell Core

如果您使用 Homebrew 安裝 PowerShell，解除安裝很簡單：

```sh
brew cask uninstall powershell
```

如已透過直接下載安裝 PowerShell，即必須手動移除 PowerShell：

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

若要解除安裝其他的 PowerShell 路徑，請參閱本文件中的[路徑](#paths)一節，使用 `sudo rm` 移除所要的路徑。

> [!NOTE]
> 如果使用 Homebrew 安裝，此即非必要。

## <a name="paths"></a>路徑

* `$PSHOME` 是 `/usr/local/microsoft/powershell/6.1.0/`
* 會從 `~/.config/powershell/profile.ps1` 讀取使用者設定檔
* 會從 `$PSHOME/profile.ps1` 讀取預設設定檔
* 會從 `~/.local/share/powershell/Modules` 讀取使用者模組
* 會從 `/usr/local/share/powershell/Modules` 讀取共用的模組
* 會從 `$PSHOME/Modules` 讀取預設模組
* PSReadline 記錄會記錄在 `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`

設定檔會採用 PowerShell 的每個主機設定。
因此預設主機特定設定檔便會存在於相同位置的 `Microsoft.PowerShell_profile.ps1`。

PowerShell 遵循 macOS 上的 [XDG 基底目錄規格][xdg-bds]。

因為 macOS 是 BSD 的衍生項，所以使用的前置詞是 `/usr/local` 而非 `/opt`。
因此，`$PSHOME` 是 `/usr/local/microsoft/powershell/6.1.0/`，而符號連結放置在 `/usr/local/bin/pwsh`。

## <a name="additional-resources"></a>其他資源

* [Homebrew Web][brew]
* [Homebrew Github 存放庫][GitHub]
* [Homebrew-Cask][cask]

[brew]: http://brew.sh/
[Cask]: https://github.com/Homebrew/homebrew-cask
[cask-versions]: https://github.com/Homebrew/homebrew-cask-versions
[GitHub]: https://github.com/Homebrew
[版本]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
