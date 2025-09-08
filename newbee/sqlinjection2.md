# Description of the vulnerability
The newbee-mall project is an e-commerce system developed based on Spring Boot and related technology stacks. The front desk mall system includes modules such as the home page portal, product classification, personal order management, etc. The background management system includes modules such as data panels, order management, and Settings.There is an unauthorized SQL injection in the system's front desk
# System situation
## version
V1.0.0
## Project address
https://github.com/newbee-ltd/newbee-mall

# analyse
1. There is an SQL injection for the keyword parameter on line 125 of src/main/resources/mapper/NewBeeMallGoodsMapper.xml, as shown in the following figure: 
<img width="1456" height="639" alt="image" src="https://github.com/user-attachments/assets/41406bf7-e7b7-4081-af0e-0f9e4fa6a582" />
2.Reverse trace to the mapping interface, and the mapping interface code is located
src/main/java/ltd/newbee/mall/dao/NewBeeMallGoodsMapper.java 
<img width="1366" height="723" alt="image" src="https://github.com/user-attachments/assets/a4c3e09e-9e87-4336-b808-211d697a420f" />
3.Tracing back, the searchNewBeeMallGoods method in NewBeeMallGoodsServiceImpl.java finds the getTotalNewBeeMallGoodsBySearch method call
<img width="1396" height="845" alt="image" src="https://github.com/user-attachments/assets/1ac131d0-cefd-4d6e-b9c3-d87aafeb9806" />
4.Continue the reverse tracing at src/main/java/ltd/newbee/mall/controller/mall/GoodsController.java
Line 57 uses the searchNewBeeMallGoods method.
<img width="1411" height="849" alt="image" src="https://github.com/user-attachments/assets/dc16fec4-8715-49c9-8137-0c3b6e18f388" />
5.Code analysis GoodsController searchPage methods in line 30 params introduced into external controllable parameters, Eventually passed newBeeMallGoodsService.searchNewBeeMallGoods methods perform the SQL query, can trigger a SQL injection
<img width="1398" height="905" alt="image" src="https://github.com/user-attachments/assets/c498e029-dd22-4e6d-87d6-8da7d5cccc7b" />

# verify
There is SQL injection in the search function
<img width="1866" height="1041" alt="image" src="https://github.com/user-attachments/assets/036a55cf-cb95-4eac-a1d3-4def5dc804b5" />

r.txt

<img width="930" height="526" alt="image" src="https://github.com/user-attachments/assets/3ed03e63-661b-4507-9e76-5487dc838c61" />




sqlmap test results

``` sqlmap.py -u http://127.0.0.1:28089/search?keyword=222```

<img width="1597" height="380" alt="image" src="https://github.com/user-attachments/assets/b0300e75-9014-425e-946e-db513ee1f9cf" />
<img width="1590" height="316" alt="image" src="https://github.com/user-attachments/assets/9fd1a432-4e26-472c-9cd0-1bb4b7ee43be" />




