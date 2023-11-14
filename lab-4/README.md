# ЗИС ПР №4. WAF

Выполнил Сердюков Матвей, группа ББМО-01-23

## Запуск приложения

![](screenshots/start-docker.png)

![](screenshots/dvwa-welcome.png)

![](screenshots/init-app.png)

## Часть 1. Найденные уязвимости

### Command Injection

![](screenshots/os-inj-low.png)

![](screenshots/os-inj-medium.png)

![](screenshots/os-inj-high.png)

### File Inclusion

![](screenshots/file-inclusion-low.png)

![](screenshots/file-inclusion-medium.png)

![](screenshots/file-inclusion-high.png)

### SQL Injection

![](screenshots/sqli-low.png)

![](screenshots/sqli-medium.png)

![](screenshots/sqli-high-1.png)

![](screenshots/sqli-high-2.png)

### Cross-site Scripting

![](screenshots/xss-low.png)

![](screenshots/xss-medium.png)

![](screenshots/xss-high-1.png)

![](screenshots/xss-high-2.png)

## Часть 2. Защита приложения с помощью WAF `modsecurity`

### Разработанные правила

```
# modsecurity rules for DVWA #

# cmd injection

SecRule REQUEST_URI "@contains /vulnerabilities/exec/" "phase:2,log,deny,status:403,msg:'Possible command injection',id:170501,t:none,chain"
SecRule ARGS:ip "!@rx (?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)"

# LFI

SecRule REQUEST_URI "@contains /vulnerabilities/fi/" "phase:2,log,deny,status:403,msg:'Local File Inclusion',id:170502,t:none,chain"
SecRule ARGS_GET:page "!@rx (include\.php|file[1-3]\.php)"

# SQLi

SecRule REQUEST_URI "@contains /vulnerabilities/sqli/" "phase:2,log,deny,status:403,msg:'SQL Injection',id:170503,t:none,chain"
SecRule ARGS_GET:id "@detectSQLi"

# XSS

SecRule REQUEST_URI "@contains /vulnerabilities/xss_r/" "phase:2,log,deny,status:403,msg:'Cross-site Scripting',id:170504,t:none,chain"
SecRule ARGS_GET:name "@detectXSS"

```

### Запуск проверочного скрипта

![](screenshots/modsecurity-works.png)

### Отражённые атаки в логах приложения

![](screenshots/rule-os-inj.png)

![](screenshots/rule-file-inc.png)

![](screenshots/rule-sqli.png)

![](screenshots/rule-xss.png)