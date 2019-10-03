# 组件相关

1. [Virtual Dom](#Virtual-DOM)
2. [Ant Design](#Ant-Design)
3. [Vue 生命周期](#Vue-生命周期)
4. [React 生命周期](#React-生命周期)

## Virtual DOM
用 JavaScript 对象结构表示 DOM 树的结构,并用这个树构建一个真正的 DOM 树插到文档当中,
当状态变更的时候,重新构造一棵新的对象树,然后用新的树和旧的树进行比较,记录两棵树差异把所记录的差异应用到所构建的真正的DOM树上从而进行视图更新.
Virtual DOM 本质上就是在 JavaScript 和 DOM 之间做了一个缓存  

## Ant Design
优点
>组件非常全面,样式效果也都比较不错

缺点
>框架自定义程度低,默认UI风格修改困难

## Vue 生命周期

| 生命周期 | 事件状态 |
|-|-|
| beforeCreate | 在实例初始化之后,数据观测和事件配置之前被调用,此时组件的选项对象还未创建, el 和 data 并未初始化 |
| created | 实例已经创建完成之后被调用,已完成数据观测、属性和方法的运算, watch/event 事件回调,完成了data 数据的初始化,但el没有 |
| beforeMount | 挂载开始之前被调用,相关的render函数首次被调用,已完成编译模板,把 data 里面的数据和模板生成html,完成了 el 和 data 初始化,但此时还没有挂载 HTML 到页面上 |
| mounted | 挂载完成,也就是模板中的 HTML 渲染到 HTML 页面中,此时一般可以做一些ajax操作,mounted只会执行一次. |
| beforeUpdata | 在数据更新之前被调用,发生在 Virtual DOM 重新渲染和打补丁之前,可以在该钩子中进一步地更改状态,不会触发附加地重渲染过程 |
| updated | 在由于数据更改导致地 Virtual DOM 重新渲染和打补丁时调用,可以执行依赖于DOM的操作 |
| beforeDestrioy | 在实例销毁之前调用,实例仍然完全可用,这一步还可以用this来获取实例,一般进行一些重置的操作,比如清除掉组件中的定时器和监听的 DOM 事件|
| destroyed | 在实例销毁之后调用,调用后,所有的事件监听器会被移出,所有的子实例也会被销毁 |

## React 生命周期

| 生命周期 | 事件状态 |
|-|-|
| initialization | 使用`super(props)`调用基类的构造方法,也将父组件的 props 注入给子组件,供子组件读取;constructor()用来对组件进行初始化,如定义this.state的初始内容 |
| componentWillMount | 在组件挂载到 DOM 前调用,且只会被调用一次,此时调用this.setState不会引起组件重新渲染 |
| render | 根据组件的 props 和 state 返回一个React元素,不负责组件实际渲染工作,之后由React自身根据此元素去渲染出页面DOM |
| componentDidMount | 组件挂载到DOM后调用,且只会被调用一次;相对于 Vue 中的 `mounted` |
| componentWillReceiveProps | 组件将要接收新属性，此时，只要这个方法被触发，就证明父组件为当前子组件传递了新的属性值;首次并不会触发函数 |
| shouldComponentUpdate | 此方法通过比较传入的参数 nextProps, nextState 及当前组件的this.props,this.state进行判断；返回true时当前组件将继续执行更新过程,返回false则当前组件更新停止,以此可用来减少组件的不必要渲染,优化组件性能 |
| componentWillUpdate | 此方法在调用render方法前执行,在这边可执行一些组件更新发生前的工作,一般较少用 |
| componentDidUpdate | 此时页面又被重新渲染了, state 、 Virtual DOM 和页面已经完成保持同步 |
| componentWillUnmount | 此方法在组件被卸载前调用,执行一些清理工作,比如清除组件中使用的定时器,componentDidMount中手动创建的DOM元素等 |

