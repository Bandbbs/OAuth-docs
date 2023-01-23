# Bandbbs OAuth API documentation

### 1. Obtian appid and appkey

Usage 
appid：Unique id of your application
appkey：The key assigned to the appid

### 2. Add Bandbbs Account Login Button

Insert the Bandbbs Account Login button or selection into your app or webpage  

### 3. Redirect to interface to get Authorization Code

redirect URL：  
```https://www.bandbbs.cn/oauth/```  

Request Parameters：  
|  Parameter   | Description |
|  ----  | ----  |
| response_type  | Authorization type, the value is "code" |
| client_id  | The appid assigned to the app  |
| redirect_uri  | User will callback address after successful authorization, the callback address must be provided when apply for appid, note that requires URLEncode |
| state  | Status value, which must be a 32-digit value composed of lowercase letters and/or numbers. It is used to prevent CSRF attacks and will be called back after successful authorization. Please make sure to strictly check the binding of the user to the state parameter status |

URL example：  
```https://www.bandbbs.cn/oauth/?response_type=code&client_id=1&redirect_uri=https%3A%2F%2Ftest.bandbbs.cn%2Fcallback.php&state=7a990681fc5c697092236ee1e4ece2d0```  

Return：  
1. If the user successfully login to authorize, the user will be redirected to the callback address provided, with the Authorization Code and the original state value at the end of the redirect_uri address.  
such as：  
```https://test.bandbbs.cn/callback.php?code=988940bb8e7ebcae2fdfa77f2c825cd7&state=7a990681fc5c697092236ee1e4ece2d0```
Note: The Authorization Code expires 10 minutes after the user has successfully login and authorized.  

| Parameter   | Description  |
|  ----  | ----  |
| code  | Authorization Code, This value is a 32-digit value composed of lowercase letters and/or numbers |
| state  | Status value. It is used to prevent CSRF attacks and will be called back after successful authorization. Please make sure to strictly check the binding of the user to the state parameter status |

2. If the user cancels the login process during the login authorization process, the login page will be closed directly  
3. If the input parameters are wrong, the wrong parameters will be displayed on page directly. Error Response is at the end of this doc.

### 4. Get Access Token by Authorization Code

This step must be performed on your server

Request Address：  
```https://api.bandbbs.cn/oauth/api/token.php```  
Request Method：  
GET  
Request Parameters：  
|  Parameter   | Description  |
|  ----  | ----  |
| grant_type  | Authorization type, this value is "authorization_code" |
| client_id  | The appid assigned to your app |
| client_secret  | The appkey assigned to your app |
| code  | The Authorization Code contained in the parameter from callback address of the previous step |
| redirect_uri  | User will callback address after successful authorization, the callback address must be provided when apply for appid, note that requires URLEncode |


Return value：  
If the return is successful, the content of the return will be an Access Token.  
If error, the status code will be not 200 and the return content is the error message.
Error Response is at the end of this doc.

### 5. Access to resources by Access Token  

This step must be performed on your server  

Please contact the administrator for the details of this step  


------------------------------------------------

Error Response：  
|  Response   | Description  |
|  ----  | ----  |
| unsupported_response_type  | Invalid authorization type |
| unauthorized_client  | client_id or api_key Invalid |
| invalid_grant  | Invalid Authorization Code  |
| invalid_redirect_uri  | Invalid callback address |
