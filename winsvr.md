$url = "https://github.com/git-for-windows/git/releases/download/v2.44.0.windows.1/Git-2.44.0-64-bit.exe"

$dest = "$env:TEMP\GitInstaller.exe"

Invoke-WebRequest -Uri $url -OutFile $dest

Start-Process -FilePath $dest -ArgumentList "/VERYSILENT /NORESTART" -Wait

Remove-Item $dest


$newPath = "C:\Your\New\Folder"

$currentPath = [Environment]::GetEnvironmentVariable("Path", "Machine")

[Environment]::SetEnvironmentVariable("Path", "$currentPath;$newPath", "Machine")

$env:Path += ";C:\your\new\path"



Start-Service sshd

Set-Service -Name sshd -StartupType 'Automatic'

Get-Service sshd

New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22





Install-WindowsFeature -name Web-Server -IncludeManagementTools

New-Item -Path "C:\win-acme" -ItemType Directory  
Set-Location "C:\win-acme"

$url = "https://github.com/win-acme/win-acme/releases/download/v2.2.9.1701/win-acme.v2.2.9.1701.x64.trimmed.zip"  
$out = "C:\win-acme\win-acme.zip"

Invoke-WebRequest -Uri $url -OutFile $out

Expand-Archive -Path "C:\win-acme\win-acme.zip" -DestinationPath "C:\win-acme"

Remove-Item "C:\win-acme\win-acme.zip"

Invoke-WebRequest -Uri "https://yourdomain.com" -Method Head


$myDomain = "yourdomain.com"

New-WebBinding -Name "Default Web Site" -IPAddress "*" -Port 80 -HostHeader $myDomain


AWS CLI

Invoke-WebRequest "https://awscli.amazonaws.com/AWSCLIV2.msi" -OutFile "AWSCLIV2.msi"

Start-Process msiexec.exe -Wait -ArgumentList "/i AWSCLIV2.msi /qn"

$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User")

dotnet new web -n MyApi --no-https

dotnet publish -c Release -o ./publish



