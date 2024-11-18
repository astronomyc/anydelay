$host.UI.RawUI.BackgroundColor = "Black"
# Verificar si el script se esta ejecutando como administrador
if (-not ([Security.Principal.WindowsPrincipal] [Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole] "Administrator")) {
    Write-Host "Reejecutando como administrador..." -ForegroundColor Green
    Start-Process -FilePath "powershell" -ArgumentList "-NoProfile -ExecutionPolicy Bypass -File `"$PSCommandPath`"" -Verb RunAs
    exit
}

function Show-Menu {
    param (
        [string[]]$Options,
        [string]$Prompt,
        [int]$DefaultIndex = 0
    )

    $selectedIndex = $DefaultIndex
    $selectedOptions = @($false) * $Options.Count

    while ($true) {
        Clear-Host
        Write-Host $Prompt -ForegroundColor Cyan
        Write-Host "Use las flechas para navegar, Enter para seleccionar" -ForegroundColor Yellow
        Write-Host ""

        for ($i = 0; $i -lt $Options.Count; $i++) {
            if ($i -eq $selectedIndex) {
                $prefix = if ($MultiSelect) {
                    if ($selectedOptions[$i]) { "-> [X]" } else { "-> [ ]" }
                } else {
                    "->"
                }
                Write-Host "$prefix $($Options[$i])" -ForegroundColor Green
            } else {
                $prefix = if ($MultiSelect) {
                    if ($selectedOptions[$i]) { "   [X]" } else { "   [ ]" }
                } else {
                    "  "
                }
                Write-Host "$prefix $($Options[$i])" -ForegroundColor White
            }
        }

        $key = $Host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown")

        switch ($key.VirtualKeyCode) {
            38 { $selectedIndex = ($selectedIndex - 1 + $Options.Count) % $Options.Count } # Flecha arriba
            40 { $selectedIndex = ($selectedIndex + 1) % $Options.Count } # Flecha abajo
            32 { if ($MultiSelect) { $selectedOptions[$selectedIndex] = -not $selectedOptions[$selectedIndex] } } # Espacio
            13 { # Enter
                if ($MultiSelect) {
                    return $Options.Where({ $selectedOptions[$Options.IndexOf($_)] })
                } else {
                    return $Options[$selectedIndex]
                }
            }
        }
    }
}

function DelayRemove {
    Clear-Host
    # Detener AnyDesk
    Write-Host "Deteniendo Servicio de AnyDesk..." -ForegroundColor Cyan
    Stop-Service -Name "AnyDesk" -ErrorAction SilentlyContinue
    Get-Process -Name "AnyDesk" -ErrorAction SilentlyContinue | Stop-Process -Force
    Write-Host "Servicio Detenido" -ForegroundColor Green
    Write-Host ""

    # Rutas de configuración
    $allUsersProfile = "$env:ALLUSERSPROFILE\AnyDesk"
    $appData = "$env:APPDATA\AnyDesk"
    $temp = "$env:TEMP\AnyDesk"

    # Limpiar configuraciones
    Write-Host "Limpiando configuraciones de AnyDesk..." -ForegroundColor Cyan
    New-Item -ItemType Directory -Path $temp -Force | Out-Null
    Write-Host ""

    # Respaldar configuraciones
    Write-Host "Respaldando Sesiones del Anydesk..." -ForegroundColor Cyan
    Copy-Item -Path "$appData\user.conf" -Destination "$temp\" -Force -ErrorAction SilentlyContinue
    Copy-Item -Path "$appData\thumbnails" -Destination "$temp\thumbnails" -Recurse -Force -ErrorAction SilentlyContinue
    Write-Host "Sesiones Respaldadas" -ForegroundColor Green
    Write-Host ""

    # Eliminar configuraciones y datos
    Write-Host "Eliminando Configuraciones Antiguas del Anydesk..." -ForegroundColor Cyan
    Remove-Item -Path "$allUsersProfile\*" -Recurse -Force -ErrorAction SilentlyContinue
    Remove-Item -Path "$appData\*" -Recurse -Force -ErrorAction SilentlyContinue
    Write-Host "Configuraciones Eliminadas" -ForegroundColor Green
    Write-Host ""

    # Restaurar configuraciones necesarias
    Write-Host "Restaurando Sesiones de Respaldo..." -ForegroundColor Cyan
    Move-Item -Path "$temp\user.conf" -Destination "$appData\user.conf" -Force -ErrorAction SilentlyContinue
    Copy-Item -Path "$temp\thumbnails" -Destination "$appData\thumbnails" -Recurse -Force -ErrorAction SilentlyContinue
    Remove-Item -Path "$temp" -Recurse -Force -ErrorAction SilentlyContinue
    Write-Host "Sesiones Restauradas" -ForegroundColor Green
    Write-Host ""

    # Iniciar AnyDesk
    Write-Host "Iniciando Servicio de AnyDesk..." -ForegroundColor Yellow
    Start-Service -Name "AnyDesk" -ErrorAction SilentlyContinue
    $paths = @(
        "$env:ProgramFiles\AnyDesk\AnyDesk.exe",
        "$env:ProgramFiles(x86)\AnyDesk\AnyDesk.exe"
    )
    foreach ($path in $paths) {
        if (Test-Path $path) {
            Start-Process -FilePath $path
        }
    }

    Write-Host "Proceso completado. El Delay del Anydesk ha Sido Restablecido" -ForegroundColor Green
}

while ($true) {
    $mainOption = Show-Menu -Options @("Remover Delay", "Salir") -Prompt "Seleccione una opcion:"

    switch ($mainOption) {
        "Remover Delay" { DelayRemove }
        "Salir" { exit }
    }

    Write-Host "`nPresione cualquier tecla para volver al menu principal..."
    $null = $Host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown")
}