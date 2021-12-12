# Angular 中的路由

## 一、 Angular 创建一个默认带路由的项目

1. 命令创建项目

ng new ng-demo --skip-install

![avactor](/pic/01.png)

2. 创建需要的组件

ng g component components/home
ng g component components/news
ng g component components/newscontent

3. 找到 app-routing.module.ts 配置路由

引入组件

import { HomeComponent } from './components/home/home.component';
import { NewsComponent } from './components/news/news.component';
import { ProductComponent } from './components/product/product.component';

配置路由

const routes: Routes = [
{path: 'home', component: HomeComponent},
{path: 'news', component: NewsComponent},
{path:'product', component:ProductComponent },
{path: '*', redirectTo: '/home', pathMatch: 'full' }
];

4. 找到 app.component.html 根组件模板，配置 router-outlet 显示动态加载的路由

```javascript
<h1>
    <a routerLink="/home">首页</a>
    <a routerLink="/news">新闻</a>
</h1>
<router-outlet></router-outlet>
```

## 二、Angular routerLink 跳转页面默认路由

```javascript

<a routerLink="/home">首页</a>
<a routerLink="/news">新闻</a>

```

```javascript

//匹配不到路由的时候加载的组件 或者跳转的路由
{
    path: '**', /*任意的路由*/
    // component:HomeComponent
    redirectTo:'home'
}

```

## 三、Angular routerLinkActive 设置 routerLink 默认选中路由

```javascript
<h1>
  <a routerLink="/home" routerLinkActive="active">
    首页
  </a>
  <a routerLink="/news" routerLinkActive="active">
    新闻
  </a>
</h1>
```

```javascript
<h1>
    <a [routerLink]="[ '/home' ]" routerLinkActive="active">首页</a>
    <a [routerLink]="[ '/news' ]" routerLinkActive="active">新闻</a>
</h1>
```

## 四、动态路由

### 4.1.问号传参

跳转方式，页面跳转或js跳转
问号传参的url地址显示为 …/list-item?id=1

<!-- 页面跳转 -->
queryParams属性是固定的

<a [routerLink]="['/list-item']" [queryParams]="{id:item.id}">
<span>{{ item.name }}</span>
</a>

//js跳转
//router为ActivatedRoute的实例

```javascript

import { Router } from '@angular/router';
.
constructor(private router: Router) {}
.
this.router.navigate(['/newscontent'],{
  queryParams:{
    name:'laney',
    id:id
  },
  skipLocationChange: true 
  //可以不写，默认为false,设为true时路由跳转浏览器中的url会保持不变，传入的参数依然有效
});
```

获取参数方式

```javascript

import { ActivatedRoute } from '@angular/router';

constructor(public route:ActivatedRoute) { }
ngOnInit() { 
    this.route.queryParams.subscribe((data)=>{
      console.log(data);
 })
}

```

### 4.2 路径传参
路径传参的url地址显示为 …/list-item/1

<!-- 页面跳转 -->
<a [routerLink]="['/list-item', item.id]">
  <span>{{ item.name }}</span>
</a>

//js跳转
//router为ActivatedRoute的实例

this.router.navigate(['/list-item', item.id]);

路径配置：
{path: 'list-item/:id', component: ListItemComponent}

获取参数方式
```javascript
this.route.params.subscribe(
  param => {
      this.id= param['id'];
  }
)
```

## 五、父子路由

1. 创建组件引入组件

import { WelcomeComponent } from './components/home/welcome/welcome.component';
import { SettingComponent } from './components/home/setting/setting.component';

2. 配置路由

```javascript
{
    path:'home',
    component:HomeComponent,
    children:[{
      path:'welcome',
      component:WelcomeComponent
    },{
      path:'setting',
      component:SettingComponent
    },
    {path: '**', redirectTo: 'welcome'}
  ]
},

```

3. 父组件中定义router-outlet

<router-outlet></router-outlet>
