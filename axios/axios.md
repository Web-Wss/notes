# json-server搭建：

安装：

```
npm install -g json-server
```

在文件夹下创建一个db.json文件

```json
{
  "posts": [
    { "id": 1, "title": "json-server", "author": "typicode" }
  ],
  "comments": [
    { "id": 1, "body": "some comment", "postId": 1 }
  ],
  "profile": { "name": "typicode" }
}
```

启动：

```
json-server --watch db.json
```

# axios基本使用：

```javascript
<script>
    const btns = document.querySelectorAll('button');

    btns[0].onclick = function () {
      // 发送AJAX请求
      axios({
        // 请求类型
        method: 'GET',
        // URL
        url: 'http://localhost:3000/posts/2',
      }).then(response => {
        console.log(response);
      })
    }
    // 添加新的文章
    btns[1].onclick = function () {
      // 发送AJAX请求
      axios({
        // 请求类型
        method: 'POST',
        // URL
        url: 'http://localhost:3000/posts',
        // 设置请求体
        data: {
          title: "今天是星期天",
          author: "张三"
        }
      }).then(response => {
        console.log(response);
      })
    }
    // 更新数据
    btns[2].onclick = function () {
      // 发送AJAX请求
      axios({
        // 请求类型
        method: 'PUT',
        // URL
        url: 'http://localhost:3000/posts/3',
        // 设置请求体
        data: {
          title: "今天是星期天",
          author: "李四"
        }
      }).then(response => {
        console.log(response);
      })
    }
    // 删除数据
    btns[3].onclick = function () {
      // 发送AJAX请求
      axios({
        // 请求类型
        method: 'DELETE',
        // URL
        url: 'http://localhost:3000/posts/3',
      }).then(response => {
        console.log(response);
      })
    }
  </script>
```

# axios其他使用：

```javascript
  <script>
    const btns = document.querySelectorAll('button');

    // 发送GET请求
    btns[0].onclick = function () {
      axios.request({
        method: 'GET',
        url: 'http://localhost:3000/comments',
      }).then(response => {
        console.log(response);
      })
    }

    // 发送POST请求
    btns[1].onclick = function () {
      // axios
      axios.post('http://localhost:3000/comments',
        {
          "body": "评论",
          "postId": 2
        }).then(response => {
          console.log(response);
        })
    }
  </script>

```

# axios默认配置：

```javascript
    // 默认配置
    axios.defaults.method = 'GET';//设置默认请求为GET
    axios.defaults.baseURL = 'http://localhost:3000';//设置基础URL
    axios.defaults.params = { id: 100 }
    axios.defaults.timeout = 3000;
    ......
```

# axios创建实例对象：

```javascript
  <script>
    const btns = document.querySelectorAll('button');
    const duanzi = axios.create({
      baseURL: 'https://api.apiopen.top',
      timeout: 2000
    })
    // 这里duanzi与axios对象的功能几近是一样的
    duanzi({
      url: '/getJoke'
    }).then(response => {
      console.log(response);
    })
    console.log(duanzi);

    duanzi.get('/getJoke').then(response => { console.log(response.data); })
  </script>
```

# axios源码分析：
