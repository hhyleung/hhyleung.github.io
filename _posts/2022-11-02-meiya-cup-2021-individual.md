---
title: "美亞杯 2021 - 個人賽"
excerpt: "Writeup for the Meiya Cup 2021 - Individual round"
last_modified_at: 2022-11-02
stickies: true
stickies_path: "/assets/stickies/meiya-cup.png"
toc: true
toc_label: "Content"
toc_sticky: true
categories:
  - Writeups
tags:
  - Meiya Cup
---

## 案情背景
2021年10月某日早上，本市一个名为“大路建设”的高速公路工地主管发现办公室的计算机被加密并无法开启，其后收到了勒索通知。考虑到高速公路的基建安全，主管决定报警。警方调查人员到达现场取证，发现办公室内有三部个人计算机，通过一个老款路由器接入互联网。经调查相关电子证据后，警方怀疑一位本地男子–阿力士与本案有关，并将他拘捕。现在你被委派处理这起案件，请由以下资料分析阿力士在本案中的违法犯罪行为，并还原事件经过。

<br>

## 检材
1. 阿力士的背景资料：调查报告\阿力士\阿力士背景資料.pdf
2. 阿力士的调查报告：调查报告\阿力士\阿力士調查報告.pdf
3. 警方现场勘查的调查报告：调查报告\警方现场勘查的调查报告\现场勘查的调查报告.pdf
4. 高速公路工地办公室路由器的记录：image\VTM\Router Log\20211018.log
5. 工地主管办公室计算机的电子数据：image\VTM\VTM_computer\VTM-computer.e01 及 
6. 工地主管办公室计算机存储器提取的镜像文件：image\VTM\VTM_computer_memdump\Vtm-computer-memdump.mem
7. 工地主管移动电话的电子数据：image\VTM\VTM_iphone6\Apple_iPhone 6 (A1586)\VTM iPhone6.ufdr
8. 阿力士计算机的电子数据：image\Alex\Alex_Windows_Computer\Alex_Windows_Computer.E01
9. 阿力士FTP服务器的电子数据：image\Alex\FTP\FTP.E01
10. 阿力士移动电话(1)的电子数据：image\Alex\Alex iPHone 12 pro\Apple_A2341 MGLW3LL_A iPhone 12 Pro\Alex iPHone 12 pro.ufdr
11. 阿力士移动电话(2)的电子数据：\image\Alex\Alex iPhone XR\Apple_iPhone XR (A2105)\Alex iPhone XR.ufdr

<br>

## 题目
> 1. [单选题] 工地主管电话的微信账号是什么? (1分)
> A. Kasier751111
> B. Kasierlee751111
> C. Kasierlee
> D. 以上皆非

The evidence in interest is the VTM iPhone 6 belonged to the manager. The provided `CellebriteReader` was used to read the image file `VTM iPhone 6.ufdr`.

Searched for the keywords "wechat" and "weixin" but both returned no results. It is believed that WeChat was not used at all and therefore, no associated account information.

![meiya-cup-2021-ip6-wechat.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ip6-wechat.jpg)

答案：`D`

<br>

> 2. [填空题] 工地主管的隔空投送装置编号是什么? (请以英文全大写及阿拉伯数字回答) (1分)

The AirDrop ID is right at the top of the `Device Info` section at the `Extraction Summary` page.

![meiya-cup-2021-ip6-airdrop.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ip6-airdrop.jpg)

答案：`780F624DF099`

<br>

> 3. [单选题] 工地主管电话的哪一个应用程序有关于于经纬度24.490474, 118.110220的纪录? (2分)
> A. 照片
> B. WhatsApp
> C. Apple Maps
> D. 以上皆非

Searched for the keyword "24.490474" and the result matched the location, showing the information source as Apple Maps.

![meiya-cup-2021-ip6-location.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ip6-location.jpg)

答案：`C`

<br>

> 4. [多选题] 工地主管的手提电话中下列哪些数据正确? (1分)
> A. iOS版本为12.5.4
> B. IMEI为454120637213361
> C. Apple ID为kaiserlee3660@gmail.com
> D. 手机曾经安装dropbox应用程序

The first three options can all be found under the `Device Info` section. The OS version and Apple ID are correct, while the IMEI should be `359282063436571`, the listed one should be the IMSI number.

Searched for the keyword "dropbox" and no results were found, it is believed that the device had never installed the application Dropbox.

![meiya-cup-2021-ip6-info.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ip6-info.jpg)

答案：`A,C`

<br>

> 5. [填空题] 工地主管的电话最常使用的浏览器是什么? (请以英文全大写回答) (1分)

Looking at the `Search & Web > Web History` part under `Analyed Data`, there are only entries for the browser Safari.

![meiya-cup-2021-ip6-browser.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ip6-browser.jpg)

答案：`SAFARI`

<br>

> 6. [单选题] 工地主管的电话连接过哪一个WiFi? (1分)
> A. Kaiser Lee
> B. Kaiser
> C. Free Wifi
> D. Kaiser Home

The `Devices & Networks > Wireless Networks` page revealed 2 previously connected WiFi, with the SSID as `Kaiser Lee` and `Apple Store`.

![meiya-cup-2021-ip6-wifi.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ip6-wifi.jpg)

答案：`A`

<br>

> 7. [多选题] 工地主管与Alex Chan的Whatsapp对话中，曾提及以下哪个TeamViewer的用户号码? (3分)
> A. 435334881
> B. 453851521
> C. 435475200
> D. 456874155
> E. 435270306

The `Messages > Chats > WhatsApp` page revealed the conversation between the manager and Alex Chan. From the chat history, it was found that the manager has sent four photos of the TeamViewer screens and each of them contained an TeamViewer ID, with one of them being a duplicate.

![meiya-cup-2021-ip6-teamviewer-1.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ip6-teamviewer-1.jpg)

![meiya-cup-2021-ip6-teamviewer-2.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ip6-teamviewer-2.jpg)

答案：`A,C,E`

<br>

> 8. [填空题] 工地主管的WhatsApp中有多少个黑名单的记录? (请以阿拉伯数字回答) (2分)

From the source file of the chat history viewed earlier, the location of the WhatsApp database was found to be at `「Kaiser」的 iPhone/mobile/Containers/Shared/AppGroup/group.net.whatsapp.WhatsApp.shared/ChatStorage.sqlite`.

![meiya-cup-2021-ip6-blacklist-1.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ip6-blacklist-1.jpg)

Navigating to the database revealed the table `ZWABLACKLISTITEM`, which should contains the blacklisted records and the number was found to be 0.

![meiya-cup-2021-ip6-blacklist-2.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ip6-blacklist-2.jpg)

答案：`0`

<br>

> 9. [多选题] 以下哪个蓝牙装置的Uuid曾连接过工地主管的手机? (2分)
> A. 7F1FE70D-2B15-C245-853D-4196F13CC446
> B. 1B057C1D-83D3-99A6-D2B1-EC54846C7CEE
> C. 134ACD1-83D3-99A6-D2B1-EC54846C7CEE
> D. 7D1BE70D-2C16-D246-851D-491613DD776

The `Devices & Networks > Device Connectivity > Bluetooth` page revealed two Bluetooth connections, yet the UUID was not displayed. The source file revealed the location of the entries at `「Kaiser」的 iPhone/containers/Shared/SystemGroup/systemgroup.com.apple.bluetooth/Library/Database/com.apple.MobileBluetooth.ledevices.other.db`.

![meiya-cup-2021-ip6-bluetooth-1.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ip6-bluetooth-1.jpg)

Navigating to the database revealed the two UUIDs of the two previously connected Bluetooth devices.

![meiya-cup-2021-ip6-bluetooth-2.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ip6-bluetooth-2.jpg)

答案：`A,B`

<br>

> 10. [填空题] 工地主管计算机的E盘的Bitlocker修复密钥标识符是甚么? (请以英文全大写及阿拉伯数字回答，不用输入"-") (1分)

Meiya Pico's `ForensicsMaster` was used to analyse the image file `VTM-computer.e01`. After processing the image file, right clicked on the partition E to bring up the `BitLocker Decryption` prompt. The `Recovery Key` option revealed the key GUID as `36EBC180-95F7-41FF-BE5B-4E56E7AF48B1`.

![meiya-cup-2021-vtm-bitlocker.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-vtm-bitlocker.jpg)

答案：`36EBC18095F741FFBE5B4E56E7AF48B1`

<br>

> 11. [填空题] 工地主管计算机內的FTP程序FileZilla的用户名称是甚么? (请以英文全大写及阿拉伯数字回答) (3分)

The `Download Tools Analysis > FileZilla > Client > Quick Connect Record` page revealed the user name as `alex`.

![meiya-cup-2021-vtm-filezilla.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-vtm-filezilla.jpg)

答案：`ALEX`

<br>

> 12. [填空题] 工地主管的Team Viewer ID是甚么? (请以英文全大写及阿拉伯数字回答) (2分)

The TeamViewer ID was found earlier from the WhatsApp chat history as `435 270 306`.

答案：`435270306`

<br>

> 13. [填空题] 工地主管的Team Viewer与哪一个ID连接? (请以英文全大写及阿拉伯数字回答) (3分)

The `Others > TeamViewer > Connected By Other Machines Record` page revealed the TeamViewer ID `420190768` was previously connected to the device.

![meiya-cup-2021-vtm-teamviewer.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-vtm-teamviewer.jpg)

答案：`420190768`

<br>

> 14. [多选题] 工地主管曾用计算机浏览器作搜寻，以下哪一个关键词他曾经搜寻? (3分)
> A. tiktok
> B. web whatsapp
> C. facebook
> D. lihkg
> E. hkgolden
> F. web wechat

The `Web History > Google Chrome > IDS_BROWSER_SEARCH`  page revealed the web search history. The keywords "facebook" and "web whatsapp" were found in the history. Note that the keyword "lighk" was searched instead of "lihkg".

![meiya-cup-2021-vtm-search.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-vtm-search.jpg)

答案：`B,C`

<br>

> 15. [填空题] 工地主管计算机的Windows系统的产品标识符是甚么? (请以英文全大写及阿拉伯数字回答，不用输入"-") (1分)

The `System Artifacts > System Info > System Info` revealed the Windows Product ID to be `00331-10000-00001-AA962`.

![meiya-cup-2021-vtm-productid.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-vtm-productid.jpg)

答案：`003311000000001AA962`

<br>

> 16. [填空题] 工地主管曾用计算机使用WhatsApp，他曾和以下哪个电话号码沟通? (请以阿拉伯数字回答) (2分)

Searched for the keyword "whatsapp" and revealed the web search history and proved the usage of web WhatsApp on the computer. However, the web history did not reveal any phone numbers.

![meiya-cup-2021-vtm-whatsapp-1.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-vtm-whatsapp-1.jpg)

Referring back to the iPhone 6 analysed earlier, after scrolling through all of the conversations, it was found that the manager has only replied Alex Chan and another unknown contact shortly. It is believed that the question is referring to the number of Alex Chan, which was found to be `85246761157`.

![meiya-cup-2021-vtm-whatsapp-2.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-vtm-whatsapp-2.jpg)

答案：`85246761157`

<br>

> 17. [多选题] 工地主管计算机的用户名称是甚么? 其用户标识符是甚么? (2分)
> A. 用户名称：PC1
> B. 用户名称：PC2
> C. 用户名称：PC3
> D. 用户标识符：0x000003E7
> E. 用户标识符：0x000003E8
> F. 用户标识符：0x000003E9

The `System Artifacts > System Info > User Info` page revealed the user account information. The account `PC1` was found to have the SID `S-1-5-21-1376663006-2626393931-4032423365-1001`. Converting the last part of the SID `1001` from decimal to hexadecimal gives `0x03E9`.

![meiya-cup-2021-vtm-user.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-vtm-user.jpg)

答案：`A,F`

<br>

> 18. [单选题] 工地主管计算机的预设浏览器是甚么? (2分)
> A. Chrome
> B. Firefox
> C. Safari
> D. 以上皆否

The registry key at `HKCU\SOFTWARE\Microsoft\Windows\Shell\Associations\URLAssociations\http\UserChoice` stores the default application handler for websites, ie the default browser.

![meiya-cup-2021-vtm-browser-1.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-vtm-browser-1.jpg)

The registry hive at `C:\Users\PC1\NTUSER.dat` was parsed with the `Registry Parser`. The registry key was navigated and revealed the default browser as Chrome.

![meiya-cup-2021-vtm-browser-2.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-vtm-browser-2.jpg)
# 18. D
答案：`A`

<br>

> 19. [填空题] 工地主管计算机的其中一个分区被人加密，分区内的电子表格Material3.xlsx的哈希值(SHA1)是甚么? (请以英文全大写及阿拉伯数字回答) (1分)

The BitLocker recovery key is usually stored within the text file named after the key identifier. Searched for the keyword "36EBC180" and revealed the file at `C:/Users/PC1/Desktop/BitLocker Recovery Key 36EBC180-95F7-41FF-BE5B-4E56E7AF48B1.TXT`.

![meiya-cup-2021-vtm-material-1.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-vtm-material-1.jpg)

However, when navigated to the location, the file was no longer existing.

![meiya-cup-2021-vtm-material-2.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-vtm-material-2.jpg)

At a later stage when the other image files were also analysed, the keyword search was done again and revealed the recovery key `209451-527087-001254-240735-481855-489566-611721-343497`.

![meiya-cup-2021-vtm-material-3.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-vtm-material-3.jpg)

The actual file was located in the `FTP.E01` image file, located at `\var\lib\docker\overlay2\575db3795cb5fff7cadb347f10cfcaad5fd5fe3e5b3e31418ffdd415cf754e53\diff\home\Dangerous_Project\1\BitLocker Recovery Key 36EBC180-95F7-41FF-BE5B-4E56E7AF48B1.TXT`.

![meiya-cup-2021-vtm-material-4.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-vtm-material-4.jpg)

Upon decrypting the partition with the `BitLocker Decryption`, the file in interest was found at `E:\Material info\Material3.xlsx`. The SHA1 hash was calculated with `Hash Current File`.

![meiya-cup-2021-vtm-material-5.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-vtm-material-5.jpg)

答案：`40418B21F6C3E4AF306D5EF3B80A776DA72FC1D2`

<br>

> 20. [多选题] 路由器的记录中显示以下有哪些IP是公司的电子器材? (3分)
> A. 192.168.40.128
> B. 192.168.40.129
> C. 192.168.40.130
> D. 192.168.40.131
> E. 192.168.40.132

The log file `20211018.log` was opened with `Notepad++` and the IPs were searched within the log file. Apart from the IP `192.168.40.132`, all of the other IPs were found within the log.

![meiya-cup-2021-log-ip.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-log-ip.jpg)

# 20. B,C
答案：`A,B,C,D`

<br>

> 21. [填空题] 路由器的记录中显示公司的计算机下载了FTP软件，该下载网站的IP是什麼?(请以亚拉伯数字作答，省去"."符号) (3分)

It was found previously that the FTP client FileZilla was used. The keyword "filezilla" was searched and revealed the IP `49.12.121.47`.

![meiya-cup-2021-log-filezilla.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-log-filezilla.jpg)

答案：`491212147`

<br>

> 22. [多选题] 路由器的记录中显示公司计算机的资料用FTP软件传到了甚么IP地址及利用端口? (2分)
> A. IP地址：2*.2*.2*.114
> B. IP地址：8*.8*.1*.20
> C. IP地址：1*.1*.0*.13
> D. 端口：21
> E. 端口：80

Previously when finding for the FileZilla user name, the IP `218.225.242.114` and port `23` were also revealed. When searched for the regex `2\d+\.2\d+\.2\d+\.114` in the log, the same IP was found but with the port `21`, which matched the answer options. The other IPs were also found in the log file, but does not seem to match the context of FTP traffic.

![meiya-cup-2021-log-ftp.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-log-ftp.jpg)

答案：`A,D`

<br>

> 23. [多选题] 路由器的记录中显示以下哪些关键词是表示公司计算机与外界网络联机? (2分)
> A. destination
> B. ICMP echo request
> C. inside
> D. outside
> E. 以上皆是

From the log entries identified in the previous two questions, the external network connections were logged in the format of `to outside: <IP>/<port> (<IP>/<port>), destination <IP>`.

答案：`A,D`

<br>

> 24. [单选题] 路由器的记录中显示哪一个IP曾以teamviewer连接公司计算机? (1分)
> A. 110.152.0.14
> B. 52.152.117.114
> C. 180.152.0.13
> D. 83.26.80.131

Searched for the keyword "teamviewer" but returned no results. According to TeamViewer's documentation, the main port used is `5938`.

![meiya-cup-2021-log-teamviewer-1.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-log-teamviewer-1.jpg)

Searched for the keyword "/5938" and the only external IP found was `52.152.117.114`.

![meiya-cup-2021-log-teamviewer-2.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-log-teamviewer-2.jpg)

答案：`B`

<br>

> 25. [多选题] 路由器的记录中显示以下哪一个有可能是以teamviewer遥控公司计算机的时间? (3分)
> A. 09:31，09:37
> B. 09:33，09:39
> C. 10:29，10:36
> D. 10:40
> E. 10:42

Bookmarked all lines containing the keyword "/5938" and removed all unmarked lines. The remaining logs revealed the TeamViewer connections were likely to be happened at `09:31:12`, `09:37:45`, `10:29:15`, `10:36:45`, and `10:42:14`.

![meiya-cup-2021-log-teamviewer-3.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-log-teamviewer-3.jpg)

答案：`A,C,E`

<br>

> 26. [填空题] 路由器的记录中显示有多少电子器材有可能曾被入侵? (请以阿拉伯数字作答) (2分)

From the WhatsApp chat history viewed previously, it is believed that a total of three machines were compromised (the three TeamViewer IDs).

答案：`3`

<br>

> 27. [多选题] 阿力士iPhone 12 pro电话于2021年10月21日，以下哪一张相片可能曾被分享 (UTC+8)? (3分)
> A. IMG_0011.HEIC
> B. IMG_0010.HEIC
> C. IMG_0009.HEIC
> D. IMG_0008.HEIC
> E. IMG_0007.HEIC

Switching to the image file `Alex iPHone 12 pro.udfr`. At the `Media > Images` page, it was found that none of the images has the timestamp 2021-10-21, which made sense as sharing an image might not have modified the timestamps.


![meiya-cup-2021-ip12-image-1.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ip12-image-1.jpg)

When searched for the keywords of the image names, only the image `IMG_0010.HEIC` was found under an `OutgoingTemp` directory. The name is the only hint that matches the question context.

![meiya-cup-2021-ip12-image-2.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ip12-image-2.jpg)

# 27. B,C,D
答案：`B`

<br>

> 28. [单选题] 阿力士iPhone 12 pro电话中哪一张相片可能曾被修改拍摄时间? (2分)
> A. IMG_0011.HEIC
> B. IMG_0010.HEIC
> C. IMG_0009.HEIC
> D. IMG_0008.HEIC

There were multiple duplicated images, but when checking at the timestamps of the duplicated pairs, most of them were the same or with a different of a second. Except for the image `IMG_0011.HEIC`, which the duplicate has a different name `PreviewWellImage.tiff` and the timestamps were almost a minute apart.

![meiya-cup-2021-ip12-image-3.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ip12-image-3.jpg)

答案：`A`

<br>

> 29. [填空题] 阿力士iPhone 12 pro 的GSM媒体访问控制地址是什么? (请以英文全大写及阿拉伯数字回答，不用输入“:”) (2分)

Google searched for the keyword in question and seemed to be pointing at the MAC address, which was found at the `Device Info` part.

![meiya-cup-2021-ip12-mac.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ip12-mac.jpg)

# 29. E06D1740FDBE
答案：`E06D17382420`

<br>

> 30. [单选题] 阿力士的iphone 12 pro以什么屏幕密码保护? (1分)
> A. 6位阿拉伯数字密码
> B. 4位阿拉伯数字密码
> C. 图形密码
> D. 以上皆非

Supposedly the file at `Apple_A2341 MGLW3LL_A iPhone 12 Pro.zip/Backup Service/00008101-000254A10A21001E/Snapshot/Manifest.plist` should contain the key `WasPasscodeSet` and value `false` to indicate that screen password was not set. However, the exported file did not include such key value pair.

# 30. D
答案：`D`

<br>

> 31. [多选题] 阿力士iphone 12 pro内以下哪一张相片是实况相片(live Photos)? (2分)
> A. IMG_0011.HEIC
> B. IMG_0010.HEIC
> C. IMG_0012.HEIC
> D. IMG_0009.HEIC

Live photos are essentially a short video clip, with a still photo has the cover photo. At the `Media > Videos` page, the video names and thumbnail suggested which images were live photos. The metadata of the videos also supported that the videos belong to live photos.

![meiya-cup-2021-ip12-livephoto.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ip12-livephoto.jpg)

答案：`A,B,D`

<br>

> 32. [单选题] 以下哪一个是阿力士iphone 12 pro可能曾经连接的装置名称? (2分)
> A. Chris’s MacBook Pro
> B. Chirs’s iPhone
> C. Chirs’s Computer
> D. Chirs’s Linux

Searched for the keyword "chris" and the only result return was a contact named `Chris's MacBook Pro`.

![meiya-cup-2021-ip12-chris.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ip12-chris.jpg)

答案：`A`

<br>

> 33. [多选题] 接上题，记录连接时间是什么时候(UTC+8)? (2分)
> A. 2021年10月21日 00:58:01
> B. 2021年10月21日 08:58:01
> C. 2021年10月21日 00:58:29
> D. 2021年10月21日 08:58:29

From the previous contact screen of `Chris's MacBook Pro`, there was also a created timestamp at `2021-10-21 08:58:01 (UTC+8)`.

# 33. B,C
答案：`B`

<br>

> 34. [多选题] 阿力士iPhone XR中在软件WhatsApp中工地主管与阿力士的对话中曾提到：[佢叫我俾钱喎，BTC係唔係呢个啊？]。在进行电子数据取证分析后，以下哪一个是有可能关于此对话的正确描述？ (2分)
> A. 此对话被Kariser Lee删除
> B. 此对话的附件为一张图片文件
> C. 此对话被Alex Chan删除
> D. 此对话是引用Alex Chan回复

Switching to the image file `Alex iPhone XR.ufdr`. The `Messages > Chats > WhatsApp` page revealed the WhatsApp conversation in interest. The message has the deleted icon and an image thumbnail. Given that the message is still available on this mobile device, it is believed that the message was deleted by the manager, Kariser Lee, instead of the device owner, Alex Chan.

![meiya-cup-2021-ipxr-whatsapp.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ipxr-whatsapp.jpg)

答案：`A,B`

<br>

> 35. [填空题] 阿力士iPhone XR的WhatsApp对话中，阿力士曾要求工地主管支付多少个BTC? (请以阿拉伯数字回答) (1分)

The followed message from the previous question was requesting for 10 bitcoins.

答案：`10`

<br>

> 36. [多选题] 阿力士iPhone XR中 “IMG_0056.HEIC"的图像与"5005.JPG”(MD5: 96c48152249536d14eaa80086c92fcb9)看似为同一张相片，在电子数据取证分析下，以下哪样描述是正确? (2分)
> A. 储存在不同的.db里
> B. 有不同哈希值
> C. IMG_0056.HEIC为原图，5005.JPG(MD5: 96c48152249536d14eaa80086c92fcb9)为缩略图
> D. IMG_0056.HEIC曾被开启过，所以在IOS系统中创建了缩略图5005.JPG(MD5: 96c48152249536d14eaa80086c92fcb9)

The images were found at the `Media > Images` page, under the same parent directory path `Alex的iPhone/mobile/Media`. It was found that the two images have different MD5 hash values, file sizes, and pixel resolution. The image `5005.JPG` was stored under the directories `Thumbnails` and `IMG_0056.HEIC`, with a much smaller file size and lower resolution than the image `IMG_0056.HEIC`, suggesting the former to be the thumbnail of the latter.

![meiya-cup-2021-ipxr-image-1.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ipxr-image-1.jpg)

![meiya-cup-2021-ipxr-image-2.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ipxr-image-2.jpg)

答案：`B,C`

<br>

> 37. [多选题] 阿力士iPhone XR中相片檔IMG_0056.HEIC提供了什么电子数据取证的信息? (3分)
> A. 此相片是由隔空投送(Airdrop)得来
> B. 此相片由iPhone XR拍摄
> C. 此相片的拍摄时间为2021-10-21 17:45:48(UTC+8)
> D. 此相片的拍摄时间为2021-09-08 17:35:00(UTC+8)

The metadata of the image `IMG_0056.HEIC` revealed the camera model is `iPhone 12 Pro` and the capture time is `2021-09-28 17:35:00 (UTC+8)`. Given that the device is `iPhone XR` and the created time of the image on the device is later than the capture time, it is believed that the photo was obtained through AirDrop from another device, likely the `iPhone 12 Pro` used to capture the photo.

答案：`A,D`

<br>

> 38. [单选题] 阿力士iPhone XR中阿力士的电邮账户Alexc19851016@gmail.com的密码有可能是什么? (1分)
> A. Ac19851016
> B. Alex1985!
> C. Aa475869!
> D. 以上皆非

Searched for the keyword "alexc19851016" and found the password `Aa475869!` written within a notes.

![meiya-cup-2021-ipxr-pw.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ipxr-pw.jpg)

答案：`C`

<br>

> 39. [填空题] 阿力士iPhone XR曾经连接Wifi "Alex Home"的密码是什么? (请以英文全大写及阿拉伯数字回答) (1分)

Searched for the keyword "alex home" and the only result returned revealed the WiFi password `12345678`.

![meiya-cup-2021-ipxr-wifi.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ipxr-wifi.jpg)

答案：`12345678`

<br>

> 40. [单选题] 阿力士iPhone XR经iCloud备份的最后时间是什么?(UTC+8)? (1分)
> A. 2021-10-21 17:51:38 (UTC+8)
> B. 2021-10-21 18:02:13 (UTC+8)
> C. 2021-10-21 09:51:38 (UTC+8)
> D. 2021-10-21 10:02:13 (UTC+8)

The last cloud backup date was found under the `Device Info` part to be `2021-10-21 09:51:38 UTC`.

![meiya-cup-2021-ipxr-backup.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ipxr-backup.jpg)

答案：`A`

<br>

> 41. [填空题] 阿力士iPhone XR中的iBoot版本是iBoot-__________？ (请以阿拉伯数字回答，不用输入".") (1分)

Details of an iPhone can be found in the file at `Lockdown Service/PhoneInfo.xml`, which revealed the firmware version `iBoot-6723.120.36`.

![meiya-cup-2021-ipxr-iboot.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ipxr-iboot.jpg)

答案：`672312036`

<br>

> 42. [多选题] 阿力士iPhone XR中的WhatsApp群组『团购-新鲜猪肉牛肉-东涌群组-9/30』有以下哪一个成员? (2分)
> A. 85260617332@s.whatsapp.net
> B. 85260452579@s.whatsapp.net
> C. 85248791565@s.whatsapp.net
> D. 85264630956@s.whatsapp.net

The WhatsApp group conversion was found at the `Messages > Chats > WhatsApp` page, with the five participants listed.

![meiya-cup-2021-ipxr-group.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ipxr-group.jpg)

答案：`A,D`

<br>

> 43. [单选题] 阿力士的计算机显示曾于hongkongcard.com的论坛登记成为会员，以下哪个是他的帐户密码? (3分)
> A. Aa475869!
> B. Bb475869!
> C. Cd475869!
> D. 以上皆非

Searched for the keyword "hongkongcard", found the login name as `alexc19851016@gmail.com`, which was the same account used in a previous question, with the password found in the notes as `Aa475869!`.

![meiya-cup-2021-alex-hkcard.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-alex-hkcard.jpg)

答案：`A`

<br>

> 44. [单选题] 阿力士的计算机显示阿力士曾用什么方法进入受害者(主管)的计算机? (1分)
> A. 远程操控
> B. 特洛伊木马程序
> C. 勒索软件
> D. 恶意软件

From the previous questions, it is pretty obvious that TeamViewer was used to get access to the manager's computer. From the image file `Alex_Windows_Computer.E01`, the TeamViewer ID and timestamps of the outgoing connection at `Others > TeamViewer > Connect Other Machines Record` matched the previous findings from the manager's computer and router log.

![meiya-cup-2021-alex-teamviewer.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-alex-teamviewer.jpg)

答案：`A`

<br>

> 45. [单选题] 续上题，阿力士最后一次进入受害者(主管)计算机的时间是什么? (2分)
> A. 于2021年10月18日10时36分
> B. 于2021年10月18日18时36分
> C. 于2021年10月18日6时53分
> D. 于2021年10月18日18时42分

From the records, the last entry has the timestamp `2021-10-18 10:42:29 UTC`.

答案：`D`

<br>

> 46. [填空题] 阿力士的计算机显示他曾经使用FTP程序，FTP的主机IP地址是什麼? (请以亚拉伯数字作答，省去"."符号) (2分)

The `Download Tools Analysis > FileZilla > Client > Quick Connect Record` page revealed the host IP `218.255.242.114`.

![meiya-cup-2021-alex-ftp.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-alex-ftp.jpg)

答案：`218255242114`

<br>

> 47. [填空题] 阿力士的计算机显示于2021年9月至2021年11月期间，计算机曾被登入过多少次? (请以阿拉伯数字回答) (1分)

The `System Artifacts > System Info > User Info` page revealed the user `Alex` has a login time of 30.

![meiya-cup-2021-alex-login.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-alex-login.jpg)

答案：`30`

<br>

> 48. [填空题] 阿力士计算机所安装的Microsoft Office 2007 是以下哪一个版本? (请以亚拉伯数字作答，省去"."符号) (2分)

The `System Artifacts > Installed Software > Other Software` page revealed the version of `Microsoft Office Professional Plus 2007` as `12.0.4518.1014`.

![meiya-cup-2021-alex-office.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-alex-office.jpg)

答案：`12045181014`

<br>

> 49. [填空题] 以下是阿力士计算机中的Basic data partition (EFI 3)的Volume ID? (请以英文全大写及阿拉伯数字回答) (2分)

The basic data partition is just the primary drive using GPT, which is the C drive in this case.

# 49. 94C44CA5C44C8B84
答案：`94C44CA5C44C8B84`

<br>

> 50. [填空题] 阿力士计算机的Window product ID是什么? (请以英文全大写及阿拉伯数字回答，不用输入"-") (1分)

The `System Artifacts > System Info > System Info` page revealed the Windows product ID `00331-10000-00001-AA411`.

![meiya-cup-2021-alex-windows.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-alex-windows.jpg)

答案：`003311000000001AA411`

<br>

> 51. [单选题] 阿力士计算机曾经下载一张猴子的图片，以下哪一项描述正确? (1分)
> A. 该图片是由"https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSgn6ABvcqTfFPjcIbjc9hdx1H4PtQsAuVyTQ&usqp=CAU"下载的
> B. 该图片经过加密
> C. 该图片于2021-09-30下载
> D. 该图片是由GIF档转换成PNG檔

The downloaded image was found at `C:\Users\Alex\Downloads\images(1).png`, with the created time `2021-09-29 08:52:57 UTC`. The associated `Zone.Identifier` file revealed the download website.

![meiya-cup-2021-alex-monkey.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-alex-monkey.jpg)

答案：`A`

<br>

> 52. [填空题] 阿力士计算机所安装的Microsoft Office 2007的密钥是甚么? (请以英文全大写及阿拉伯数字回答，不用输入"-") (1分)

When looking for the image from the previous question, it was found that the `Microsoft Office Pro Plus 2007` is under `C:\Users\Alex\Desktop`, which contained the file `License Key.txt` that revealed the key `V77WQ-RPVP6-7MTPG-WH3G9-D44MJ`.

![meiya-cup-2021-alex-license.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-alex-license.jpg)

答案：`V77WQRPVP67MTPGWH3G9D44MJ`

<br>

> 53. [单选题] 阿力士FTP服务器用户使用命令行安装了甚么程序? (1分)
> A. Docker
> B. Chrome
> C. FileZilla
> D. TeamViewer

Switching to the image file `FTP.E01`. The parsed information at `User Artifacts > Built-in Apps(Linux) > Bash History` revealed the command line histories. It was found that `docker` was installed with `apt install`.

![meiya-cup-2021-ftp-install.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ftp-install.jpg)

答案：`A`

<br>

> 54. [多选题] 以下哪些档案于阿力士FTP服务器曾重复出现? (3分)
> A. Material1
> B. Material2
> C. Material3
> D. Staff1
> E. Staff2
> F. Staff3

Given that `Material3.xlsx` was mentioned in a previous question, the Excel documents were the first location to be investigate. The parsed information at `File Analysis > File Category > Document > Excel Table` revealed the Excel documents in the FTP server. It was found that those with the name starting with `Staff` have duplicates.

![meiya-cup-2021-ftp-excel.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ftp-excel.jpg)

答案：`D,E,F`

<br>

> 55. [填空题] 在阿力士FTP服务器中，文件夹___________曾被用户变更了访问权限 (请以英文全大写及阿拉伯数字回答) (2分)

The command line history analysed earlier also revealed that the directory `Dangerous_Project` had permissions modified.

![meiya-cup-2021-ftp-bash.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ftp-bash.jpg)

答案：`Dangerous_Project`

<br>

> 56. [填空题] 在阿力士FTP服务器建设后，有______个额外用户被加入 (请以阿拉伯数字回答) (2分)

Also from the command line history, the user `wai` was added to the FTP server.

答案：`1`

<br>

> 57. [单选题] 根据阿力士FTP服务器设定显示，此服务器是以_____方式连接网络，且是一个_______网络状态 (1分)
> A. 无线，公开
> B. 无线，私人
> C. 有线，公开
> D. 有线，私人

The parsed information at `System Artifacts > NetWork Config Info > Static NetWork Config Info` revealed the network connection of the FTP server (IP `218.255.242.114` found previously) is a wired connection and the IPs were within the public range.

![meiya-cup-2021-ftp-netconn.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ftp-netconn.jpg)

答案：`C`

<br>

> 58. [填空题] 阿力士FTP服务器设定最多使用者数目是_____ (请以阿拉伯数字回答) (2分)

The command line history revealed the FTP service to be `pure-ftpd`. The configuration file is located at `/etc/pure-ftpd/pure-ftpd.conf` but it was not found.

The file name `pure-ftpd` was used as a filter at the `Uncategorized` file list and the configuration file was found at `\var\lib\docker\overlay2\9052aa3377b45f65ab7c3eca6ef00c18a43e702d00136d3ae5772efc0e8a0b24\diff\etc\pure-ftpd\pure-ftpd.conf`. The maximum number of users was found to be `50`.

![meiya-cup-2021-ftp-conf.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ftp-conf.jpg)

# 58. 5
答案：`50`

<br>

> 59. [填空题] 阿力士FTP服务器使用Docker安装了一个FTP程序为___________。 (例如 space docker /1.1，请输入 spacedocker/1.1，不要输入空格) (2分)

The command line history also revealed the `docker` command to install `stilliard/pure-ftpd`.

![meiya-cup-2021-ftp-ftpd.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ftp-ftpd.jpg)

答案：`stilliard/pure-ftpd`

<br>

> 60. [多选题] 阿力士FTP服务器曾使用过甚么版本的Linux内核? (2分)
> A. linux-headers-5.11.0-16
> B. linux-headers-5.11.0-17
> C. linux-headers-5.11.0-36
> D. Linux-headers-5.11.0-37
> E. linux-headers-5.11.0-40

Linux headers are usually located under the path `/usr/src`. Navigating to the directory revealed two versions of Linux headers.

![meiya-cup-2021-ftp-linux.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ftp-linux.jpg)


答案：`A,D`

<br>

> 61. [多选题] 阿力士FTP服务器的磁盘分区，有以下哪一种文件系统? (2分)
> A. FAT16
> B. FAT32
> C. ExFAT
> D. HFS+
> E. Ext4

Clicking at the top level of the partition revealed the partition type, with partition 2 as `FAT32` and partition 3 as `EXT4`.

![meiya-cup-2021-ftp-type-1.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ftp-type-1.jpg)

![meiya-cup-2021-ftp-type-2.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ftp-type-2.jpg)

答案：`B,E`

<br>

> 62. [填空题] 阿力士FTP服务器用户输入了指令_____________去检查现存的Docker容器 (例如netstat lntp，请输入netstatlntp，不要输入空格) (3分)

The command line history revealed the command used to be `docker container ps -a`.

![meiya-cup-2021-ftp-docker.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-ftp-docker.jpg)

答案：`dockercontainerps-a`

<br>
