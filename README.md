# how to install Alpine Linux on WSL

one line to install latest Alpine Linux on wsl

> default Alpine instalation has ```root``` user only, no password.


## wsl version 2
```
powershell -Command "$gg = ((Invoke-WebRequest """https://dl-cdn.alpinelinux.org/alpine/latest-stable/releases/x86_64/latest-releases.yaml""").RawContent | findstr /C:""" file: alpine-miniroot""").Trim(""" """).Trim("""file: """) ; $uri1 = """https://dl-cdn.alpinelinux.org/alpine/latest-stable/releases/x86_64/""" ; $uri = $uri1 + $gg; Invoke-WebRequest -outFile alpine.tar.gz -Uri $uri; wsl --import Alpine %UserProfile%\AlpineLinuxWsl alpine.tar.gz ; del alpine.tar.gz" && wsl -d Alpine
```

## wsl version 1
```
powershell -Command "$gg = ((Invoke-WebRequest """https://dl-cdn.alpinelinux.org/alpine/latest-stable/releases/x86_64/latest-releases.yaml""").RawContent | findstr /C:""" file: alpine-miniroot""").Trim(""" """).Trim("""file: """) ; $uri1 = """https://dl-cdn.alpinelinux.org/alpine/latest-stable/releases/x86_64/""" ; $uri = $uri1 + $gg; Invoke-WebRequest -outFile alpine.tar.gz -Uri $uri; wsl --import Alpine %UserProfile%\AlpineLinuxWsl alpine.tar.gz --version 1; del alpine.tar.gz" && wsl -d Alpine
```

## export file system and remove ( saves to users Downloads folder )
```
wsl --export Alpine %UserProfile%\Downloads\alpine.tar && wsl --unregister Alpine
```

## remove without exporting file syste
```
wsl --unregister Alpine
```

## how it works?

download https://dl-cdn.alpinelinux.org/alpine/latest-stable/releases/x86_64/latest-releases.yaml  
extract filename of latest miniroot  
download latest miniroot tar.gz from https://dl-cdn.alpinelinux.org/alpine/latest-stable/releases/x86_64/  
save as *alpine.tar.gz*  
run ```wsl --import Alpine %UserProfile%\AlpineLinuxWsl alpine.tar.gz```  
run ```del alpine.tar.gz```  
run ```wsl -d Alpine```  


## links
[Alpine linux](https://www.alpinelinux.org/)
