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
    Put any usage instructions here.
    Example syntax:
    PS C:\> .\STIG-ID-WN11-CC-000185.ps1
#>

# Define the registry path and value for WN11-CC-000185
$registryPath = "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Explorer"
$valueName = "NoDriveTypeAutoRun"
$valueData = 255 # 0x000000FF in hexadecimal

# Check if the registry path exists, if not create it
if (-not (Test-Path $registryPath)) {
    New-Item -Path $registryPath -Force
}

# Set the NoDriveTypeAutoRun value
Set-ItemProperty -Path $registryPath -Name $valueName -Value $valueData -Type DWord

# Output success message
Write-Host "Registry value '$valueName' set to '$valueData' at '$registryPath'."

# Confirmation of success
Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Explorer" -Name "NoDriveTypeAutoRun"
# Expected Value: NoDriveTypeAutoRun = 255
