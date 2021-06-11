# our-group-js-code-standard

> 我们团队的 JavaScript 代码规范



# TODO

* [ ] 事件方法，匿名函数？手动绑定this？函数表达式？
* [ ] 注释使用 `/** xxx */`
* [ ] 属性接收字符串的，不需要使用{}包裹
* [ ] service里的方法以 api 开头
* [ ] 如果使用 class 组件，还要不要构造函数
* [ ] antd table column 写在 render 里



# 前言

不断完善ing...



情况介绍，

团队使用的是 React 技术栈，使用的前端应用框架是 Umi，主要做基于微前端的后管基座平台、后管子应用、及周边。



代码格式化这块，

使用的是 Prettier，使用的配置统一是：


> 参考：
>
> https://github.com/AlloyTeam/eslint-config-alloy/blob/master/README.zh-CN.md#如何结合-prettier-使用



代码检查这块，

使用的是 Alloy Team 的 eslint-config-alloy

> 参考：
>
> https://github.com/AlloyTeam/eslint-config-alloy



个人认为，

应该最大化地利用工具提高效率，而不是一遍又一遍开会手把手说哪里哪里应该加空格、加逗号、换行等。只有对某些代码，工具也无能为力的时候，才使用人为约定的规范进行约束，以提高效率。



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



## 13. 关于变量、函数的命名单词拼写问题

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

