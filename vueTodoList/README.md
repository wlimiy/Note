![Image text](https://github.com/wlimiy/Note/tree/master/vueTodoList/image/img.png)
### 功能开发
1. input输入框的内容回车显示在列表页
2. 列表页的内容可以点击删除按钮删除
3. 统计还有几件事没有做完
4. 点击列表，可以修改列表内容
5. 点击单选框，表示已完成
6. 点击面板底部全部任务、已完成、未完成，三个按钮，列表依次显示相应内容
7. 使用localStorage，把列表页内容存到本地
### 实现单页开发的方式
1. 通过hash记录跳转的路径（可以产生历史管理）
2. 浏览器自带的历史管理的方法history
* history.pushState()可能会导致404错误
* 开发时使用hash方式，上线的活会使用history方式
### localStorage：本地存储
* localStorage默认存的是字符串，用JSON.stringify转成对象

```
存
localStorage.setItem('data',JSON.stringify(this.todos))
获取
//如果localStorage里有数据，就用localStorage里的，没有数据就用默认的。
this.todos=JSON.parse(localStorage.getItem('data'))||this.todos;
```