# Web_Bug_Hunting

# XSS
跨站腳本攻擊是目前我尋找的網頁漏洞最多的之一，其中以反射型XSS為最大宗

心得與找security bug的方法:
1. 找到注入點:

反射型XSS常出現在`搜尋框`

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
