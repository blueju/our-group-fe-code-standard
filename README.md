# our-group-fe-code-standard

> 我们团队的 frontend 代码规范



# TODO

* [x] 事件方法，匿名函数？手动绑定this？函数表达式？
* [x] 注释使用 `/** xxx */`
* [ ] 属性接收字符串的，不需要使用{}包裹
* [x] service里的方法以 api 开头
* [ ] 如果使用 class 组件，还要不要构造函数
* [ ] antd table column 写在 render 里



# 前言

不断完善ing...

因为以下错误（可能是）来自日常项目各组员的代码 😂😂😂

<br />

情况介绍，

团队使用的是 React 技术栈，使用的前端应用框架是 Umi，使用的前端 UI 组件库是 Ant Design，主要做基于微前端的后管基座平台、后管子应用及周边。

<br />

代码格式化这块，

使用的是 Prettier，使用的配置统一是：

> 参考：
>
> https://github.com/AlloyTeam/eslint-config-alloy/blob/master/README.zh-CN.md#如何结合-prettier-使用

<br />

代码检查这块，

使用的是 Alloy Team 的 eslint-config-alloy

> 参考：
>
> https://github.com/AlloyTeam/eslint-config-alloy

<br />

个人认为，

应该最大化地利用工具提高效率，而不是一遍又一遍开会手把手说哪里哪里应该加空格、加逗号、换行等。只有对某些代码，工具也无能为力的时候，才使用人为约定的规范进行约束，以提高效率。

<br />

不过，

以下部分也不就是定死没得商量的啦，如果有疑问可以提出来讨论修正修正。



# 正文

## 1. 导出默认时，不直接使用 export default

### 示范

> 错误示范

```javascript
export default [
  {
    name: "Tom",
  },
  {
    name: "Jerry",
  },
];
```

> 正确示范

```javascript
const nameList = [
  {
    name: "Tom",
  },
  {
    name: "Jerry",
  },
];

export default nameList;
```

### 原因

这么写，可以让 IDE 识别出该导出变量被哪些文件引用，方便追踪溯源。

![](https://user-images.githubusercontent.com/49681036/121682606-dfc21d80-caee-11eb-8ae2-2b6b5f6329c5.png)



## 2. 每个 React 组件都需要对其定制化命名

### 示范

> 错误示范

![](https://user-images.githubusercontent.com/49681036/121682833-26b01300-caef-11eb-8e16-e013ce2c9997.png)

> 正确示范

![](https://user-images.githubusercontent.com/49681036/121683080-7989ca80-caef-11eb-9617-d9a6bc47c3e4.png)

### 原因

方便搜索、区分组件，定位错误。



## 3. 渲染 DOM 的函数的命名以 render 开头

### 示范

> 错误示范

```
/** 获取搜索表单 */
getSearchForm(){}

/** 获取应用表格 */
getAppTable(){}
```

> 正确示范

```
/** 获取搜索表单 */
renderSearchForm(){}

/** 获取应用表格 */
renderAppTable(){}
```

### 原因

感觉更语义化一些，参考自 render 函数的命名，与之保持一致风格。



## 4. 提交代码需找至少一位同事审查并记录在 commit message 中

### 示范

> 错误示范

```
git commit -m 'xxxx'
```

> 正确示范

```
git commit -m 'xxxx（审查人：blueju/ypf/...）'
```

### 原因

引入第三方检查，参考自本人在大公司实习时的前端约定。



## 5. DOM 的 style 并非都要抽离，超过 3 个时才抽离

### 示范

> 错误示范

```react
// index.less
.xxx {
  color: red;
}

// index.jsx
import styles from './index.less'

<div className={styles.xxx}></div>
```

> 正确示范

```react
<div style={{ color: 'red' }}></div>
```

### 原因

据日常同事反映，如每个都抽离，其实反而更麻烦。



## 6. CSS 模块化引入 CSS 文件时，变量名统一为 styles

### 示范

> 错误示范

```javascript
import style from './index.less'

import Styles from './index.less'
```

> 正确示范

```javascript
import styles from './index.less'
```

### 原因

参考自 umi 示例工程

> 参考：
>
> https://umijs.org/zh-CN/docs/assets-css#css-modules



## 7. 不可擅自新增第三方依赖

### 示范

> 错误示范

```
/
```

> 正确示范

```
/
```

### 原因

避免滥用依赖的情况，也参考自本人在大公司实习时的规范；

如有需要，向前端组长咨询、讨论、对比、决定。



## 8. 目录结构

### 示范

> 错误示范

```
/
```

> 正确示范

```
/
```

### 原因

```
/
```



## 9. service 中的 api 方法命名以 api 开头

### 示范

> 错误示范

```react
// service.js
export function getTradeCodes() {}

// index.jsx
import React from 'react';
import { getTradeCodes } from './service

class TradeCode extends React.Component{
	// 是不是觉得为该函数取名为 getTradeCodes，则与 service 里的 getTradeCodes 重名了，
	// 但不取吧，又一时间想不到其他同样能表达“获取交易代码“的英文了
	getTradeCodes(){
		getTradeCodes().then(res=>{})
	}
	componentDidMount(){
		this.getTradeCodes()
	}
}
```

> 正确示范

```react
// service.js
export function apiGetTradeCodes() {}

// index.jsx
import React from 'react';
import { apiGetTradeCodes } from './service

class TradeCode extends React.Component{
	getTradeCodes(){
		apiGetTradeCodes().then(res=>{})
	}
	componentDidMount(){
		this.getTradeCodes()
	}
}
```

### 原因

针对 “ 在 service 定义 api 方法并在组件中使用 ” 这一必经流程，避免同一意思却命名不一致的经常性情况；

同时也方便区分 ” 组件方法 “ 与 ” api 方法 “ ；



## 10. 文件夹命名规范

### 示范

> 错误示范

```javascript
// 没有错误示范，只要团队内认可且保持一致即可
```

> 正确示范

大驼峰命名

![](https://user-images.githubusercontent.com/49681036/121685839-02eecc00-caf3-11eb-95ee-e228079842b8.png)

### 原因

参考自 ant-design-pro，因为它是一个后管平台，更接近于日常项目，尽管 ant-design 中使用的文件夹命名规范使用的是短横线命名。

>  参考：
>
> 1. https://github.com/ant-design/ant-design-pro
> 2. https://github.com/ant-design/ant-design





## 11. 文件命名规范

### 示范

> 错误示范

```react
// 没有错误示范，只要团队内认可且保持一致即可
```

> 正确示范

大驼峰命名

![](https://user-images.githubusercontent.com/49681036/121686900-5281c780-caf4-11eb-9448-9dabaaa8c1c7.png)

### 原因

因为根据 React 规范，组件名必须大写，因此强烈建议文件名与组件命名保持一致，同时也参考自 ant-design-pro，因为它是一个后管平台，更接近于日常项目。

>  参考：
>
>  https://github.com/ant-design/ant-design-pro



## 12. HTML 标签内为空时，使用自闭合标签

### 示范

> 错误示范

```react
import React from 'react';
import { Input, Table } from 'antd';

class TradeCode extends React.Component{
	render(){
        return (
        	<>
                <Input value="username"></Input>
                <Table>
                    <Table.Column title="用户名" dataIndex="username"></Table.Column>
                <Table>
            </>
        )
    }
}
```

> 正确示范

```react
import React from 'react';
import { Input, Table } from 'antd';

class TradeCode extends React.Component{
	render(){
        return (
        	<>
            	<Input value="username" />
                <Table>
                	<Table.Column title="用户名" dataIndex="username" />
                <Table>
            </>
        )
    }
}
```

### 原因

HTML 规范，没啥好说的，如果不按规范写，ESLint（如果你使用了的话）也会报错。



## 13. 关于变量存放在哪里的问题

### 示范

> 错误示范

```
/
```

> 正确示范

```react
// 正确示范一
export const data = []

// 正确示范二
class Login extends React.Component{
    this.data2 = []
}

// 正确示范三
class Login extends React.Component{
    this.state = {
        data3: []
    }
}
```

### 原因

1. 如果变量需要被其他组件共享，则放组件外定义，参考如上正确示范一；
2. 如果变量只是在组件内部被使用，且不需要频繁改变，则直接在组件内部定义，但不要 state 中，参考如上正确示范二：
3. 如果变量只是在组件内部被使用，且需要频繁改变，则放入 state 中，参考如上正确示范三；

> 参考：
>
> https://segmentfault.com/q/1010000012396988



## 14. 关于变量、函数的命名单词拼写问题

### 示范

> 错误示范

```react
tsCode
tsElement
TSelement 
getTSelementsList
```

![](https://user-images.githubusercontent.com/49681036/121690233-2ec08080-caf8-11eb-807c-de242865ee64.png)

> 正确示范

```react
txnCode
tradeCode
```

### 原因

宁愿变量名长一些，也不要擅自缩写成既不是接口属性的名称，也不是业界统一认同的名称，如：交易代码。

正确缩写：

- txnCode（接口属性是这么定义，如果有现成的，那就与它保持一致咯）
- tradeCode（按照中文直译的，完整，即使不认识，也可以通过翻译工具得知其意思）

错误缩写：

tsCode、tsElement、TSelement 等



## 15. 尽量少使用 Ant Design Form 中的 defaultValue、initialValue 等属性

### 示范

错误示范

```
/
```

正确示范

```
/
```

### 原因

如果你不清楚什么不轻易使用，那就先不要使用，请使用其他方式使用你的功能，并后续去了解其中的原因。

因为我发现不止一次，有多名组件在这块上面犯错误。

### 参考

> https://ant.design/components/form-cn/#Form-的-initialValues-与-Item-的-initialValue-区别？



## 16. Class 组件使用 constructor 构造器

### 示范

错误示范

```
class Login extends Component {
	this.state = {}
	componentDidMount(){}
}
```

正确示范

```
class Login extends Component {
	constructor(props){
		super(props)
		this.state = {}
	}
	componentDidMount(){}
}
```

### 原因

虽然两者在实际编译后的代码中是一致的，社区中也同时存在着这两种写法，但为了保持团队内一致，统一取下面的写法（即正确示例）。

同时也是为了与 componentDidMount 等生命周期区分开来（因为我发现挺多组员写代码时，代码顺序乱七八糟混在一块），毕竟有时候我们在组件里需要定义的东西可不止 this.state 这么一个。

### 参考

> https://segmentfault.com/a/1190000022521222?utm_source=tag-newest



## 17. 新项目中，尽管看似可共用的部分，也暂不轻易做组件封装复用

### 示范

错误示范

```
/
```

正确示范

```
/
```

### 原因

项目特点，需求变动尤其大，因此尽管看似有可共用的部分，也暂不轻易做组件封装复用，等到项目稳定了再考虑，减少后续麻烦。

> 真实案例：quota 项目的查看/编辑/新增页面，一开始觉得页面都差不多，结果需求后面改到完全不一样了，逻辑很多很乱，结果还不如分开写。



## 18. 关于 React 组件中 this 指向绑定的问题

### 示范

错误示范

```javascript
// 非错误示范，而是不建议示范
class LoggingButton extends React.Component {
  handleClick() {
    console.log('this is:', this);
  }

  render() {
    // 此语法确保 `handleClick` 内的 `this` 已被绑定。
    return (
      <button onClick={() => this.handleClick()}>
        Click me
      </button>
    );
  }
}
```

正确示范

```javascript
// 正确示范一
// class fields 语法
class LoggingButton extends React.Component {
  // 此语法确保 `handleClick` 内的 `this` 已被绑定。
  // 注意: 这是 *实验性* 语法。
  handleClick = () => {
    console.log('this is:', this);
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        Click me
      </button>
    );
  }
}

// 正确示范二
// 构造器中绑定 this
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // 为了在回调中使用 `this`，这个绑定是必不可少的
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(prevState => ({
      isToggleOn: !prevState.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}
```

### 原因

> （如上错误示范）
>
> 此语法问题在于每次渲染 `LoggingButton` 时都会创建不同的回调函数。在大多数情况下，这没什么问题，但如果该回调函数作为 prop 传入子组件时，这些组件可能会进行额外的重新渲染。我们通常建议在构造器中绑定或使用 class fields 语法来避免这类性能问题。

React 官方更建议我们在构造器中绑定 this，或使用 class fields 语法来避免这类性能问题。

**那我们选一个？**

### 参考

> 事件处理：
>
> https://zh-hans.reactjs.org/docs/handling-events.html



## 19. 向事件处理程序传递参数

### 示范

错误示范

```javascript
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
```

正确示范

```javascript
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```

### 原因

由于上一条 18 的原因，可能实际操作中没有了匿名函数，就有同学不知道需要事件处理时如何进行传参了。同样根据参考的建议，如果我们不使用匿名函数的话，那我们可以使用 bind 这些方式进行事件处理传参。

### 参考

> 向事件处理程序传递参数：
>
> https://zh-hans.reactjs.org/docs/handling-events.html#passing-arguments-to-event-handlers



## 20. import 顺序

### 示范

错误示范

```
/
```

正确示范

```
/
```

### 原因

其实 vscode 是自带有 import sort 功能的，不过个人更倾向于自己分类，主要由上到下分为：

- 第三方依赖
- 样式文件
- 其他自定义组件/自定义 js 文件



## 21. 关于 package-lock.json / yarn.lock 依赖版本锁定的问题

### 示范

错误示范

```
// 未上传 package-lock.json
// 或
// 上传了 yarn.lock
```

正确示范

```
// 上传了 package-lock.json
```

### 原因

没啥原因，去 GitHub 看各大明星项目，都使用了版本锁定，只是大多数使用的是 yarn.lock（因为 yarn 安装依赖更快），鉴于我们使用的是内部 npm 仓库，即使不使用 yarn 也已经很快了。

因此我们统一使用 node 自带的 npm 的依赖版本锁定文件 package-lock.json。



## 22. 注释尽可能使用 /** */

### 示范

错误示范

```javascript
// 年龄
let age = 25

// 人
let person = {
	// 姓名
	name: "姓名",
	// 年龄
	age: "年龄",
}

// 处理交易要素的选中，展示要素值框
handleEleSelect(record, selected) {
  if (selected) {
    this.setState({
      elementValueDis: true,
      txnElementId: record.txnElementId,
    });
  }
}
```

正确示范

```javascript
/** 年龄 */
let age = 25

/** 人 */
let person = {
	/** 姓名 */
	name: "姓名",
	/** 年龄 */
	age: "年龄",
}

/**
 * 处理交易要素的选中，展示要素值框
 * @param {string} record
 * @param {boolean} selected
 */
handleEleSelect(record, selected) {
  if (selected) {
    this.setState({
      elementValueDis: true,
      txnElementId: record.txnElementId,
    });
  }
}
```

### 原因

因为这样，IDE 能更好的解析注释，达到以下效果，让其他人能更好地读懂代码。

![image](https://user-images.githubusercontent.com/49681036/122330165-3f904c80-cf65-11eb-81a9-dad7e53f6991.png)

![image](https://user-images.githubusercontent.com/49681036/122330118-28e9f580-cf65-11eb-89e8-59fea927e16d.png)

![image](https://user-images.githubusercontent.com/49681036/122330001-f3dda300-cf64-11eb-91ac-ba7c13a18344.png)

