### 重绘和重排的区别：

当盒子的位置、大小以及其他属性，例如颜色、字体大小等都确定下来之后，浏览器便把这些原色都按照各自的特性绘制一遍，将内容呈现在页面上。

#### **重绘（repaint或redraw）**：

重绘是指一个元素外观的改变所触发的浏览器行为，浏览器会根据元素的新属性重新绘制，使元素呈现新的外观。重绘发生在元素的可见的外观被改变，但并没有影响到布局的时候。比如，仅修改DOM元素的字体颜色（只有Repaint，因为不需要调整布局）

#### **重排（重构/回流/reflow）**：

当渲染树中的一部分(或全部)因为元素的规模尺寸，布局，隐藏等改变而需要重新构建, 这就称为回流(reflow)。每个页面至少需要一次回流，就是在页面第一次加载的时候。

触发重排的条件：任何页面布局和几何属性的改变都会触发重排：

- 页面渲染初始化(无法避免)
- 添加或删除可见的DOM元素
- 元素位置的改变，或者使用动画
- 元素尺寸的改变——大小，外边距，边框
- 浏览器窗口尺寸的变化
- 填充内容的改变，比如文本的改变或图片大小改变而引起的计算值宽度和高度的改变

**重排必定会引发重绘，但重绘不一定会引发重排。**

#### **如何避免触发回流和重绘**：

- 避免频繁使用 style，而是采用修改`class`的方式。
- 将动画效果应用到`position`属性为`absolute`或`fixed`的元素上。
- 也可以先为元素设置`display: none`，操作结束后再把它显示出来。因为在`display`属性为`none`的元素上进行的DOM操作不会引发回流和重绘
- 使用`createDocumentFragment`进行批量的 DOM 操作。
- 对于 resize、scroll 等进行防抖/节流处理。
- 避免频繁读取会引发回流/重绘的属性，如果确实需要多次使用，就用一个变量缓存起来。
- 利用 CSS3 的`transform`、`opacity`、`filter`这些属性可以实现合成的效果，也就是`GPU`加速。