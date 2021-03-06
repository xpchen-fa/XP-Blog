---
title: 踩坑
date: 2018-08-20 14:41:30
updated: 2018-12-03 14:41:30
tags: javascript,vue
description: 踩坑
---
#2018-12-03
> 使用element ui框架进行项目开发,表格的列是根据后台数据动态生成的，但是发现在增加列的情况下表格正常，但是一旦表格列减少时就会出问题表格完全空白

```
//解决在node_modules/element-ui/lib/elementui.common.js 
removeColumn: function removeColumn(states, column) {
 var _columns = states._columns;
 if (_columns) {
  _columns.splice(_columns.indexOf(column), 1);
 }
 //这个函数中_columns是一个数组，column是一个对象，当indexOf匹配不到的时候，返回-1，但是splice函数会执行删除操作，所以必须加入判断。
 //修改成以下
 removeColumn: function removeColumn(states, column) {
 var _columns = states._columns;
 if (_columns.indexOf(column) != -1) {
  _columns.splice(_columns.indexOf(column), 1);
 }
```
#2018-12-01
> flex布局中 justify-content: evenly;存在兼容性问题；在安卓中不适用
```
    display: flex;
    justify-content: evenly;
```
#2018-09-19 02
> beforeRouteUpdate(2.2 新增)

> 在当前路由改变，但是该组件被复用时调用
举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
可以访问组件实例 this

*************
#2018-09-19 01
> <keep-alive>是Vue的内置组件，能在组件切换过程中将状态保留在内存中，防止重复渲染DOM
> keep-alive导致的页面不刷新

> keep-alive生命周期钩子函数：activated、deactivated

> 使用<keep-alive>会将数据保留在内存中，如果要在每次进入页面的时候获取最新的数据，需要在activated阶段获取数据，承担原来created钩子中获取数据的任务。
*************
#2018-09-11
> 前端阿里直传图片，当服务器上的地址是https时，是不能请求http;配置的sdk要修改https
```
//html
<script src="https://gosspublic.alicdn.com/aliyun-oss-sdk-4.4.4.min.js"></script>
//alioss配置
const BUCKET = "thenewwork";
const REGION = "oss-cn-shanghai";
const option = {
    accessKeyId: accessKeyId,  //后端给
    accessKeySecret: accessKeySecret, //后端给
    stsToken: securityToken, //后端给
    secure: true,       //https时要加这句
    bucket: BUCKET,
    region: REGION
};
this.client = new OSS.Wrapper(option);

```
*************
# 2018-08-20

> 如下写法：图片当作背景平铺，当url里面的图片路径有括号时，图片显示不出来
```
//HTML
<div class="preview-card" 
    :style="'background-image: url('+ basicInfo.cardOne +')'"
></div>

//CSS
    .preview-card{
        width: 120px;
        height: 182px;
        float: left;
        margin-bottom: 10px;
        margin-right: 10px;
        background-size: cover;
        background-position: center;
        border-radius: 4px;
        cursor: pointer;
    }
```
> 修改方面
```
<div class="preview-card" 
    :style="`background-image: url('${basicInfo.activityUrl}')`"
></div>
```
