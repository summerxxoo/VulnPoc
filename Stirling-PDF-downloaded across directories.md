

The path verification defect causes files to be downloaded across directories



in the attack Endpoint 

/api/v1/database/download/{fileName}

in stirling.software.SPDF.controller.api.DatabaseController#downloadFile

# Code description

Gets the filename parameter entered by the user

![img](https://cdn.nlark.com/yuque/0/2024/png/2897054/1732534150857-58b16939-e0fe-41d3-99d5-902a0ffbe447.png)

then follow in the function getBackupFilePath

![img](https://cdn.nlark.com/yuque/0/2024/png/2897054/1732534314134-185b5a2e-f67a-410c-adfa-e9b840ac26a0.png)

but There is a flaw in this function Use newlines \n to bypass this

![img](https://cdn.nlark.com/yuque/0/2024/png/2897054/1732534241306-a6b07fe4-d928-4ee9-9e9f-dcec172141c0.png)

and then return the file

![img](https://cdn.nlark.com/yuque/0/2024/png/2897054/1732534397573-544bf473-51cf-413f-b951-c51d228b604a.png)

# 
