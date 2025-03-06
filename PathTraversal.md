# Description of the vulnerability
Office automation (OA) is the most frequently used application system for the daily operation and management of the organization, which greatly improves the office efficiency of the company.The system is not strictly filtered, resulting in path traversal problems
# System situation
## version
V1.0
## Project address
https://gitee.com/aaluoxiang/oa_system

## analyse
In the ProcedureController, replacing the /show in the URI path value obtained by getRequestURI with null directly outputs the file stream to the browser, and does not filter the characters related to directory traversal, resulting in the problem of directory traversal.
![image](https://github.com/user-attachments/assets/f2546850-dea5-40ad-ad48-dca6e5ec15d8)

## verify
By constructing poc /show.. / will be replaced with.. /, and finally implement path traversal to read the file.
![image](https://github.com/user-attachments/assets/76e0bb47-ff49-47bf-bffd-a29f4ecd6415)
