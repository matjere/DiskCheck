# DiskCheck
I'm using the following Powershell command to check Computer Lab computers.
It works very well when the computer is online.  But when the computers are not online or has an issue, it gives an error message that isn't helpful for me to pinpoint which ones are having problem!

Powershell command:
Get-WmiObject -class Win32_LogicalDisk -computername (Get-Content testcomputers.txt)  -filter "drivetype=3" |
Sort-Object -property DeviceID |
Format-Table -property PSComputerName,DeviceID,
@{label='FreeSpace(MB)';expression={$_.FreeSpace / 1MB -as [int]}},
@{label='Size(GB)';expression={$_.Size / 1GB -as [int]}},
@{label='%Free';expression={$_.FreeSpace / $_.Size * 100 -as [int]}}
