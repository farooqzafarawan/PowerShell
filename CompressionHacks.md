# Compressing XML File


```PowerShell
$Path = "$env:TEMP\data1.xml"

# serialize data (results in large text files)
Get-Process | Export-Clixml -Path $Path

$length1 = (Get-Item -Path $Path).Length

$ZipPath = [IO.Path]::ChangeExtension($Path, ".zip")

Compress-Archive -Path $Path -Destination $ZipPath -CompressionLevel Optimal -Force
Remove-Item -Path $Path

$length2 = (Get-Item -Path $ZipPath).Length

$compression = $length2 * 100 / $length1
"Compression Ratio {0:n2} %" -f $compression 
```






















Thanks to [Idera Power Tips](https://community.idera.com/database-tools/powershell/powertips/b/tips/posts/compressing-serialized-data) for the script