```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>发请求</title>
</head>
<body>
<div id="app">
    <input type="button" value="get请求" @click="getInfo">
    <input type="button" value="post请求" @click="postInfo">
    <input type="button" value="jsonp请求" @click="jsonpInfo">
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script src="https://cdn.jsdelivr.net/npm/vue-resource@1.5.1"></script>
<script>
    var vm = new Vue({
        el: '#app',
        data: {},
        methods: {
            getInfo() {//发起get请求，通过.then来设置成功的事件
                this.$http.get('https://www.yiqigoumall.com/index/items/is_best').then(function (result) {
                        console.log(result)
                        document.write('成功请求')
                    }
                )
            },
            postInfo() {//发起post请求   手动发起的post请求默认没有表单格式，有的服务器无法处理
                // 通过post方法的第三个参数{emulateJSON：true}，设置提交的表单为普通表单数据格式
                this.$http.post('http://vue.studyit.io/api/post', {}, {emulateJSON: true}).then(result => {
                    console.log(result)
                    document.write('成功请求')
                }).err(
                    document.write('请求失败')
                )
            },
            jsonpInfo() {
                this.$http.jsonp('http://vue.studyit.io/api/jsonp').then(result => {
                    console.log(result)
                }).err(
                    document.write('请求失败')
                )
            }
        },
    })
</script>
</body>
</html>
```