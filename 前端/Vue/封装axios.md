# 封装axios

创建 api文件夹用来管理所有的API，创建 `axios.js` 文件二次封装axios，其他文件就是对应项目中的功能模块

![image-20220201194456657](Untitled.assets/image-20220201194456657.png)



## axios.js



```javascript
import axios from "axios";
// 从配置文件获取api地址
let baseApi = "";
if (process.env.VUE_APP_URL) {
  baseApi = process.env.VUE_APP_URL;
}

function myAxios(axiosConfig) {
  const service = axios.create({
    // 同一请求
    baseURL: baseApi,
    // 超时时长
    timeout: 10000
  });
  return service(axiosConfig);
}

export default myAxios;
// 返回的是 Promise 对象
```

关于 `export default`



## user.js

post请求

```javascript
import myAxios from "./axios";

export function login(paramsList) {
  return myAxios({
    url: "/api/login",
    method: "post",
    data: paramsList
  });
}
```

对post参数进行序列化处理

```javascript
import myAxios from "./axios";

export function loginApi(paramsList) {
  return myAxios({
    url: "/login",
    method: "post",
    data: paramsList,
    handers: {
      "Content-type": "application/x-www-form-urlencoded"
    },
    transformRequest: [
      data => {
        let result = "";
        for (let key in data) {
          result +=
            encodeURIComponent(key) + "=" + encodeURIComponent(data[key]) + "&";
        }
        return result.slice(0, result.length - 1);
      }
    ]
  });
}

```

通过 `headers` 来指定Content-Type的形式，对于 `transformRequest` 就是允许在向服务器发送前，修改请求数据，但只能用在 'PUT'，'POST' 和 'PATCH' 这几个请求方法，且后面数组中的函数必须返回一个字符串，或 ArrayBuffer，或 Stream，更多的还有 `transformResponse` 能在传递给 then/catch 前，允许修改响应数据，其余更多参数的可以去 [Axios文档](https://link.juejin.cn?target=https%3A%2F%2Fwww.npmjs.com%2Fpackage%2Faxios) 查看。

### 使用第三方模块进行序列化

```
npm i qs;
```

使用

```javascript
import myAxios from "./axios";
import qs from "qs";

export function loginApi(paramsList) {
  return myAxios({
    url: "/login",
    method: "post",
    data: paramsList,
    handers: {
      "Content-type": "application/x-www-form-urlencoded"
    },
    transformRequest: [
      data => {
        return qs.stringify(data);
      }
    ]
  });
}
```

使用

```vue
<template>
  <div class="home">
    <h3>登录</h3>
    <form>
      <div>
        用户名：
        <input type="text" v-model="loginFrom.username" />
      </div>
      <div>
        密码：
        <input type="password" v-model="loginFrom.password" />
      </div>
    </form>
    <div>
      <button @click="login">登录</button>
    </div>
  </div>
</template>

<script>
import { loginApi } from "@/api/user.js";
export default {
  name: "home",
  data() {
    return {
      loginFrom: {
        username: "admin",
        password: "123456"
      }
    };
  },
  methods: {
    login() {
      loginApi(this.loginFrom).then(res => {
        console.log(res.data);
        localStorage.setItem("token", res.data.data.token);
      });
    }
  },
  mounted() {}
};
```

## goods.js

```javascript
import myAxios from "./axios";

// eslint-disable-next-line no-unused-vars
export function getListApi(paramsList) {
  return myAxios({
    url: "/goods",
    method: "get",
    params: paramsList
  });
}
```

使用

```vue
<template>
  <div class="about">
    <button @click="getGoodsList">获取商品列表</button>
  </div>
</template>
<script>
import { getListApi } from "@/api/goods.js";
export default {
  name: "home",
  methods: {
    getGoodsList() {
      getListApi({ pagenum: 1, pagesize: 5 }).then(res => {
        console.log(res);
      });
    }
  },
  mounted() {
    let baseApi = "";
    if (process.env.VUE_APP_URL) {
      baseApi = process.env.VUE_APP_URL;
    }
    console.log(baseApi);
  }
};
</script>
```







## 请求自动携带 token

```javascript
import axios from "axios";

// 从配置文件获取api地址
let baseApi = "";
if (process.env.VUE_APP_URL) {
  baseApi = process.env.VUE_APP_URL;
}

// 获取token
const token = localStorage.getItem("token");

function myAxios(axiosConfig, customOptions, loadingOptions) {
  const service = axios.create({
    // 同一请求
    baseURL: baseApi,
    // 超时时长
    timeout: 10000
  });
  service.interceptors.request.use(config => {
    // 自动携带token
    if (token && typeof window !== "undefined") {
      config.headers.Authorization = token;
    }
    return config;
  });
  return service(axiosConfig);
}

export default myAxios;
// 返回的是 Promise 对象
```



## 简洁的数据响应结构

```javascript
import axios from "axios";

// 从配置文件获取api地址
let baseApi = "";
if (process.env.VUE_APP_URL) {
  baseApi = process.env.VUE_APP_URL;
}

// 获取token
const token = localStorage.getItem("token");

function myAxios(axiosConfig, customOptions, loadingOptions) {
  const service = axios.create({
    // 同一请求
    baseURL: baseApi,
    // 超时时长
    timeout: 10000
  });

  // 自定义配置
  let custom_options = Object.assign({
    // 是否开启简洁数据结构响应，默认为true
    reduct_data_format: true
  });

  service.interceptors.response.use(response => {
    return custom_options.reduct_data_format ? response.data : response;
  });

  service.interceptors.request.use(config => {
    // 自动携带token
    if (token && typeof window !== "undefined") {
      config.headers.Authorization = token;
    }
    return config;
  });
  return service(axiosConfig);
}

export default myAxios;
// 返回的是 Promise 对象
```



































































