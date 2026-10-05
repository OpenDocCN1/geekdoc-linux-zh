# CHAPTER 2 AUTOMATING VSPHERE HYPERVISOR DEPLOYMENT AND CONFIGURATION

```
$IPAddress
```

'

```
[int]
$Port=3333
End {
[byte[]]$B = 0..255 | Foreach-Object {
```

```
$ip = [Net.IPAddress]::Parse($IPAddress)
$listener = New-Object System.Net.Sockets.TcpListener(
$ip, $Port)
$listener.Start()
```

```
Write-Debug "Waiting for a connection on port $port..."
```

```
$client = $listener.AcceptTcpClient()
$RemoteEndpoint = $client.Client.RemoteEndpoint
$stream = $client.GetStream()
```

```
$raw = while (($i = $stream.Read($B, 0, $B.Length)) -ne 0) {
$B[0..($i-1)] | Foreach-Object { $_ }
}
```

```
$client.Close()
$listener.Stop()
```

```
Write-Debug "Connection closed."
```

```
New-Object PSOject -Property @{
'Source' = $RemoteEndpoint.Address.ToString().Split(':') [0]
'Data' = [string]::Join("",[char[]]$raw)
}
```