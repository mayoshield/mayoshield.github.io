---
title: "Crypto Mining Using Pi"
date: 2025-04-25
categories: [Project using Pi]
tags: [project, Raspberry Pi, Bitcoin Mining, Monero]
---

# Mining Monero using pi

## **Step 1: Bake your pi**
Download the latest version of pi OS from [here](https://downloads.raspberrypi.org/raspios_lite_arm64/images/).
To load the image in your SD card use any imager tool *recommeded: Raspberry pi imager: [download_here](https://downloads.raspberrypi.org/imager/imager_latest.exe)*. 
Load the operating system into the SD card using pi imager 
Start your pi

## **Step 2 (optional): For remote SSH connection to pi** 
Enter the following commands to enable and start SSH connections 
```
sudo systemctl enable ssh
sudo systemctl start ssh
```

If you are using windows machine to make SSH connection to pi:  
### Install open ssh client for windows  
Enter the following command in the command prompt  ```ssh pi@local_IP``` *replace pi with your pi username and local_IP to its local IP address*  
### Use Termux on android *(Recommeded)*    :  
Install Termux from Playstore  
Enter the following commands to install open ssh client in termux  ```pkg update && pkg install openssh```  
Enter these commands to connect to pi  ```ssh pi@local_IP``` *(replace pi with your pi username and local_IP to its local IP address)*   
You can find Pi local ip using  ```ifconfig``` command

```
mayo@raspberrypi:~ $ ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.100.13 (Local IPv4) netmask 255.255.255.0  broadcast 192.168.100.255
        inet6 fe80::e674:3d39:dcc2:5a57  prefixlen 64  scopeid 0x20<link>
        ether d8:3a:dd:d6:05:d0  txqueuelen 1000  (Ethernet)
        RX packets 57108  bytes 23981378 (22.8 MiB)
        RX errors 0  dropped 11238  overruns 0  frame 0
        TX packets 14877  bytes 1415104 (1.3 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 23  bytes 2564 (2.5 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 23  bytes 2564 (2.5 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

## **Step 3: Setting up Pi**
Run the following command to update package lists
```
sudo apt update
```
Clone the xmrig repo from gitclone 
```
git clone https://github.com/xmrig/xmrig.git
```
Enter the following commands:
```
cd xmrig
mkdir build
cd build
cmake ..
make
```
## **Step 4: Setting up a WALLET**
[Download_you_wallet_here](https://web.getmonero.org/downloads/)


![Screenshot 2025-04-27 021508.png](<https://ik.imagekit.io/MK1/Website/Screenshot%202025-04-27%20021508.png?updatedAt=1745700885723>)


Download and install monero GUI wallet  
Open and copy your Wallet address from here...

![wallet.png](https://ik.imagekit.io/MK1/Website/Screenshot%202025-04-27%20021944.png?updatedAt=1745700980163)

## **Step 5: Setting up the pool**
Create a config.json file in build folder ```nano config.json```  
Copy and paste this configuration and replace "your wallet address" with your wallet address


```
{
    "api": {
        "id": null,
        "worker-id": null
    },
    "http": {
        "enabled": false,
        "host": "127.0.0.1",
        "port": 0,
        "access-token": null,
        "restricted": true
    },
    "autosave": true,
    "background": false,
    "colors": true,
    "title": true,
    "randomx": {
        "init": -1,
        "init-avx2": -1,
        "mode": "auto",
        "1gb-pages": false,
        "rdmsr": true,
        "wrmsr": false,
        "cache_qos": false,
        "numa": true,
        "scratchpad_prefetch_mode": 1
    },
    "cpu": {
        "enabled": true,
        "huge-pages": true,
        "huge-pages-jit": false,
        "hw-aes": null,
        "priority": null,
        "memory-pool": false,
        "yield": true,
        "argon2-impl": null,
        "argon2": [0, 1, 2, 3],
        "cn": [0, 1, 2, 3],
        "cn-heavy": [0, 1, 2, 3],
        "cn-lite": [0, 1, 2, 3],
        "cn-pico": [0, 1, 2, 3],
        "cn/upx2": [0, 1, 2, 3],
        "ghostrider": [
            [8, 0],
            [8, 1],
            [8, 2],
            [8, 3]
        ],
        "rx": [0, 1, 2, 3],
        "rx/wow": [0, 1, 2, 3],
        "cn-lite/0": false,
        "cn/0": false,
        "rx/arq": "rx/wow"
    },
    "opencl": {
        "enabled": false,
        "cache": true,
        "loader": null,
        "platform": "AMD",
        "adl": true
    },
    "cuda": {
        "enabled": false,
        "loader": null,
        "nvml": true
    },
    "log-file": null,
    "donate-level": 1,
    "donate-over-proxy": 1,
    "pools": [
        {
            "algo": null,
            "coin": null,
            "url": "gulf.moneroocean.stream:10128",
            "user": "Your wallet address",
            "pass": "x",
            "rig-id": null,
            "nicehash": false,
            "keepalive": true,
            "enabled": true,
            "tls": false,
            "sni": false,
            "tls-fingerprint": null,
            "daemon": false,
            "socks5": null,
            "self-select": null,
            "submit-to-origin": false
        }
    ],
    "retries": 5,
    "retry-pause": 5,
    "print-time": 60,
    "health-print-time": 60,
    "dmi": true,
    "syslog": false,
    "tls": {
        "enabled": false,
        "protocols": null,
        "cert": null,
        "cert_key": null,
        "ciphers": null,
        "ciphersuites": null,
        "dhparam": null
    },
    "dns": {
        "ipv6": false,
        "ttl": 30
    },
    "user-agent": null,
    "verbose": 0,
    "watch": true,
    "pause-on-battery": false,
    "pause-on-active": false
}
```

Save the file and inside build folder run this command ```./xmrig```  
You might have to Configure your DNS if your results are like this:  
![Screenshot 202...27 024048.png](https://ik.imagekit.io/MK1/Website/Screenshot%202025-04-27%20024048.png?updatedAt=1745702024907)  
press CTRL+C to stop the mining and enter the following commands to configure your DNS to use google's DNS servers  ```sudo bash -c 'echo "nameserver 8.8.8.8" > /etc/resolv.conf'```  
Retart the mining using ```./xmrig```  

![Screenshot 202...27 024244.png](https://ik.imagekit.io/MK1/Website/Screenshot%202025-04-27%20024244.png?updatedAt=1745702245999)  
Now you have successfully started mining Monero **CONGRATULATIONS !!**

## Extra commands
while mining press H to view your CPU hashing effeciency  
![Screenshot 202...27 025131.png](https://ik.imagekit.io/MK1/Website/Screenshot%202025-04-27%20025131.png)  
Or press S to view any shares you have accpeted form the pool  
![]()  
You can use these commands for specific actions  
![Screenshot 202...27 025441.png](https://ik.imagekit.io/MK1/Website/Screenshot%202025-04-27%20025441.png)  
For additional information on your shares, go to [this website](https://moneroocean.stream/) and enter your wallet address  
![2025-04-27 03_... Explorer.png](https://ik.imagekit.io/MK1/Website/2025-04-27%2003_01_03-Screenshots%20-%20File%20Explorer.png)