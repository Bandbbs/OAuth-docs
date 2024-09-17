# Bandbbs OAuth API documentation

### 1. Obtian Client ID and Client Secret

Client ID: The unique identifier for the application, used to identify the identity of the connected app.
Client Secret: The secret associated with the Client ID, used to verify the application when accessing user resources.
Scope: Used to define the type of permissions requested.

### 2. Add Bandbbs Account Login Button

Insert the Bandbbs Account Login button or selection into your app or webpage  

### 3. Redirect to interface to get Authorization Code

User redirection URL:  
```https://www.bandbbs.cn/oauth2/authorize```  

Request Parameters:  
| Parameter    | Description  |
| ------------ | ------------- |
| type         | Authorization type, fixed as "authorization_code" |
| client_id    | Client ID assigned to the application |
| redirect_uri | Callback URL after successful authorization, must be the same as the callback URL provided during Client ID application. Ensure URL is properly URL-encoded. |
| state        | A 32-character value composed of lowercase letters and/or numbers, used to prevent CSRF attacks. The same state value will be returned in the callback after successful authorization. Ensure strict validation of the user's session with the state parameter. |
| response_type | Response type, fixed as "code" |
| scope        | The requested permission type, with multiple permissions separated by `%20` |

Example:  
```https://www.bandbbs.cn/oauth2/authorize?type=authorization_code&client_id=2550505&redirect_uri=https://test.bandbbs.cn/callback.php&response_type=code&scope=user%3Aread%20user%3Awrite&state=7a990681fc5c697092236ee1e4ece2d0```  

Response Explanation:  
1. If the user successfully log-in and authorizes, they will be redirected to the specified callback URL, with the Authorization Code and original state value appended to the redirect_uri. For example:  
```https://test.bandbbs.cn/callback.php?code=988940bb8e7ebcae2fdfa77f2c825cd7&state=7a990681fc5c697092236ee1e4ece2d0```  

| Parameter | Description  |
| --------- | ------------- |
| code      | Authorization code (Authorization Code) |
| state     | The state value provided during the request, used to prevent CSRF attacks. Ensure strict validation of the user's session with the state parameter. |

2. If the user cancels the login process during authorization, the login page will close directly.


### 4. Get Authorization Code for Access Token

This step must be completed on your application server.

Request URL:  
```https://www.bandbbs.cn/api/oauth2/token```  
Request Method:  
POST  

Request Parameters:  
| Parameter    | Description  |
| ------------ | ------------- |
| grant_type   | Authorization type, this value is "authorization_code" |
| client_id    | The Client ID assigned to the application |
| client_secret| The Client secret assigned to the application |
| code         | The Authorization Code from the previous step, provided in the callback URL |
| redirect_uri | The callback URL after successful authorization, must be the same as the callback URL provided during Client ID application. Ensure URL is properly URL-encoded. |

Response:  
If the request is successful, it will return a response similar to the following:
```
{
    "access_token": "4f40d5ee8bf0476cb6b6f42ed53247a1",
    "refresh_token": "f6bec4e6ef7470fc6f0101e3975ad4b9",
    "token_type": "bearer",
    "expires_in": 7200,
    "issue_date": 1722550505
}
```
Please ensure to save the Access Token and Refresh Token.

### 5. Accessing Resources Using Access Token  

This step must be completed on your application server.

To retrieve information about the current token, use the following:

Request URL:  
```https://www.bandbbs.cn/api/oauth2/token```  
Request Method:  
GET

Request Parameters:  
| Parameter  | Description  |
| ---------- | ------------- |
| token      | The user's Access Token |

Response:  
If the request is successful, it will return a response similar to the following:

```
{
    "user_id": 1,
    "scope": {
        "user:read": true,
        "user:write": true
    },
    "expires_in": 7200,
    "issue_date": 1722550505
}
```


For other API usage, please refer to:  
[https://xenforo.com/community/pages/api-endpoints/](https://xenforo.com/community/pages/api-endpoints/)

Use the appropriate API directly. Authorization is done via Bearer Token, where the token value is the user's Access Token.

No need to use XF-Api-Key or other authorization keys and request parameters.

### 6. Refreshing Access Token

This step must be completed on your application server.

Request URL:  
```https://www.bandbbs.cn/api/oauth2/token```  

Request Method:  
POST  

Request Parameters:  
| Parameter      | Description  |
| -------------- | ------------- |
| grant_type     | Authorization type, this value is "refresh_token" |
| client_id      | The Client ID assigned to the application |
| client_secret  | The client secret assigned to the application |
| refresh_token  | The user's Refresh Token |
| redirect_uri   | The callback URL after successful authorization, must be the same as the callback URL provided during Client ID application. Ensure URL is properly URL-encoded. |

Response:  
If the request is successful, it will return a response similar to the following:

```
{
    "access_token": "4f40d5ee8bf0476cb6b6f42ed53247a1",
    "refresh_token": "f6bec4e6ef7470fc6f0101e3975ad4b9",
    "token_type": "bearer",
    "expires_in": 7200,
    "issue_date": 1722550505
}
```

Please ensure to save the Access Token and Refresh Token.



