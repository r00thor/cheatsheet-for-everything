# Windows Enumeration
## Get Information About the Current Machine
```powershell
PS C:\> Get-WmiObject
```

### Get All of the class list over Get-WmiObject Command
```powershell
PS C:\> Get-WMIObject -List| Where{$\_.name -match "^Win32\_"} | Sort Name | Format-Table Name
```
[Reference Link About that](https://docs.microsoft.com/en-us/windows/win32/cimwin32prov/computer-system-hardware-classes?redirectedfrom=MSDN)
## List Local User
```powershell
PS C:\> Get-LocalUser
```

## List Local Groups
```powershell
PS C:\> Get-LocalGroup
```

## Get IP Address Info
```powershell
PS C:\> Get-NetIPAddress | Format-Table
```

```powershell
PS C:\> Get-NetIPConfiguration
```

## Get TCP Connection
```powershell
PS C:\> Get-NetTCPConnection
```

## Get List All of the patchs
```powershell
PS C:\> Get-Hotfix
```