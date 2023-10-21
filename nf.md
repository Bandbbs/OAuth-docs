# Bandbbs OAuth API Notify APP Documentation


### Get User Information

You'll need to complete this step on your application server.

Request URL:
```https://api.bandbbs.cn/oauth/api/nf.php```  

Request Method:  
GET  

Request Headers:    
|  Parameter   | Description  |
|  ----  | ----  |
| access-token  | Access Token obtained in the previous step |
| client-id  | appid assigned to the application |
| client-secret  | appkey assigned to the application |


Response Details: 

Response Format   
JSON
 
JSON Content:：

Success:  
Status code is 200  
|  Parameter   | Description  |
|  ----  | ----  |
| success  | True when request successful and valid. |
| user_id  | User ID  |
| user_name  | Username |
| avatar_urls  | User's avatar URL |
| nf_miband_pro_mac  | MAC binding of Notify For Miband  |
| nf_amazfit_pro_mac  | MAC binding of Notify For Amazfit |
| nf_xiaomi_pro_mac  | MAC binding of Notify For Xiaomi |
| nf_miband_pro  |  If the User purchased Notify For Miband Pro, it would be true. |
| nf_amazfit_pro  | If the User purchased Notify For Amazfit Pro, it would be true. |
| nf_xiaomi_pro  | If the User purchased Notify For Xiaomi Pro, it would be true. |



Failure:     
Status code is not 200   
|  Parameter   | Description  |
|  ----  | ----  |
| success  | False when request has something wrong. |
| msg  | Only exists if "success" is false, content contains failure reason and error response content is attached at the end of the document. |


------------------------------------------------

Error Content:  
|  msg Return Value | Description  |
|  ----  | ----  |
| unauthorized_client  | client_id or api_key is not valid |
| invalid_grant  |  authorization code is invalid |
| account_banned  | User account is banned |
| account_not_activated  | User account is not activated or banned |


