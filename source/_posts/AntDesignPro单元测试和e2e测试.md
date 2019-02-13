#AntDesignPro单元测试和e2e测试
UI 测试是项目研发流程中的重要一环，有效的测试用例可以梳理业务需求，保证研发的质量和进度，让工程师可以放心的重构代码和新增功能，分为单元测试和e2e测试。
##单元测试
单元测试用于测试 React UI 组件的表现。antDesignPro使用 [jest](http://facebook.github.io/jest/)和 [enzyme](http://airbnb.io/enzyme/docs/api/index.html)作为测试框架。如何在react项目中搭建jest+enzyme测试环境可参照（https://github.com/superman66/react-test-demo）
 >站在程序员的角度测试
单元测试是把代码看成是一个个的组件。从而实现每一个组件的单独测试，测试内容主要是组件内每一个函数的返回结果是不是和期望值一样。
 1.组件渲染标签是否正确
 2.组件渲染值props是否正确
 3.props传递的函数在模拟交互时是否可以正确触发

###[Enzyme](http://airbnb.io/enzyme/docs/api/)库的主要api解析
1. `shallow`方法返回React组件的浅渲染；`render`方法将React组件渲染成静态的HTML字符串； `mount`方法用于将React组件加载为真实DOM节点。
2. `find`方法返回一个对象，包含了所有符合条件的子组件。
3. `expect`方法表示预期值，如组件的状态、文本、标签等。
4. `simulate`方法表示模拟在这个组件上触发某种行为。
5. `toBexxx`表示判断预期值与结果是否符合，正确则通过测试。

###写一个单元测试用例
比如，我们可以建一个文件 `src/routes/Result/Success.test.js` 来测试成功页面组件的 UI 表现。
```
import React from 'react';
import { shallow } from 'enzyme';
import Success from './Success';   // 引入对应的 React 组件

it('renders with Result', () => {
  const wrapper = shallow(<Success />);                           // 进行渲染
  expect(wrapper.find('Result').length).toBe(1);                  // 有 Result 组件
  expect(wrapper.find('Result').prop('type')).toBe('success');    // 组件的类型是成功
});
```
###本地执行测试脚本
使用以下的命令将统一搜索和执行`src`下`*.test.js`格式的用例文件。
```
$ npm test .test.js
```
执行单个或一组用例
```
$ npm test src/routes/Result/Success.test.js  # 测试 Success.test.js
$ npm test src/routes                         # 测试 routes 下的所有用例文件
```
###测试 dva 包装组件
被 dva `connect` 的 React 组件可以使用下面方式进行测试。
```
import React from 'react';
import { shallow,mount,render } from 'enzyme';
import HomePage from './HomePage';

it('renders HomePage', () => {
  const dispatchFn = jest.fn();
  //WrappedComponent表示被dva包裹的UI组件
  const wrapper = shallow(
    <HomePage.WrappedComponent count={{ record: 0, current: 0 }} dispatch={ dispatchFn }/>
  );

  //1.组件渲染标签是否正确
  expect(wrapper.find('Card').length).toBe(1);
  //expect(wrapper.find('PageHeaderLayout').length).toBe(1);
  //2.测试初始状态 record=0，current=0
  expect(wrapper.find('#current').text()).toEqual('0');
  expect(wrapper.find('#record').text()).toEqual('Highest Record: 0');
  expect(wrapper.find('Card').props().title).toEqual("计数器");

  //3.测试按钮 add minus点击后值改变,测试是否调用add函数
  wrapper.find('#add').at(0).simulate('click');
  expect(dispatchFn).toBeCalled();

  wrapper.find('#minus').at(0).simulate('click');
  expect(dispatchFn).toBeCalled();
});
```
##e2e测试
>注意 e2e 测试需要集成环境支持 electron，如果不支持，你可以使用 npm test .test.js 单独运行单元测试。

端到端测试也叫冒烟测试，用于测试真实浏览器环境下前端应用的流程和表现，相当于代替人工去操作应用。antDesignPro引入了 [nightmare](http://www.nightmarejs.org/) 作为 e2e 测试的工具，`nightmare` 默认使用 electron 作为浏览器环境运行你的应用，并且提供了非常语义化的 API 来描述业务逻辑。

>站在用户角度的测试
 e2e测试是把我们的程序当作一个黑盒子，我不懂你内部是怎么实现的，我只负责打开浏览器，把测试内容在页面上输入一遍，看是不是我想要得到的结果。

###[nightmare](https://github.com/miccuci/nightmare)主要api解析
1. `Nightmare()`方法创建一个nightmare实例
2. `goto`方法模拟请求某个页面，传入页面url。
3. `type`方法用于模拟输入数据。
4. `wait`方法等待响应结果。
5. `evaluate`表示执行函数将结果转换成想要的类型。

###写一个 e2e 用例
假设有一个需求，用户在登录页面输入错误的用户名和密码，点击登录后，出现错误提示框。
![模拟登陆](http://upload-images.jianshu.io/upload_images/8245634-ef528b90f7418e6b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

我们写一个用例来保障这个流程。在 `src/e2e/` 目录下建一个`login.e2e.js` 文件，按上述业务需求描述测试用例。
```
import Nightmare from 'nightmare';

describe('Login', () => {
  it('should login successfully', async () => {
    const page = Nightmare();
    page.goto('http://localhost:8001/#/user/login')
      .type('#userName', 'mockuser')
      .type('#password', '888888')
      .click('button[type="submit"]')
      .wait('.ant-layout-sider h1') // should display error
      .evaluate(() => document.querySelector('.ant-layout-sider h1').innerHTML)
      .end()
      .then(text => expect(text).toContain('统一门户管理'))
  });
});
```
![测试结果](http://upload-images.jianshu.io/upload_images/8245634-f6720949fc757c3c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###运行用例
运行下列命令将执行 src 下所有的 *.e2e.js 用例文件。
```
$ npm test .e2e.js
```
运行如下命令执行单个e2e测试文件
```
$ npm test src/e2e/count.e2e.js
```
>注意，本地测试 e2e 用例需要启动 npm start，否则会报 Failed: navigation error 的错误。

###watch 模式
添加 --watch 配置可以进入 watch 模式，当你修改和保存文件时，Jest 会自动执行相应用例。Jest 的命令行工具也提供了各种方便的快捷键来执行你需要的用例。
```
$ npm test -- --watch
```
![watch模式](http://upload-images.jianshu.io/upload_images/8245634-3bc43392bac367a2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)