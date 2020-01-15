---
layout: post
title: Powershell
categories: study powershell
---

### [console]
 - BEEP sound in the console: `[console]::beep(<frequency>,<duration>)` for ex : `[console]::beep(200,300)`
### How To?
- SET and INVOKE a command
 - SET a variable: `$<variableName>="<expression/command>"`
  For ex. : `$pushAll="git push origin head; git push poc head"`
 - INVOKE this variable as an expression: `Invoke-Expression $variableName` or `iex $variableName`
  For ex. `iex $pushAll`
 - EXECUTE a command with different variables?
  - `'var1','var2' | ForEach {echo $_}` will output the following in the console:  
    `var1`  
    `var2`  
