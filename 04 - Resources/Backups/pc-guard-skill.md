---
name: pc-guard
description: PC xavfsizlik, musr tozalash va optimizatsiya skaneri
user-invocable: true
---

# PC Guardian — Skill Protocol

Bu skill PC ni 3 yo'nalishda tekshiradi: **Xavfsizlik**, **Musr (Junk)**, **Optimizatsiya**.
Hech narsa avtomatik o'chirilmaydi — faqat hisobot + tavsiya. O'chirish faqat foydalanuvchi tasdiqlagandan keyin.

## XAVFSIZLIK QOIDALARI — DOIMO RIOYA QIL

- **HECH QACHON** faylni avtomatik o'chirma
- **HECH QACHON** `C:\Windows\System32`, `C:\Program Files`, `C:\Program Files (x86)` ichki fayllarini o'zgartirma
- Faqat hisobot ber, tavsiya ber, tasdiqlash so'ra
- Har bir topilgan fayl uchun **sabab** tushuntir

---

## ISHGA TUSHIRISH TARTIBI

Quyidagi 3 modulni ketma-ket bajar, keyin yakuniy hisobot chiqar.

---

## MODUL 1: XAVFSIZLIK SKANERI

### 1.1 Xavfli fayl pattern lari

Quyidagi papkalarda xavfli nom pattern larini qidir:
- `C:/Users/User/Downloads`
- `C:/Users/User/OneDrive/Рабочий стол` (Desktop)
- `$TEMP`
- `C:/Users/User/AppData/Local/Temp`

```bash
# Xavfli nom patternlari (case-insensitive)
find "/c/Users/User/Downloads" "/c/Users/User/OneDrive/Рабочий стол" "$TEMP" \
  -maxdepth 3 \
  -iname "*crack*" -o -iname "*keygen*" -o -iname "*patch*" \
  -o -iname "*activator*" -o -iname "*kms*" -o -iname "*loader*" \
  -o -iname "*hack*" \
  2>/dev/null
```

### 1.2 Shubhali executable fayllar

Downloads va Desktop da `.exe`, `.bat`, `.cmd`, `.ps1`, `.vbs` kengaytmali fayllarni ro'yxatla:

```bash
find "/c/Users/User/Downloads" "/c/Users/User/OneDrive/Рабочий стол" \
  -maxdepth 2 \
  \( -iname "*.bat" -o -iname "*.cmd" -o -iname "*.ps1" -o -iname "*.vbs" \) \
  2>/dev/null
```

### 1.3 Startup papkasi

```bash
ls -la "/c/Users/User/AppData/Roaming/Microsoft/Windows/Start Menu/Programs/Startup/" 2>/dev/null
```

### 1.4 Task Scheduler (shubhali tasklar)

```bash
powershell.exe -Command "Get-ScheduledTask | Where-Object { \$_.State -eq 'Ready' -and \$_.TaskPath -notlike '\\Microsoft*' } | Select-Object TaskName, TaskPath, State | Format-Table -AutoSize" 2>/dev/null
```

**Natijani saqlash:** topilgan xavfli fayllar sonini va ro'yxatini yozib ol.

---

## MODUL 2: MUSR TOZALASH (JUNK CLEANER)

### 2.1 Temp papkalar hajmi

```bash
powershell.exe -Command "
  \$tempUser = (Get-ChildItem \$env:TEMP -Recurse -ErrorAction SilentlyContinue | Measure-Object -Property Length -Sum).Sum / 1GB
  \$tempWin = (Get-ChildItem 'C:\\Windows\\Temp' -Recurse -ErrorAction SilentlyContinue | Measure-Object -Property Length -Sum).Sum / 1GB
  Write-Output \"User Temp: \$([math]::Round(\$tempUser, 2)) GB\"
  Write-Output \"Windows Temp: \$([math]::Round(\$tempWin, 2)) GB\"
"
```

### 2.2 Browser cache hajmi

```bash
powershell.exe -Command "
  \$paths = @{
    'Chrome' = \"\$env:LOCALAPPDATA\\Google\\Chrome\\User Data\\Default\\Cache\"
    'Edge' = \"\$env:LOCALAPPDATA\\Microsoft\\Edge\\User Data\\Default\\Cache\"
    'Firefox' = \"\$env:LOCALAPPDATA\\Mozilla\\Firefox\\Profiles\"
  }
  foreach (\$browser in \$paths.Keys) {
    \$p = \$paths[\$browser]
    if (Test-Path \$p) {
      \$size = (Get-ChildItem \$p -Recurse -ErrorAction SilentlyContinue | Measure-Object -Property Length -Sum).Sum / 1GB
      Write-Output \"\$browser cache: \$([math]::Round(\$size, 2)) GB\"
    } else {
      Write-Output \"\$browser cache: topilmadi\"
    }
  }
"
```

### 2.3 Downloads dagi eski installerlar (30+ kun)

```bash
find "/c/Users/User/Downloads" -maxdepth 2 \
  \( -iname "*.exe" -o -iname "*.msi" \) \
  -mtime +30 \
  -exec ls -lh {} \; 2>/dev/null
```

### 2.4 Recycle Bin hajmi

```bash
powershell.exe -Command "
  \$shell = New-Object -ComObject Shell.Application
  \$rb = \$shell.Namespace(0xA)
  \$count = \$rb.Items().Count
  Write-Output \"Recycle Bin: \$count ta element\"
" 2>/dev/null
```

### 2.5 Katta node_modules (foydalanilmayotgan)

```bash
find "/c/Users/User" -maxdepth 5 -type d -name "node_modules" 2>/dev/null | head -20
```

Har bir topilgan `node_modules` uchun parent papka hajmini ko'rsat va so'nggi o'zgartirilgan vaqtini tekshir.

### 2.6 Log, thumbcache, prefetch

```bash
powershell.exe -Command "
  \$prefetch = (Get-ChildItem 'C:\\Windows\\Prefetch' -ErrorAction SilentlyContinue | Measure-Object -Property Length -Sum).Sum / 1MB
  Write-Output \"Prefetch: \$([math]::Round(\$prefetch, 2)) MB\"
"
```

**Natijani saqlash:** jami tozalash mumkin bo'lgan hajmni hisoblash (GB).

---

## MODUL 3: PC OPTIMIZATSIYA

### 3.1 Disk hajmi

```bash
powershell.exe -Command "
  \$disk = Get-PSDrive C
  \$free = [math]::Round(\$disk.Free / 1GB, 2)
  \$used = [math]::Round(\$disk.Used / 1GB, 2)
  \$total = [math]::Round((\$disk.Free + \$disk.Used) / 1GB, 2)
  Write-Output \"C: disk — Jami: \$total GB | Ishlatilgan: \$used GB | Bo'sh: \$free GB\"
"
```

### 3.2 Top 20 eng katta fayl

```bash
powershell.exe -Command "
  Get-ChildItem 'C:\\Users\\User' -Recurse -File -ErrorAction SilentlyContinue |
    Sort-Object Length -Descending |
    Select-Object -First 20 |
    ForEach-Object {
      \$size = [math]::Round(\$_.Length / 1MB, 2)
      Write-Output \"\$size MB — \$(\$_.FullName)\"
    }
" 2>/dev/null
```

### 3.3 RAM va CPU holati

```bash
powershell.exe -Command "
  \$os = Get-CimInstance Win32_OperatingSystem
  \$totalRAM = [math]::Round(\$os.TotalVisibleMemorySize / 1MB, 2)
  \$freeRAM = [math]::Round(\$os.FreePhysicalMemory / 1MB, 2)
  \$usedRAM = [math]::Round(\$totalRAM - \$freeRAM, 2)
  Write-Output \"RAM — Jami: \$totalRAM GB | Ishlatilgan: \$usedRAM GB | Bo'sh: \$freeRAM GB\"
  \$cpu = (Get-CimInstance Win32_Processor).LoadPercentage
  Write-Output \"CPU yuklanishi: \$cpu%\"
"
```

### 3.4 Startup dasturlar

```bash
powershell.exe -Command "
  Get-CimInstance Win32_StartupCommand |
    Select-Object Name, Command, Location |
    Format-Table -AutoSize
" 2>/dev/null
```

### 3.5 Keraksiz bo'lishi mumkin bo'lgan Service lar

```bash
powershell.exe -Command "
  Get-Service | Where-Object {
    \$_.StartType -eq 'Automatic' -and \$_.Status -eq 'Running' -and
    \$_.Name -notmatch 'Windows|Microsoft|wuauserv|Winmgmt|EventLog|Dhcp|Dnscache|LanmanServer|LanmanWorkstation|RpcSs|Schedule|SENS|Themes|AudioSrv|Spooler|WSearch|SecurityHealthService'
  } | Select-Object Name, DisplayName, StartType | Format-Table -AutoSize
" 2>/dev/null
```

---

## YAKUNIY HISOBOT

Barcha modullar tugagandan keyin quyidagi formatda hisobot chiqar:

```
╔══════════════════════════════════════╗
║        PC GUARDIAN — Hisobot         ║
╠══════════════════════════════════════╣
║ Xavfsizlik:  X ta xavfli fayl       ║
║ Musr:        X.X GB tozalash mumkin  ║
║ Disk:        XX GB bo'sh (C:)        ║
║ Startup:     XX ta dastur            ║
╚══════════════════════════════════════╝
```

Keyin har bir modul uchun batafsil ro'yxat:

### Xavfsizlik bo'limi:
- Har bir topilgan fayl uchun: fayl nomi, joylashuvi, nega xavfli, tavsiya

### Musr bo'limi:
- Har bir kategoriya uchun: hajm, joylashuv, tozalash usuli
- O'chirish uchun tasdiqlash so'ra — AskUserQuestion ishlatib

### Optimizatsiya bo'limi:
- Disk holati
- Eng katta fayllar
- RAM/CPU
- Startup tavsiyalar
- Service tavsiyalar

---

## TOZALASH BOSQICHI (faqat foydalanuvchi tasdiqlasa)

Agar foydalanuvchi tozalashni tasdiqlasa, quyidagi buyruqlarni ishga tushir:

### Temp tozalash
```bash
powershell.exe -Command "Remove-Item '$env:TEMP\*' -Recurse -Force -ErrorAction SilentlyContinue"
```

### Browser cache tozalash (Chrome)
```bash
powershell.exe -Command "Remove-Item '$env:LOCALAPPDATA\Google\Chrome\User Data\Default\Cache\*' -Recurse -Force -ErrorAction SilentlyContinue"
```

### Recycle Bin tozalash
```bash
powershell.exe -Command "Clear-RecycleBin -Force -ErrorAction SilentlyContinue"
```

**OGOHLANTIRISH:** Har bir tozalash amalidan oldin foydalanuvchidan tasdiqlash ol!
