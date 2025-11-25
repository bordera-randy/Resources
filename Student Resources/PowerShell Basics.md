# PowerShell Basics

## Introduction

PowerShell is a task automation and configuration management framework from Microsoft, consisting of a command-line shell and associated scripting language.

## Getting Started

### Installation

To install PowerShell, follow these steps:

1. Visit the [PowerShell GitHub releases page](https://github.com/PowerShell/PowerShell/releases).
2. Download the appropriate installer for your operating system.
3. Follow the installation instructions.

### Running PowerShell

- **Windows**: Open the Start Menu, search for "PowerShell", and select "Windows PowerShell" or "PowerShell".
- **macOS/Linux**: Open a terminal and type `pwsh`.

## Basic Commands

Here are some basic PowerShell commands to get you started:

- `Get-Help`: Displays help about PowerShell cmdlets.

    ```powershell
    Get-Help Get-Process
    ```

- `Get-Command`: Lists all available cmdlets.

    ```powershell
    Get-Command
    ```

- `Get-Process`: Displays a list of currently running processes.

    ```powershell
    Get-Process
    ```

- `Set-Location`: Changes the current directory.

    ```powershell
    Set-Location C:\Path\To\Directory
    ```

- `Get-ChildItem`: Lists the contents of a directory.

    ```powershell
    Get-ChildItem
    ```

## Scripting Basics

### Variables

Variables in PowerShell are declared using the `$` symbol.

```powershell
$greeting = "Hello, World!"
```

### Loops

PowerShell supports various loops, such as `foreach` and `while`.

```powershell
foreach ($item in $collection) {
        Write-Output $item
}
```

### Functions

Functions are blocks of code that can be reused.

```powershell
function Get-Greeting {
        param ($name)
        return "Hello, $name!"
}
```

## Conclusion

This guide covers the basics of PowerShell. For more detailed information, refer to the [official PowerShell documentation](https://docs.microsoft.com/powershell/).


