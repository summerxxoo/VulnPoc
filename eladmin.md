
#eladmin-File upload across directories

# introduce

Front end Entrance

![img](https://cdn.nlark.com/yuque/0/2024/png/2897054/1732537131666-c614f26c-84a6-4bb1-be80-db2ea72daa6a.png)

in the attack endpoint /api/database/upload

![img](https://cdn.nlark.com/yuque/0/2024/png/2897054/1732537181771-47900999-6e9d-4a18-8b5c-c94a4e4656c0.png)

edit filename for ../../../../tmp/1.txt

![img](https://cdn.nlark.com/yuque/0/2024/png/2897054/1732537192844-420aff21-cf29-429c-9587-4707374dce80.png)

and then u will see  the file content has write into /tmp/1.txt

![img](https://cdn.nlark.com/yuque/0/2024/png/2897054/1732537261033-a2f05dd9-0c5c-4f87-b862-ab3830b22916.png)

# code Audit

as you can see 。 the fileName parameter has not valid the attack char with ../../../

![img](https://cdn.nlark.com/yuque/0/2024/png/2897054/1732537346867-71d0d1c5-db27-42cf-9f8a-dc3dabe3dd10.png)
