
# Angular入门

## 一、Angular介绍

Angular是谷歌开发的一款开源的web前端框架，诞生于2009年，由Misko Hevery 等人创建，后为Google所收购。是一款优秀的前端JS框架，已经被用于Google的多款产品当中。
根据项目数统计angular（1.x 、2.x 、4.x、5.x、6.x、7.x 、8.x、9.x）是现在网上使用量最大的框架。

Angular基于TypeScript和react、vue相比 Angular更适合中大型企业级项目。

关于Angular版本，Angular官方已经统一命名Angular 1.x统称为Angular JS；Angular 2.x及以上统称Angular；

目前2019年12月25日angular最新版本angular9.x。根据官方介绍，Angular每过几个月就会更新一个版本。Angular2.x以后所有的Angular版本用法都是一样的，此教程同样适用于Angular7.x 、Angular8.x、Angular9.x 以及未来的其它版本....。

**学习Angular必备基础**
必备基础：html  、css 、js、es6、ts

## 二、Angular环境搭建

1、安装前准备工作：

1.1、安装nodejs
安装angular的计算机上面必须安装最新的nodejs--注意安装nodejs稳定版本

1.2、选择一个 命令工具， npm,  cnpm, yarn ,任选其一

设置淘宝源镜像 ，如果你用npm 

npm config set registry https://registry.npm.taobao.org


如果你用cnpm ， 安装cnpm
npm可能安装失败建议先用npm安装一下cnpm用淘宝镜像安装
https://npm.taobao.org/
npm install -g cnpm --registry=https://registry.npm.taobao.org

或者 安装yarn ,注意，只要选 一个命令工具就行

**yarn**
Yarn自称是比npm快十倍的包管理工具，并且还有一些很赞的特性，应该是2017年前端的一个惊喜，根据我的亲身体验，真的是快到飞起，所以强烈建议各位小伙伴也用起来吧！使用方式很简单，用你的npm 安装它

npm install yarn -g

然后切换为淘宝源你才能感受到速度：

yarn config set registry https://registry.npm.taobao.org --global
yarn config set disturl https://npm.taobao.org/dist --global

好了，真的很简单，它的命令与npm几乎一样：

初始化：yarn init
安装一个包：yarn add 包名
更新一个包：yarn upgrade 包名
删除一个包：yarn remove 包名
安装所有包：yarn或者yarn install

设置成功后，会有惊喜。

## 三、安装Angular CLI

### 3.1 背景介绍：
​     CLI是Command Line Interface的简写，是一种命令行接口，实现自动化开发流程，比如：ionic cli、vue cli等；它可以创建项目、添加文件以及执行一大堆开发任务，比如测试、打包和发布。

### 3.2 安装Angular CLI

1. 全局安装typescript（可选）
$ npm install -g typescript 
// 新建项目的时候会自动安装typescript(非全局)所以这里也可以不用安装。
2. 全局安装Angular CLI

yarn global add @angular/cli  或者 npm install @angular/cli -g

* 如果要卸载，执行下面命令：
yarn global remove @angular/cli

经过不算漫长的等待，你的Angular CLI就装好了。确认一下：

* 检验安装是否成功
ng version 或者 ng v


## 四、新建Angular项目 

### 4.1. 新建Angular项目：

ng new my-app

如果要跳过npm i安装
ng new my-app --skip-install

趁着它在下载，来看一下运行ng new之后Angular cli已经帮我们干了什么：

那么，这时候Angular cli帮你干了以下这么多事情：

* 创建 my-app 目录
* 应用程序相关的源文件和目录将会被创建
* 应用程序的所有依赖 (package.json中配置的依赖项) 将会被自动安装
* 自动配置项目中的 TypeScript 开发环境
* 自动配置 Karma 单元测试环境
* 自动配置 Protractor (end-to-end) 测试环境
* 创建 environment 相关的文件并初始化为默认的设置

### 4.2. 启动项目
安装完成之后就可以启动项目了：

cd my-app   //进入my-app
npm start  或者 ng serve     //启服务

ng serve命令会启动开发服务器，监听文件变化，并在修改这些文件时重新构建此应用。
使用--open（或-o）参数可以自动打开浏览器并访问http://localhost:4200/。

ng serve命令提供了很多参数，可以适当参考。
以下参数仅供参考：

```javascript
--dry-run: boolean, 默认为 false, 若设置 dry-run 则不会创建任何文件
--verbose: boolean, 默认为 false
--link-cli: boolean, 默认为 false, 自动链接到 @angular/cli 包
--skip-install: boolean, 默认为 false, 表示跳过 npm install
--skip-git: boolean, 默认为 false, 表示该目录不初始化为 git 仓库
--skip-tests: boolean, 默认为 false, 表示不创建 tests 相关文件
--skip-commit: boolean, 默认为 false, 表示不进行初始提交
--directory: string, 用于设置创建的目录名，默认与应用程序的同名
--source-dir: string, 默认为 'src', 用于设置源文件目录的名称
--style: string, 默认为 'css', 用于设置选用的样式语法 ('css', 'less' or 'scss')
--prefix: string, 默认为 'app', 用于设置创建新组件时，组件选择器使用的前缀
--mobile: boolean, 默认为 false,表示是否生成 Progressive Web App 应用程序
--routing: boolean, 默认为 false, 表示新增带有路由信息的模块，并添加到根模块中
--inline-style: boolean, 默认为 false, 表示当创建新的应用程序时，使用内联样式
--inline-template: boolean, 默认为 false, 表示当创建新的应用程序时，使用内联模板

```

其他文件：
```javascript

  .editorconfig： 给你的编辑器看的一个简单配置文件
  .gitignore： git 排除文件
  angular.json： angular cli 的配置文件
  package.json：npm 配置文件，项目使用到的第三方依赖包
  protractor.conf.js：运行 ng e2e 的时候会用到
  README.md：项目的基础文档
  tsconfig.json：TypeScript 编译器的配置
  tslint.json：运行 ng lint 时会用到
```

## 五、Angular CLI简单使用


### 5.1. 新建组件
$ ng generate component news
installing component
  create src/app/great-angular/news.component.css
  create src/app/great-angular/news.component.html
  create src/app/great-angular/news.component.spec.ts
  create src/app/great-angular/news.component.ts
  update src/app/app.module.ts

  如你所见，Angular cli帮我们干了如下事情：

  src/app/news 目录被创建
news目录下会生成以下四个文件：
CSS 样式文件，用于设置组件的样式
HTML 模板文件，用于设置组件的模板
TypeScript 文件，里面包含一个 组件类和组件的元信息
Spec 文件，包含组件相关的测试用例
news 组件会被自动地添加到 app.module.ts  @NgModule 装饰器的 declarations 属性中。

### 5.2. 其他命令
Angualr CLI提供了许多常用命令供我们选择：
ng generate class my-new-class              // 新建类，  新建一个名为my-new-class的类 (class)
ng generate component my-new-component      // 新建组件
ng generate directive my-new-directive      // 新建指令
ng generate enum my-new-enum                // 新建枚举
ng generate module my-new-module            // 新建模块
ng generate pipe my-new-pipe                // 新建管道
ng generate service my-new-service          // 新建服务

当然选择。。简写：

ng g cl my-new-class        // 新建 class
ng g c my-new-component     // 新建组件
ng g d my-new-directive     // 新建指令
ng g e my-new-enum          // 新建枚举
ng g m my-new-module        // 新建模块
ng g p my-new-pipe          // 新建管道
ng g s my-new-service       // 新建服务

### 5.3. 单元测试
Angular默认帮我们集成了``karma`测试框架，我们只需要：
ng test

### 5.4. 端到端测试
ng e2e

### 5.5. 构建应用程序
ng build

其中过程应该是这样的：
Angular CLI 从 .angular-cli.json 文件中加载配置信息
Angular CLI 运行 Webpack 打包项目相关的 JavaScript、 CSS 等文件
打包后的资源，将被输出到配置文件中 outDir 所指定的目录，默认是输出到 dist 目录。

**Angular开发工具介绍**

Visual Studio Code
![插件](/pic/plugin.png)

## 六、Angular目录结构分析、app.module.ts详解、以及Angular中创建组件、组件详解、 绑定数据

### 6.1 目录结构分析
文件	说明
```javascript
|--E2e	应用的端对端(e2e)测试，用 Jasmine 写成并用 protractor 端对端测试运行器测试。
|--Node_modules	依赖包
|--Src	
   |--App	Angular应用文件
      |--App.module.ts	
      |---App.component.ts	
   |--assets	资源文件
   |--environments	环境配置：开发、部署
   |--index.html	应用的宿主页面。 它以特定的顺序加载一些基本脚本。 然后它启动应用，将根AppComponent放置到自定义<my-app>标签里。
   |--main.ts	项目的入口文件
   |--polyfills.ts	处理浏览器兼容问题
|--angular.json	Cli配置文件
|--.editorconfig	统一代码风格工具配置，不支持的需要安装插件
|--.gitignore	Git配置文件
|--karma.conf.js	在测试指南中提到的 karma 测试运行器的配置。
|--package.json	项目指定npm依赖包
|--tsconfig.app.json	Typescript编译配置
|--tsconfig.spec.json	Typescript测试编译配置
|--tsconfig.json	Typescript编译配置
|--tslint.json	Typescript语法检查器

```
详情参考：https://www.angular.cn/guide/file-structure


### 6.2 app.module.ts、组件分析
#### 6.2.1 app.module.ts

定义 AppModule，这个根模块会告诉 Angular 如何组装该应用。 目前，它只声明了 AppComponent。 稍后它还会声明更多组件。
![avactor](/pic/app-module.png)

#### 6.2.2 自定义组件

https://cli.angular.io/

创建组件：

ng g component components/header
组件内容详解：
![avactor](/pic/module-de.png)

### 6.3 app.component.ts组件分析

Angular应用中，模板指的的是@Component装饰器的template或templateUrl指向的HTML页面
例如：

```javascript
import { Component } from '@angular/core';
interface Course {
  id:number,
  description:string
}
@Component({
  selector: 'app-root',
  // templateUrl: './app.component.html',
  template:`
    <div class="course">
        <span class="description">{{courseObj.description}}</span>
    </div>
  `,
  styleUrls: ['./app.component.css']
})

export class AppComponent{
  title = 'ng-module-routes';
    id:number = 1;
    description:string = 'sss';
   
   public courseObj: Course = {
      id: 1,
      description: "Angular For Beginners"
  };
}

```

很明显Angular不是简单地用一个字符串来处理模板。 那么这是如何工作的？

Angular不会生成HTML字符串，它直接生成DOM数据结构

实际上，Angular把组件类中的数据模型应用于一个函数（DOM component renderer）。 该函数的输出是对应于此HTML模板的DOM数据结构。

一旦数据状态发生改变，Angular数据检测器检测到，将重新调用
该DOM component renderer。

mvvm

Mvvm定义MVVM是Model-View-ViewModel的简写。即模型-视图-视图模型。

- 【模型】指的是后端传递的数据。
- 【视图】指的是所看到的页面。
- 【视图模型】mvvm模式的核心，它是连接view和model的桥梁。

它有两个方向：

- 一是将【模型】转化成【视图】，即将后端传递的数据转化成所看到的页面。实现的方式是：数据绑定。
- 二是将【视图】转化成【模型】，即将所看到的页面转化成后端的数据。

实现的方式是：DOM 事件监听。这两个方向都实现的，我们称之为数据的双向绑定。
### 1.2 总结

在MVVM的框架下视图和模型是不能直接通信的。它们通过ViewModel来通信，ViewModel通常要实现一个observer观察者，当数据发生变化，ViewModel能够监听到数据的这种变化，然后通知到对应的视图做自动更新，而当用户操作视图，ViewModel也能监听到视图的变化，然后通知数据做改动，这实际上就实现了数据的双向绑定。

并且MVVM中的View 和 ViewModel可以互相通信。MVVM流程图如下：
![MVVM流程图](./pic/img-mv.png)

## 七、 angular 组件 以及组件里面的模板
ngdemo1\src\app\components\home


### 7.1 Angular 绑定数据

#### 7.1.1. 数据文本绑定 
```javascript
Angular 中使用{{}}绑定业务逻辑里面定义的数据
 {{}}

 <div class="title"> {{title}}</div>
 {{userinfo.username}} {{message}} {{student}}
```

#### 7.1.2. angualr模板里面绑定属性
```javascript
<div [title]="student">
    张三
</div>
```
#### 7.1.3. angualr模板里面绑定Html
```javascript
<span [innerHTML]='content' class="red"></span>
```
#### 7.1.4. angualr模板里面允许做简单的运算

 1+2={{1+2}}

### 7.2.数据循环 *ngFor

#### 7.2.1 *ngFor 普通循环
```javascript
 <ul>
    <li *ngFor="let item of list">{{item}}</li>
 </ul>
```

#### 7.2.2 循环的时候设置 key
```javascript
 <ul>
    <li *ngFor="let item of list;let key=index;">
        {{key}}---{{item.title}}
    </li>
 </ul>
```
### 7.3 条件判断语句 *ngIf
```javascript
<div *ngIf="flag">
    <img src="assets/images/02.png" />
</div>
<div *ngIf="!flag">
    <img src="assets/images/01.png" />
</div>

<ul>
<li *ngFor="let item of list;let key=index;">
    <span  *ngIf="key==1" class="red">{{key}}---{{item.title}}</span> 
    <span  *ngIf="key!=1">{{key}}---{{item.title}}</span> 
</li>
</ul>
```
### 7.4 条件判断语句 *ngSwitch
```javascript
<span [ngSwitch]="orderStatus">
      <p *ngSwitchCase="1">
          表示已经支付
      </p>
      <p *ngSwitchCase="2">
          支付并且确认订单
      </p>
      <p *ngSwitchCase="3">
          表示已经发货
      </p>
      <p *ngSwitchCase="4">
          表示已经收货
      </p>
      <p *ngSwitchDefault>
        无效订单
      </p>
    </span>
```
### 7.5 属性[ngClass]
```javascript
  <div class="red">
    ngClass演示 （尽量不要用dom来改变class）
</div>
<div [ngClass]="{'blue':true,'red':false}">
    ngClass演示
</div>
<div [ngClass]="{'orange':flag,'red':!flag}">
    ngClass演示
</div>
<strong>循环数组，让数组的第一个元素的样式为red ,第二个为orange,第三个为blue</strong>
<ul>
    <li *ngFor="let item of list;let key=index;" [ngClass]="{'red':key==0,'orange':key==1,'blue':key==2}">
        {{key}}---{{item.title}}
    </li>
</ul>
```
### 7.6 属性[ngStyle]
```javascript
<p style="color:red">我是一个p标签</p>
<p [ngStyle]="{'color':'blue'}">我是一个p标签</p>
<p [ngStyle]="{'color': attr}">我是一个p标签  </p>
```
### 7.7 管道
```javascript
{{today | date:'yyyy-MM-dd HH:mm ss'}}
```

#### 7.8 执行事件(click)
home.component.html
```javascript
<strong>{{title}}</strong>
<button (click)="run()">执行事件</button>  
<button (click)="setData()">执行方法改变属性里面的数据</button>
<button (click)="runEvent($event)">执行方法获取事件对象</button>

```
home.component.ts
```javascript
  run(){
    console.log('这是一个自定义方法')
    console.log(this.title);
  }
  setData(){
    this.title='我是一个改变后的title';
  }
  // $event
  runEvent(event){
    //ionic必须这样写
    let dom:any=event.target;
    dom.style.color="red";
  }
```

#### 7.9 表单事件 事件对象
home.component.ts
```javascript
keyDown
<input type="text" (keydown)="keyDown($event)" />
<br>
keyUp:
<input type="text" (keyup)="keyUp($event)" />
```
home.component.ts
```javascript
  keyDown(e){
    if(e.keyCode==13){
        console.log('按了一下回车')
    }else{
      //e.target 获取dom对象
      console.log(e.target.value);
    }
  }
  keyUp(e){
    if(e.keyCode==13){
        console.log(e.target.value);
        console.log('按了一下回车');
    }  
  }
```
#### 7.10 双向数据绑定--MVVM 只是针对表单

**<input [(ngModel)]="inputValue">**

1. 在app.module.ts导入FormsModule
2. 并在imports导入
```javascript

 import { FormsModule } from '@angular/forms'; 
 ....
 imports: [  /*配置当前模块运行依赖的其他模块*/
    FormsModule
  ],

```

使用:
<input type="text" [(ngModel)]='keywords' />
{{keywords}}
<button (click)="changeKeywords()">改变keywords的值</button>



## Angular 配置文件常见配置注解

angular.json, 这个文件是整个项目的概要，包含了 不同的环境，测试、代理、第三方资源 和 众多内置工具。

angular.json
```javascript
{
  "$schema": "./node_modules/@angular/cli/lib/config/schema.json", //angular-cli.json规则文件
  "version": 1, // 指明了Angular 工作空间 概要的版本。
  "newProjectRoot": "projects",//定义了由CLI创建的新的内部应用和库放置的位置。默认值为`projects`
  "projects": {  //包含了工作空间中所有项目的配置信息。
    "angularTest": {  //项目配置详情(项目名称)
      "root": "", //指定了项目文件的根文件夹，可能为空，但是它指定了一个特定的文件夹。
      "sourceRoot": "src",//指定了项目源文件位置
      "projectType": "application",//表明了 项目的状态 是 `appliaction`还是`library`。
      "prefix": "app",//当CLI创建 `component`或者`directive`时，使用该属性来区别他们。组件selector默认前缀
      "schematics": {},
      "architect": {//自定义自动化命令
        "build": { //build模块配置
          "builder": "@angular-devkit/build-angular:browser",//build执行的自动化程序
          "options": {
            "outputPath": "dist/angularTest",//编译后的输出目录，默认为dist
            "index": "src/index.html", //指定首页文件，默认值为"index.html"
            "main": "src/main.ts", //指定应用的入门文件
            "polyfills": "src/polyfills.ts",// 指定polyfill文件
            "tsConfig": "src/tsconfig.app.json",//指定tsconfig文件
            "assets": [ //记录资源文件夹，构建时复制到`outDir`指定的目录
              "src/favicon.ico",//网站ico图标
              "src/assets"
            ],
            "styles": [//引入全局样式，构建时会打包进来，常用于第三方库引用样式
              "src/styles.css"
            ],
            "scripts": [ ]// 引入全局脚本，构建时会打包进来，常用语第三方库引入的脚本
          },
          "configurations": {//代表这个命令的多种调用模式 
            "production": {//打包命令-–prod()的配置
              "fileReplacements": [
                {
                  "replace": "src/environments/environment.ts",
                  "with": "src/environments/environment.prod.ts"
                }
              ],
              "optimization": true,
              "outputHashing": "all",
              "sourceMap": false,
              "extractCss": true,
              "namedChunks": false,
              "aot": true,
              "extractLicenses": true,
              "vendorChunk": false,
              "buildOptimizer": true
            }
          }
        },
        "serve": {//serve模块配置
          "builder": "@angular-devkit/build-angular:dev-server",//serve执行的自动化程序
          "options": {
            "browserTarget": "angularTest:build"
          },
          "configurations": {
            "production": {
              "browserTarget": "angularTest:build:production"
            }
          }
        },
        "extract-i18n": {
          "builder": "@angular-devkit/build-angular:extract-i18n",
          "options": {
            "browserTarget": "angularTest:build"
          }
        },
        "test": {
          "builder": "@angular-devkit/build-angular:karma",
          "options": {
            "main": "src/test.ts",
            "polyfills": "src/polyfills.ts",
            "tsConfig": "src/tsconfig.spec.json",
            "karmaConfig": "src/karma.conf.js",
            "styles": [
              "src/styles.css"
            ],
            "scripts": [],
            "assets": [
              "src/favicon.ico",
              "src/assets"
            ]
          }
        },
        "lint": {
          "builder": "@angular-devkit/build-angular:tslint",
          "options": {
            "tsConfig": [
              "src/tsconfig.app.json",
              "src/tsconfig.spec.json"
            ],
            "exclude": [
              "**/node_modules/**"
            ]
          }
        }
      }
    },
    "angularTest-e2e": { //项目测试详细配置
      "root": "e2e/",
      "projectType": "application",
      "architect": {
        "e2e": {
          "builder": "@angular-devkit/build-angular:protractor",
          "options": {
            "protractorConfig": "e2e/protractor.conf.js",
            "devServerTarget": "angularTest:serve"
          },
          "configurations": {
            "production": {
              "devServerTarget": "angularTest:serve:production"
            }
          }
        },
        "lint": {
          "builder": "@angular-devkit/build-angular:tslint",
          "options": {
            "tsConfig": "e2e/tsconfig.e2e.json",
            "exclude": [
              "**/node_modules/**"
            ]
          }
        }
      }
    }
  },
  "defaultProject": "angularTest"//当使用CLI命令时，`defaultProject`代表显示的名字。
}

```


















