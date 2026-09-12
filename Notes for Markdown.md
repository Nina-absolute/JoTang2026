# 标题 & 文本格式 & 列表 & 引用块 & 代码
`#` 号必须在行首，前面不能有其他字符（空格或制表符）。

_唯一的一级标题_：在一个文档中，通常只使用一个一级标题作为文档的主标题，这符合良好的文档结构规范。
  
许多 Markdown 处理器和编辑器支持自动生成标题编号，因此在源码中通常不需要手动添加编号：
  
大多数 Markdown 处理器会自动为标题创建锚点（anchor），便于页面内跳转：
[跳转到方法论部分](#方法论)

## 语法格式

Markdown 段落没有特殊的格式，直接编写文字就好，**段落的换行是使用两个以上空格加上回车**。
当然也可以在段落后面使用一个空行来表示重新开始一个段落。

**粗体语法：**使用两个星号 ** 或两个下划线 __ 包围文字

**斜体语法：**使用一个星号 * 或一个下划线 _ 包围文字

**粗斜体组合：**使用三个星号 *** 或三个下划线 ___

推荐使用星号 `*` 而不是下划线 `_`，因为星号在各种 Markdown 解析器中兼容性更好

在中英文混合时，建议在强调符号前后加空格以提高可读性

你可以在一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西。你也可以在星号或是减号中间插入空格。

如果段落上的文字要添加删除线，只需要在文字的两端加上两个波浪线 ~~ 即可


下划线可以通过 HTML 的 <u> 标签来实现：

<u>带下划线文本</u>

[^要注明的文本]： 示例1

行内代码标记 ：使用一个 ` 包围 
- 例子： `commit`
包含反引号的代码 使用两个 ` 包围

高亮文本：使用一个==包围

正确的段落：无缩进 有空行分隔

## 列表  

### 无序列表
用 - 来标记
### 有序列表
用数字加上.号
- 例子：1.

列表可嵌套 只需在 - 号前加上两个空格
- 例子：
1. 主要任务
  - 子任务A
  - 子任务B

### ==任务列表==

- [ ] 未完成任务
- [x] 已完成任务

## 引用块
用>然后加一个空格
- 示例：
> 第一段打出>即可包括后面所有内容，
示例如上
> > 第二层嵌套
> > > 第三层嵌套

如果要在列表项目内放进区块，那么就需要在 > 前添加四个空格的缩进。
- 第一项
> 示例内容

## 代码
### 缩进式代码块

代码区块使用 **4 个空格**或者一个**制表符（Tab 键）**。

	`tab` 键 be like

    这是缩进式代码块
    每行前面有四个空格
    保持代码的原始格式


继续正常文本

三反引号（```）是最常用的代码块语法，支持语法高亮和多行代码展示。

```javascript
$(document).ready(function () {
    alert('RUNOOB');
});
```

- ==缩进式代码块前后需要空行分隔==
- 所有代码行必须保持一致的缩进
- ==不支持语法高亮==
- ==在列表中使用时需要8个空格缩进==

### 语言标识和语法高亮

在三反引号后添加语言标识符可以启用语法高亮功能。

**常用语言标识符列表：**

- `javascript` / `js` - JavaScript

```javascript
const users = [
    { name: "Alice", age: 25 },
    { name: "Bob", age: 30 }
];

const adults = users.filter(user => user.age >= 18);
console.log(adults);
```

- `python` / `py` - Python
- `html` - HTML
- `css` - CSS
- `sql` - SQL
- `json` - JSON
- `xml` - XML
- `yaml` / `yml` - YAML
- `bash` / `shell` - Shell脚本
- `java` - Java
- `cpp` / `c++` - C++
- `csharp` / `c#` - C#
- `php` - PHP
- `ruby` / `rb` - Ruby
- `go` - Go语言
- `rust` - Rust
- `typescript` / `ts` - TypeScript

### 代码差异对比

用于显示代码的添加、删除或修改，常用于展示版本控制中的变更。

**Diff 语法：**

```diff
function calculateTotal(items) {
-   let total = 0;
+   let total = 0.0;
    
    for (let item of items) {
-       total += item.price;
+       total += parseFloat(item.price);
    }
    
+   // 保留两位小数
+   total = Math.round(total * 100) / 100;
    return total;
}
```

![](https://www.runoob.com/wp-content/uploads/2019/03/653e1bce-e2d7-4c8b-8329-7b5ecfef3807.png)

**Git 风格的差异显示：**

```diff
@@ -1,5 +1,8 @@
 function greetUser(name) {
-    console.log("Hello " + name);
+    if (!name) {
+        throw new Error("Name is required");
+    }
+    console.log(`Hello, ${name}!`);
 }
```

**语言特定的差异对比：**

```javascript
// 之前的代码
const oldFunction = () => {
    var x = 10;  // &#x274c; 使用 var
    console.log("Value: " + x);  // &#x274c; 字符串拼接
}

// 改进后的代码  
const newFunction = () => {
    const x = 10;  // &#x2705; 使用 const
    console.log(`Value: ${x}`);  // &#x2705; 模板字符串
}
```

![](https://www.runoob.com/wp-content/uploads/2019/03/3ba07b77-1570-48b8-86dd-a041a52ece21.png)
