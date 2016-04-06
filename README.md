## 百度前端技术学院任务提交代码及笔记

### Mission1_1

#### About

还是决定从0基础开始做任务，通过这第一个最简单的连CSS都没有的任务，复习了基础知识，看了大家的代码，知道了许多之前不知道的标签，发现大家每个人写的都不一样，都有自己的特色，或许这就是前端的魅力吧。

#### Label and Point
1.除了之前学习的有序列表`<ol>`和无序列表`<ul>`，还知道了自定义列表`<dl>`,自定义列表以`<dl>`标签开始。
每个自定义列表项以`<dt>`开始。每个自定义列表项的定义以`<dd>`开始.
  ```html
  <dl>
    <dt>计算机</dt>
    <dd>用来计算的仪器 ... ...</dd>
    <dt>显示器</dt>
    <dd>以视觉方式显示信息的装置 ... ...</dd>
  </dl>
  ```
2.Html5语义化标签的使用，如`<nav>`标签，`<aside>`标签，`<time>`标签,`<article>`标签，`<header>`标签，以及`<figure>`,`<figcaption>`标签等.

3.利用 maxlength 和 minlength 属性来控制 input 标签输入的最大长度及最小长度.
```html
<input type="password" minlength="6" maxlength="16"/>
```

4.利用pattern属性匹配正则表达式来验证输入格式.
```html
<input type="password" pattern="[A-Za-z0-9\-]*" placeholder="这是一个只能输入英文字母和数字的密码输入框"/>
```
