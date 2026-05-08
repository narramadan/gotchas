# Development Environment Setup on Windows

## WSL

```
$ wsl --install Ubuntu-26.04

$ wsl -u root
$ sudo apt update && sudo apt upgrade
```

## Node

Fast Node Manager - https://github.com/Schniz/fnm/blob/master/docs/commands.md

```
$ winget install Schniz.fnm
$ fnm completions --shell powershell
$ fnm env --use-on-cd | Out-String | Invoke-Expression
$ fnm install --lts
```

## Java

```
$ winget search Microsoft.OpenJDK
$ winget install Microsoft.OpenJDK.25
$ $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User")
$ java -version
```

## Go

```
$ winget search golang.go
$ winget install GoLang.Go
$ $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User")
$ go version
```

## Python

```
$ winget search Python.Python
$ winget install Python.Python.3.9
$ $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + [System.Environment]::GetEnvironmentVariable("Path","User")
$ python -version
```
