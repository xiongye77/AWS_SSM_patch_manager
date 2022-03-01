# AWS_SSM_patch_manager
![image](https://user-images.githubusercontent.com/36766101/156069719-5f92ff20-2653-4ab0-b94e-d22455a03e46.png)
![image](https://user-images.githubusercontent.com/36766101/156071675-29cf5fd0-87c3-4e9f-b6de-396213fe4f37.png)
![image](https://user-images.githubusercontent.com/36766101/156071761-30f3988a-4602-4579-86d6-4c434172c60b.png)
![image](https://user-images.githubusercontent.com/36766101/156075241-acb01fc1-85e5-4377-82b1-1aefdcc88b6e.png)
![image](https://user-images.githubusercontent.com/36766101/156080689-8e5639b4-9538-4574-80d5-3d689812800f.png)

[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.SecurityProtocolType]::Tls12


get-packageprovider



install-module -Name pswindowsupdate



get-wuhistory




Get-EventLog -LogName Application -Newest 10



Read-S3Object -BucketName "csn-operations"-Key "installers/cloud_watch_mem.json" -file "C:\cloud_watch_mem.json"


Invoke-WebRequest -Uri  https://s3.amazonaws.com/amazoncloudwatch-agent/windows/amd64/latest/amazon-cloudwatch-agent.msi  -OutFile c:\amazon-cloudwatch-agent.msi


msiexec /i "C:\amazon-cloudwatch-agent.msi" /quiet


cd 'C:\Program Files\Amazon\AmazonCloudWatchAgent\'


.\amazon-cloudwatch-agent-ctl.ps1 -a fetch-config -m EC2 -c file:c:\cloud_watch_mem.json -s



Cross account copy Windows AMI , AWS  aws ec2 get-password-data --instance-id instance-id could not work, so use powershell to reset windows box password and login.



$Password = (Read-Host -Prompt "New Password" -AsSecureString)

$User = (Read-Host -Prompt "Username")

$UserAccount = Get-LocalUser -Name $User

$UserAccount | Set-LocalUser -Password $Password
