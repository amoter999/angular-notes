# Angular中使用ngrx做状态管理

## 简介
ngrx/store的灵感来源于Redux，是一款集成RxJS的Angular状态管理库，由Angular的布道者Rob Wormald开发。它和Redux的核心思想相同，但使用RxJS实现观察者模式。它遵循Redux核心原则，但专门为Angular而设计。


Angular中的状态管理大部分可以被service接管,那么在一些中大型的项目中,这样做的弊端就会显露出来,其中之一就是状态流混乱,不利于后期维护,后来便借鉴了redux的状态管理模式并配上rxjs流式编程的特点形成了@ngrx/store这么一个作用于Angular的状态管理工具.

* StoreModule: 
  StoreModule是@ngrx/store API中的一个模块，它被用来在应用模块中配置reducer。
* Action: 
  Action是状态的改变。它描述了某个事件的发生，但是没有指定应用的状态如何改变。

* Store: 
  它提供了Store.select()和Store.dispatch()来与reducer协同工作。Store.select()用于选择一个selector，
  Store.dispatch(
    {
      type:'add',
      payload:{name:'111'}
    }
  )
  用于向reducer分发action的类型。



## @NgRx/Store 状态管理的三个原则

首先，@NgRx/Store 同样遵守 Redux 的三个基本原则：

* 单一数据源

这个原则是整个单页应用的状态通过object tree（对象树）的形式存储在store 里面。
这个定义十分抽象其实就是把所有需要共享的数据通过javascript 对象的形式存储下来

```javascript
state =
{
    application:'angular app',
    shoppingList:['apple', 'pear']
}
```
* state is read-only(状态只能是只读形式)


这个 ngrx/store 核心之一就是用户不能直接修改状态内容。 举个例子，如果我们需要保存了登录页面状态，状态信息需要记录登录用户的名字。 当登录名字改变，我们不能直接修改状态保存的用户名字

```javascript
state={'username':'kat'},
//用户重新登录别的账户为tom
state.username = 'tom'  //在ngrx store 这个行为是绝对不允许的

```

* changes are made with pure functions（只能通过调用函数来改变状态）

由于不能直接需改状态，ngrx/store 同时引入了一个叫做reducer（聚合器）的概念。通过reducer 来修改状态。

```javascript
function reducer(state = 'SHOW_ALL', action) {
    switch (action.type) {
      	case 'SET_VISIBILITY_FILTER':
        	return Object.assign({}, state  ,newObj);  
        default:
        	return state  
        }
	}

```

## ngrx/store使用实例

### 1.安装@ngrx/store 
yarn add @ngrx/store


### 2. 创建 state, action, reducer

**state 状态：**
app\store\state.ts
```javascript

//下面是使用接口的情况， 更规范
export interface TaskList {
  id: number;
  text: string;
  complete: boolean;
}

export const TASKSAll: TaskList[] = [
  {id: 1, text: 'Java Article 1', complete: false},
  {id: 2, text: 'Java Article 2', complete: false}
]

export interface AppState {
  count: number;
  todos: TaskList;
  // 如果要管理多个状态,在这个接口中添加即可
}

//这个是不用接口的情况
// export interface AppState {
//     count: number;
//     todos: any;
//     // 如果要管理多个状态,在这个接口中添加即可
//   }

```

**reducer**
app\store\reducer.ts

```javascript

// reducer.ts,一般需要将state,action,reducer进行文件拆分
import { Action } from '@ngrx/store';

export const INCREMENT = 'INCREMENT';
export const DECREMENT = 'DECREMENT';
export const RESET = 'RESET';

const initialState = 0;
// reducer定义了action被派发时state的具体改变方式
export function counterReducer(state: number = initialState, action: Action) {
  switch (action.type) {
    case INCREMENT:
      return state + 1;

    case DECREMENT:
      return state - 1;

    case RESET:
      return 0;

    default:
      return state;
  }
}

```
**actions**

如果需要把action 单独提取出来， 参考 后面的
 5  如果想把action分离出来如何处理？

### 3. 注册store

根模块：
app/app.module.ts

```javascript
import { NgModule } from '@angular/core';
import { StoreModule } from '@ngrx/store';
// StoreModule: StoreModule是@ngrx/storeAPI中的一个模块，
// 它被用来在应用模块中配置reducer。

import {counterReducer} from './store/reducer';

@NgModule({
  imports: [
  	StoreModule.forRoot({ count: counterReducer }), // 注册store
  ],
})
export class AppModule {}


```

### 4. 使用store

在组件或服务中注入store进行使用

以 app\module\article\article.component.ts 组件为例:

```javascript
// 组件级别
import { Component } from '@angular/core';
import { Store, select } from '@ngrx/store';
import { Observable } from 'rxjs';
import { INCREMENT, DECREMENT, RESET} from '../../store/reducer';

interface AppState {
  count: number;
}

@Component({
  selector: 'app-article',
  templateUrl: './article.component.html',
  styleUrls: ['./article.component.css']
})
export class ArticleComponent  {
  count: Observable<number>;

  constructor(private store: Store<AppState>) { // 注入store
    this.count = store.pipe(select('count')); 
    // 从app.module.ts中获取count状态流
  }

  increment() {
    this.store.dispatch({ type: INCREMENT });
  }

  decrement() {
    this.store.dispatch({ type: DECREMENT });
  }

  reset() {
    this.store.dispatch({ type: RESET });
  }
}

```

模板页面：
app\module\article\article.component.html

```javascript
<div class="state-count">

    <button (click)="increment()">增加Increment</button>
    <div>Current Count: {{ count | async }}</div>
    <button (click)="decrement()">减少Decrement</button>

    <button (click)="reset()">Reset Counter</button>
</div>

```


这里使用了 管道符 async, 在子模块里直接使用快报错 ， 如果在子模块要实现 数据的双向绑定也会报错，具体原因参照 课件说明的 问题： The pipe 'async' could not be found？




**如何做到在模板页面中不使用管道 来渲染页面 ？**


修改如下：

```javascript

count: Observable<number>;

constructor(private store: Store<AppState>) { // 注入store
    var stream = store.pipe(select('count')); 
    // 从app.module.ts中获取count状态流
    stream.subscribe((res)=>{
          this.count = res;
      })
  }

```

**为了管理方便， 一般会把 type , state, actions,reducers 分开来管理**

### 5  如果想把action分离出来如何处理？

1. 新建 \app\store\actions.ts 文件

```javascript
import { Injectable } from '@angular/core';
import { INCREMENT, DECREMENT, RESET } from './types';

@Injectable()
export class CounterAction{
    // Add=function(){}
    Add(){
        return { type: INCREMENT }
    }
}

// 就只这样导出是不行的
// export function Add1(){
//     return { type: INCREMENT }
// }

```

2. 在根模块 app.module.ts 注册

```javascript
import {CounterAction} from './store/actions';

... 

providers: [CounterAction],

```

3.  在组件中使用 -- article.component.ts

```javascript
import {CounterAction} from '../../store/actions';

export class ArticleComponent implements OnInit {

  constructor(
    private action: CounterAction  //注入CounterAction
    ) { }

    increment() {
    // this.store.dispatch({ type: INCREMENT }); 
    //把 actions分离出去
    this.store.dispatch(this.action.Add()); 
    
  }
}
```