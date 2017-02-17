### 不同订阅之间拷贝虚拟机

在两个订阅之间复制虚拟机的步骤如下：  
1. 在原订阅中， 删除虚拟机，但是保留VHD.  
2. 将VHD解除锁定，Break Lease，否则后续无法基于这个VHD创建VM.  
3. 将VHD从原订阅拷贝到目标订阅。  

第3步的PowerShell命令如下：
    
    $sourceStorageAccount=""
    $sourceAccountKey=""

    $destStorageAccount=""
    $destAccountKey=""

    $sourceContainer="vhds"
    $file="ubuntu212-ubuntu212-2017-02-13.vhd"
    $destContext=New-AzureStorageContext -Environment azurechinacloud  -StorageAccountName $destStorageAccount -StorageAccountKey $destAccountKey
    $sourceContext=New-AzureStorageContext -StorageAccountName $sourceStorageAccount -StorageAccountKey $sourceAccountKey -Environment azurecloud

    $blob1=Get-AzureStorageBlob -Blob $file -Container $sourceContainer -Context $sourceContext
    
    #New a Container if the vhds container doesn't exist in destination storage account.
    New-AzureStorageContainer -Name vhds -Permission Container -Context $destContext
    $blob1|Start-AzureStorageBlobCopy -DestContext $destContext -DestContainer vhds 

查询拷贝进度：

    $blob=Get-AzureStorageBlob -Blob $file -Container vhds -Context $destContext
    $blob|Get-AzureStorageBlobCopyState