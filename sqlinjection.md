# Description of the vulnerability
Office automation (OA) is the most frequently used application system for the daily operation and management of the organization, which greatly improves the office efficiency of the company.There is SQL injection vulnerability in the background of the system
# System situation
## version
V1.1
## Project address
https://gitee.com/aaluoxiang/oa_system

# analyse
1.The global search found that ${baseKey} is used as a connection parameter in src/main/resources/mappers/address-mapper.xml.  So, if we can control the parameters, it's going to cause SQL injection.
![image](https://github.com/user-attachments/assets/01f5a411-8f54-4d2c-a3ee-36060213eb99)

2.Find the allDirector() method declaration in src/main/java/cn/gson/oasys/mappers/AddressMapper.java.  You can control baseKey.  Let's go ahead and find where the allDirector() method is called.
![image](https://github.com/user-attachments/assets/c41cad96-9f00-4f68-96ef-8c8d18cd64cf)

3.Clearly, we directly into the controller layer and found baseKey parameters in src/main/Java/cn/gson/oasys/controller/address/AddrController Java:483 incoming. The allDirector () method is then called on line 489 to execute the SQL query. Therefore, as long as we are able to pass the corresponding parameters over HTTP, the SQL injection vulnerability can be triggered.
![image](https://github.com/user-attachments/assets/9a6c6bbd-a890-4a32-8ba9-4e99d4504347)

# verify
![image](https://github.com/user-attachments/assets/b98bdd8d-e24c-46a3-a6b6-565109cf4b4d)

r.txt
![image](https://github.com/user-attachments/assets/a18389be-0cab-4f30-81d7-124a10199f30)

sqlmap test results

```sqlmap.py -r r.txt```

![image](https://github.com/user-attachments/assets/1b68078b-8ab0-4840-8498-ad8a57027fce)
![image](https://github.com/user-attachments/assets/5ab5db03-942a-41ac-b6a0-3489265df483)




