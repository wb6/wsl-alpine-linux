# how to install Alpine Linux on WSL

one line to install latest Alpine Linux on wsl

> default Alpine instalation has ```root``` user only, no password.


## wsl version 2
```
powershell -Command "$_file = ((Invoke-WebRequest 'https://dl-cdn.alpinelinux.org/alpine/latest-stable/releases/x86_64/latest-releases.yaml').RawContent | findstr /C:' file: alpine-miniroot').Trim(' ').Trim('file: ') ; $_uri = 'https://dl-cdn.alpinelinux.org/alpine/latest-stable/releases/x86_64/' ; $uri = $_uri + $_file; Invoke-WebRequest -outFile alpine.tar.gz -Uri $uri; wsl --import Alpine %UserProfile%\AlpineLinuxWsl alpine.tar.gz ; del alpine.tar.gz" && wsl -d Alpine
```

## wsl version 1
```
powershell -Command "$_file = ((Invoke-WebRequest 'https://dl-cdn.alpinelinux.org/alpine/latest-stable/releases/x86_64/latest-releases.yaml').RawContent | findstr /C:' file: alpine-miniroot').Trim(' ').Trim('file: ') ; $_uri = 'https://dl-cdn.alpinelinux.org/alpine/latest-stable/releases/x86_64/' ; $uri = $_uri + $_file; Invoke-WebRequest -outFile alpine.tar.gz -Uri $uri; wsl --import Alpine %UserProfile%\AlpineLinuxWsl alpine.tar.gz --version 1; del alpine.tar.gz" && wsl -d Alpine
```

## export file system and remove ( saves to users Downloads folder )
```
wsl --export Alpine %UserProfile%\Downloads\alpine.tar && wsl --unregister Alpine
```

## remove without exporting file syste
```
wsl --unregister Alpine
```

## how does it works?

download https://dl-cdn.alpinelinux.org/alpine/latest-stable/releases/x86_64/latest-releases.yaml  
extract filename of latest miniroot  
download latest miniroot tar.gz from https://dl-cdn.alpinelinux.org/alpine/latest-stable/releases/x86_64/  
save as *alpine.tar.gz*  
run ```wsl --import Alpine %UserProfile%\AlpineLinuxWsl alpine.tar.gz```  
run ```del alpine.tar.gz```  
run ```wsl -d Alpine```  


# extras

## setup wsl2 bridged network

### install Hyper-V virtual switch

```
powershell -Command "Get-NetAdapter"
```

```
powershell -Command "New-VMSwitch -Name wsl-switch  -NetAdapterName <netadapter-name>"
```

### .wslconfig 
edit ```.wslconfig``` file in ```%UserProfile%``` folder and add 

```
[wsl2]
networkingMode = bridged
vmSwitch = wsl-switch
```

## install openrc

```
apk add openrc
touch /run/openrc/softlevel
```


## install sshd
```
apk add openssh
ssh-keygen -A
rc-update add sshd
rc-service sshd restart
```



## install docker
```
apk add docker
addgroup root docker
rc-update add docker default
rc-service docker restart
```

# links
[Alpine linux](https://www.alpinelinux.org/)
