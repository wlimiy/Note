![Image text](https://github.com/wlimiy/Note/blob/master/vueTodoList/image/img.png)
### 功能开发
1. input输入框的内容回车显示在列表页
2. 列表页的内容可以点击删除按钮删除
3. 统计还有几件事没有做完
    * 使用计算属性
    * 使用filter方法
    * 计算一下当前没有被选中的个数
```
     computed:{
         count(){
             return this.todos.filter(item=>!item.isSelected).length;
         }
     }
```
4. 点击列表，可以修改列表内容
    * 使用双击事件：@dblclick="remember(todo)"
    * 当我点击li时 我可以知道点击的是那一项，如果我点击的todo和当前循环的某一个相等的时候 应该显示输入框-
```
    remember(todo){//当前传递的是todo（当前点击的这一项）
        this.cur = todo;
    }

```
5. 点击单选框，表示已完成，有一个del样式
    动态绑定样式 :class="{del:todo.isSelected}"
```
    <style>
        .del{text-decoration: line-through;color:#cccccc!important;}
    </style>
```
6. 点击面板底部全部任务、已完成、未完成，三个按钮，列表依次显示相应内容

   * 通过hash记录跳转的路径
   * hash即URL中"#"字符后面的部分
   * 通过window.location.hash属性获取和设置hash值
   * window.location.hash值的变化会直接反应到浏览器地址栏（#后面的部分会发生变化），同时，浏览器地址栏hash值的变化也会触发window.location.hash值的变化，从而触发onhashchange事件。
   * hashchange事件触发时，事件对象会有hash改变前的URL（oldURL）和hash改变后的URL（newURL）两个属性：
     ```
     window.addEventListener('hashchange',function(e) { console.log(e.oldURL);  console.log(e.newURL) },false);
     ```
   * 在created初始化数据
```
    created(){ // ajax获取 初始化数据
        // 监控hash值的变化, 如果页面以及有hash了 重新刷新页面也要获取hash值
        this.hash = window.location.hash.slice(2) || 'all';
        window.addEventListener('hashchange',()=>{
            // 当hash值变化 重新操作记录的数据
            this.hash = window.location.hash.slice(2);
        },false);
    },
    <li role="presentation" class="active"><a href="#/all">全部任务</a></li>
    <li role="presentation"><a href="#/finish">已完成</a></li>
    <li role="presentation"><a href="#/unfinish">未完成</a></li>
    computed:{
        filterTodos(){
            if(this.hash === 'all')  return this.todos;
            if(this.hash === 'finish') return this.todos.filter(item=>item.isSelected);
            if(this.hash === 'unfinish') return this.todos.filter(item=>!item.isSelected);
            window.location.hash = '/all';
        }
    }
```
7. 使用localStorage，把列表页内容存到本地

### localStorage：本地存储
* localStorage默认存的是字符串，用JSON.stringify转成对象

```
存
localStorage.setItem('data',JSON.stringify(this.todos))
获取
//如果localStorage里有数据，就用localStorage里的，没有数据就用默认的。
this.todos=JSON.parse(localStorage.getItem('data'))||this.todos;
```