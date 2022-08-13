# 手机刷lineageos系统(android 11)
## 1. 备份好手机数据
## 2. 下载所需工具
### 下载`adb.exe fastboot.exe`  
>下载地址：`https://dl.google.com/android/repository/platform-tools-latest-windows.zip`  
### 下载`twrp-3.6.1_9-0-oneplus3.img`  
>一加三下载地址：`https://dl.twrp.me/oneplus3/twrp-3.6.1_9-0-oneplus3.img`  
>其它手机型号下载地址`https://twrp.me/Devices`
### 下载lineage系统[`lineage-18.1-20220502-nightly-oneplus3-signed.zip`]  
>一加三下载地址：`https://mirrorbits.lineageos.org/full/oneplus3/20220502/lineage-18.1-20220502-nightly-oneplus3-signed.zip`  
>其它手机型号下载地址`https://download.lineageos.org`
### [可选]下载谷歌全家桶[`MindTheGapps-11.0.0-arm64-20220217_100228.zip`]  
>`lineage-18.1-20220502-nightly-oneplus3-signed.zip` 对应的下载地址为： `http://downloads.codefi.re/jdcteam/javelinanddart/gapps/MindTheGapps-11.0.0-arm64-20220217_100228.zip`  
>其它系统下载地址：`https://wiki.lineageos.org/gapps`  
### 下载`Magisk-v24.3.apk`  
>下载地址:`https://github.com/topjohnwu/Magisk/releases`  
## 3. 刷入lineageos系统
>1. 新建文件夹`刷机`，把上面下载的资源放入其中。
>2. 手机打开`开发者选项`  
>3. 开启USB调试  
>4. USB连接电脑  
>5. 电脑上打开`cmd`  
>6. 进入刷机文件夹`cd C:\Users\Welcome WQ\Desktop\刷机`  
>### 解锁手机OEM  
>1. `adb.exe reboot bootloader`  
>2. `fastboot.exe oem unlock`  
>### 刷入twrp-3.6.1_9-0-oneplus3.img  
>2. `fastboot.exe flash recovery twrp-3.6.1_9-0-oneplus3.img`  
>### 安装lineage  
>1. 重启手机到`recovery模式`  
>2. `Wipe -> Format Data`  
>3. `Advanced Wipe -> Cache and System`  
>4. `Advanced -> ADB Sideload`  
>5. 安装lineage系统：`adb sideload lineage-18.1-20220502-nightly-oneplus3-signed.zip`  
>6. [可选]安装谷歌全家桶: `adb sideload MindTheGapps-11.0.0-arm64-20220217_100228.zip`  
>### [可选]去掉WiFi受限的提示  
>1. `adb.exe shell settings put global ntp_server ntp1.aliyun.com`  
>2. `adb.exe shell settings put global captive_portal_http_url http://connect.rom.miui.com/generate_204`  
>3. `adb.exe shell settings put global captive_portal_https_url https://connect.rom.miui.com/generate_204`   
## 4. 手机root  
>1. 手机安装`Magisk-v24.3.apk`  
>> `adb.exe install Magisk-v24.3.apk`  
>2. 从手机安装包`lineage-18.1-20220502-nightly-oneplus3-signed.zip`中解压出`boot.img`
>3. 把`boot.img`发送到手机;  
>> 我这里使用adb.exe工具发送，`adb.exe push C:\Users\Welcome WQ\Desktop\刷机\lineage-18.1-20220502-nightly-oneplus3-signed\boot.img /storage/emulated/0/Download`  
>> 不会的可以使用别的方式，如微信传输。  
>4. 在手机上用`Magisk-v24.3.apk`生成`magisk_patched***.img`  
>5. 把手机上生成的`magisk_patched***.img`发送到电脑  
>> 我这里使用adb.exe工具发送，`adb.exe pull /storage/emulated/0/Download/magisk_patched***.img C:\Users\Welcome WQ\Desktop\刷机`
>6. 手机进入bootloader模式`adb.exe reboot bootloader`  
>7. 把`magisk_patched***.img`刷到手机
>> `fastboot.exe flash boot magisk_patched-24300_6MwHT.img`  