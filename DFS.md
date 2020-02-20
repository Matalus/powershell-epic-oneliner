# collection of Distributed File System Commands

```PowerShell
$DFSR_Conn = Get-DfsReplicationGroup | Out-GridView -PassThru | Get-DfsrConnection; For(;;){ $DFSR_Conn | % {$conn = $_; Write-Host "`nGET: $($conn.GroupName) : SMem:$($conn.SourceComputerName) RMem:$($conn.DestinationComputerName) : $($conn.State)";  $conn |  Get-DfsrBacklog -Verbose -ErrorAction SilentlyContinue | Select *,@{N="DFSR";E={$conn.GroupName}},@{N="SMem";E={$conn.SourceComputerName}},@{N="RMem";E={$conn.DestinationComputerName}} } | Tee-Object -Variable DFSData | Group-Object -Property DFSR,SMem,RMem -NoElement | ft -AutoSize; Write-Host -ForegroundColor Yellow "Note Get-DFSRBacklog only retrieves the 1st 100 backlog files" }
```
