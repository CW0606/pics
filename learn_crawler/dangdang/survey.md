#当当网号码注册信息爬取
[TOC]
##调研
###调研方式
    主要通过浏览器工具比如Chrome。认为的去忘记密码，登陆，注册界面去尝试通过手机号码验证手机号码是否存在
    针对注册页面需要了解手机号码验证url，请求方式，已注册返回值，未注册返回值


###实际调研
    注册页面：
![register page](https://raw.githubusercontent.com/CW0606/pics/master/learn_crawler/dangdang/register_page.png)
    
    
    
    参数页面：
![params](https://raw.githubusercontent.com/CW0606/pics/master/learn_crawler/dangdang/params.png)
![param2](https://raw.githubusercontent.com/CW0606/pics/master/learn_crawler/dangdang/params2.png)
    
    已注册信息：
![param2](https://raw.githubusercontent.com/CW0606/pics/master/learn_crawler/dangdang/registered.png)
    未注册信息
![param2](https://raw.githubusercontent.com/CW0606/pics/master/learn_crawler/dangdang/unregistered.png)
    
    
##编码实现
###实现方式
    使用Python开发时，主要使用requests 库，模拟请求，获得相关数据。当对方返回的信息为json时，可以直接通过将返回结果通过json库转换为字典。
    然后对结果进行操作。如果返回的结果为html页面源码，可以借助beautifulsoup 库对页面解析。获得想要的值
    
###具体实现
    注意：在使用浏览器访问时，会设置一个请求头，表明客户端是一个浏览器，同时向服务器说明对结果的要求【编码，语言，是否压缩，压缩格式等】，
    在构建一个请求时，需要构建一个Session，来保证请求的持续性。然后将请求更新头加入到请求中间
    
    主要代码部分：
    ```python
    request = requests.Session()
    request.header.update({})
    url = '当当号码验证地址'
    data ＝ 
    {
        需要传入的参数，通过调研获得
    }
    response ＝ request.post(url,data)
    
    获得返回结果后：
    json：
        results＝ json.loads(response.content)
        value = results.get(key)
    html:
        results = BeautifulSoup(response.content,'html5lib')
        value = results.find('div',{'name':'login'}).get('value')
    
    ```
    在编写代码之前需要安装好相应的库，如requests ，BeautifulSoup4 ，html5lib库
    
##总结
    以上就是对当当网进行号码探测的部分教程。主要工作在调研上。 
    
    
    


