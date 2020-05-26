# HTTP 模块
## 服务器对象
`http.createServer()`

```js
let http=require('http')

http.createServer((req, res)=>{
    console.log('server start.')

    res.write('server res.');
    res.end('server end');
}).listen(8080)
```

使用浏览器访问`localhost:8080`，控制台显示：
> server start

浏览器显示：
> server res.<br />
server end

```js
let http=require('http')
let fs=require('fs')
http.createServer((req, res)=>{
    // part1
    console.log(req.url)

    // part2
    fs.readfile(`./${req.url}`, (err, data) => {
        if(err){
            console.log(err)
            res.writeHead(404)
            res.end('404 not found')
        } else {
            res.end(data)
        }
    })
}).listen(8080)
```
### part1 
使用浏览器访问`localhost:8080`，控制台显示：
> /

使用浏览器访问`localhost:8080/1.html`，控制台显示：
> /1.html

### part2
使用浏览器访问`localhost:8080/1.html`，浏览器显示1.html的内容。


# Node中的数据交互
HTTP报文组成：
- 头： 不大于32k
- 体： 不大于2g

- get 获取数据，数据在url里进行传输，容量小
- post
- put
- delete
- ...

## Get 请求
```js
const http = require('http')
const url=require('url')
http.createServer((req, res)=>{
    console.log(req.url)
    console.log(url.parse(req.url))
    console.log(url.parse(req.url, true))

    let {pathname, query} = url.parse(req.url, true)
    console.log(pathname, query)
}).listen(8080)
```

```html
<form action="http://localhost:8080/aaa" method='GET'>
    <label for='username'>用户名</label>
    <input type='text' name='username' />
    <input type='submit' value='提交'>
</form>
```

## Post请求 
```js
const http = require('http')
const querystring=require('querystring')
http.createServer((req, res)=>{
    let result = []
    req.on('data', (buffer)=>{
        result.push(buffer)
    })
    req.on('end', ()=>{
        let postdata = Buffer.concat(result).toString()
        console.log(querystring.parse(postdata))
    })
}).listen(8080)
```

```html
<form action="http://localhost:8080/aaa" method='POST'>
    <label for='username'>用户名</label>
    <input type='text' name='username' />
    <input type='submit' value='提交'>
</form>
```

## 用到的模块
- http
- url
- querystring