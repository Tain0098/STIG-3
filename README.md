# STIG-3

<#
.SYNOPSIS
    This PowerShell script ensures that default Autorun behavior is configured to prevent executing commands.

.NOTES
    Author          : Htain Ney
    Date Created    : 2026-06-12
    Last Modified   : 2026-06-12
    Version         : 1.0
    CVEs            : N/A
    Plugin IDs      : N/A
    STIG-ID         : WN11-CC-000185

.TESTED ON
    Date(s) Tested  : 2026-11-14
    Tested By       : Htain Ney
    Systems Tested  : Windows 11
    PowerShell Ver. : 5.1

.USAGE
    PS C:\> .\STIG-ID-WN11-CC-000185.ps1
#>

$registryPath = "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Explorer"
$valueName = "NoDriveTypeAutoRun"
$valueData = 255

if (-not (Test-Path $registryPath)) { New-Item -Path $registryPath -Force }
Set-ItemProperty -Path $registryPath -Name $valueName -Value $valueData -Type DWord
Write-Host "Registry value '$valueName' set to '$valueData' at '$registryPath'."
