
- Select **System ▸ Administration ▸ Software Sources**. Enter your password if asked, and then click the **Other Software** tab in the Software Sources window that appears.

- Click **Add**. You'll be prompted to enter the APT line, so paste it into the box, and then click **Add Source** (Figure 6-7). A new entry should appear in the Other Source list.

- Select the **Authentication** tab, and click **Import Key File**. Use the window that appears to find the `.key` file you downloaded earlier. (It's probably in your Downloads folder.)

- Select the `.key*` file by clicking it once, and then click **OK**. Check the list of trusted software providers to make sure that the GetDeb Automatic Signing Key is now present, as it is in Figure 6-8.

# Enter the complete APT line of the repository that you want to add as source

The APT line includes the type, location and components of a repository, for example `deb http://archive.ubuntu.com/ubuntu lucid main`.

```
APT line: deb http://archive.getdeb.net/ubuntu-lucid-getdeb-apps
```

Figure 6-7: Entering the APT line for the GetDeb repository

![](img/58abec7ac6c22ade6357fd77ea421da3_123_0.png)

Figure 6-8: Checking the list of trusted software providers to see whether the GetDeb key is there

- 5. Close the Software Sources window. You'll be told that the information about available software is outdated, so click Reload to fetch the most recent package information. It might take a little while to download.

- 6. Open the Ubuntu Software Center (or close it and then reopen it, if it was already open), and search for the program you wanted from the new repository. (从新仓库中获取你想要的程序，打开 Ubuntu 软件中心（如果它已经打开，请先关闭再重新打开），并搜索你从新仓库中需要的程序。)

- 5. 关闭“软件源”窗口。系统会提示可用软件信息已过时，因此请点击“刷新”（Reload）以获取最新的软件包信息。下载可能需要一点时间。

- 6. 打开 Ubuntu 软件中心（如果它已经打开，请先关闭再重新打开），并搜索你从新仓库中需要的程序。

When you're in Firefox, you'll also need to grab the repository's GPG key (which I'll explain at the end of this section). It should be linked to the same website you went for the APT line; in the case of GetDeb, go to `http://archive.getdeb.net/getdeb-archive.key`, when the Opening getdeb-archive window opens, select **Save File**, and click **OK** to save the key file.

当你在 Firefox 中时，你还需要获取该存储库的 GPG 密钥（我将在本节末尾解释它）。它应该链接到你获取 APT 行的同一个网站；以 GetDeb 为例，访问 `http://archive.getdeb.net/getdeb-archive.key`，当 getdeb-archive 窗口打开时，选择**另保存文件**，并点击**确定** 保存密钥文件。

Now that you're in possession of these vital bits of information, adding the repository to your system is pretty straightforward:

现在你已经拥有了这些关键信息，将存储库添加到你的系统中就非常简单了：

- Select **System ▸ Administration ▸ Software Sources**. Enter your password if asked, and then click the **Other Software** tab in the Software Sources window that appears.

- Click **Add**. You'll be prompted to enter the APT line, so paste it into the box, and then click **Add Source** (Figure 6-7). A new entry should appear in the Other Source list.

- Select the **Authentication** tab, and click **Import Key File**. Use the window that appears to find the `.key` file you downloaded earlier. (It's probably in your Downloads folder.)

- Select the `.key*` file by clicking it once, and then click **OK**. Check the list of trusted software providers to make sure that the GetDeb Automatic Signing Key is now present, as it is in Figure 6-8.

- 选择**系统 ▸ 管理 ▸ 软件源**。如果提示，请输入你的密码，然后点击弹出的“软件源”窗口中的**其他软件**选项卡。

- 点击**添加**。系统会提示你输入 APT 行，请将其粘贴到框中，然后点击**添加源**（图 6-7）。其他源列表中应该出现一个新项目。

- 选择**身份验证**选项卡，点击**导入密钥文件**。使用出现的窗口找到你之前下载的 `.key` 文件。（它可能在你的“下载”文件夹中。）

- 点击一次选中 `.key*` 文件，然后点击**确定**。检查受信任软件提供者列表，确保 GetDeb 自动签名密钥现在存在，如图 6-8 所示。
