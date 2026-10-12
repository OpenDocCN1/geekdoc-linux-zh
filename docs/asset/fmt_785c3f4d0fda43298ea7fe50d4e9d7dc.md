
## Ungoogled-Chromium

访问 `Ungoogled-Chromium` 官方网站 https://github.com/ungoogled-software/ungoogled-chromium 获取有关 `Ungoogled-Chromium` 的信息。

通过软件管理器获取 `DEB`/`FLATPAK` 软件包：
打开软件管理器并搜索 `Ungoogled-Chromium`。
点击 `Ungoogled-Chromium`，然后点击源选择框。
选择系统软件包或 `Flatpak` 并点击安装。

通过 `Flatpak` 安装 `Ungoogled-Chromium`：
在终端输入：

```
flatpak install flathub com.github.Eleston.UngoogledChromium
```

## Google Chrome

访问 `Google Chrome` 官方网站 https://www.google.com/intl/en_uk/chrome/ 获取有关 `Google Chrome` 的信息。

通过 `APT` 仓库安装 `Google Chrome`：
在终端输入以下命令：

```
sudo apt update
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
sudo apt update
sudo apt install google-chrome-stable
```

通过 `GUI` 从 `.deb` 安装 `Google Chrome`：
前往发布页面：
https://www.google.com/chrome/

- 点击下载
- 点击 64 位 `.deb`（适用于 `Debian`/`Ubuntu`）旁边的圆圈
- 点击“接受并安装”以下载 `Chrome`

进入 `~/Downloads`

双击 `google-chrome-stable_current_amd64.deb`

点击“安装”

## Microsoft Edge

访问 `Microsoft Edge` 官方网站 https://www.microsoft.com/en-us/edge 了解有关 `Microsoft Edge` 的所有信息。

通过终端中的 `APT` 存储安装 `Microsoft Edge`：

只需输入以下命令：

```
sudo apt update
```

```
sudo sh -c 'echo "deb [arch=amd64] http://packages.microsoft.com/repos/edge/ stable main" >> /etc/apt/sources.list.d/microsoft_edge.list'
```

```
sudo apt update
```

```
sudo apt install microsoft-edge-stable
```

通过图形用户界面使用 `.deb` 安装 `Microsoft Edge`：

转到发布页面：

https://www.microsoft.com/en-us/edge/download?form=MA13FJ

- 点击“接受并下载”以下载 `Microsoft Edge`

进入 `~/Downloads`

双击 `microsoft-edge-stable_122.0.2365.52-1_amd64.deb`

点击“安装”

## Thorium

访问 `Thorium` 官方网站 https://thorium.rocks/ 了解有关 `Thorium` 的所有信息。

通过图形用户界面使用 `.deb` 安装 `Thorium`：

转到发布页面：

https://github.com/Alex313031/thorium/releases

- 点击最新的 `thorium-browser_AVX2.deb` 下载 `Thorium`

进入 `~/Downloads`

双击 `thorium-browser_121.0.6167.204_AVX2.deb`

点击“安装”

## Vivaldi

访问 `Vivaldi` 官方网站 https://vivaldi.com/ 了解有关 `Vivaldi` 的所有信息。

通过终端中的 `APT` 存储安装 `Vivaldi`：

只需输入以下命令：

```
sudo apt update
wget https://repo.vivaldi.com/stable/linux_signing_key.pub
gpg --import linux_signing_key.pub
sudo sh -c 'echo "deb http://repo.vivaldi.com/stable/deb/ stable main" >> /etc/apt/sources.list.d/vivaldi.list'
sudo apt update
sudo apt install vivaldi-stable
```

通过图形用户界面使用 `.deb` 安装 `Vivaldi`：

转到下载页面：

https://vivaldi.com/download/?platform=linux

- 点击 `Vivaldi for Linux DEB` 下载 `Vivaldi`

进入 `~/Downloads`

双击 `vivaldi-stable_6.5.3206.63-1_amd64.deb`

点击“安装”

## Brave

访问 `Brave` 官方网站 https://brave.com/ 了解有关 `Brave` 的所有信息。

通过软件管理器获取 `DEB`/`FLATPAK` 包：

- 打开软件管理器并搜索 `Brave`。
- 点击 `Brave`，然后点击源选择框。
- 选择系统级包（`System Package`）或 `Flatpak`，并点击安装。

通过终端中的 `APT` 存储安装 `Brave`：

只需输入以下命令：

```
sudo apt update
```

```
sudo apt install curl
```

```
sudo curl -fSLO /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg
```

```
echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg] https://brave-browser-apt-release.s3.brave.com/ stable main"|sudo tee /etc/apt/sources.list.d/brave-browser-apt-release.list
```

```
sudo apt update
```

```
sudo apt install brave-browser
```

### 通过 Snap Store 获取 Snap 包

在 `Snap Store` 中查找 `Brave`。
点击 `Brave`，然后点击源选择框。
选择 `Snap` 下的最新/稳定版本并点击安装。

### 通过终端使用 Snap 安装 Brave

输入此命令：

```
sudo snap install brave
```

### 通过终端使用 Flatpak 安装 Brave

输入此命令：

```
flatpak install flathub com.brave.Browser
```

## Firefox

访问 `Firefox` 官方网站 https://www.mozilla.org/en-GB/firefox/new/ 了解有关 `Firefox` 的所有信息。

通过软件管理器获取 `DEB`/`FLATPAK` 包：

- 打开软件管理器并搜索 `Firefox`。
- 点击 `Firefox`，然后点击源选择框。
- 选择系统级包（`System Package`）或 `Flatpak`，并点击安装。

通过终端中的 `APT` 安装 `Firefox`：

只需输入以下命令：

```
sudo apt update
```

```
sudo apt install firefox
```

### 通过 Snap Store 获取 Snap 包

在 `Snap Store` 中查找 `Firefox`。
点击 `Firefox`，然后点击源选择框。
选择 `Snap` 下的最新/稳定版本并点击安装。

### 通过终端使用 Snap 安装 Firefox

输入此命令：

```
sudo snap install firefox
```

### 通过终端使用 Flatpak 安装 Firefox

输入此命令：
```
