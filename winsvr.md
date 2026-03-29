Install-WindowsFeature -name Web-Server -IncludeManagementTools

New-Item -Path "C:\win-acme" -ItemType Directory  
Set-Location "C:\win-acme"

$url = "https://github.com/win-acme/win-acme/releases/download/v2.2.9.1701/win-acme.v2.2.9.1701.x64.trimmed.zip"  
$out = "C:\win-acme\win-acme.zip"

Invoke-WebRequest -Uri $url -OutFile $out

Expand-Archive -Path "C:\win-acme\win-acme.zip" -DestinationPath "C:\win-acme"

Remove-Item "C:\win-acme\win-acme.zip"

Invoke-WebRequest -Uri "https://yourdomain.com" -Method Head

# 1. Define your domain
$myDomain = "yourdomain.com"

# 2. Add the binding to the Default Web Site
# This tells IIS to listen for "yourdomain.com" on Port 80
New-WebBinding -Name "Default Web Site" -IPAddress "*" -Port 80 -HostHeader $myDomain

# 3. (Optional) If you have a 'www' version, add that too
New-WebBinding -Name "Default Web Site" -IPAddress "*" -Port 80 -HostHeader "www.$myDomain"

AWS CLI

# 1. Download the 64-bit MSI installer
Invoke-WebRequest "https://awscli.amazonaws.com/AWSCLIV2.msi" -OutFile "AWSCLIV2.msi"

# 2. Run the installer silently (/qn)
Start-Process msiexec.exe -Wait -ArgumentList "/i AWSCLIV2.msi /qn"

# 3. Refresh your environment variables (so you can use 'aws' immediately)
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User")

dotnet new web -n MyApi --no-https

dotnet publish -c Release -o ./publish
