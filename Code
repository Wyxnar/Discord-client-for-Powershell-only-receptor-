# --- CONFIGURAION ---
$TOKEN = "YOUR_TOKEN_HERE" 

$friends = [ordered]@{
    "INSERT_HERE_FRIEND_1_NAME" = "INSTER_HERE_FRIEND_1_CHANNEL_NUMBER_HERE"
    "INSERT_HERE_FRIEND_2_NAME" = "INSTER_HERE_FRIEND_2_CHANNEL_NUMBER_HERE"
}

[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
[Console]::OutputEncoding = [System.Text.Encoding]::UTF8

function Show-Logo {
    Clear-Host
    $logo = @'

 /$$$$$$$  /$$                     /$$        /$$$$$$              /$$    
| $$__  $$| $$                    | $$       /$$__  $$            | $$    
| $$  \ $$| $$  /$$$$$$   /$$$$$$$| $$   /$$| $$  \__/  /$$$$$$  /$$$$$$  
| $$$$$$$ | $$ |____  $$ /$$_____/| $$  /$$/| $$       |____  $$|_  $$_/  
| $$__  $$| $$  /$$$$$$$| $$      | $$$$$$/ | $$        /$$$$$$$  | $$    
| $$  \ $$| $$ /$$__  $$| $$      | $$_  $$ | $$    $$ /$$__  $$  | $$ /$$
| $$$$$$$/| $$|  $$$$$$$|  $$$$$$$| $$ \  $$|  $$$$$$/|  $$$$$$$  |  $$$$/
|_______/ |__/ \_______/ \_______/|__/  \__/ \______/  \_______/   \___/  
                                                                          
                                                                          
                                                                                                                  
'@
    Write-Host $logo -ForegroundColor Green
}

$running = $true
while ($running) {
    Show-Logo
    Write-Host "`n--- CHAT MONITOR ---" -ForegroundColor Red
    $keyList = @($friends.Keys)
    for ($i = 0; $i -lt $keyList.Count; $i++) { Write-Host "$($i + 1). $($keyList[$i])" -ForegroundColor White }
    Write-Host "0. Exit" -ForegroundColor Gray
    
    $choice = Read-Host "Select a number"
    if ($choice -eq "0") { $running = $false }
    elseif ($choice -match '^\d+$' -and [int]$choice -le $keyList.Count -and [int]$choice -gt 0) {
        $targetName = $keyList[[int]$choice - 1]
        $channelID = $friends[$targetName]
        
        try {
            $url = "https://discord.com"
            
            $headers = @{ 
                "Authorization"    = $TOKEN
                "Accept"           = "*/*"
                "User-Agent"       = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36"
                "X-Discord-Locale" = "us-US"
            }
            
            $webResponse = Invoke-WebRequest -Uri $url -Headers $headers -Method Get -UseBasicParsing -ErrorAction Stop
            $rawContent = [System.Text.Encoding]::UTF8.GetString($webResponse.RawContentStream.ToArray())
            
            if ($rawContent -like '*[*]*' -or $rawContent -like '*{*}*') {
                $messages = $rawContent | ConvertFrom-Json
                
                Write-Host "`n--- LAST MESSAGES IN $targetName ---" -ForegroundColor Green
                
                if ($messages.Count -eq 0) {
                    Write-Host "[!] The chat is empty or the channel ID is wrong." -ForegroundColor Yellow
                } else {
                    $rev = @($messages); [Array]::Reverse($rev)
                    foreach ($msg in $rev) {
                        $time = if ($msg.timestamp) { [DateTime]::Parse($msg.timestamp).ToString("HH:mm:ss") } else { "??:??:??" }
                        $user = if ($msg.author) { $msg.author.username } else { "Sistema" }
                        $text = if ($msg.content) { $msg.content } else { "[Imagen/Sticker/Embed]" }
                        
                        Write-Host "[$time] " -NoNewline -ForegroundColor Gray
                        Write-Host "${user}: " -NoNewline -ForegroundColor Cyan
                        Write-Host "$text"
                    }
                }
            } else {
                throw "Answer is not a valid JSON. Discord sent: $rawContent"
            }
        } catch {
            Write-Host "`n[!] ERROR DETECTADO:" -ForegroundColor Red
            Write-Host $_.Exception.Message -ForegroundColor Yellow
            if ($_.Exception.Response) {
                $stream = $_.Exception.Response.GetResponseStream()
                $reader = New-Object System.IO.StreamReader($stream)
                Write-Host "Server reply: $($reader.ReadToEnd())" -ForegroundColor Gray
            }
        }
        Write-Host "Press enter to return..."
        $null = Read-Host
    }
}
