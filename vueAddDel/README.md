### 添加删除人员信息:index.html
![Image text](https://github.com/wlimiy/Note/blob/master/vueAddDel/images/img.png)
1. v-model实现双向数据绑定
2. v-for实现数据循环展示
3. @click='del'点击删除按钮删除相应列表，使用filter方法过滤，返回索引不相同的数组
4. @click='add'点击添加按钮添加内容到相应列表
### vue原生ajax调用json文件:把添加删除人员信息页面的数据用原生ajax调用
1. 使用生命周期钩子函数：created，用来在一个实例被创建之后执行代码：indexAjax.html
```
created:function(){
    let that=this;
    let xhr=new XMLHttpRequest();
    xhr.open("get","./users.json");
    xhr.onreadystatechange=function () {
        if(this.readyState===4&&/^2\d{2}$/.test(this.status)){
            console.log(this.response);
            let initData=JSON.parse(this.responseText);
            that.result=initData;
        }
    };
    xhr.send();
}
```
### 使用axios调用json文件：indexAxios.html
1. 安装axios：这里就简单使用cdn链接：
```
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```
2. 在created函数里使用axios
```
created(){
    axios.get('./user.json')
        .then((response)=>{
            console.log(response);
            let initData=response.data;
            this.users=initData;
        })
        .catch(function(error){
            console.log(error);
        });
}
```
### 封装Promise模式的ajax：indexProAjax.html
### 商品列表:vueTotal.html
![Image text](https://github.com/wlimiy/Note/blob/master/vueAddDel/images/vuetotal.png)
1. 总计方法total(){}
2. 避免闪烁
```
<style type="text/css">
    v-cloak{
        display: none;
    }
</style>
<div id="app" class="container" v-cloak>
```
### 京东购物车案例
1.