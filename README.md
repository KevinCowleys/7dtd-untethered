# 7 Days To Die Untethered

## Introduction

First off, this guide will be really technically and requires some setup. The way all of this will work is by redirecting all EOS traffic to our own local server which uses about ~5MB of memory.

## Block EOS IPs

If you're looking at this guide then you've probably already blocked these or have been wanting to block them. You can start by following the mentioned guide, but it's important that you set the IPs to **127.0.0.1** instead of the suggested 0.0.0.0.

*Remember to remove the spaces before the .com*

https://steamcommunity.com/sharedfiles/filedetails/?id=2594056744

## Requirements

[OpenResty](https://openresty.org/en/download.html#windows)  
[Win64 OpenSSL v1.1.1m Light](https://slproweb.com/products/Win32OpenSSL.html)

## OpenResty

Unzip to your preferred location.

## OpenSSL

After installation you now need to create security certificates for the api.epicgames.dev domain, because all .dev domains require it.

Open CMD and type in `cd C:\OpenSSL-Win64\bin` or your install location.

Now we need to create the certificates with the following command:

`openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout public.key -out public.crt`

This will start creating your security certificates and you can just continue by pressing enter till you get to the `Common Name` field which needs to be `api.epicgames.dev`.

You now need to move your public.key and public.crt files from the OpenSSL folder to the openresty/conf folder.

We aren't done with authentication yet, now you need to press Win+R and type in `mmc`.

Steps:  
File  
Add/Remove Snap-In...  
Certificates  
Computer account  
Finish  

Navigate to "Trusted Root Certification Authorities"  
Right click "Certificates"  
All Tasks  
Import...  
Browse and select public.crt  
Finish  

## 7dtd-untethered

Now you need to unzip the downloaded 7dtd-untethered and move the `html` and `conf` folder to your openresty folder.

It's also recommended that you open html/users.json and replace the `product_user_id` (also referred to as PUID) with your own SteamID. It's currently set to mine, `76561198074415908`. The ID will be used for your save files.

## Run OpenResty

Now you just need to cd the OpenResty folder and use the commands below to start and stop your server. 

### How to start
nginx

### How to stop
nginx -s stop

## Servers

You should now technically be able to join servers too. I haven't tested this on public servers, but EAC does it's own authentication which makes your local PUID not matter.

If you're running your own server then it should automatically be using EAC and won't be blocked by the above. EAC does it's own authentication with EOS on their own servers, which would give you the correct PUID for the server.

## Conclusion

I hope this helped anyone else struggling with the same issues as I did or whatever other reason you have. This probably won't last long, so expect it to be broken in about a year due to how 7 Days To Die updates work.
