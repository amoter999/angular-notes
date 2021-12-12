# 课程目标

1. Angular 中的 Dom 操作以及@ViewChild 

2. Angular 执行 css3 动画

3. Angular 中的父子组件的传值

父传子  @input
子传父  viewChild

4. 子组件通过@Output触发父组件的方法

5. 简单配置路由

6. window安装yarn环境变量的简单说明


## 一、 Angular 中的 Dom 操作以及@ViewChild、 Angular 执行 css3 动画


### 1.1 原生js的 dom 操作以及动画

演示组件：app\components\transition
HTML

```javascript

<div class="content">

    <p>内容区域</p>

    <div id="box">
          this is box
    </div>
    <br>
    <div id="box1" *ngIf="flag">
      this is box1  
    </div>

    <button (click)="showAside()">弹出侧边栏</button>
    <button (click)="hideAside()">隐藏侧边栏</button>
  </div>
  
  <aside id="aside">
    这是一个侧边栏
  </aside>

```

组件ts：

```javascript
public flag:boolean=true;
  constructor() { }

  ngOnInit(): void {
      //组件和指令初始化完成   并不是真正的dom加载完成
      let oBox:any=document.getElementById('box');
      console.log(oBox.innerHTML);
      oBox.style.color="red";
      //获取不到dom节点
     /*
      let oBox1:any=document.getElementById('box1');
      console.log(oBox1.innerHTML);
      oBox1.style.color="blue";
     
     */
  }
     //视图加载完成以后触发的方法    dom加载完成  （建议把dom操作放在这个里面）  
    ngAfterViewInit(){
        let oBox1:any=document.getElementById('box1');
        console.log(oBox1.innerHTML);
        oBox1.style.color="blue";
    }

  showAside(){
    //原生js获取dom节点
    var asideDom:any=document.getElementById('aside');
    asideDom.style.transform="translate(0,0)";

 }

hideAside(){
   //原生js获取dom节点
   var asideDom:any=document.getElementById('aside');
   asideDom.style.transform="translate(100%,0)";

}
```

### 1.2 Angular 中的 dom 操作（ViewChild）
ViewChild：属性装饰器
演示文件：\ngDemo\src\app\components\news

1. 现在组件模板文件定义属性 ，通过#
```javascript
<div #myBox>
   我是一个dom节点
</div>
```
2. 现在组件ts通过ViewChild 获取dom

![avator](/pic/viewchild.png)


### 1.3 父组件获取子组件的数据和方法

也就是说 子组件给父组件传数据和方法
**通过ViewChild**
演示例子：
父组件：news
子组件：header


假如子组件header有个run方法 
run(){
    console.log('我是header里面的run方法');
  }

在父组件调用子组件header的run方法

1. 在父组件中调用子组件，并给子组件定义一个名称
```javascript

<app-header #header></app-header>
```

![父组件调用子组件](/pic/父调子组件方法01.png)

2. 在父组件引入ViewChild
import { Component,OnInit ,ViewChild} from '@angular/core';

3. 利用属性装饰器ViewChild 和刚才的子组件关联起来
@ViewChild('header') 
Header:any;

4. 调用子组件的方法
 getChildRun(){
    this.Header.run();
 }

![父组件或者子组件数据和方法](/pic/父调子组件方法.png)


## 二、父组件给子组件传值-@input

演示例子：
父组件：home
子组件：header

父组件不仅可以给子组件传递简单的数据，还可把自己的方法以及整个父组件传给子组件

所以在子组件中可以调用 父组件的方法

1. 父组件调用子组件的时候传入数据
```javascript
 <app-header [title]="title" [homeWork]="homeWork"  [homepage]='this'></app-header>

```
![avator](/pic/父组件给子组件传值01.png)

2. 子组件引入 Input 模块

import { Component, OnInit ,Input } from '@angular/core';

3. 子组件中 @Input 接收父组件传过来的数据

```javascript
export class HeaderComponent implements OnInit {
    @Input()  title:string

    constructor() { }
    ngOnInit() {}
}
```

4. 子组件中使用父组件的数据
这是头部组件-- {{title}}


![avator](/pic/父组件给子组件传值02.png)

5.  子组件中使用父组件的方法
总结：
父传子： @input
子传父：ViewChild

## 三、子组件通过@Output触发父组件的方法

演示例子：
父组件：news
子组件：footer

1. 子组件引入 Output 和 EventEmitter
import { Component, OnInit ,Input,Output,EventEmitter} from '@angular/core';

2. 子组件中实例化 EventEmitter

@Output() 
private outer=new EventEmitter<string>();
/*用 EventEmitter 和 output 装饰器配合使用 <string>指定类型变量*/

3. 子组件通过 EventEmitter 对象 outer 实例广播数据
sendParent(){ 
    this.outer.emit('msg from child') 
 }

![avator](/pic/子组件触发父组件的方法01.png)
 
4.父组件调用子组件的时候，定义接收事件 ,outer 就是子组件的 EventEmitter 对象 outer

文件：components\news\news.component.html
<!-- data就是 子组件给父组件的数据  outer是定义的事件名称-->
<app-footer (outer)="getFooterRun(data)"></app-footer>

![avator](/pic/子组件触发父组件的方法02.png)


5.父组件接收到数据会调用自己的 getFooterRun 方法，这个时候就能拿到子组件的数
文件：components\news\news.component.ts

//接收子组件传递过来的数据 
 getFooterRun(data){
    console.log(data);
  }


## 五、非父子组件通讯

1、公共的服务 
2、Localstorage(推荐) 
3、Cookie



## 总结：


###  vue中 关于$emit的用法

1、父组件可以使用**属性**把数据传给子组件，子组件通过props接受。
2、子组件可以使用 $emit 触发父组件的自定义事件。


vm.$emit( event, arg ) //触发当前实例上的事件

vm.$on( event, fn );//监听event事件后运行 fn； 

###  angular中 关于emit的用法


1、父组件可以使用**属性**把数据传给子组件,子组件通过@input接受。
2、子组件可以使用 Output 和 EventEmitter 触发父组件的自定义事件。

父组件
<!-- data 就是 子组件给父组件的数据-->
<app-footer (event)="getFooterRun(data)"></app-footer>

子组件
```javascript
@Output() 
private event=new EventEmitter<string>();
/*用 EventEmitter 和 output 装饰器配合使用 <string>指定类型变量*/

sendParent(){ 
    // outer 相当于是事件名称
    this.event.emit(data)  
 }

 ```
<button (event)="sendParent()">通过@Output给父组件广播数据</button>





