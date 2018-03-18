# JSX 文档详情

我们之前已经说过一些和 `JSX` 相关的特性:

- `jsx` 可以嵌入表达式
- `jsx` 本身可以当做表达式
- `jsx` 之间可以相互嵌套
- 每一份声明的 `jsx` 要有一个闭合标签包含
- 关键字属性需要换种形式: `class => className`
- 属性需要驼峰写法
- 声明 `jsx` 的地方, 需要 `React` 在作用域内

另外一些小特性你也需要注意:

- 自闭和标签结尾处一定要 `/>`.
---

以下内容来自文档, 我进行了一些简化:
你可以原版查看: [JSX in deep](https://reactjs.org/docs/jsx-in-depth.html) | [深入 JSX](https://doc.react-china.org/docs/jsx-in-depth.html)

## React 元素类型

#### 点表示法

```jsx
  <Layout.Content>
  </Layout.Content>
```

#### 内置组件首字母小写

比如: `<div/>`, `<span/>`. :speak_no_evil:

#### 自定义组件首字母大写

比如: `<Foo/>`. :speak_no_evil:

```jsx
<Foo/>
```

#### 标签名不能是表达式
```jsx
// 你不能这样
<components[props.storyType] story={props.story} />

// 可以这样
const SpecificStory = components[props.storyType];

<SpecificStory story={props.story} />;
```
---
## 属性

#### 属性中使用表达式

```jsx
<MyComponent foo={1 + 2 + 3 + 4} />
```

#### 字符串字面量
以下是等价的:
```jsx
<MyComponent message="hello world" />

<MyComponent message={'hello world'} />
```

字符串常量不会被转义, 以下会相等:

```jsx
<MyComponent message="&lt;3" />

<MyComponent message={'<3'} />
```

表达式的字符串会被转义, 以下**不**相等: :smiling_imp::smiling_imp:
```jsx
<MyComponent message='&lt;3' />

<MyComponent message={'&lt;3'} />
```

#### 默认值为 True :balloon::balloon:

```jsx
<MyTextBox autocomplete />
// === 这两种表示等价
<MyTextBox autocomplete={true} />
```

#### 属性的展开 :balloon::balloon:

以下会等价

```jsx
<Greeting firstName="Ben" lastName="Hector" />;
}
//===

const props = {firstName: 'Ben', lastName: 'Hector'};

<Greeting {...props} />;

```
---

## Children

标签之间的内容 就是 `children`, 自定义标签通过 `props.children` 来访问 `children`.

:pill::pill::pill:
空行, 开始 和 结尾的空格. 会被移除.

标签临近的新行, 字符串内部换行被压缩成一个空格:

以下等价:

```jsx
<div>Hello World</div>

// 临近标签处的换行和空格被移除
<div>
  Hello World
</div>

// 字符串内换行变成一个空格
<div>
  Hello
  World
</div>

<div>

  Hello World
</div>
```

:pill::pill::pill: :exclamation::exclamation::exclamation:

**没有闭合标签包含的元素需要在数组里**,
```jsx
[
  // 不要忘记 key :)
  <li key="A">First item</li>,
  <li key="B">Second item</li>,
  <li key="C">Third item</li>,
];
```

#### 关于children需要注意的 :evergreen_tree::evergreen_tree::evergreen_tree::evergreen_tree::evergreen_tree:
自定义组件的 children 可以是任何数据类型, 你通过 props.children 都可以访问到.

这不以为着所有的东西都会被渲染, 仅有以下东西会被渲染:

- React element
- 字符串
- 数字
- 元素是 React node 的数组

**布尔值、Null 和 Undefined 被忽略**

要注意一点是:

```jsx
// 此表达式返回 0, 0会被渲染
{0 && 'abc'}
```
[回到大纲:point_left::point_left:](../README.md#outline)