# Description of the vulnerability
The newbee-mall project is an e-commerce system developed based on Spring Boot and related technology stacks. The front desk mall system includes modules such as the home page portal, product classification, personal order management, etc. The background management system includes modules such as data panels, order management, and Settings.
# System situation
## version
V1.0.0
## Project address
https://github.com/newbee-ltd/newbee-mall

# analyse
1.In PersonalController. Java files in the line 116 mallUser entity class the nickName of external controllable parameters, XSS holes, the address is affected/admin/personal/updateInfo
<img width="1519" height="815" alt="image" src="https://github.com/user-attachments/assets/f7c9c367-bcf9-4e60-b595-1eb285416c6a" />
2.In line 78 of the NewBeeMallUserServiceImpl.java file, SQL execution is called to store the data in the database
<img width="1486" height="831" alt="image" src="https://github.com/user-attachments/assets/0a471c2f-954a-4e7c-8a6d-40818d8a698f" />
3.The XSS vulnerability can be triggered when viewing member information in the member management office
<img width="1547" height="704" alt="image" src="https://github.com/user-attachments/assets/8af16221-57d1-4869-9ef3-d7bfd01c825f" />
<img width="1512" height="544" alt="image" src="https://github.com/user-attachments/assets/e5c184c7-2ed3-40a6-ba25-bb44a2205a8b" />




# verify
When the user modifies the personal information, the test statement is filled in the nickname, and the vulnerability can be triggered when the member information is viewed in the member management office of the system background
<img width="1829" height="919" alt="image" src="https://github.com/user-attachments/assets/c7845c45-eced-44fd-9c3a-503947af3db3" />
<img width="1624" height="725" alt="image" src="https://github.com/user-attachments/assets/8c14480a-8fb2-4a59-b15a-b1596d1587f9" />
<img width="1874" height="1025" alt="image" src="https://github.com/user-attachments/assets/968d86aa-8f66-4cce-82ef-fbc141e35a38" />











