# Advanced PowerShell

## Table of Contents
1. [Introduction](#introduction)
2. [Scripting and Automation](#scripting-and-automation)
3. [Advanced Functions](#advanced-functions)
    - [Creating and Using Advanced Functions](#creating-and-using-advanced-functions)
    - [Parameter Attributes and Validation](#parameter-attributes-and-validation)
    - [Using `CmdletBinding` and `Parameter` Attributes](#using-cmdletbinding-and-parameter-attributes)
4. [Error Handling](#error-handling)
5. [Working with APIs](#working-with-apis)
6. [PowerShell Remoting](#powershell-remoting)
7. [Modules and Packages](#modules-and-packages)
8. [Best Practices](#best-practices)

## Introduction
Advanced PowerShell techniques can help you automate complex tasks, manage systems more efficiently, and improve your scripting skills. This guide covers various advanced topics to enhance your PowerShell proficiency.

## Scripting and Automation
Learn how to create robust scripts to automate repetitive tasks. Topics include:
- Writing and running scripts
- Scheduling tasks with Task Scheduler
- Using loops and conditional statements

### Writing and Running Scripts
PowerShell scripts are text files with a `.ps1` extension. You can write scripts using any text editor and run them in the PowerShell console.

```powershell
# Example script to display a message
Write-Output "Hello, PowerShell!"
```

### Scheduling Tasks with Task Scheduler
Automate script execution using Task Scheduler. Create a task that runs your script at specified intervals.

```powershell
# Schedule a task to run a script daily
$action = New-ScheduledTaskAction -Execute 'PowerShell.exe' -Argument 'C:\Scripts\MyScript.ps1'
$trigger = New-ScheduledTaskTrigger -Daily -At 9AM
Register-ScheduledTask -Action $action -Trigger $trigger -TaskName "DailyScript"
```

### Using Loops and Conditional Statements
Loops and conditional statements control the flow of your scripts.

```powershell
# Example of a loop
for ($i = 1; $i -le 5; $i++) {
    Write-Output "Iteration $i"
}

# Example of a conditional statement
if ($true) {
    Write-Output "Condition is true"
} else {
    Write-Output "Condition is false"
}
```

## Advanced Functions
Explore advanced function features such as:
- Creating and using advanced functions
- Parameter attributes and validation
- Using `CmdletBinding` and `Parameter` attributes

### Creating and Using Advanced Functions
Advanced functions in PowerShell are essentially scripts that behave like cmdlets. They allow for more complex and reusable code. You can define an advanced function using the `function` keyword and the `[CmdletBinding()]` attribute.

```powershell
function Get-SampleData {
    [CmdletBinding()]
    param (
        [Parameter(Mandatory=$true)]
        [string]$Name
    )
    process {
        Write-Output "Hello, $Name"
    }
}
```

### Parameter Attributes and Validation
Parameters in advanced functions can have attributes that enforce validation rules, making your functions more robust and user-friendly.

```powershell
function Set-UserAge {
    [CmdletBinding()]
    param (
        [Parameter(Mandatory=$true)]
        [ValidateRange(0,120)]
        [int]$Age
    )
    process {
        Write-Output "User age is set to $Age"
    }
}
```

### Using `CmdletBinding` and `Parameter` Attributes
The `[CmdletBinding()]` attribute turns a function into an advanced function, enabling cmdlet-like features such as common parameters (`-Verbose`, `-Debug`, etc.). The `[Parameter()]` attribute allows you to define parameter properties like `Mandatory`, `Position`, and `ValueFromPipeline`.

```powershell
function Invoke-ProcessData {
    [CmdletBinding()]
    param (
        [Parameter(Mandatory=$true, ValueFromPipeline=$true)]
        [string]$Data
    )
    process {
        Write-Output "Processing $Data"
    }
}
```

## Error Handling
Implement effective error handling in your scripts:
- Try, Catch, Finally blocks
- ErrorAction and ErrorVariable
- Handling non-terminating errors

### Try, Catch, Finally Blocks
Use `Try`, `Catch`, and `Finally` blocks to handle errors gracefully.

```powershell
try {
    # Code that may throw an exception
    $result = 1 / 0
} catch {
    Write-Error "An error occurred: $_"
} finally {
    Write-Output "This runs regardless of success or failure"
}
```

### ErrorAction and ErrorVariable
Control error behavior and capture error details using `ErrorAction` and `ErrorVariable`.

```powershell
# Example of using ErrorAction and ErrorVariable
Get-Item "C:\NonExistentFile.txt" -ErrorAction SilentlyContinue -ErrorVariable myError
if ($myError) {
    Write-Output "An error occurred: $myError"
}
```

### Handling Non-Terminating Errors
Handle non-terminating errors using `ErrorActionPreference`.

```powershell
# Example of setting ErrorActionPreference
$ErrorActionPreference = "Stop"
Get-Item "C:\NonExistentFile.txt"
```

## Working with APIs
Interact with REST APIs using PowerShell:
- Using `Invoke-RestMethod` and `Invoke-WebRequest`
- Authentication and headers
- Parsing JSON responses

### Using `Invoke-RestMethod` and `Invoke-WebRequest`
Use these cmdlets to interact with REST APIs.

```powershell
# Example of using Invoke-RestMethod
$response = Invoke-RestMethod -Uri "https://api.example.com/data" -Method Get
Write-Output $response
```

### Authentication and Headers
Include authentication and headers in your API requests.

```powershell
# Example of adding headers and authentication
$headers = @{
    "Authorization" = "Bearer your_token"
    "Content-Type"  = "application/json"
}
$response = Invoke-RestMethod -Uri "https://api.example.com/data" -Method Get -Headers $headers
Write-Output $response
```

### Parsing JSON Responses
Parse JSON responses to work with the data.

```powershell
# Example of parsing JSON response
$response = Invoke-RestMethod -Uri "https://api.example.com/data" -Method Get
$data = $response | ConvertFrom-Json
Write-Output $data.property
```

## PowerShell Remoting
Manage remote systems with PowerShell Remoting:
- Setting up remoting
- Using `Enter-PSSession` and `Invoke-Command`
- Configuring trusted hosts and authentication

### Setting Up Remoting
Enable PowerShell Remoting on your systems.

```powershell
# Enable remoting
Enable-PSRemoting -Force
```

### Using `Enter-PSSession` and `Invoke-Command`
Run commands on remote systems.

```powershell
# Example of using Enter-PSSession
Enter-PSSession -ComputerName "RemotePC"

# Example of using Invoke-Command
Invoke-Command -ComputerName "RemotePC" -ScriptBlock { Get-Process }
```

### Configuring Trusted Hosts and Authentication
Configure trusted hosts and authentication for remoting.

```powershell
# Example of setting trusted hosts
Set-Item WSMan:\localhost\Client\TrustedHosts -Value "RemotePC"

# Example of using alternate credentials
$cred = Get-Credential
Invoke-Command -ComputerName "RemotePC" -Credential $cred -ScriptBlock { Get-Process }
```

## Modules and Packages
Extend PowerShell functionality with modules and packages:
- Installing and importing modules
- Creating custom modules
- Using the PowerShell Gallery

### Installing and Importing Modules
Install and import modules to extend functionality.

```powershell
# Example of installing a module
Install-Module -Name "PSReadLine"

# Example of importing a module
Import-Module -Name "PSReadLine"
```

### Creating Custom Modules
Create custom modules to organize your scripts.

```powershell
# Example of creating a custom module
New-Module -Name "MyModule" -ScriptBlock {
    function Get-Greeting {
        param ($Name)
        Write-Output "Hello, $Name"
    }
} | Export-ModuleMember -Function Get-Greeting
```

### Using the PowerShell Gallery
Find and install modules from the PowerShell Gallery.

```powershell
# Example of finding a module
Find-Module -Name "Pester"

# Example of installing a module from the gallery
Install-Module -Name "Pester"
```

## Best Practices
Follow best practices for writing and maintaining PowerShell scripts:
- Commenting and documentation
- Code formatting and style
- Version control with Git

### Commenting and Documentation
Add comments and documentation to your scripts for clarity.

```powershell
# Example of adding comments
# This function returns a greeting message
function Get-Greeting {
    param ($Name)
    Write-Output "Hello, $Name"
}
```

### Code Formatting and Style
Maintain consistent code formatting and style.

```powershell
# Example of consistent formatting
function Get-Greeting {
    param (
        [string]$Name
    )
    Write-Output "Hello, $Name"
}
```

### Version Control with Git
Use Git for version control to track changes and collaborate.

```powershell
# Example of initializing a Git repository
git init

# Example of committing changes
git add .
git commit -m "Initial commit"
```

