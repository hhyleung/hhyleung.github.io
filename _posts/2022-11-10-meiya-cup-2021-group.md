---
title: "美亞杯 2021 - 團體賽"
excerpt: "Writeup for the Meiya Cup 2021 - Group round"
last_modified_at: 2022-11-10
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
几天后，“大路建设”旗下有一家名为“元材原料”的材料供应子公司，该公司发现几名员工的个人财务资料在网上遭公开发布。为了员工安全，主管决定报警求助。经警方调查发现黑客入侵的手法与“大路建设”的案件十分相似，因此引起调查人员怀疑两起案件有所关联。经调查后，警方拘捕了“常威”和“特普”两名本地男子，怀疑他们与本案有关。警方在搜查他们的住宅及公司后，扣押了数台数码设备，请分析以下电子数据并重建电子数据痕迹，以确认“常威”和“特普”在本案中是否有违法犯罪，并还原事件经过。

<br>

## 检材
### 与“大路建设”相关的资料
1.  工地职员A的办公室计算机的电子数据：image\\StaffA\_computer\\StaffA\_Computer.E01
2.  工地职员B的办公室计算机的电子数据：image\\StaffB\_computer\\StaffB\_Computer.E01

<br>

### 与“元材原料”相关的资料
1.  网页服务器的电子数据：image\\Yuen\_Choi\_Webserver\\Yuen\_Choi\_Webserver.E01

<br>

### 与“常威”相关的资料
1.  常威的背景资料：调查报告\\常威\\常威的背景资料.pdf
2.  常威的调查报告：调查报告\\常威\\常威调查报告.pdf
3.  常威手机的电子数据：image\\Wai\\Wai phone\\Wai Phone\\Wai Phone.ufdr
4.  常威USB设备的电子数据：image\\Wai\\Wai USB\\Wai USB.E01
5.  常威Windows计算机的电子数据：image\\Wai\\Wai\_Windows\_Computer\\Wai\_\_Windows\_Computer.E01
6.  常威矿机的电子数据：image\\Wai\\HIVE OS\\HIVE OS.E01
7.  常威无人机的电子数据：image\\Wai\\Wai Drone\\Drone_DJI - Spark\\Wai Drone.ufdr
8.  常威无人机内存储卡的电子数据：image\\Wai\\Wai DJI Drone SD Card\\DJI Drone SD Card.E01
9.  常威MAC计算机的电子数据：image\\Wai\\Wai\_MacBook\\Wai\_Macbook.aff4
10. 常威LINUX计算机的电子数据：image\\Wai\\Wai\_Linux\\Wai\_Linux1\\Wai_Linux1.E01

<br>

### 与“特普”相关的资料
1.  特普的背景资料：调查报告\\特普\\特普的背景资料.pdf
2.  特普的调查报告：调查报告\\特普\\特普调查报告.pdf
3.  特普手机的电子数据：image\\DaK Pou\\Dak Pou phone\\LG GSM_H961N V10\\Dak Pou Phone.ufdr
4.  特普Windows计算机的电子数据：image\\DaK Pou\\Dak Pou Windows\\VTM-computer.e01
5.  特普Windows计算机存储器提取的镜像文件：image\\DaK Pou\\Dak Pou Windows_memdump\\Vtm-computer-memdump.mem

<br>

## 题目
### 工地职员A的办公室计算机的电子数据
> 1) [填空题] 工地职员A计算机的修复密钥标识符是什么? (请以大写英文及阿拉伯数字输入答案，不要输入“-”) (1分)

Drive E is the BitLocker encrypted partition, bringing up the `BitLocker Decryption` prompt and selecting the `Recovery Key` option reveals the key identifier `230C1BB3-106A-4E4E-BF5D-3D10961585D4`.

![meiya-cup-2021-staffa-bitlocker-1.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-staffa-bitlocker-1.jpg)

答案：`230C1BB3106A4E4EBF5D3D10961585D4`

<br>

> 2) [填空题] 工地职员A计算机的修复密钥解除锁定是什么? (请以数字输入答案，不要输入“-”) (1分)

Searched for the keyword `230C1BB3` and revealed the recovery key file at `\var\lib\docker\overlay2\575db3795cb5fff7cadb347f10cfcaad5fd5fe3e5b3e31418ffdd415cf754e53\diff\home\Dangerous_Project\3\BitLocker 修復金鑰 230C1BB3-106A-4E4E-BF5D-3D10961585D4.TXT` within the `FTP.E01` image file, with the recovery key is found to be `483714-461582-060962-373351-019646-502348-309628-684431`.

![meiya-cup-2021-staffa-bitlocker-2.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-staffa-bitlocker-2.jpg)

答案：`483714461582060962373351019646502348309628684431`

<br>

> 3) [单选题] 工地职员A的计算机被什么程式加密? (1分)
> A. Ransomware
> B. BitLocker
> C. AxCrypt
> D. PGP
> E. FileVault 2

From the previous questions, it is proved that the partition was indeed encrypted by BitLocker. The recovery key found was provided at `BitLocker Decryption` and successfully decrypted the partition.

答案：`B`

<br>

> 4) [单选题] 工地职员A的孩子有可能正准备就读什么学校? (2分)
> A. 小学
> B. 中学
> C. 幼儿园
> D. 大学

The parsed information at `Web History > Google Chrome > IDS_BROWSER_SEARCH` revealed search histories regarding kindergarten applications.

![meiya-cup-2021-staffa-kindergarten.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-staffa-kindergarten.jpg)

答案：`C`

<br>

> 5) [多选题] 工地职员A并没有打开过哪一个档案? (2分)
> A. Staff3.xlsx
> B. Staff4.xlsx
> C. Staff1.xlsx
> D. Staff2.xlsx
> E. BTC address.bmp

The parsed information at `User Artifacts > Last Accessed History > IDS_USERTRACE_RECENTVISIT_DOC` revealed that staff A has once viewed the documents `BTC address.bmp` and `Staff1.xlsx`.

![meiya-cup-2021-staffa-recents.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-staffa-recents.jpg)

答案：`A,B,D`

<br>

> 6) [填空题] 工地职员A的计算机被远程控制了多少分钟? (请以阿拉伯数字回答) (2分)

The parsed information at `Others > TeamViewer > Connected By Other Machines Record` revealed that the device was connected by the remote TeamViewer user `alex` for a session of around 11 minutes.

![meiya-cup-2021-staffa-teamviewer.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-staffa-teamviewer.jpg)

答案：`11`

<br>

> 7) [单选题] 工地职员A的计算机被加密后，被要求存入的虚疑货币是什么? (1分)
> A. 比特币现金
> B. 比特币
> C. 以太币
> D. 泰达币

Given that staff A has visited `BTC address.bmp` and referring back to the WhatsApp conversation between the manager and Alex Chan, it is believe that `BTC` was the cryptocurrency requested to use.

答案：`B`

<br>

> 8) [填空题] 在工地职员A的计算机曾经打开过的Excel档案中，有多少人有可能在法律部门工作? (请以阿拉伯数字回答) (1分)

The file in interest is at `E:\Staff Data\Staff1.xlsx`. By filtering the `post` column to `Legal`, it was found that there were `22` staffs within the legal department.

![meiya-cup-2021-staffa-legal.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-staffa-legal.jpg)

答案：`22`

<br>

### 工地职员B的办公室计算机的电子数据
> 9) [多选题] 工地职员B的计算机在什么日期和时间被黑客控制? (2分)
> A. 2021-10-19
> B. 2021-09-16
> C. 11:16:41 (UTC +8:00)
> D. 05:55:50 (UTC +8:00)
> E. 18:40:06 (UTC +8:00)

The parsed information at `Others > TeamViewer > Connected By Other Machines Record` revealed that the device was connected by the remote TeamViewer user `alex` on `2021-10-18` between `10:29:27 UTC` to `10:42:02 UTC`.

![meiya-cup-2021-staffb-teamviewer.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-staffb-teamviewer.jpg)

答案：`E`

<br>

> 10) [填空题] 工地职员B的计算机的MAC Address是什么? (请以大写英文及数字输入答案) (1分)

The parsed information at `System Artifacts > System Info > Network Config > Network Adapter` revealed the address of the network card, aka the MAC address of the device, to be `00-0C-29-E2-53-2D`.

![meiya-cup-2021-staffb-mac.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-staffb-mac.jpg)

答案：`000C29E2532D`

<br>

> 11) [填空题] 工地职员B的计算机用户FaFa的Profile ID是什么? (请以大写英文及数字输入答案，不要输入“-”) (1分)

The parsed information at `System Artifacts > System Info > User Info` revealed the SID of user `FaFa` to be `S-1-5-21-1634007002-1203460028-4027450868-1001`.

![meiya-cup-2021-staffb-fafa.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-staffb-fafa.jpg)

答案：`S15211634007002120346002840274508681001`

<br>

> 12) [填空题] 工地职员B的办公室计算机的Windows CD Key是什么? (请以大写英文及数字输入答案，不要输入“-”) (1分)

The Windows CD key is stored within the registry key at `HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SoftwareProtectionPlatform\BackupProductKeyDefault`. The registry hive at `C:\Windows\System32\config\SOFTWARE` was processed by the `Registry Parser`. The key was found to be `VK7JG-NPHTM-C97JM-9MPGT-3V66T`.

![meiya-cup-2021-staffb-cdkey1.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-staffb-cdkey1.jpg)

The key is also stored within the registry key at `HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\DigitalProductId`. However, the key is encoded here and required to be decoded by [`WinProdKeyFinder`](https://github.com/mrpeardotnet/WinProdKeyFinder/releases) in the following format (when exported directly from the registry editor).

```text
"DigitalProductId"=hex:A4,00,00,00,03,00,00,00,30,30,33,33,30,2D,38,30,30,30,30,2D,30,30,30,30,30,2D,41,41,32,38,31,00,EC,0C,00,00,5B,54,48,5D,58,31,39,2D,39,38,38,34,31,00,00,00,EC,0C,00,00,00,00,A8,D2,7B,6E,89,81,4F,6D,09,00,00,00,00,00,C5,6E,5C,61,B9,57,CE,71,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,69,4A,1B,59
```

![meiya-cup-2021-staffb-cdkey2.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-staffb-cdkey2.jpg)

答案：`VK7JGNPHTMC97JM9MPGT3V66T`

<br>

> 13) [单选题] 检查过工地职员B的计算机登录档后(Window Registry)，计算机感染了什么恶意软件? (2分)
> A. Adware
> B. Worms
> C. Rootkits
> D. 没有感染任何恶意软件

Unsure where exactly to look for this, checked the registry key `HKLM\SYSTEM\ControlSet1\Services\WinDefend\Start` that the value `2` indicates Windows Defender will start automatically and unlikely that it was disabled.

![meiya-cup-2021-staffb-defender.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-staffb-defender.jpg)

答案：`D`

<br>

> 14) [单选题] 工地职员B的计算机中被加密硬盘内的图片“\_120778782\_58759559.jpg”，有可能是从下列哪个的途径载入计算机? (1分)
> A. 电邮下载附件
> B. USB盘
> C. 网上下载
> D. 蓝芽传入
> E. Direct-link

Same as the computer of staff A, the BitLocker recovery key identifier was revealed to be `49737A2E-6E82-4EAF-94B5-E1DB4F7CA642` by the `BitLocker Decryption` and the key was found within the `FTP.E01` at `\var\lib\docker\overlay2\575db3795cb5fff7cadb347f10cfcaad5fd5fe3e5b3e31418ffdd415cf754e53\diff\home\Dangerous_Project\2\BitLocker 修復金鑰 49737A2E-6E82-4EAF-94B5-E1DB4F7CA642.TXT` to be `575025-204820-336325-067067-589996-389829-603361-712272`.

The key was used to decrypt the partition E and found the image in interest. The associate zone identifier file revealed that the image was downloaded from `https://ichef.bbci.co.uk/news/640/cpsprodpb/7073/production/_120778782_58759559.jpg`.

![meiya-cup-2021-staffb-image2.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-staffb-image2.jpg)

答案：`C`

<br>

> 15) [多选题] 工地职员B的计算机中被加密硬盘内的图片中，人物中衣着有什么颜色? (2分)
> A. 黄色
> B. 红色
> C. 紫色
> D. 蓝色
> E. 绿色

Two images, `30-08624-001.jpg` and `_120778782_58759559.jpg`, were found in the BitLocker partition. Both images were screenshots from the TV series Squid Game, with the characters wearing clothes in pink and green.

![meiya-cup-2021-staffb-colour.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-staffb-colour.jpg)

答案：`A,D`

<br>

> 16) [填空题] 工地职员B的计算机有多少个磁盘分区? (请以阿拉伯数字输入答案) (1分)

There are a total of 5 partitions on the device.

![meiya-cup-2021-staffb-partition.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-staffb-partition.jpg)

答案：`5`

<br>

> 17) [填空题] 工地职员B的计算机硬盘分割表是什么? (答案请以首字母大写作答) (2分)

When checking from the top at the `Hex` view of the image file, the signature of GUID Partition Table (GPT), `0x4546492050415254` or `EFI PART`, was found. If it was using Master Boot Record (MBR) instead, the signature would have been `0x55AA`.

![meiya-cup-2021-staffb-gpt.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-staffb-gpt.jpg)

答案：`GPT`

<br>

> 18) [填空题] 在工地职员B的计算机Event Log中最后登入时services.exe的Process ID是什么? (请以阿拉伯数字输入) (3分)

The Windows Security Event ID `4688` records new processes that were created. The parsed information at `Log Parser > Windows Logs > Security > Detailed Tracking` revealed the latest `services.exe` process at `2021-10-19 10:39:55 UTC`. The process ID was found to be `0x027c`, the value right before the process name `C:\Windows\System32\services.exe`. Converting the value from hex to decimal gives the process ID `636`.

![meiya-cup-2021-staffb-event.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-staffb-event.jpg)

答案：`636`

<br>

### 网页服务器的电子数据
> 19) [填空题] 甚么IP曾经上传档案到网页服务器? (请以阿拉伯数字回答，不用输入“.”) (2分)

The parsed information at `Log Parser > Apache Logs (Windows) > Log Details` revealed the web server access history. By filtering the `Request` column with the keyword `upload`, the only IP `203.145.94.120` was identified to have `POST` requests to the `www.yuenchoi.ceom.hk/uploader.php` page.

![meiya-cup-2021-web-upload.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-web-upload.jpg)

答案：`20314594120`

<br>

> 20) [多选题] 承上题，以下哪试档案曾被上传到网页服务器? (3分)
> A. kjk2.jpg
> B. kjk2.php
> C. b6778k-9.0.php
> D. b374k-2.5.php
> E. d374k-2.5.php

Searched with the file names and the files `kjk2.jpg`, `kjk2.php`, and `b374k-2.5.php` were found within the Apache log.

![meiya-cup-2021-web-file1.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-web-file1.jpg)

![meiya-cup-2021-web-file2.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-web-file2.jpg)

![meiya-cup-2021-web-file3.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-web-file3.jpg)

答案：`A,B,D`

<br>

> 21) [单选题] 入侵者可能使用甚么漏洞进行入侵网页服务器? (1分)
> A. 文件上传漏洞
> B. SQL注入
> C. 跨站脚本攻击
> D. 格式化字符串弱点

Given the context of the previous questions, it is believed that the vulnerability that was exploited was through file upload.

答案：`A`

<br>

> 22) [多选题] 在网页服务器找到的所有文件档(doc 及 docx)中，有以下哪些文件制作人(Author)? (2分)
> A. Kevin L. Brown
> B. Peter R. Lee
> C. Mary
> D. May
> E. Colin

The parsed information at `File Analysis > File Category > Document > Word Documents` revealed all documents within the image file. By filtering the `Name` column with the keyword `.doc`, only 7 documents remain. Manually checked all of the documents for the author name and only `Kevin L. Brown` and `Mary` were found.

![meiya-cup-2021-web-author1.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-web-author1.jpg)

![meiya-cup-2021-web-author2.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-web-author2.jpg)

答案：`A,C`

<br>

> 23) [多选题] 在网页服务器中，哪个是可疑档案?它如何取得计算机控制权? (3分)
> A. 可疑档案: b6778k-9.0.php
> B. 可疑档案: b374k-2.5.php
> C. 可疑档案: upload.php
> D. 透过浏览器远程管理取得计算机控制权
> E. 透过 PuTTY(远程登录工具) 取得计算机控制权

Located the files in interest by searching the file names. `upload.php` was not found and `b677bk-9.0.php` was found to be a webpage source file in HTML.

![meiya-cup-2021-web-php1.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-web-php1.jpg)

For `b374k-2.5.php`, it was found to be an PHP webshell. Hence, it is believed that this webshell was uploaded to the web server and used as a backdoor to gain control.

![meiya-cup-2021-web-php2.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-web-php2.jpg)

![meiya-cup-2021-web-php3.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-web-php3.jpg)

答案：`B,D`

<br>

> 24) [填空题] 在网页服务器中，运行可疑档案需要密码，其密码的哈希值(Hash Value)是甚么? (请以英文全大写及阿拉伯数字回答) (3分)

The webshell source code revealed the shell password to be `b374k`, wi the MD5 value as `0de664ecd2be02cdd54234a0d1229b43`.

答案：`0DE664ECD2BE02CDD54234A0D1229B43`

<br>

> 25) [单选题] 在网页服务器中，可疑档案的译码函数是甚么? (2分)
> A. unzip_file('$x,$y')
> B. gzdecode(base64_decode($x))
> C. gzinflate(base64_decode($x))
> D. 以上皆否

The webshell source code revealed the function `gz.inflate(base64_decode($x))` was used.

答案：`C`

<br>

> 26) [填空题] 解压后的脚本档的档案大小是多少? (请以字节及阿拉伯数字回答) (3分)

The code was decoded at [https://www.mobilefish.com/services/eval_gzinflate_base64/eval_gzinflate_base64.php](https://www.mobilefish.com/services/eval_gzinflate_base64/eval_gzinflate_base64.php). The decoded code was downloaded as a file and the size was found to be 109,041 bytes.

![meiya-cup-2021-web-decode.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-web-decode.jpg)

答案：`109041`

<br>

> 27) [多选题] 解压后的脚本文件内有甚么功能? (3分)
> A. 编辑文件
> B. 删除文件
> C. 更改用户密码
> D. 加密文件
> E. 重新命名文件

Referring back to the webshell project webpage, it was mentioned that the shell supports file `view, edit, rename, delete, upload, and download as archive`.

答案：`A,B,E`

<br>

> 28) [单选题] 解压后的脚本含有压缩功能，当中使用的解压方法是甚么? (2分)
> A. PclZip.php
> B. Unzip_gz()
> C. ZipArchive()
> D. 以上皆否

Searched for the above keywords and only `ZipArchive()` returned hits.

![meiya-cup-2021-web-zip.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-web-zip.jpg)

答案：`C`

<br>

### 特普手机的电子数据
> 29) [多选题] 特普的电话中一张于2021年09月30日10:45:12拍摄的相片包含以下哪些字? (1分)
> A. 精忠
> B. 报国
> C. 忠诚
> D. 勇毅

At the `Media > Images` page, the filter of capture time `2021-09-30 10:30:00 to 2021-09-30 11:00:00` was applied and only one image was found, where the capture time matches the one in the question. Scanning the QR code gives the string `忠誠勇毅`.

![meiya-cup-2021-dpphone-qrcode.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-dpphone-qrcode.jpg)

答案：`C,D`

<br>

> 30) [多选题] 特普的电话中的whatsapp账号85268421495@s.whatsapp.net中，有哪些其他人的WhatsApp用户数据记录? (2分)
> A. 85222117188@s.whatsapp.net
> B. 85289853825@s.whatsapp.net
> C. 85264795287@s.whatsapp.net
> D. 85231882226@s.whatsapp.net

The `Contacts > WhatsApp > 85268421495@s.whatsapp.net` page revealed three contacts. Only two contacts has a legitimate phone number, `CS Hotline: 31882226` and `MD-CC Hotline: 22117188`. Since the third contact `MD-Recharge: 193193` is not in the typical HK phone number format, it is believed that it would not fit in the WhatsApp user record.

![meiya-cup-2021-dpphone-contacts.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-dpphone-contacts.jpg)

答案：`A,D`

<br>

> 31) [单选题] 特普电话的热点分享密码是什么? (1分)
> A. 12345678
> B. 69447401bceb
> C. Jioijo4542554
> D. Dak Pou Home

The `Device Info` part revealed the hotspot tethering password to be `69447401bceb`.

![meiya-cup-2021-dpphone-hotspot.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-dpphone-hotspot.jpg)

答案：`B`

<br>

> 32) [多选题] 特普于经纬度22.278843, 114.165783，没有做什么? (2分)
> A. 拍影片
> B. 拍照
> C. 使用google map
> D. 在Whatsapp中分享实时位置

Searched for the keyword "22.278843" and only two results were returned, with the image `20210924_202939.jpg` taken at the location, and the location record associated to the image.

![meiya-cup-2021-dpphone-location.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-dpphone-location.jpg)

答案：`A,C,D`

<br>

> 33) [多选题] 特普于电话中安装了一个可疑软件(版本为2020033001)，跟据该可疑软件的安装档，下列哪项描述正确? (2分)
> A. 软件名称是安全防护
> B. 软件名称是安心回家
> C. 软件签名(Sign Algorithm)以SHA512 with RSA加密
> D. 封包名称(Package Name)是org.chromium.webapk.a5b80edf82b436506_v2

Searched for the keyword "2020033001" and revealed an installed application with the source file at `userdata (ExtX)/Root/app/www.icthna.net-1/base.apk/AndroidManifest.xml`. 

![meiya-cup-2021-dpphone-app1.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-dpphone-app1.jpg)

Since the `AndroidManifest.xml` is encoded with most of the information unreadable, `aapt` was used instead to view the application information from the exported `base.apk` file.

![meiya-cup-2021-dpphone-app2.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-dpphone-app2.jpg)

```bash
>aapt dump badging base.apk
package: name='www.icthna.net' versionCode='1' versionName='2020033001' platformBuildVersionName='6.0-2438415' compileSdkVersion='23' compileSdkVersionCodename='6.0-2438415'
sdkVersion:'19'
targetSdkVersion:'26'
...
application-label:'安全防护'
application-label-zh-CN:'安全防护'
```

The package name was found to be `www.icthna.net` and application name is `安全防护`. For SDK versions above 18, by default signing algorithm would be `SHA256 RSA`. To confirm, [`print-apk-signature`](https://github.com/warren-bank/print-apk-signature) was used and revealed the signing algorithm `RSA` with a key size of `2048 bits`, ie `SHA256 RSA` was used.

```bash
>print-apk-signature base.apk
Verifies
Verified using v1 scheme (JAR signing): true
Verified using v2 scheme (APK Signature Scheme v2): true
Verified using v3 scheme (APK Signature Scheme v3): true
Number of signers: 1
Signer #1 certificate DN: CN=dfrn, OU=dfrn, O=dfrn, L=CN, ST=HK, C=HK
Signer #1 certificate SHA-256 digest: f5e1c2d25bea2deabb47851df418bb5a45bbedb2e2ecb4a071239aa70bc974c6
Signer #1 certificate SHA-1 digest: e844ff317c55222780701017f747ab454bd642a5
Signer #1 certificate MD5 digest: 28f47ccef7d827892e432c81908ef558
Signer #1 key algorithm: RSA
Signer #1 key size (bits): 2048
Signer #1 public key SHA-256 digest: 1e5c1ae4fe6a2e3106a36f4cda2278b0e5b9579774bb679e43b616d61dedbd9e
Signer #1 public key SHA-1 digest: ae7d84c7ce7bbb9b52e1bc4605e05879ec6f8a7c
Signer #1 public key MD5 digest: 21b2cf592962b2e9b7b8bfbe8875d666
```

答案：`A`

<br>

> 34) [多选题] 特普于电话中安装了一个可疑软件(版本为2020033001)，跟据该可疑软件的安装档，可疑软件中涉及以下安全许可? (2分)
> A. android.permission.READ_SMS 读取短信内容
> B. android.permission.SEND_SMS 发送短信
> C. android.permission.READ_CONTACTS 读取联系人
> D. android.permission.BLUETOOTH 使用蓝牙
> E. android.permission.CLEAR\_APP\_CACHE 清除应用缓存

The output from `aapt` also revealed the permissions of the application.

```bash
>aapt dump badging base.apk
...
uses-permission: name='android.permission.RECEIVE_SMS'
uses-permission: name='android.permission.READ_SMS'
uses-permission: name='android.permission.WRITE_SMS'
uses-permission: name='android.permission.RECEIVE_MMS'
uses-permission: name='android.permission.INTERNET'
uses-permission: name='android.permission.READ_PHONE_STATE'
uses-permission: name='android.permission.WRITE_EXTERNAL_STORAGE'
uses-permission: name='android.permission.ACCESS_WIFI_STATE'
uses-permission: name='android.permission.ACCESS_NETWORK_STATE'
uses-permission: name='android.permission.READ_CONTACTS'
uses-permission: name='android.permission.WRITE_CONTACTS'
uses-permission: name='android.permission.READ_CALL_LOG'
uses-permission: name='android.permission.WRITE_CALL_LOG'
uses-permission: name='android.permission.CALL_PHONE'
uses-permission: name='android.permission.WAKE_LOCK'
uses-permission: name='android.permission.SEND_SMS'
uses-permission: name='android.permission.READ_EXTERNAL_STORAGE'
```

答案：`A,B,C`

<br>

> 35) [填空题] 特普可能在电话中被可疑软件窃取了的验证码是什么? (请以英文全大写及阿拉伯数字回答) (2分)

The `Messages > Chats > Native Messages` revealed the SMS messages received. Out of the 7 messages, a CITIC Bank verification code `113476`, two Telegram verification codes `74041` and `55558`, one WhatsApp registration code `389-349`, and a Google verification code `G-147321` were found. Given that the bank verification code should be the one that the adversary would be most interested, `113476` shall be the target for this question.

![meiya-cup-2021-dpphone-sms.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-dpphone-sms.jpg)

答案：`113476`

<br>

### 特普Windows计算机的电子数据
> 36) [填空题] 特普的计算机可能中了病毒，病毒的加壳(Packing)方法是甚么? (请以英文全大写作答) (2分)

Given that malware is often downloaded to a device, the malware was found at `D:\Users\user\Downloads\malware.exe`. Switching to the `Hex` view revealed the keywords `UPX0` and `UPX1`. To confirm the packer, [`PEiD`](https://www.aldeid.com/wiki/PEiD) was used and `UPX` was indeed the PE packer.

![meiya-cup-2021-dppc-packer.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-dppc-packer.jpg)

答案：`UPX`

<br>

> 37) [单选题] 特普的计算机可能中了病毒，病毒的编译工具是甚么? (2分)
> A. GCC
> B. Borland
> C. TCC
> D. Microsoft Visual C/C++

Unpacked the executable `malware.exe` with `upx`.

```bash
>upx.exe -d malware.exe
                       Ultimate Packer for eXecutables
                          Copyright (C) 1996 - 2022
UPX 4.0.0       Markus Oberhumer, Laszlo Molnar & John Reiser   Oct 28th 2022

        File size         Ratio      Format      Name
   --------------------   ------   -----------   -----------
     13312 <-      8704   65.38%    win32/pe     malware.exe
```

[`Exeinfo PE`](http://www.exeinfo.byethost18.com/) was then used on the unpacked executable and revealed `Microsoft Visual C++`.

![meiya-cup-2021-dppc-complier.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-dppc-complier.jpg)

答案：`D`

<br>

> 38) [填空题] 特普的计算机可能中了病毒，病毒的编译者使用可能使用的账户名称是甚么? (请以英文全大写作答) (3分)

The unpacked executable was loaded in `IDA`. The `Strings` view was brought up with the shortcut `Shift + F12`. The first string `C:\\Users\\gpgf\\Desktop\\malware\\Release\\malware.pdb` revealed the username `gpgf`.

![meiya-cup-2021-dppc-user.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-dppc-user.jpg)

答案：`GPGF`

<br>

> 39) [单选题] 特普的计算机可能中了病毒，病毒的自我复制位置是甚么? (2分)
> A. C:\Temp\temp.txt
> B. C:\Users\<profile>\Desktop\malware.exe
> C. C:\Users\public\malware.exe
> D. C:\a.txt

The `Strings` view also revealed the possible function name `CopyFileA`. Double clicking the string brings to the corresponding address. Continue the process until arriving at the actual function code, scrolling up revealed the file path variables. When decoded, the full path is `C:\Users\public\malware.exe`.

![meiya-cup-2021-dppc-copy1.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-dppc-copy1.jpg)

![meiya-cup-2021-dppc-copy2.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-dppc-copy2.jpg)

![meiya-cup-2021-dppc-copy3.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-dppc-copy3.jpg)

![meiya-cup-2021-dppc-copy4.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-dppc-copy4.jpg)

答案：`C`

<br>

> 40) [单选题] 特普的计算机可能中了病毒，病毒的修改登录文件位置是甚么? (3分)
> A. HKLM\Software\Microsoft\Windows\CurrentVersion\Run
> B. HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnce
> C. HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList
> D. HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Authentication\LogonUI\Background

The `Strings` view also revealed the possible function names starting with `Reg` that is likely regarding registry activities. Same as above, followed to the arrive at the function code and revealed the registry key `SOFTWARE\Microsoft\Windows\CurrentVersion\Authentication\LogonUI\Background` by hovering above the variable to display the full text.

![meiya-cup-2021-dppc-reg1.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-dppc-reg1.jpg)

![meiya-cup-2021-dppc-reg2.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-dppc-reg2.jpg)

![meiya-cup-2021-dppc-reg3.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-dppc-reg3.jpg)

答案：`D`

<br>

> 41) [多选题] 特普的计算机可能中了病毒，病毒留下了ASCII ART(ASCII艺术，文字图)，以下哪个不是病毒留下? (3分)
> A. HI
> B. HELLO
> C. HOW ARE YOU
> D. GOODBYE

Quickly scrolled through the entire code and only spotted the ASCII art for the word `HELLO`.

![meiya-cup-2021-dppc-ascii.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/meiya-cup-2021-dppc-ascii.jpg)

答案：`A,C,D`

<br>

> 42) [单选题] 特普的计算机可能中了病毒，病毒扰乱文件目标文件名是甚么? (2分)
> A. C:\Users\<profile>\Documents\target.txt
> B. C:\Users\<profile>\Desktop\target.txt
> C. C:\c.txt
> D. C:\temp.txt

答案：`B`

<br>

> 43) [单选题] 特普的计算机可能中了病毒，病毒扰乱文件方法是甚么? (3分)
> A. + 3
> B. XOR 5
> C. + 4
> D. – 4

答案：`A`

<br>

### 特普Windows计算机存储器提取的镜像文件
> 44) [填空题] 特普的计算机中，哪一个是FTK Imager.exe的程式编号(PID)? (请阿拉伯数字回答) (1分)

The `Volatility 3` plugin `windows.pslist` revealed the process `FTK Imager.exe` with the PID `6136`.

```bash
>python vol.py -f Vtm-computer-memdump.mem windows.pslist
Volatility 3 Framework 2.0.1
Progress:  100.00               PDB scanning finished
PID     PPID    ImageFileName   Offset(V)       Threads Handles SessionId       Wow64   CreateTime      ExitTime        File output
...
6136    4496    FTK Imager.exe  0xb563d900      21      -       2       False   2021-10-19 10:49:27.000000      N/A     Disabled
```

答案：`6136`

<br>

> 45) [多选题] 特普的计算机中，cmd.exe (PID:4496)它的执行日期及时间是? (1分)
> A. 2021-10-17
> B. 2021-10-18
> C. 2021-10-19
> D. 10:42:51
> E. 10:43:09
> F. 10:43:25

The above output also revealed the created time of the process `cmd.exe` with the PID `4496` as `2021-10-19 10:43:09`.

```bash
>python vol.py -f Vtm-computer-memdump.mem windows.pslist
Volatility 3 Framework 2.0.1
Progress:  100.00               PDB scanning finished
PID     PPID    ImageFileName   Offset(V)       Threads Handles SessionId       Wow64   CreateTime      ExitTime        File output
...
4496    3288    cmd.exe 0x9336c980      1       -       2       False   2021-10-19 10:43:09.000000      N/A     Disabled
```

答案：`C,E`

<br>

> 46) [填空题] 特普的计算机曾经以FTP 对外连接，连接的IP是? (请以阿拉伯数字回答，不用输入“.”) (2分)

The `Volatility 3` plugin `windows.netscan` revealed the network connections. However, none of the connections were using the FTP ports.

```bash
>python vol.py -f Vtm-computer-memdump.mem windows.netscan
Volatility 3 Framework 2.0.1
Progress:  100.00               PDB scanning finished
Offset  Proto   LocalAddr       LocalPort       ForeignAddr     ForeignPort     State   PID     Owner   Created

0x817b8de0      TCPv4   0.0.0.0 49410   0.0.0.0 0       LISTENING       1232    svchost.exe     2021-09-18 01:39:47.000000
0x81841c50      TCPv4   0.0.0.0 49409   0.0.0.0 0       LISTENING       1100    svchost.exe     2021-09-18 01:39:46.000000
0x81841c50      TCPv6   ::      49409   ::      0       LISTENING       1100    svchost.exe     2021-09-18 01:39:46.000000
0x81843e30      TCPv4   0.0.0.0 49409   0.0.0.0 0       LISTENING       1100    svchost.exe     2021-09-18 01:39:46.000000
0x819b6f40      TCPv4   0.0.0.0 49410   0.0.0.0 0       LISTENING       1232    svchost.exe     2021-09-18 01:39:47.000000
0x819b6f40      TCPv6   ::      49410   ::      0       LISTENING       1232    svchost.exe     2021-09-18 01:39:47.000000
0x819e0e20      TCPv4   0.0.0.0 49411   0.0.0.0 0       LISTENING       1800    spoolsv.exe     2021-09-18 01:39:47.000000
0x819e0e20      TCPv6   ::      49411   ::      0       LISTENING       1800    spoolsv.exe     2021-09-18 01:39:47.000000
0x8e4f6a68      TCPv4   192.168.1.64    62027   23.200.142.82   443     CLOSED  452     explorer.exe    2021-10-19 10:45:47.000000
0x8eebba00      UDPv4   127.0.0.1       512     *       0               3768    svchost.exe     2021-10-19 10:48:44.000000
0x8eeee4f8      TCPv4   192.168.1.64    61979   124.217.179.74  80      CLOSED  1232    svchost.exe     2021-10-02 07:27:56.000000
0x8f691bb8      TCPv4   0.0.0.0 7680    0.0.0.0 0       LISTENING       1232    svchost.exe     2021-09-18 01:51:41.000000
0x8f691bb8      TCPv6   ::      7680    ::      0       LISTENING       1232    svchost.exe     2021-09-18 01:51:41.000000
0x8f6c2300      TCPv4   192.168.1.64    61838   104.21.22.84    443     CLOSED  -       -       2021-10-02 07:25:02.000000
0x90226748      UDPv6   ::1     5888    *       0               3768    svchost.exe     2021-10-19 10:48:44.000000
0x90566190      TCPv4   192.168.1.64    62064   104.79.121.189  80      CLOSED  1232    svchost.exe     2021-10-19 10:46:28.000000
0x92f850f8      TCPv4   192.168.1.64    61828   13.225.93.22    443     CLOSED  -       -       2021-10-02 07:25:01.000000
0x93329e30      TCPv4   0.0.0.0 49409   0.0.0.0 0       LISTENING       1100    svchost.exe     2021-09-18 01:39:46.000000
0x9332bc50      TCPv4   0.0.0.0 49409   0.0.0.0 0       LISTENING       1100    svchost.exe     2021-09-18 01:39:46.000000
0x9332bc50      TCPv6   ::      49409   ::      0       LISTENING       1100    svchost.exe     2021-09-18 01:39:46.000000
0x933b4f40      TCPv4   0.0.0.0 49410   0.0.0.0 0       LISTENING       1232    svchost.exe     2021-09-18 01:39:47.000000
0x933b4f40      TCPv6   ::      49410   ::      0       LISTENING       1232    svchost.exe     2021-09-18 01:39:47.000000
0x933cdde0      TCPv4   0.0.0.0 49410   0.0.0.0 0       LISTENING       1232    svchost.exe     2021-09-18 01:39:47.000000
0x933e1e20      TCPv4   0.0.0.0 49411   0.0.0.0 0       LISTENING       1800    spoolsv.exe     2021-09-18 01:39:47.000000
0x933e1e20      TCPv6   ::      49411   ::      0       LISTENING       1800    spoolsv.exe     2021-09-18 01:39:47.000000
0x94818b80      TCPv4   192.168.1.64    61793   104.212.68.135  443     CLOSED  -       -       2021-10-02 07:24:09.000000
0x9492e648      TCPv4   0.0.0.0 135     0.0.0.0 0       LISTENING       716     svchost.exe     2021-09-18 01:39:41.000000
0x9492e648      TCPv6   ::      135     ::      0       LISTENING       716     svchost.exe     2021-09-18 01:39:41.000000
0x9495e170      TCPv4   0.0.0.0 49408   0.0.0.0 0       LISTENING       416     wininit.exe     2021-09-18 01:39:41.000000
0x94964f40      TCPv4   0.0.0.0 135     0.0.0.0 0       LISTENING       716     svchost.exe     2021-09-18 01:39:41.000000
0x9497df40      TCPv4   0.0.0.0 49408   0.0.0.0 0       LISTENING       416     wininit.exe     2021-09-18 01:39:41.000000
0x9497df40      TCPv6   ::      49408   ::      0       LISTENING       416     wininit.exe     2021-09-18 01:39:41.000000
0x9ea1e678      TCPv4   192.168.1.64    61787   104.18.7.51     443     CLOSED  -       -       2021-10-02 07:24:09.000000
0x9ea3d9b0      TCPv4   192.168.1.64    61958   40.126.35.128   443     CLOSED  1232    svchost.exe     2021-10-02 07:27:45.000000
0x9eaae318      TCPv4   192.168.1.64    62023   23.78.217.190   80      CLOSED  452     explorer.exe    2021-10-19 10:45:47.000000
0x9eb3a888      TCPv4   192.168.1.64    61894   117.18.237.29   80      CLOSED  -       -       2021-10-02 07:25:31.000000
0xa0e00b30      TCPv4   0.0.0.0 49411   0.0.0.0 0       LISTENING       1800    spoolsv.exe     2021-09-18 01:39:47.000000
0xa0eb6240      TCPv4   0.0.0.0 49412   0.0.0.0 0       LISTENING       488     services.exe    2021-09-18 01:39:48.000000
0xa0ed3628      UDPv4   127.0.0.1       512     *       0               -       -       2021-10-19 10:48:13.000000
0xa0f4e008      TCPv4   0.0.0.0 49412   0.0.0.0 0       LISTENING       488     services.exe    2021-09-18 01:39:48.000000
0xa0f4e008      TCPv6   ::      49412   ::      0       LISTENING       488     services.exe    2021-09-18 01:39:48.000000
0xa0fcc728      TCPv4   0.0.0.0 445     0.0.0.0 0       LISTENING       4       System  2021-09-18 01:39:48.000000
0xa0fcc728      TCPv6   ::      445     ::      0       LISTENING       4       System  2021-09-18 01:39:48.000000
0xa182bd58      UDPv4   192.168.1.64    512     *       0               3768    svchost.exe     2021-10-19 10:45:44.000000
0xa18631c0      TCPv4   0.0.0.0 49413   0.0.0.0 0       LISTENING       504     lsass.exe       2021-09-18 01:39:51.000000
0xa18a21c0      TCPv4   0.0.0.0 49413   0.0.0.0 0       LISTENING       504     lsass.exe       2021-09-18 01:39:51.000000
0xa18a21c0      TCPv6   ::      49413   ::      0       LISTENING       504     lsass.exe       2021-09-18 01:39:51.000000
0xa1921df0      TCPv4   192.168.1.64    62071   23.77.28.235    443     CLOSED  1232    svchost.exe     2021-10-19 10:46:41.000000
0xa19c9468      TCPv4   192.168.1.64    62029   23.200.142.82   443     CLOSED  452     explorer.exe    2021-10-19 10:45:47.000000
0xa3d47be0      TCPv4   192.168.1.64    62013   124.217.179.74  80      CLOSED  1232    svchost.exe     2021-10-19 10:45:45.000000
0xabd12488      TCPv4   192.168.1.64    61969   52.254.114.65   443     CLOSED  1232    svchost.exe     2021-10-02 07:27:53.000000
0xabda6bd8      TCPv4   192.168.1.64    61961   124.217.179.74  80      CLOSED  1232    svchost.exe     2021-10-02 07:27:46.000000
0xabdfb3f0      UDPv4   0.0.0.0 0       *       0               1256    svchost.exe     2021-10-19 10:47:07.000000
0xafa31680      UDPv4   0.0.0.0 0       *       0               1172    svchost.exe     2021-10-19 10:48:44.000000
0xafa31680      UDPv6   ::      0       *       0               1172    svchost.exe     2021-10-19 10:48:44.000000
0xafa3edf0      TCPv4   192.168.1.64    61788   54.230.85.10    443     CLOSED  -       -       2021-10-02 07:24:09.000000
0xafa51830      UDPv4   127.0.0.1       512     *       0               -       -       2021-10-19 10:47:21.000000
0xafb11988      TCPv4   192.168.1.64    62068   23.77.28.235    443     CLOSED  1232    svchost.exe     2021-10-19 10:46:31.000000
0xafb513e0      TCPv4   192.168.1.64    62069   20.190.163.19   443     CLOSED  1232    svchost.exe     2021-10-19 10:46:41.000000
0xafb51748      UDPv4   0.0.0.0 0       *       0               1232    svchost.exe     2021-09-20 03:08:38.000000
0xafba0288      UDPv6   ::1     5888    *       0               3768    svchost.exe     2021-10-19 10:48:44.000000
0xb569dad8      UDPv4   127.0.0.1       512     *       0               3768    svchost.exe     2021-10-19 10:48:44.000000
0xb57ad7d8      TCPv4   192.168.1.64    62079   157.55.109.226  80      CLOSED  1572    OneDrive.exe    2021-10-19 10:48:02.000000
0xb57fdbc8      TCPv4   192.168.1.64    61966   124.217.179.74  80      CLOSED  1232    svchost.exe     2021-10-02 07:27:50.000000
0xb62c3df0      TCPv4   192.168.1.64    62073   20.190.163.19   443     CLOSED  1232    svchost.exe     2021-10-19 10:46:50.000000
0xc0507b30      TCPv4   0.0.0.0 49411   0.0.0.0 0       LISTENING       1800    spoolsv.exe     2021-09-18 01:39:47.000000
0xd2487170      TCPv4   192.168.1.64    61925   54.192.19.207   80      CLOSED  4824    SearchUI.exe    2021-10-02 07:25:43.000000
0xd25043f0      TCPv4   192.168.1.64    61928   13.226.123.102  80      CLOSED  4824    SearchUI.exe    2021-10-02 07:25:44.000000
0xe77e2350      TCPv4   192.168.1.64    61944   124.217.179.74  443     CLOSED  1232    svchost.exe     2021-10-02 07:27:02.000000
0xef1161c0      TCPv4   192.168.1.64    61869   13.225.96.50    443     CLOSED  -       -       2021-10-02 07:25:30.000000
0xef119708      TCPv4   192.168.1.64    61899   104.16.14.243   443     CLOSED  -       -       2021-10-02 07:25:31.000000
0xef122b28      TCPv4   192.168.1.64    61862   104.18.6.51     443     CLOSED  -       -       2021-10-02 07:25:29.000000
0xef131ad0      TCPv4   192.168.1.64    61901   34.96.81.209    443     CLOSED  -       -       2021-10-02 07:25:31.000000
```

答案：`218255242114`

<br>

> 47) [多选题] 特普的计算机中，以下哪一个指令于上述连接中有使用过? (3分)
> A. get
> B. put
> C. delete
> D. bye
> E. quit

答案：`A,B,D`

<br>

> 48) [多选题] 在Linux的“Volatility”中，哪一个指令可以知道此程式支持哪一个Windows版本? (2分)
> A. vol.py --profile
> B. vol.py --systeminfo
> C. vol.py --info
> D. vol.py --verinfo

Google searched and found both options `--profile` and `--info` will list the Windows profiles.

答案：`A,C`

<br>
