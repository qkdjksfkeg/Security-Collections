# Description of the vulnerability
The newbee-mall project is an e-commerce system developed based on Spring Boot and related technology stacks. The front desk mall system includes modules such as the home page portal, product classification, personal order management, etc. The background management system includes modules such as data panels, order management, and Settings.
# System situation
## version
V1.0.0
## Project address
https://github.com/newbee-ltd/newbee-mall

# analyse
1. The carousel parameters on line 62 of the NewBeeMallCarouselController file are externally controllable.
<img width="1342" height="695" alt="image" src="https://github.com/user-attachments/assets/92853153-4eeb-4b9a-8ac4-6b1e534c9e16" />
2.The SQL execution is triggered on line 35 of NewBeeMallCarouselServiceImpl to add data to the database
<img width="1497" height="660" alt="image" src="https://github.com/user-attachments/assets/5d5f2646-e9cf-4a47-bc58-edd4e98bf82a" />
3、Stored XSS can be triggered when conducting data queries
<img width="1426" height="567" alt="image" src="https://github.com/user-attachments/assets/7a557d8d-e481-4c1b-a7bf-7089fcf125a3" />
<img width="1427" height="541" alt="image" src="https://github.com/user-attachments/assets/4bb8acdc-b3fb-4196-bea2-841e41c8f4a6" />
# verify
There is an XSS in the carousel configuration of the system's background page at the "New" section. When viewed, it can trigger a vulnerability
<img width="1864" height="992" alt="image" src="https://github.com/user-attachments/assets/fa4db75b-9415-41a5-a904-24f2b7dfc81b" />
<img width="1697" height="614" alt="image" src="https://github.com/user-attachments/assets/c1ee47e3-948c-4c62-b517-c626432db450" />
<img width="1879" height="930" alt="image" src="https://github.com/user-attachments/assets/e226d9eb-2507-4b5c-b261-6bca28366c0d" />







