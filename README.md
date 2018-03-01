# 將 Node.js 部署至 Heroku

## 環境安裝

1. 註冊 Heroku
2. 安裝 Git
3. 安裝 Heroku CLI
4. 執行 Heroku login 確認是否安裝成功

參考：[Getting Started on Heroku with Node.js](https://devcenter.heroku.com/articles/getting-started-with-nodejs#introduction)，一步一步照著做。

安裝 Heoku CLI 後，在 CLI 執行 `heroki login` 做用戶認證登入

```shell
$ heroku login
Enter your Heroku credentials:
Email: eden90267@gmail.com
Password: *********
Logged in as eden90267@gmail.com
```

## Node.js 程式碼講解

```javascript
var http = require('http');
http.createServer(function (req, res) {
  if (req.url === '/') {
    res.writeHead(200, {
      'Content-Type': 'text/html'
    });
    res.write('<h1>index!</h1>');
    res.end();
  } else {
    res.writeHead(200, {
      'Content-Type': 'text/html'
    });
    res.write('<h1>404!</h1>');
    res.end();
  }
}).listen(process.env.PORT || 8080);
```

```json
{
  "name": "heroku",
  "version": "0.0.1",
  "engines": {
    "node": "6.11.1"
  },
  "scripts": {
    "start": "node app.js"
  }
}
```

## 將 Node.js 部署至 Heroku

新建：

```shell
$ cd heroku
$ git init
$ git add .
$ git commit -m "Add app.js"
$ heroku create 
$ git push heroku master
$ heroku open
```

更新：

```shell
$ git add .
$ git commit -m "Edit app.js"
$ git push heroku master
```

## NPM 載入細節講解

有 npm 要注意哪些細節？

```shell
$ npm i nodemon --save
```

記得要加 .gitignore ，排除掉 node_modules 資料夾

```
# .gitignore
node_modules
```

```shell
$ git add .
$ git commit -m "Add npm"
$ git push heroku master
```

heroku 就會自動幫你安裝 npm