# 米坛社区 OAuth API 表盘自定义工具定制 文档


### 获取用户信息

此步骤必须在您的应用服务器完成

请求地址： 
```https://api.bandbbs.cn/oauth/api/wftools.php```  

请求方法：  
GET  

请求头：  
|  参数   | 说明  |
|  ----  | ----  |
| access-token  | 前序步骤中获取到的授权码(Authorization Code) |
| client-id  | 分配给应用的appid |
| client-secret  | 分配给应用的appkey |


返回说明：  

返回格式  
JSON
 
JSON内容：

成功：  
状态码为200  
|  参数   | 说明  |
|  ----  | ----  |
| success  | 请求是否成功 成功时为true |
| user_id  | 用户ID |
| user_name  | 用户名 |
| avatar_urls  | 米坛用户头像URL |
| mac  | 用户的表盘自定义工具的MAC绑定 |


失败：  
状态码不为200  
|  参数   | 说明  |
|  ----  | ----  |
| success  | 请求是否成功 失败时为false |
| msg  | 仅当success为false时存在 内容为失败原因 文档末尾附错误响应内容 |



  
------------------------
      

### 修改用户MAC地址

此步骤必须在您的应用服务器完成

此接口不会校验是否修改成功，请比对输入的新MAC地址与返回的MAC地址确保修改成功

请求地址： 
```https://api.bandbbs.cn/oauth/api/wftools.php```  

请求方法：  
POST 

请求头：  
|  参数   | 说明  |
|  ----  | ----  |
| access-token  | 前序步骤中获取到的授权码(Authorization Code) |
| client-id  | 分配给应用的appid |
| client-secret  | 分配给应用的appkey |

请求体：  
form-data  

|  参数   | 说明  |
|  ----  | ----  |
| NEW_MAC  | 新的MAC地址 |



返回说明：  

返回格式  
JSON
 
JSON内容：

成功：  
状态码为200  
|  参数   | 说明  |
|  ----  | ----  |
| success  | 请求是否成功 成功时为true |
| user_id  | 用户ID |
| user_name  | 用户名 |
| avatar_urls  | 米坛用户头像URL |
| mac  | 用户的表盘自定义工具的MAC绑定 |


失败：  
状态码不为200  
|  参数   | 说明  |
|  ----  | ----  |
| success  | 请求是否成功 失败时为false |
| msg  | 仅当success为false时存在 内容为失败原因  文档末尾附错误响应内容 |


------------------------------------------------

错误内容：  
|  msg返回值   | 说明  |
|  ----  | ----  |
| unauthorized_client  | client_id或api_key有误 |
| invalid_grant  | 用户授权码无效 |
| invalid_mac  | mac地址不合法 |
| account_banned  | 用户账户被封禁 |
| account_not_activated  | 用户账户未激活或被封禁 |


