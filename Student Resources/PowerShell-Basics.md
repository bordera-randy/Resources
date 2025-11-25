# PowerShell Basics

A Practical Introduction for Beginners and a Reference Guide for Daily Use

---

## 📌 What Is PowerShell?

PowerShell is a cross-platform automation and configuration shell built by Microsoft. It combines:
- An interactive command-line interface
- A powerful scripting language
- Deep integration with .NET, Windows, Azure, and modern APIs

PowerShell is designed for automation, system management, and repeatable workflows across Windows, Linux, and macOS.

---

## 1. Getting Started

### 1.1 Installing PowerShell

**Windows / macOS / Linux**
1. Go to the official release page: https://github.com/PowerShell/PowerShell/releases
2. Download the latest stable installer for your OS.
3. Install normally.

**Running PowerShell**

| Platform | How to Launch |
|----------|---------------|
| Windows  | Search PowerShell in Start Menu. Use PowerShell (Core) or Windows PowerShell (legacy). |
| macOS    | Open Terminal → `pwsh` |
| Linux    | Open your shell → `pwsh` |

**Tip:** Prefer PowerShell (Core) for modern scripting.

---

## 2. Understanding PowerShell

### 2.1 Cmdlets

PowerShell commands are called cmdlets (pronounced "command-lets"). They follow a simple naming pattern:

```
Verb-Noun
```

**Examples**
- `Get-Process`
- `Set-Location`
- `New-Item`
- `Remove-Item`
- `Get-ChildItem`

**Discovering Cmdlets**

```powershell
Get-Command
Get-Command -Name *service*
```

**Getting Help**

```powershell
Get-Help Get-Process
Get-Help Get-Process -Examples
Update-Help
```

---

## 3. Navigating the File System

PowerShell treats the file system like a drive.

### 3.1 Common Commands

| Action | Command | Example |
|--------|---------|---------|
| Change directory | `Set-Location` / `cd` | `cd C:\Scripts` |
| List items | `Get-ChildItem` / `ls` | `ls /var/log` |
| Show current directory | `Get-Location` / `pwd` | `pwd` |

**Examples**

```powershell
Set-Location C:\Users
Get-ChildItem -Recurse
```

---

## 4. Working With Objects

Unlike shells that return plain text, PowerShell returns objects.

```powershell
Get-Process | Select-Object Name, CPU, Id
```

You can pipe objects between cmdlets to filter, sort, or transform them.

**Common Object Cmdlets**
- `Select-Object`
- `Sort-Object`
- `Where-Object`
- `Format-Table`
- `Format-List`

**Example Pipeline**

```powershell
Get-Process |
    Where-Object { $_.CPU -gt 1 } |
    Sort-Object CPU -Descending |
    Format-Table -AutoSize
```

---

## 5. Variables & Data Types

### 5.1 Declaring Variables

```powershell
$name = "Randy"
$count = 5
$items = @(1,2,3)
```

### 5.2 Inspecting Types

```powershell
$name.GetType()
```

Use `$null` for empty or missing values.

---

## 6. Writing Scripts

PowerShell scripts have the `.ps1` extension.

**Running a Script**

```powershell
.\myscript.ps1
```

**Execution Policy**

If your system blocks script execution:

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

---

## 7. Control Flow

### 7.1 If/Else

```powershell
if ($value -gt 10) {
    "High"
} elseif ($value -gt 5) {
    "Medium"
} else {
    "Low"
}
```

### 7.2 Loops

**Foreach Loop**

```powershell
foreach ($i in 1..5) {
    Write-Output "Number: $i"
}
```

**While Loop**

```powershell
while ($x -lt 10) {
    $x++
}
```

---

## 8. Functions

Functions make your code reusable.

```powershell
function Get-Greeting {
    param(
        [string]$Name
    )
    "Hello, $Name!"
}
```

Call it:

```powershell
Get-Greeting -Name "Randy"
```

---

## 9. Error Handling

### 9.1 Try/Catch

```powershell
try {
    Get-Item "C:\does-not-exist.txt"
}
catch {
    Write-Error "File not found!"
}
```

### 9.2 Throwing Errors

```powershell
throw "Something went wrong"
```

---

## 10. Modules

Modules extend PowerShell's capabilities.

### 10.1 Listing Modules

```powershell
Get-Module -ListAvailable
```

### 10.2 Installing Modules

```powershell
Install-Module Az
Import-Module Az
```

---

## 11. Working With External Systems

PowerShell integrates easily with REST APIs, cloud platforms, and services.

**Example: Calling a REST API**

```powershell
Invoke-RestMethod -Uri "https://api.github.com/repos/PowerShell/PowerShell"
```

---

## 12. Best Practices

- Use Verb-Noun naming for functions.
- Validate inputs (`[int]`, `[string]`, etc.).
- Comment your code for readability.
- Avoid hardcoding passwords or secrets.
- Prefer `Write-Output` over `Write-Host`.
- Keep scripts idempotent (safe to run multiple times).
- Organize related functions into modules.
- Use consistent indentation and formatting.

---

## 13. Helpful Tools

- VS Code with the PowerShell extension
- Git + GitHub for source control
- PSScriptAnalyzer for code quality
- PowerShell Gallery (https://www.powershellgallery.com/) for modules

---

## 14. Quick Reference Cheat Sheet

### Common Cmdlets

| Purpose | Cmdlet |
|---------|--------|
| Find commands | `Get-Command` |
| Get help | `Get-Help` |
| List files | `Get-ChildItem` |
| Copy file | `Copy-Item` |
| Move file | `Move-Item` |
| Delete file | `Remove-Item` |
| Check services | `Get-Service` |
| Stop process | `Stop-Process` |

### Useful Aliases

```powershell
ls     # Get-ChildItem
cd     # Set-Location
pwd    # Get-Location
```

---

## Conclusion

You now have a practical introduction to PowerShell and a solid reference for everyday scripting. For deeper learning, refer to the official documentation:

https://learn.microsoft.com/powershell