#### 扩展:git提交规范

. 核心格式
提交信息（Commit Message）的标准格式如下：
text

编辑

<type>(<scope>): <subject>
// 空一行

<body>
// 空一行
<footer>
Header (必填): <type>(<scope>): <subject>
Body (可选): 详细描述修改内容。
Footer (可选): 用于关联 Issue 或说明破坏性变更。
注意：<type> 和 (<scope>) 之间没有空格，但 (<scope>): 和 <subject> 之间必须有一个空格。
. Type (提交类型) - 最重要部分
<type> 用于描述提交的性质，常用的类型如下：
表格
类型	含义	示例
feat	新增功能 (Feature)	feat: 增加用户登录功能
fix	修复 Bug	fix: 修复登录页面验证码不显示的问题
docs	文档更新 (Documentation)	docs: 更新 README 安装说明
style	代码格式调整 (不影响逻辑)	style: 移除多余的空格，格式化代码
refactor	代码重构 (既不是新增功能也不是修 Bug)	refactor: 优化数据库连接池逻辑
perf	性能优化 (Performance)	perf: 优化图片加载速度，减少首屏时间
test	测试相关 (添加或修改测试用例)	test: 增加用户注册接口的单元测试
chore	构建过程或辅助工具变动 (依赖升级、配置修改等)	chore: 升级 lodash 到最新版本
ci	CI/CD 配置文件修改	ci: 修改 GitHub Actions 构建脚本
revert	回滚之前的提交	revert: 回滚 "feat: 增加支付功能"
. Scope (影响范围) - 可选
<scope> 用于说明本次提交影响的范围（如模块名、文件名、组件名）。
如果改动涉及整个项目，可以省略。
示例：feat(auth): 增加短信登录、fix(ui): 修复按钮颜色。
. Subject (简短描述) - 必填
简洁明了：一句话概括做了什么，建议不超过 50 个字符。
时态语气：
推荐使用祈使句（现在时），像在下命令。
✅ 正确：add login page / 增加登录页
❌ 错误：added login page / 增加了登录页 (过去时)
❌ 错误：adding login page / 正在增加登录页 (进行时)
结尾不要加句号。
. Body (详细描述) - 可选
如果改动比较复杂，可以在这里详细说明：
为什么做这个修改（动机）。
怎么做的（实现思路）。
与之前的行为有什么不同。
. Footer (页脚) - 可选
主要用于两种情况：
破坏性变更 (Breaking Changes)：如果不兼容旧版本，必须以 BREAKING CHANGE: 开头。
示例：BREAKING CHANGE: 移除了旧的 API 接口 /v1/users
关联 Issue：关闭或引用问题追踪系统中的 Ticket。
示例：Closes #123, Fixes #456, Refs #789
✅ 优秀示例
场景 1：新增功能
text

编辑

feat(user): 增加用户头像上传功能

- 支持 jpg, png 格式
- 限制文件大小为 2MB
- 增加裁剪组件

Closes #1024
场景 2：修复 Bug
text

编辑

fix(order): 修复订单金额计算精度丢失问题

在计算总价时，将 float 类型改为 decimal 类型以避免精度误差。

Fixes #567
场景 3：破坏性变更
text

编辑

refactor(api): 重构用户认证模块

- 移除旧的 Token 生成逻辑
- 引入 JWT 标准

BREAKING CHANGE: 旧的 /auth/login 接口不再支持返回 session_id，客户端需适配新的 JWT 流程。
🛠️ 如何强制执行规范？
靠人工自觉很难保证，通常配合工具使用：
Commitizen: 一个交互式命令行工具，引导你按步骤填写提交信息，自动生成符合规范的字符串。
安装：npm install -g commitizen
使用：git cz (代替 git commit)
Commitlint: 在 Git Hook 中检查提交信息格式，不符合规范则阻止提交。
通常配合 husky 使用。
VS Code 插件: 搜索 "Git Commit Message Editor" 或 "Conventional Commits" 插件，提供模板和提示。
💡 小贴士
中文还是英文？ 团队内部统一即可。国内团队常用中文，开源国际项目常用英文。
粒度控制：一次提交只做一件事。如果一个提交既修了 Bug 又加了功能，请拆分成两个提交。
