### 添加删除人员信息
![Image text](https://github.com/wlimiy/Note/blob/master/vueAddDel/images/img.png)
1. v-model实现双向数据绑定
2. v-for实现数据循环展示
3. @click='del'点击删除按钮删除相应列表，使用filter方法过滤，返回索引不相同的数组
4. @click='add'点击添加按钮添加内容到相应列表
### 商品列表
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