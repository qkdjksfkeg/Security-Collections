# Description of the vulnerability
Office automation (OA) is the most frequently used application system for the daily operation and management of the organization, which greatly improves the office efficiency of the company.There is SQL injection vulnerability in the background of the system
# System situation
## version
V1.0.0
## Project address
https://github.com/newbee-ltd/newbee-mall

# analyse
1. There is an SQL injection for the goodsName parameter on line 70 of src/main/resources/mapper/NewBeeMallGoodsMapper.xml, as shown in the following figure
<img width="1481" height="881" alt="image" src="https://github.com/user-attachments/assets/30cc932b-075c-45f0-844b-0c0f011a1c11" />
2.Reverse trace to the mapping interface, and the mapping interface code is located
src/main/java/ltd/newbee/mall/dao/NewBeeMallGoodsMapper.java 
<img width="1338" height="873" alt="image" src="https://github.com/user-attachments/assets/28e1daf0-c234-4ccb-b73b-0c617d335af4" />
3.Tracing back, the getNewBeeMallGoodsPage method in NewBeeMallGoodsServiceImpl.java finds the findNewBeeMallGoodsList method call
<img width="1439" height="845" alt="image" src="https://github.com/user-attachments/assets/3a207d26-a3ad-400f-bf87-7e412d6d7c06" />
4.Continue the reverse tracing at src/main/java/ltd/newbee/mall/controller/admin/NewBeeMallGoodsController.java
Line 134 uses the getNewBeeMallGoodsPage method.
<img width="1425" height="610" alt="image" src="https://github.com/user-attachments/assets/9056a304-9ca3-4d52-9eac-48698e2efe3d" />
5.Code analysis NewBeeMallGoodsController list methods in line 129 params introduced into external controllable parameters, Eventually passed newBeeMallGoodsService. GetNewBeeMallGoodsPage methods perform the SQL query, can trigger a SQL injection
<img width="1470" height="614" alt="image" src="https://github.com/user-attachments/assets/2a43083e-331a-4f06-97a4-7ce7809f0c55" />

# verify
![image](https://github.com/user-attachments/assets/813a3e4c-46af-4ec3-a254-451c87f44887)

r.txt

![image](https://github.com/user-attachments/assets/a76490f4-f670-4e88-a61c-28a4aa857f30)

sqlmap test results

```sqlmap.py -r r.txt```

![image](https://github.com/user-attachments/assets/9ff7a993-b6e9-427e-abeb-f07da0516efa)
![image](https://github.com/user-attachments/assets/b27d4207-df5d-4e52-80f9-de45d16ccac8)
