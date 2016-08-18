# 消除单页面应用（SPA）路由上的#前缀

1. $locationProvider.html5mode(true)
    
    $locationProvider.html5mode([mode])
        
    mode: 
    
    type: Object
    
    properties:
        
    * enabled-{boolean}-(default: false)，如果为true，会在支持history.pushState的浏览器依靠pushState来改变url，在不支持pushState的浏览器会变回#前缀的路径
    * requireBase-{boolean}-(default: true)，如果html5mode被使用，此参数指定是否需要呈现一个base标签。如果enabled requireBase都设置为true，并且没有base标签，那么在注入$location时angular会抛出错误
    * rewriteLinks-{boolean}-(default: true)，是否重写html5mode下的相对路径
    
    type: boolean
    
    只设置enabled
    
2. `<head>`中增加`<base href="/">`指定base路径

3. 刷新页面时给出get请求错误

    > Cannot GET /detail?workid=4
    
    3.1. 出现原因
    
    当第一次访问页面/detail，就是刷新页面后，浏览器无从得知这是否是一个真的url还是html5的state。
    所以浏览器直接去服务器寻址，并返回了404的错误。
    
    然而，如果根页面（index.html）以及所以的javascript代码全部加载完成，此时尝试导航到/detail，angular就能在浏览器尝试寻址服务器之前迅速地导航到该state。
    
    详见[stackoverflow](http://stackoverflow.com/questions/16569841/reloading-the-page-gives-wrong-get-request-with-angularjs-html5-mode)
    
    3.2. 此处的关键，在于将服务器上未解决的请求转移到SPA的根路径