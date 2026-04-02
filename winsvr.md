### Git, Vim
```
$url = "https://github.com/git-for-windows/git/releases/download/v2.53.0.windows.1/Git-2.53.0-64-bit.exe"
$dest = "$env:TEMP\GitInstaller.exe"
Invoke-WebRequest -Uri $url -OutFile $dest
Start-Process -FilePath $dest -ArgumentList "/VERYSILENT /NORESTART" -Wait
```

### path
```
$newPath = "C:\Your\New\Folder"
$currentPath = [Environment]::GetEnvironmentVariable("Path", "Machine")
[Environment]::SetEnvironmentVariable("Path", "$currentPath;$newPath", "Machine")
$env:Path = [Environment]::GetEnvironmentVariable("Path", "Machine")
```

### sshd
```
Start-Service sshd
Set-Service -Name sshd -StartupType 'Automatic'
Get-Service sshd
New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22
C:\ProgramData\ssh\administrators_authorized_keys
```

### IIS
```
Install-WindowsFeature Web-Server

New-WebBinding -Name "Default Web Site" -IPAddress "*" -Port 80 -HostHeader "yourdomain.com"
```

### ACME
```
wacs
```

### .NET
```
https://dotnet.microsoft.com/en-us/download/dotnet/8.0
dotnet-host /install /quiet /norestart
dotnet-sdk /install /quiet /norestart

dotnet new webapi -n api
dotnet publish -c Release -o ./publish

$apiPath = "C:\inetpub\wwwroot\api"
New-Item -Path $apiPath -ItemType Directory -Force
Copy-Item -Path "C:\YourBuildFolder\*" -Destination $apiPath -Recurse

$appPoolName = "ApiPool"
New-WebAppPool -Name $appPoolName
Set-ItemProperty "IIS:\AppPools\$appPoolName" -Name "managedRuntimeVersion" -Value ""

$siteName = "Default Web Site"
$subPath = "api" # This becomes yourdomain.com/api
New-WebApplication -Site $siteName -Name $subPath -PhysicalPath $apiPath -ApplicationPool $appPoolName

$acl = Get-Acl $apiPath
$permission = "IIS AppPool\$appPoolName","ReadAndExecute","Allow"
$accessRule = New-Object System.Security.AccessControl.FileSystemAccessRule $permission
$acl.SetAccessRule($accessRule)
Set-Acl $apiPath $acl
```

### AWS
```
Invoke-WebRequest "https://awscli.amazonaws.com/AWSCLIV2.msi" -OutFile "AWSCLIV2.msi"
Start-Process msiexec.exe -Wait -ArgumentList "/i AWSCLIV2.msi /qn"
aws configure
```

