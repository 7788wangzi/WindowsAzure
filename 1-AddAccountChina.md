## 在PowerShell中添加某个Mooncake订阅
### 方式一：
1. 在浏览器中打开网址https://manage.windowsazure.cn/publishsettings。  
2. 使用你的1元试用帐户登录。  
3. 在保存文件对话框中，保存发布配置文件，并命名为D:\azure-credentials.publishsettings。  
4. 打开Windows PowerShell, 运行如下命令来导入发布配置文件：  
    `Import-AzurePublishSettingsFile "D:\azure-credentials.publishsettings"`
5. 使用如下命令，测试你的发布配置文件导入是否成功：  
    `Get-AzureSubscription`

### 方式二：
使用环境参数`-Environment`, 这个参数有两个选项： azurechinacloud 和 azurecloud。  
`Add-AzureAccount -Environment azurechinacloud`