#### 正则表达式

1. 字面量方式（推荐）

const reg = /pattern/flags;
pattern：匹配模式
flags：标志（可选），如 g（全局）、i（忽略大小写）、m（多行）等
示例：

const reg = /\d+/g; // 匹配所有连续数字 2. 构造函数方式（适合动态构建）

const reg = new RegExp('pattern', 'flags');
示例：
const reg = new RegExp('\\d+', 'g'); // 注意：反斜杠需要转义
二、常用方法

1. test()：测试是否匹配（返回布尔值）
   const reg = /\d+/;
   console.log(reg.test("abc123")); // true
2. exec()：执行搜索，返回匹配结果（数组或 null）
   const reg = /\d+/g;
   let result;
   while ((result = reg.exec("a1b22c333")) !== null) {
   console.log(result[0]); // 依次输出 "1", "22", "333"
   }
3. 字符串方法中使用正则
   str.match(reg)：返回匹配项数组（或 null）
   str.search(reg)：返回第一个匹配的索引（未找到返回 -1）
   str.replace(reg, replacement)：替换匹配内容
   str.split(reg)：按正则分割字符串
   示例：
   "hello123world456".match(/\d+/g); // ["123", "456"]
   "abc-def".split(/-/); // ["abc", "def"]
   "Price: $100".replace(/\$(\d+)/, '￥$1'); // "Price: ￥100"
| 元字符   | 含义                       |
| -------- | -------------------------- | --- |
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
|`( )`   | 分组                       |
|` | ` | 或 |
