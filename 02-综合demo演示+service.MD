# Angular实例演示


## 一、Angular表单元素实现在线预约功能

表单 input、checkbox、radio、select、 textarea

test02\src\app\components\form
![avator](/pic/mod.png)

## 二、Angular实现一个完整的toDoList以及类似京东App搜索缓存数据功能

test02\src\app\components\search

http://www.todolist.cn/

![avator](/pic/todolist.png)



## 三、 Angular中的服务以及实现toDoList数据 持久化
演示文件：test02\src\app\components\todolist


### 3.1、Angualr 中的服务

## 为什么需要服务

* 在组件中定义的信息是固定的，假设另外一个组件也需要用到这些信息，这时候就用到服务，实现 共享数据 和 方法
* 组件不应该直接获取或保存数据，它们不应该了解是否在展示假数据。 它们应该聚焦于展示数据，而把数据访问的职责委托给某个服务。
* Service 可以从任何地方获取数据：Web 服务、本地存储（LocalStorage）或一个模拟的数据源

![avator](/pic/service.png)

### 1. 创建服务到指定目录下： 
https://github.com/angular/angular-cli

```javascript
ng g service my-new-service

创建到指定目录下面 
ng g service services/storage

```
![创建服务](/pic/storage.png)


###  2. app.module.ts里面引入创建的服务

import { StorageService } from './service/storage.service';

@NgModule里面的providers依赖注入服务 StorageService
provides:  [StorageService]

![app.module](/pic/app-module.png)

### 3. 使用的页面引入服务，注册服务

import { StorageService } from '../../services/storage.service';

//使用service要通过构造函数传参
constructor(public storage: StorageService) {
}

![do](/pic/do.png)

到这里todolist 组件就可以使用 storage.service 服务里的数据了

## 开始封装服务

（1）封装localStorage：

* 将数据写入localStorage           
 localStorage.setItem
* setItem不能写入数组或对象,所有要对value值进行转义      
JSON.stringify(value)

Storage.Service.ts界面：

主要通过 @Injectable() 装饰器来声明某个类可被注入实例化。


1. 实现功能组件的可注入。

```javascript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class StorageService {

  constructor() { } /*构造函数*/
  //将数据写入localStorage
  set(key:string,value:any){
    localStorage.setItem(key,JSON.stringify(value));
  }
  //从localStorage中读取key的值，转换为JSON对象
  get(key:string){
    // return 'this is a service';
    return JSON.parse(localStorage.getItem(key))

  }
  //从localStorage中删除key的值
  remove(key:string){
    localStorage.removeItem(key);
  }
}

```
上面代码把StorageService声明为可注入的服务， 这样就可以在别的组件中通过依赖注入的方式来使用

然后在 angular的根模块NgModule的providers中声明这个服务。 

ngdemo\src\app\app.module.ts

设置
import { StorageService } from './services/storage.service';
........

providers: [StorageService],  /*配置项目所需要的服务*/



构造函数是为了简单的初始化工作而设计的,比如把构造函数的参数赋值给属性.它的负担不应该过于沉重.所以我们把数据的获取放在了组件的生命周期的钩子函数中去


2. 在另外的对象中注入前面的功能组件

```javascript
 //引入服务
import {StorageService} from '../../services/storage.service';

// 在该类的构造函数中导入StorageService
constructor(public storage:StorageService) { }

// 使用注入组件的函数
getHeroes(): void {
   this.historyList=this.storage.get('searchlist');
}

```

使用

addData(){ 
    // alert(this.username);
    this.list.push(this.username);
    this.storage.set('todolist',this.list);
} 
removerData(key){
    console.log(key); 
    this.list.splice(key,1); 
    this.storage.set('todolist',this.list);
}



