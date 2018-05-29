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
```
created(){
    ajax({
        url:'./user.json'
    }).then((res)=>{
        console.log(res);
        this.users=res;
    },(err)=>{
        console.log(err)
    })
}
```
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
### vue选项卡
![Image text](https://github.com/wlimiy/Note/blob/master/vueAddDel/images/vueTab.png)
  - 利用动态绑定class，点击切换选项卡
```
<div id="app">
    <div class="oTab">
        <ul>
            <li @click="clicked='one'" :class="{active:clicked=='one'}">首页</li>
            <li @click="clicked='two'" :class="{active:clicked=='two'}">娱乐</li>
            <li @click="clicked='three'" :class="{active:clicked=='three'}">新闻</li>
        </ul>
        <div :class="{active:clicked=='one'}">首页内容</div>
        <div :class="{active:clicked=='two'}">娱乐内容</div>
        <div :class="{active:clicked=='three'}">新闻内容</div>
    </div>
</div>

new Vue({
    el:"#app",
    data:{
        clicked:'one'
    }
})
```
### 京东购物车案例：vueJDCart.html
1. 使用axios调用数据
 - created：在数据被初始化后会调用，vue提供专门获取ajax方法
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
2. 全选单选功能
 - 点击全选按钮，其余复选框都选中：利用forEach方法
 - 点击单个复选框，如果复选框都选中，全选复选框也要选中:利用every方法
 - 事件选用change，利用双向数据绑定，实时得到复选框的状态
 ```
<div id="app">
    全选 <input type="checkbox" @change="checkAll" v-model="isAll"><br>
    <input v-for="item in lists" type="checkbox" @change="select" v-model="item.isCheck">
</div>

let vm=new Vue({
    el: '#app',
    data: {
        lists: [
            {isCheck: false},
            {isCheck: false},
            {isCheck: false},
            {isCheck: false},
            {isCheck: false}
        ],
        isAll: false
    },
    methods: {
        checkAll () {
            this.lists.forEach((item)=>{
                item.isCheck=this.isAll;
            })
        },
        select(){
            this.isAll=this.lists.every(item=>item.isCheck)
        }
    }
});

 - 也可以使用计算属性
 computed:{
        checkAll:{
            get(){
                return this.products.every(item=>item.isSelected)
            },
            set(val){
                this.products.forEach(item=>item.isSelected=val)
            }
        }
     }
 ```
3. 通过计算属性计算总计，通过函数定义方法也可以算出总计，但是只要改变一次数据，函数方法都会执行一次，这会影响性能，计算属性computed是通过一个属性，计算出来一个新的属性 当这个属性变化时，新的属性也会跟着变化
 - 默认是get方法
 - 还有set方法
 ```
 <div id="app">
     <h3>计算商品总价</h3>
     商品名称：<input type="text" v-model="product"><br>
     商品单价：<input type="number" v-model="price" min="0"><br>
     商品数量：<input type="number" v-model="count" min="0"><br>
     总价：<input type="number" v-model="total">
 </div>
 let vm=new Vue({
     el:'#app',
     data:{
         product:'vue',
         price:100,
         count:1
     },
     computed:{
         total:{
             get(){
                 return this.total=this.price*this.count;
             },
             set(val){
                 this.count=val/this.price;
             }
         }
     }
 })
 ```
 4. 过滤器(filters)：自定义过滤器，可被用于一些常见的文本格式化。
 - 过滤器可以用在两个地方：双花括号插值和 v-bind 表达式
 ```
 <!-- 在双花括号中 -->
 {{ message | capitalize }}

 <!-- 在 `v-bind` 中 -->
 <div v-bind:id="rawId | formatId"></div>
 ```
 - 过滤器应该被添加在 JavaScript 表达式的尾部，由“管道”符号指示：
 ```
     <tr><td colspan="6">总价格：{{sum | toFixed(2)}}</td></tr>
     filters:{
         toFixed(input,param1){
             return '￥'+input.toFixed(param1);
         }
     }
 ```