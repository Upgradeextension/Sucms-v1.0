Title:
Stored XSS vulnerability in Sucms v1.0 web application

Download link: https://down.chinaz.com/api/index/download?id=37818&type=code.

Overview:
Sucms v1.0 web application contains a stored XSS vulnerability in the admin_ads.php?action=add page. An attacker can inject malicious XSS payloads that can be stored on the server and later executed in the context of an unsuspecting victim's browser.

Impact:
An attacker can exploit this vulnerability to steal sensitive user information, such as session cookies, login credentials, or personal data. The attacker can also use the vulnerability to perform other malicious actions, such as redirecting users to phishing pages or delivering malware payloads.

Solution:
The vulnerability can be temporarily mitigated by adding input validation and output encoding to filter out malicious XSS payloads. However, a permanent fix would require a code update to address the underlying vulnerability in the application.

Affected versions:
Sucms v1.0 web application is affected by this vulnerability.

In /upload/admin/admin_ads.php, no regular expression filtering is applied to the $intro parameter, while adname, adenname parameters are filtered. An attacker can exploit this vulnerability by adding malicious XSS payloads to the intro parameter in the request, resulting in successful XSS injection.
<img width="837" alt="image" src="https://github.com/Upgradeextension/Sucms-v1.0/assets/124221747/c9ef0681-240d-4db1-8d36-26352dc2c853">
<img width="1026" alt="image" src="https://github.com/Upgradeextension/Sucms-v1.0/assets/124221747/8b8b6735-aff6-4fd1-8384-810e49d8b3b7">
```
POST /admin/admin_ads.php?action=editsave&id=1&page=1 HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:70.0) Gecko/20100101 Firefox/70.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Content-Length: 42
Origin: http://127.0.0.1
Connection: close
Referer: http://127.0.0.1/admin/admin_ads.php?action=edit&page=1&id=1
Cookie: PHPSESSID=8k8r2hfra80o3opt0beua9mga5; zh_choose=n; _currentWebUrl_=%2Findex.php%2Findex-category-id-81.html; _currentAdminUrl_=%2Findex.php%2Fadmin-sys-managers.html; user=21232f297a57a5a743894a0e4a801fc3; DedeUserID=1; DedeUserID__ckMd5=2bc70c6d99eeb958; DedeLoginTime=1625041565; DedeLoginTime__ckMd5=7cac447604e50983; YUNYECMSADM_admusername=admin2; YUNYECMSADM_admuserid=4; YUNYECMSADM_admroleid=1; YUNYECMSADM_admloginrnd=gikoruvX045%23_%7B%60%3D.%3B%3A%7C; YUNYECMSADM_admlogintruetime=1625102419; YUNYECMSADM_admlogintime=1625102589; YUNYECMSADM_admloginlicense=yunyecmslicense; YUNYECMSADM_loginyunyecmsckpass=3ab05cc7fa6027423125becc4f1a9f54; YUNYECMSADM_loginyunyecmsfilernd=bdfhijnqstuxzCENOQRSTVXZ017
Upgrade-Insecure-Requests: 1

adname=1&adenname=1&intro=123123&adsbody=1
![image](https://github.com/Upgradeextension/Sucms-v1.0/assets/124221747/71481b60-0f67-4784-b107-94f8f0b6550f)

```
