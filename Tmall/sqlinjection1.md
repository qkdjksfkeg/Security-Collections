# Description of the vulnerability
Mini-Tmall is a mini Tmall mall based on Spring Boot, which can be quickly deployed and run, and is suitable as a template for completion.There is an SQL injection in the background of this system
# System situation
## version
2025/02/11 latest
## Project address
https://gitee.com/project_team/Tmall_demo

# analyse
1.The global search found that ${orderUtil. orderBy} is used as a connection parameter in mybatis/mapper/RewardMapper.xml:74. So, if we can control the parameters, it's going to cause SQL injection.
<img width="1586" height="497" alt="image" src="https://github.com/user-attachments/assets/15fac788-5cd7-4b35-bdfc-b82a67ccf99c" />
2.Find the select() method declaration in com/xq/tmall/dao/RewardMapper.java:17. You can control orderUtil. orderBy by passing an argument to orderUtil. Let's go ahead and find where the select() method is called.
<img width="1578" height="672" alt="image" src="https://github.com/user-attachments/assets/bb3a61e4-a19d-40d6-9ab8-5e9eb918e0a0" />
3.You can see the call to RewardMapper.select() found in com/xq/tmall/service/impl/RewardServiceImpl.java:43. Let's go up and see where getList() is called.
<img width="1424" height="635" alt="image" src="https://github.com/user-attachments/assets/5c2fd084-02c6-4089-83ff-a87e83319a31" />
4.It is obvious that we went directly to the controller layer and found that getList() was called in com/xq/tmall/controller/admin/RewardController.java:97. SQL injection can be triggered by controlling the orderUtil parameter
<img width="1499" height="710" alt="image" src="https://github.com/user-attachments/assets/37bea08c-e9c7-41f5-b700-23724018802f" />
5.The orderBy parameter without checking passed directly to OrderUtil method
<img width="1438" height="927" alt="image" src="https://github.com/user-attachments/assets/36efbb2d-be4d-46fa-9afd-b06263f62984" />

# verify

r.txt
![image](https://github.com/user-attachments/assets/a18389be-0cab-4f30-81d7-124a10199f30)

sqlmap test results

```sqlmap -r r.txt --dbs```

<img width="1343" height="824" alt="image" src="https://github.com/user-attachments/assets/671cad69-64f6-4f5f-b357-9eff6550bee6" />






