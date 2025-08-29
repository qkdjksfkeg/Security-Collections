# Description of the vulnerability
The newbee-mall project is an e-commerce system developed based on Spring Boot and related technology stacks. The front desk mall system includes modules such as the home page portal, product classification, personal order management, etc. The background management system includes modules such as data panels, order management, and Settings.
# System situation
## version
V1.0.0
## Project address
https://github.com/newbee-ltd/newbee-mall

# analyse
1. The configName and redirectUrl parameters of the indexConfig entity class at line 70 of the NewBeeMallGoodsIndexConfigController.java file are externally controllable, and there is an XSS vulnerability.
<img width="1502" height="758" alt="image" src="https://github.com/user-attachments/assets/b7bfed64-e0e5-4011-ac04-f33bc189be76" />
2.The SQL execution is triggered on line 41 of NewBeeMallIndexConfigServiceImpl.java to add data to the database
<img width="1512" height="861" alt="image" src="https://github.com/user-attachments/assets/d9a3350f-39a4-4f5c-a5ae-4163249b5db1" />
3.The stored XSS can be triggered when conducting queries in the configuration section of best-selling products
<img width="1478" height="557" alt="image" src="https://github.com/user-attachments/assets/570830fb-e67f-4e02-9716-c0a06f319e0b" />
<img width="1461" height="524" alt="image" src="https://github.com/user-attachments/assets/28a53ea5-30e5-4fe5-ae12-eb4bac919d8f" />
# verify
When adding products, enter test statements in the configName and redirectUrl fields. After successful addition, clicking on the configuration of best-selling products to view the configuration list will trigger an XSS vulnerability
<img width="1810" height="956" alt="image" src="https://github.com/user-attachments/assets/e1176a1f-e0c6-4c0b-ae60-2ca6951fa7a1" />
<img width="1450" height="636" alt="image" src="https://github.com/user-attachments/assets/968a3a5e-1b51-4a47-8c24-9126bdf667c2" />
<img width="1868" height="907" alt="image" src="https://github.com/user-attachments/assets/6287bcc3-54b5-4b04-8f95-880e299c9345" />



