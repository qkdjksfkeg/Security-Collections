# Description of the vulnerability
The newbee-mall project is an e-commerce system developed based on Spring Boot and related technology stacks. The front desk mall system includes modules such as the home page portal, product classification, personal order management, etc. The background management system includes modules such as data panels, order management, and Settings.There is a stored XSS in the system's background management interface
# System situation
## version
V1.0.0
## Project address
https://github.com/newbee-ltd/newbee-mall

# analyse
1. The goodsName and goodsIntro field parameters in the NewBeeMallGoods entity on line 155 of the NewBeeMallGoodsController.java file are externally controllable and are vulnerable to stored XSS
<img width="1368" height="874" alt="image" src="https://github.com/user-attachments/assets/4160db6d-c526-4b0a-ae70-3927d0190420" />
2.The SQL execution is triggered on line 35 of NewBeeMallGoodsServiceImpl.java to add data to the database
<img width="1304" height="539" alt="image" src="https://github.com/user-attachments/assets/454c03ee-b7af-45b1-8c9c-ac554fdfedfb" />
3.The stored XSS is triggered when a data query is executed at the commodity management module
<img width="1517" height="618" alt="image" src="https://github.com/user-attachments/assets/0c989529-92a2-4972-ad84-366a864dbef5" />
<img width="1542" height="548" alt="image" src="https://github.com/user-attachments/assets/f0966bdb-464e-4c70-8ca4-ef5c57fd1cf5" />



# verify
When adding a product, enter the test statement in the goodsName and goodsIntro fields. After the addition is successful, clicking on the product management to view the product list can trigger an XSS vulnerability
<img width="1823" height="1060" alt="image" src="https://github.com/user-attachments/assets/122d99a2-7b00-49ce-8612-d036dd2dccfa" />
<img width="1875" height="990" alt="image" src="https://github.com/user-attachments/assets/a1c24a34-f852-4f7c-90fa-ab90fa6f80b1" />
<img width="1669" height="750" alt="image" src="https://github.com/user-attachments/assets/b7798c3d-0373-40a0-beb4-26d17f8c4c42" />
<img width="1847" height="1011" alt="image" src="https://github.com/user-attachments/assets/f4f531f9-95fc-43ed-b3ac-3d27113fc6b5" />
<img width="1864" height="1023" alt="image" src="https://github.com/user-attachments/assets/8500b3a9-6a86-4185-8dbe-3026c4eb2e1b" />













