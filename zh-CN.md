# 米坛社区 OAuth API 文档

### 1. 获取 申请appid和appkey

appid和appkey的用途  
appid：应用的唯一标识。用于识别接入应用的身份  
appkey：appid对应的密钥，访问用户资源时用来验证应用的合法性  

### 2. 放置 米坛社区帐号 登录 按钮

将米坛社区帐号 登录 按钮或选项放入您的APP或者网页  

### 3. 唤起接口获取授权码(Authorization Code)

用户跳转地址：  
```https://www.bandbbs.cn/oauth/```  

请求参数：  
|  参数   | 说明  |
|  ----  | ----  |
| response_type  | 授权类型，此值固定为“code” |
| client_id  | 分配给应用的appid |
| redirect_uri  | 成功授权后的回调地址，必须是申请appid时提供的回调地址，注意需要进行URLEncode |
| state  | 状态值，必须为32位由小写字母和/或数字组成的值。用于防止CSRF攻击，成功授权后回调时会原样带回。请务必严格检查用户与state参数状态的绑定 |

例如：  
```https://www.bandbbs.cn/oauth/?response_type=code&client_id=1&redirect_uri=https%3A%2F%2Ftest.bandbbs.cn%2Fcallback.php&state=7a990681fc5c697092236ee1e4ece2d0```  

返回说明：  
1. 如果用户成功登录授权，则会跳转到指定的回调地址，并在redirect_uri地址后带上Authorization Code和原始的state值。如：  
```https://test.bandbbs.cn/callback.php?code=988940bb8e7ebcae2fdfa77f2c825cd7&state=7a990681fc5c697092236ee1e4ece2d0```
注意：授权码(Authorization Code)会在用户成功登录授权成功后10分钟过期。  

|  参数   | 说明  |
|  ----  | ----  |
| code  | 授权码(Authorization Code)，此值为32位由小写字母和/或数字组成的值 |
| state  | 请求时的状态值，用于防止CSRF攻击。请务必严格检查用户与state参数状态的绑定|

2. 如果用户在登录授权过程中取消登录流程，登录页面直接关闭  
3. 如果传入参数有误，会直接在页面弹窗显示错误参数  

### 4. 通过授权码(Authorization Code)获取访问令牌(Access Token)

此步骤必须在您的应用服务器完成

请求地址：  
```https://api.bandbbs.cn/oauth/api/token.php```  
请求方法：  
GET  
请求参数：  
|  参数   | 说明  |
|  ----  | ----  |
| grant_type  | 授权类型，此值为“authorization_code” |
| client_id  | 分配给应用的appid |
| client_secret  | 分配给应用的appkey |
| code  | 上一步用户跳转回调地址所携带的的授权码(Authorization Code) |
| redirect_uri  | 成功授权后的回调地址，必须是申请appid时提供的回调地址，注意需要进行URLEncode |


返回值：  
如果成功返回，返回内容体将会是访问令牌(Access Token)  
如果错误，返回状态码将是非200，返回内容体将会是错误信息  

### 5.通过访问令牌(Access Token)访问资源  

此步骤必须在您的应用服务器完成

此项目具体内容请与管理员商定  
