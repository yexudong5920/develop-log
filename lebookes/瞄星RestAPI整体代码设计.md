# 瞄星RestAPI整体代码设计

1. RestController
  1. Controller类添加@RestController注解（必须Spring4.0以上）
  2. 标注RequestMapping的方法必须返回org.springframework.http.ResponseEntity， 必须增加responseBody和http status code
  3. 可预料的异常与错误，必须返回通俗易懂的responsebody与http status code

2. 错误代码管理与分类
