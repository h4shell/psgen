# psgen

![Python 3.x](https://img.shields.io/badge/python-3.x-yellow.svg)

psgen is a powershell payload generator tool for hacking. It can be used to generate, minify, and encode the powershell payload (e.g., reverse-shell, download-file, runas) to copyable text format.

*NOTE : This project creates for helping me to generate the copyable powershell payload and run it on window cmd shell.*

## Installation

### Manual

The latest zip ball can be downloaded [HERE](https://github.com/bongtrop/psgen/archive/master.zip). Or perform the following commands.

```bash
git clone https://github.com/bongtrop/psgen.git
cd psgen
pip install -r requirements.txt
python setup.py install
```
### PIP

Easily install with the following command.

```bash
pip install git+https://github.com/h4shell/psgen.git
```

## Usage

For getting list of options, please perform:

```bash
psgen -h
```

## Example

For usage example, I generate and exeute hello-world payload:

```
$ psgen -l

Powershell Payloads
===================
╒══════════════════════╤═══════════════╤══════════════════════════════════════════╕
│ Name                 │ Author        │ Description                              │
╞══════════════════════╪═══════════════╪══════════════════════════════════════════╡
│ check-dir-permission │ BHARAT SUNEJA │ Check directory permission               │
├──────────────────────┼───────────────┼──────────────────────────────────────────┤
│ example              │ Jusmistic     │ Print a word [COUNT] time(s)             │
├──────────────────────┼───────────────┼──────────────────────────────────────────┤
│ download-file        │ Jusmistic     │ Download file from url                   │
├──────────────────────┼───────────────┼──────────────────────────────────────────┤
│ http-eval            │ bongtrop      │ Download and execute ps1 script from URL │
├──────────────────────┼───────────────┼──────────────────────────────────────────┤
│ find-file            │ bongtrop      │ Find files from their filename           │
├──────────────────────┼───────────────┼──────────────────────────────────────────┤
│ runas                │ bongtrop      │ Run a progrom as another user            │
├──────────────────────┼───────────────┼──────────────────────────────────────────┤
│ find-file-content    │ bongtrop      │ Find files from their content            │
├──────────────────────┼───────────────┼──────────────────────────────────────────┤
│ reverse-shell        │ @nikhil_mitt  │ Spawn Reverse shell                      │
╘══════════════════════╧═══════════════╧══════════════════════════════════════════╛

$ psgen example -s

Payload Detail
==============
Payload Name: example
Payload Author: Jusmistic
Payload Description: Print a word [COUNT] time(s)
Payload Options:
  - word => 'The word that you want to print'
  - count => 'Times you want to print the word'

$ psgen example "word=Hello World\!" count=5

Payload Detail
==============
Payload Name: example
Payload Author: Jusmistic
Payload Description: Print a word [COUNT] time(s)
Payload Options: word='Hello World!', count='5', 

Payload Output
==============
powershell.exe -E RgBvAHIAKAAkAGEAPQAwADsAIAAkAGEAIAAtAGwAdAAgADUAOwAgACQAYQArACsAKQB7AFcAcgBpAHQAZQAtAEgAbwBzAHQAIAAiAEgAZQBsAGwAbwAgAFcAbwByAGwAZAAhACIAOwB9AA==

$ # Using Linux powershell (pwsh) to test the generated 
$ pwsh -E RgBvAHIAKAAkAGEAPQAwADsAIAAkAGEAIAAtAGwAdAAgADUAOwAgACQAYQArACsAKQB7AFcAcgBpAHQAZQAtAEgAbwBzAHQAIAAiAEgAZQBsAGwAbwAgAFcAbwByAGwAZAAhACIAOwB9AA==
Hello World!
Hello World!
Hello World!
Hello World!
Hello World!
```

## Dev

For developing the powershell payload, the metadata must be set. And Jinja2 syntax can be used in the powershell script as follows:

**File:** payload/example.ps1
```
##########
Name: example
Author: Jusmistic
Description: Print a word [COUNT] time(s)
Options:
    word: "The word that you want to print"
    count: "Times you want to print the word"
##########

For ($i=0; $i -lt {{ count }}; $i++) {
    Write-Host "{{ word }}";
}
```

The psgen tool also loads payloads in the home directory as `~/.psgen/payload`. Therefore, you can put your payload there (e.g., `~/.psgen/payload/shutdown.ps1`).

*Please note that due to powershell minifier module all powershell command in the payload must end with `;` character.*
