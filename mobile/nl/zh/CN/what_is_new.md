---

copyright:
  years: 2016
lastupdated: "2016-12-01"

---
{:new_window: target="_blank"}

# Mobile 仪表板中的新功能
{: #what_is_new}


### 最新更新时间：2016 年 11 月
{: #nov-2016}

{{site.data.keyword.Bluemix}} Mobile 仪表板 2016 年 11 月的更新引进以下更改：

   * 现在，您可以从**代码**页面生成项目的 SDK 工件。
   * Cordova 现在支持“基本代码入门模板”。
   * 现在，您可以在 {{site.data.keyword.mobileanalytics_short}} 控制台的**网络请求**页面[报告网络事件](/docs/services/mobileanalytics/sdk.html#network-requests){: new_window}和[监视网络请求](/docs/services/mobileanalytics/app-monitoring.html#monitor-network-requests){: new_window}。
   * 现在，您可以在 {{site.data.keyword.mobileanalytics_short}} 控制台中[将数据导出到 dashDB](/docs/services/mobileanalytics/app-monitoring.html#dashdb){: new_window}。


### 最新更新时间：2016 年 10 月
{: #oct-2016}

{{site.data.keyword.Bluemix_notm}} Mobile 仪表板 2016 年 10 月的更新引进以下更改：

   * 现在，您可以直接从仪表板，向项目添加 Push Notifications 和 Analytics 功能。
   * [代码入门模板](starters.html#Code_Starter)现在可用。
   * 可以向通过“代码入门模板”创建的项目添加 Authentication。
   * 现在支持 Swift。


#### Analytics
{: #analytics}

   * 当您添加 Analytics 功能时，默认情况下会启用演示模式。您可以在运行应用程序后关闭演示模式，以查看您的分析。


#### UI 构建器
{: #ui_builder}

   * 现在，从项目可以访问 **Push Notifications** 功能。
   * **项目设置**选项卡已重命名为**设置**选项卡。
   * **认证**选项卡已重命名为**用户访问权**选项卡。


#### 代码
{: #code}

   * 生成的适用于 iOS 的 Objective-C 和 Swift 代码现在使用 CocoaPods 来管理依赖关系。这表示您需要安装 CocoaPods。要安装它，请运行 `sudo gem install cocoapods`。安装 CocoaPods 之后，请运行 `pod setup` 以对其进行配置（如果尚未配置的话）。最后，运行 `pod install` 以下载并安装所需的项目依赖关系，然后在 Xcode 中打开 `.xcworkspace` 文件。在已下载代码归档的 `README.md` 文件中，可以找到其他详细信息。有关更多信息，请阅读[必备开发者工具](get_code.html#prereq-dev-tools)。

经常回顾以及时了解新更新。
