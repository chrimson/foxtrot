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

### ASP
```
Install-WindowsFeature -name Web-Server -IncludeManagementTools
Install-WindowsFeature Web-Mgmt-Service

New-WebBinding -Name "Default Web Site" -IPAddress "*" -Port 80 -HostHeader "yourdomain.com"

Invoke-WebRequest -Uri "https://yourdomain.com" -Method Head

```

### ACME
```
New-Item -Path "C:\win-acme" -ItemType Directory  
Set-Location "C:\win-acme"
$url = "https://github.com/win-acme/win-acme/releases/download/v2.2.9.1701/win-acme.v2.2.9.1701.x64.trimmed.zip"  
$out = "C:\win-acme\win-acme.zip"
Invoke-WebRequest -Uri $url -OutFile $out
Expand-Archive -Path "C:\win-acme\win-acme.zip" -DestinationPath "C:\win-acme"
Remove-Item "C:\win-acme\win-acme.zip"
wacs
```


### .NET
```
https://dotnet.microsoft.com/en-us/download/dotnet/8.0
dotnet-host /install /quiet /norestart
dotnet-sdk /install /quiet /norestart

dotnet new web -n MyApi --no-https
dotnet publish -c Release -o ./publish
```

### IIS
```
Install-WindowsFeature Web-Server
Install-WindowsFeature Web-Mgmt-Service

Install-WindowsFeature Web-Metabase, Web-Mgmt-Console
```

### AWS
```
Invoke-WebRequest "https://awscli.amazonaws.com/AWSCLIV2.msi" -OutFile "AWSCLIV2.msi"
Start-Process msiexec.exe -Wait -ArgumentList "/i AWSCLIV2.msi /qn"
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User")
```

