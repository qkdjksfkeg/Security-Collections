# Description of the vulnerability
The newbee-mall project is an e-commerce system developed based on Spring Boot and related technology stacks. The front desk mall system includes modules such as the home page portal, product classification, personal order management, etc. The background management system includes modules such as data panels, order management, and Settings.There is an SQL injection in the system's background management interface
# System situation
## version
V1.0.0
## Project address
https://github.com/newbee-ltd/newbee-mall

# analyse
1. There is an SQL injection for the goodsName parameter on line 150 of src/main/resources/mapper/NewBeeMallGoodsMapper.xml, as shown in the following figure: 
<img width="1103" height="882" alt="image" src="https://github.com/user-attachments/assets/ecdd3f4c-6d2b-4d48-b3e8-5de7bb250631" />
2.Reverse trace to the mapping interface, and the mapping interface code is located
src/main/java/ltd/newbee/mall/dao/NewBeeMallGoodsMapper.java 
<img width="1228" height="805" alt="image" src="https://github.com/user-attachments/assets/dd26c75d-2a66-471f-87b3-329cecbf2e03" />
3.Tracing back, the getNewBeeMallGoodsPage method in NewBeeMallGoodsServiceImpl.java finds the getTotalNewBeeMallGoods method call
<img width="1300" height="507" alt="image" src="https://github.com/user-attachments/assets/dd9a2db8-a5cc-41fb-a715-0112561f525a" />
4.Continue the reverse tracing at src/main/java/ltd/newbee/mall/controller/admin/NewBeeMallGoodsController.java
Line 134 uses the getNewBeeMallGoodsPage method.
<img width="1425" height="610" alt="image" src="https://github.com/user-attachments/assets/9056a304-9ca3-4d52-9eac-48698e2efe3d" />
5.Code analysis NewBeeMallGoodsController list methods in line 129 params introduced into external controllable parameters, Eventually passed newBeeMallGoodsService. GetNewBeeMallGoodsPage methods perform the SQL query, can trigger a SQL injection
<img width="1470" height="614" alt="image" src="https://github.com/user-attachments/assets/2a43083e-331a-4f06-97a4-7ce7809f0c55" />

# verify
The commodity management module can trigger SQL injection
<img width="1869" height="1011" alt="image" src="https://github.com/user-attachments/assets/b7a4caf4-ee9d-47c2-9dd1-fcaa7179eea6" />

r.txt

<img width="902" height="414" alt="image" src="https://github.com/user-attachments/assets/41461267-f1f8-4703-a8ac-fac003683151" />



sqlmap test results

```sqlmap.py -r r.txt```

<img width="1885" height="786" alt="image" src="https://github.com/user-attachments/assets/0068355f-be42-47db-ae94-cbe1f0fd512c" />


