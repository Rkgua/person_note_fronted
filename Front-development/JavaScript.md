### js手写重点
#### 1. 核心原理与内置 API 实现 (高频必考)
- 这类题目考察你是否真正理解 JavaScript 的底层机制，而不是仅仅会调用 API。
1. call / apply / bind 的实现
考点：理解 this 指向的绑定、函数上下文借用、参数处理（数组与不定参数）。
核心逻辑：将函数作为目标对象的临时属性执行，执行后删除。

2. new 操作符的实现
考点：原型链继承、对象创建过程。
核心逻辑：创建一个空对象 -> 链接原型 -> 绑定 this 执行构造函数 -> 返回对象（若构造函数返回对象则返回该对象，否则返回新对象）。

3. instanceof 的实现
考点：原型链查找机制。
核心逻辑：遍历左侧实例的 __proto__，看是否能找到右侧构造函数的 prototype。

4. Promise 相关 (all, race, resolve)
考点：异步编程、状态管理、并发控制。
核心逻辑：Promise.all 需要维护一个计数器，所有 Promise 完成后 resolve；遇到 reject 立即 reject。
#### 2. 函数式编程与性能优化
- 这类题目考察对闭包、高阶函数以及浏览器运行机制的理解。

1. 防抖 (Debounce) 与 节流 (Throttle)
考点：闭包保存状态、定时器控制、高频事件处理（如滚动、输入）。
区别：防抖是“最后一次触发才执行”，节流是“固定频率执行”。
2. 函数柯里化 (Currying)
考点：闭包、参数复用、函数惰性求值。
核心逻辑：判断传入参数数量，若不足则返回新函数继续收集参数，若足够则执行原函数。
3. 深拷贝 (Deep Clone)
考点：递归、循环引用处理（WeakMap）、数据类型判断（Array, Object, Date, RegExp 等）。
核心逻辑：递归遍历对象属性，区分引用类型和基本类型，处理循环引用。
#### 3. 数组与对象操作 (实用工具类)
- 考察对数据结构的处理能力，常用于业务逻辑开发。
1. 数组扁平化 (Flat)
考点：递归、数组方法 (reduce, concat, flat)。
核心逻辑：将多维数组转化为一维数组。
2. 数组去重
考点：ES6 Set 数据结构、filter、indexOf。
3. 对象/数组的浅拷贝
考点：Object.assign、扩展运算符 ...、Array.slice。
4. map / reduce / filter 的实现
考点：数组遍历原理、回调函数处理。
#### 4. 基础算法与数据结构
- 难度通常低于 LeetCode 的 Hard 模式，侧重于基础逻辑。
1. LRU 缓存 (Least Recently Used)
考点：Map 数据结构、链表思想（虽然 JS 中常用 Map 模拟）。
2. 发布-订阅模式 (Event Bus)
考点：对象属性管理、事件监听与触发。
3. 简单的模板引擎
考点：正则表达式替换、字符串处理。
4. 常见排序算法
考点：快速排序、冒泡排序、堆排序（考察排序思想）。
#### 5. 类型判断与 DOM 操作
1. 精准类型判断 
考点：typeof 的局限性与 Object.prototype.toString.call() 的使用。
2. DOM 操作 (如事件委托)
考点：事件冒泡、e.target 的使用、性能优化（减少事件绑定）。












   



### 正则表达式

##### 1. 字面量方式（推荐）

const reg = /pattern/flags;
pattern：匹配模式
flags：标志（可选），如 g（全局）、i（忽略大小写）、m（多行）等
示例：

const reg = /\d+/g; // 匹配所有连续数字 2. 构造函数方式（适合动态构建）

const reg = new RegExp('pattern', 'flags');
示例：
const reg = new RegExp('\\d+', 'g'); // 注意：反斜杠需要转义
##### 二、常用方法

- 1. test()：测试是否匹配（返回布尔值）
   const reg = /\d+/;
   console.log(reg.test("abc123")); // true
- 2. exec()：执行搜索，返回匹配结果（数组或 null）
   const reg = /\d+/g;
   let result;
   while ((result = reg.exec("a1b22c333")) !== null) {
   console.log(result[0]); // 依次输出 "1", "22", "333"
   }
- 3. 字符串方法中使用正则
   str.match(reg)：返回匹配项数组（或 null）
   str.search(reg)：返回第一个匹配的索引（未找到返回 -1）
   str.replace(reg, replacement)：替换匹配内容
   str.split(reg)：按正则分割字符串
   示例：
``
hello123world456.match(/\d+/g); // ["123", "456"]
abc-def.split(/-/); // ["abc", "def"]
Price: $100".replace(/\$(\d+)/, '￥$1'); // "Price: ￥100"
``

| 元字符   | 含义                       |
| :---: | :--------------------------: | 
| `\d`     | 数字 [0-9]                 |
| `\w`     | 单词字符 [a-zA-Z0-9_]      |
| `\s`     | 空白字符（空格、制表符等） |
| `.`      | 任意字符（除换行符）       |
| `^`      | 行首                       |
| `$`     | 行尾                       |
|`\*`     | 0 次或多次                 |
|`+`     | 1 次或多次                 |
|`?`     | 0 次或 1 次                |
|`{n}`   | 恰好 n 次                  |
|`{n,}`  | 至少 n 次                  |
|`{n,m}` | n 到 m 次                  |
|`[abc]` | 匹配 a、b 或 c             |
|`[^abc]`| 不匹配 a、b、c             |
|`( )`   | 分组                   |
|` | ` | 或 |
