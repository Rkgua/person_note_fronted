
**为什么我写的CSS样式没有生效？**
最常见的原因是选择器优先级问题。浏览器会根据选择器的权重（ID > 类 > 标签）和书写顺序来决定应用哪个样式。应善用开发者工具的“Computed”面板来排查。
**!important 有什么作用？应该滥用吗？**
!important 用于强制提升某条CSS规则的优先级，使其覆盖其他任何规则。不应滥用，因为它会破坏CSS的层叠性，导致后续样式难以覆盖，增加维护难度。
**后代选择器（空格）和子选择器（>）有什么区别？**
A B（后代选择器）会选择A元素内部所有层级的B元素。A > B（子选择器）只会选择A元素的直接子元素B。
:nth-child(n) 和 :nth-of-type(n) 有什么区别？
:nth-child(n) 会计算父元素下所有子元素的顺序，然后判断第n个元素是否匹配选择器。:nth-of-type(n) 只计算父元素下同类型（同标签名）的子元素的顺序。
**属性选择器的值在什么情况下必须加引号？**
当属性值中包含空格、特殊字符（如 .、:、()）时，必须加引号，否则CSS解析器可能会出错并忽略该规则。
**为什么我的逗号分隔选择器组不生效？**
在一个用逗号分隔的选择器列表中（如 h1, .invalid-class, p），如果其中任何一个选择器是无效的（例如浏览器不支持的伪类），那么整个选择器组及其样式规则都会被浏览器忽略。
z-index 属性在什么情况下会失效？
z-index 只对定位元素（position 值不为 static 的元素，如 relative、absolute、fixed）生效。此外，它还会受到父元素 z-index 和层叠上下文的影响。
#### 盒模型与元素表现
**为什么我设置了 width，但元素的实际宽度比设定的要大？**
这是因为默认的 box-sizing 属性值为 content-box。此时 width 仅代表内容区的宽度，元素的总宽度还需加上 padding 和 border。推荐全局设置 * { box-sizing: border-box; }。
**什么是外边距合并（Margin Collapse）？如何避免？**
在普通文档流中，相邻的块级元素的垂直外边距（margin-top 和 margin-bottom）会合并成一个，取两者中的较大值。可以通过触发新的块级格式化上下文（BFC）（如设置 overflow: hidden）、使用 padding 或 border 来隔离元素等方式避免。
**为什么我不能给 <span> 标签设置 width 和 height？**
<span> 是内联元素，其尺寸由内容决定，不响应 width 和 height 属性。需要将其 display 属性设置为 inline-block 或 block 才能设置宽高。
**内联元素的 margin 和 padding 表现有什么特殊之处？**
内联元素的垂直方向（上下）的 margin 和 padding 不会真正影响行高或与其他元素的间距，它们可能会与其他元素重叠。水平方向（左右）的 margin 和 padding 则正常生效。
**如何清除浮动带来的影响？**
浮动元素会脱离文档流，导致父元素高度塌陷。常见清除方法有：1. 在父元素末尾添加一个空的 div 并设置 clear: both。2. 让父元素触发BFC（如 overflow: hidden）。3. 使用 ::after 伪元素清除（推荐）。
**display: none、visibility: hidden 和 opacity: 0 有什么区别？**
display: none: 元素从文档流中完全移除，不占据空间，其子元素也无法显示。
visibility: hidden: 元素不可见，但仍占据原有空间。
opacity: 0: 元素完全透明，但仍占据空间且可以接收鼠标事件。
#### 布局与定位
**如何实现一个元素的水平垂直居中？**
有多种方法：1. Flexbox: display: flex; justify-content: center; align-items: center;。2. Grid: display: grid; place-items: center;。3. 绝对定位 + transform: position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%);。
Flexbox 布局中，子元素内容过长导致父容器被撑开怎么办？
这是Flexbox的默认行为。解决方法是给Flex子项设置 min-width: 0 或 overflow: hidden，允许其内容收缩到比最小内容宽度更小。
在 Flexbox 容器中，margin: auto 有什么特殊效果？
在 Flexbox 容器中，margin: auto 可以实现子元素在对应轴向上的完美居中，因为它会吸收所有剩余空间。
Grid 布局和 Flexbox 布局应该如何选择？
Flexbox 是一维布局，适合在单行或单列中分配空间和 align 元素。Grid 是二维布局，适合处理更复杂的、同时涉及行和列的页面整体结构。
position: sticky 为什么不起作用？
sticky 元素必须满足：1. 其任何一个祖先元素的 overflow 属性不能是 hidden、scroll 或 auto。2. 必须指定 top、right、bottom 或 left 阈值。
绝对定位（absolute）是相对于谁定位的？
相对于其最近的、position 属性值不为 static 的祖先元素进行定位。如果没有这样的祖先元素，则相对于初始包含块（通常是 <html> 或 <body>）。
为什么我的 100vh 在移动端浏览器上表现不正常？
移动浏览器的地址栏和工具栏会动态显示/隐藏，影响视口高度。100vh 包含了这些工具栏的高度，可能导致内容被遮挡。可以使用 100dvh (dynamic viewport height) 等新单位来解决。

**响应式布局的核心技术是什么？**
核心是媒体查询（Media Queries），它允许你根据设备特性（如屏幕宽度）应用不同的CSS样式。

**为什么我的媒体查询不生效？**
常见原因有：1. HTML <head> 中缺少 <meta name="viewport" ...> 标签。2. 媒体查询的语法拼写错误（如 max-with）。3. 媒体查询的优先级不够，被其他样式覆盖。
rem 和 em 单位有什么区别？
em 是相对于父元素的字体大小。rem (root em) 是相对于根元素（<html>）的字体大小。使用 rem 可以避免嵌套带来的尺寸计算复杂性。
如何实现移动端适配？
常用方案包括：1. 使用媒体查询进行响应式布局。2. 使用 viewport + rem 的适配方案，通过JS动态设置根字体大小。3. 使用 vw/vh 等视口单位。
<meta name="viewport"> 标签的作用是什么？
它控制移动浏览器如何缩放和显示页面。width=device-width, initial-scale=1.0 是最常用的设置，它让页面宽度等于设备宽度，并禁止初始缩放。
样式与视觉
为什么在不同浏览器或设备上，同一个颜色值看起来不一样？
不同设备的屏幕色域、校准和显示技术存在差异，可能导致颜色显示不一致。可以使用在线颜色对照工具进行辅助检查。
使用 @font-face 加载自定义字体失败怎么办？
检查字体文件路径是否正确、服务器MIME类型配置是否准确。可以使用 font-display 属性（如 font-display: swap）来优化字体加载体验，避免文字不可见。
CSS过渡（transition）效果不平滑或卡顿怎么办？
避免对会触发布局重排（Reflow）的属性（如 width, top）进行过渡。优先使用能触发GPU硬件加速的属性，如 transform 和 opacity。
如何避免CSS变量（Custom Properties）的兼容性问题？
CSS变量在现代浏览器中已得到良好支持。对于不支持的旧浏览器，可以提供回退值，例如 color: var(--my-color, #000);。
vertical-align 属性为什么会让元素产生意外的空白间距？
vertical-align 的默认值是 baseline，它会使内联元素与父元素的基线对齐，这可能会影响行高。可以尝试将其设置为 top、middle 等值来排除干扰。
#### 性能与最佳实践
为什么不应该过度使用 !important？
它会破坏CSS的层叠规则，使得样式难以预测和维护。当需要覆盖一个 !important 规则时，你不得不使用另一个 !important，导致优先级战争。
CSS选择器过长或嵌套过深有什么坏处？
虽然对现代浏览器性能影响微乎其微，但会降低代码的可读性和可维护性。推荐使用 BEM 等命名规范来扁平化选择器。
什么是重绘（Repaint）和重排（Reflow）？如何避免？
重排: 元素几何属性（如尺寸、位置）改变，导致浏览器重新计算布局。开销大。
重绘: 元素外观（如颜色、背景）改变，但不影响布局。开销较小。
避免: 避免频繁操作会触发重排的DOM属性，使用 transform 和 opacity 实现动画。
为什么要使用CSS预处理器（如Sass/Less）？
它们提供了变量、嵌套、混合（Mixin）、函数等特性，可以极大地提高CSS代码的可维护性、复用性和组织性。
如何管理大型项目的CSS代码？
采用一套约定俗成的命名方法论，如 BEM (Block, Element, Modifier)，可以有效避免类名冲突，使代码结构更清晰。
浏览器前缀（如 -webkit-, -moz-）应该如何处理？
不要手动添加。推荐使用 Autoprefixer 等PostCSS插件，它会根据你设定的浏览器支持范围，自动为你添加所需的前缀。
为什么内联样式（style="..."）不推荐使用？
它会导致HTML和CSS高度耦合，无法复用，且优先级极高，难以被外部样式覆盖，不利于代码维护和团队协作。
will-change 属性有什么作用？
它用于提前告知浏览器某个元素即将发生变化，让浏览器可以提前进行优化（如创建新的合成层）。应谨慎使用，在动画结束后及时移除。
如何优化CSS动画的性能？
尽量只对 transform 和 opacity 属性进行动画，因为它们可以由GPU处理，不触发重排和重绘，性能最佳。
@supports 规则有什么用？
它是一个特性查询，用于检测浏览器是否支持某个CSS属性或属性值。可以用来为新特性提供优雅降级或渐进增强方案。