# Description of the vulnerability
Office automation (OA) is the most frequently used application system for the daily operation and management of the organization, which greatly improves the office efficiency of the company.There is SQL injection vulnerability in the background of the system
# System situation
## version
V1.1
## Project address
https://gitee.com/aaluoxiang/oa_system

# analyse
1.The global search found that ${pinyin} is used as a connection parameter in src/main/resources/mappers/address-mapper.xml.  So, if we can control the parameters, it's going to cause SQL injection.
![image](https://github.com/user-attachments/assets/7cd19be4-c7f7-4a4c-8db4-a7669693aa33)

2.Find the allDirector() method declaration in src/main/java/cn/gson/oasys/mappers/AddressMapper.java.  You can control pinyin.  Let's go ahead and find where the allDirector() method is called.
![image](https://github.com/user-attachments/assets/cbc97f47-49ac-434f-8097-5b86ad2187f6)

3.Clearly, we directly into the controller layer and found alph parameters in src/main/Java/cn/gson/oasys/controller/address/AddrController Java:485 incoming. The allDirector () method is then called on line 489 to execute the SQL query. Therefore, as long as we are able to pass the corresponding parameters over HTTP, the SQL injection vulnerability can be triggered.
![image](https://github.com/user-attachments/assets/e5ed64aa-1cfe-4e50-ab52-84438aa3e025)

# verify
![image](https://github.com/user-attachments/assets/813a3e4c-46af-4ec3-a254-451c87f44887)

r.txt

![image](https://github.com/user-attachments/assets/a76490f4-f670-4e88-a61c-28a4aa857f30)

sqlmap test results

```sqlmap.py -r r.txt```

![image](https://github.com/user-attachments/assets/9ff7a993-b6e9-427e-abeb-f07da0516efa)
![image](https://github.com/user-attachments/assets/b27d4207-df5d-4e52-80f9-de45d16ccac8)


