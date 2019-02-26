# MouseShaker

#Variables
$output = @()
$timeElapsed = get-date
$timeStart = Get-Date -Format t
$timeout = New-TimeSpan -Seconds $moves
$NoEvent = $true
$sw = [diagnostics.stopwatch]::StartNew()
$Step = Read-Host "Co ile sekund mam ruszac myszka?"
$moves = Read-Host "Przez ile sekund mam dzialac?"
$dzialanie = $moves / $step

 
Function MouseShaker{
$Cursor = [system.windows.forms.cursor]::Clip

[system.windows.forms.cursor]::Position = New-Object system.drawing.point(0,0)

[system.windows.forms.cursor]::Position = New-Object system.drawing.point(($Cursor.Width/2),($Cursor.Height/2))

[System.Reflection.Assembly]::LoadWithPartialName("system.windows.forms")

for ($i=1;$i -lt 1000;$i++) {

$Position = [system.windows.forms.cursor]::Position

$PositionChange = Get-Random 20

switch (Get-Random 4) {

    0 {[system.windows.forms.cursor]::Position = New-Object system.drawing.point($Position.x, ($Position.y + $PositionChange))}
    1 {[system.windows.forms.cursor]::Position = New-Object system.drawing.point(($Position.x + $PositionChange),$Position.y)}
    2 {[system.windows.forms.cursor]::Position = New-Object system.drawing.point($Position.x, ($Position.y - $PositionChange))}
    3 {[system.windows.forms.cursor]::Position = New-Object system.drawing.point(($Position.x - $PositionChange),$Position.y)}

}

}


}
while ($sw.elapsed -lt $timeout){
  MouseShaker
  start-sleep -seconds $step
  
}


    Start-Sleep 1
    $elapsedTime = new-timespan $timeElapsed $(get-date)
    $elFinal = $($elapsedTime.ToString("hh\:mm\:ss"))


Write-host "The script was activated at $timeStart and lasts for $elFinal, did $dzialanie moves." -ForegroundColor Yellow
  $output += "The script was activated at $timeStart and lasts for $elFinal, did $dzialanie moves."


$output | Out-File .\results.txt
