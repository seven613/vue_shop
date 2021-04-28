# vue_api_server
## config -> default.json -> db_config
```
  	"db_config" : {
		"protocol" : "mysql",
		"host" : "127.0.0.1",
		"database" : "mydb",
		"user" : "root",
		"password" : "xiao",
		"port" : 3306
```
## MySQL不支持客户端
```
	ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'xiao';
```
## 启动项目
```
  node app.js
```
# vue_shop

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```

### Lints and fixes files
```
yarn lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
