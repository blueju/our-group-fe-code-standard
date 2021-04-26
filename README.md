# our-group-js-code-standard

> 我们团队的 JavaScript 代码规范



TODO:

* [ ] 事件方法，匿名函数？手动绑定this？函数表达式？
* [ ] 注释使用 `/** xxx */`
* [ ] 属性接收字符串的，不需要使用{}包裹
* [ ] service里的方法以 api 开头
* [ ] 如果使用 class 组件，还要不要构造函数
* [ ] antd table column 写在 render 里
* [x] 不直接使用 export default 导出数据
* [x] 每个 React 组件都需要对其定制化命名
* [x] 渲染 DOM 的函数的命名以 render 开头
* [x] 提交代码需找至少一位同事审查并记录在 commit message 中
* [x] DOM 元素的 style 属性并不是都需要抽离，超过 3 个时才抽离
* [x] 引用的 CSS 变量名统一为 styles



# 前言

使用 Alloy Team 的 eslint config 对代码进行规范检查；

使用 Prettier 对代码进行格式检查；

最大化利用工具，对以上工具无法检查的部分，才使用人为约定的规范进行约束。

# 正文

## 1. 不直接使用 export default 导出数据

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

## 2. 每个 React 组件都需要对其定制化命名

### 示范

> 错误示范

```
/** 登录组件 */
class Index extends React.Component {}

/** 注册组件 */
class Index extends React.Component {}
```

> 正确示范

```
/** 登录组件 */
class Login extends React.Component {}

/** 注册组件 */
class Register extends React.Component {}
```

### 原因

方便搜索组件，区分组件，定位错误。

## 3. 渲染 DOM 的函数的命名以 render 开头

### 示范

> 错误示范

```
/** 获取表单 */
getSearchForm(){}
```

> 正确示范

```
/** 获取表单 */
renderSearchForm(){}
```

### 原因

没为什么，参考自 render 函数的命名，与之保持一致风格。

## 4. 提交代码需找至少一位同事审查并记录在 commit message 中

### 示范

> 错误示范

```
git commit -m 'xxxx'
```

> 正确示范

```
git commit -m 'xxxx（审查人：蓝钜/喻鹏飞/...）'
```

### 原因

引入第三方约束及检查，也参考自本人在大公司实习时的规范。

## 5. DOM 元素的 style 属性并不是都需要抽离，超过 3 个时才抽离

### 示范

> 错误示范

```
// index.less
.xxx{
  color: red;
}

// index.jsx
import styles from './index.less'

<div className={styles.xxx}></div>
```

> 正确示范

```
import styles from './index.less'

<div style={{color:'red'}}></div>
```

### 原因

每个都抽离，反而更麻烦了。

## 6. 引用的 CSS 变量名统一为 styles

### 示范

> 错误示范

```
// 不符合实际数量情况（复数）
import style from './index.less'
// 不符合小驼峰式命名
import Styles from './index.less'
```

> 正确示范

```
import styles from './index.less'
```

### 原因

参考自 umi 示例工程。
