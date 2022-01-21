---
title: 正则表达式(Js)
tags:
  - JavaScript
categories:
  - 前端
abbrlink: ce934369
date: 2020-05-30 17:12:04
index_img: https://gitee.com/Stubborner/images/raw/master/images/9bd9b167gy1g4lhiguvj4j21hc0xc4bb.jpg
---

### 什么是正则表达式

正则表达式是表示搜索模式的特殊字符串。也被称为`"regex"`,`"regexp"`它们可以帮助程序员匹配、搜索和替换文本。

<!-- more -->

### 使用测试方法

测试正则表达式的一种方法是使用`.test()`方法。`.test()`方法会把你编写的正则表达式应用到一个字符串（即括号内的内容），如果你的匹配模式成功匹配到字符，则返回`true`，反之，返回`false`。如果你想在字符串`"Hello,World"`中匹配到`"Hello"`，可以使用如下正则表达式：`/Hello/`

```javascript
let hi="Hello,World";
let testRegex=/Hello/;
testRegex.test(hi);//true
```

### 同时用多种模式匹配文字字符串

你可以使用`|`操作符来匹配多个规则,例如，你可以使用`/are|lucky|dog/`在字符串`"You are a lucky dog"`中匹配到字符串`are,lucky,dog`

```javascript
let str="You are a lucky dog";
let testRegex=/are|lucky|dog/;
testRegex.test(str);//true
```

### 匹配时忽略大小写

有时候，你可能也想匹配不同的英文字母大小写，这时我们可以在正则表达式`/`结尾加上忽略大小写标志`i`,如下示例：

```javascript
let str="hello,world";
let testRegex=/Hello,WoRld/i;
testRegex.test(str)//true
```

### 提取匹配项

到目前为止，你只是检查了一个匹配模式是否存在于字符串中。你还可以使用`.match()`方法来提取你找到的实际匹配项。请使用字符串来调用`.match()`方法，并在括号内传入正则表达式。以下是一个示例：

```javascript
let str="hello,world";
let testRegex="hello";
str.match(testRegex);//return ["hello"]
```

### 全局匹配

到目前为止，你只能提取或搜寻一次匹配模式。若要多次搜寻或提取匹配模式，你可以使用`g`标志。以下是一个示例：

```javascript
let str="hello,hello,hello";
let testRegex=/hello/g;
str.match(testRegex);//Return ["hello","hello","hello"]
```

### 用通配符.匹配任何内容

通配符`.`将匹配任何一个字符。通配符也叫`dot`或`period`。你可以像使用正则表达式中任何其他字符一样使用通配符。例如，如果你想匹配`"hug"`、`"huh"`、`"hut"`和`"hum"`，你可以使用正则表达式`/hu./`匹配以上四个单词。以下是一个示例：

```javascript
let str="aaa,aab,aac,aad";
let testRegex=/aa./g;
str.match(testRegex);//Return ["aaa","aab","aac","aad"]
```

### 将单个字符与多种可能性匹配

你可以使用`字符集`搜寻具有一定灵活性的文字匹配模式。字符集允许你通过把它们放在方括号（`[`和`]`）之间的方式来定义一组你需要匹配的字符串。例如，你想要匹配`"bag"`、`"big"`和`"bug"`，但是不想匹配`"bog"`。你可以创建正则表达式`/b[aiu]g/`来执行此操作。`[aiu]`是只匹配字符`"a"`、`"i"`或者`"u"`的字符集。以下是示例：

```javascript
let str="bag,big,bug";
let testRegex=/b[aiu]g/g;
str.match(testRegex);//Return ["bag","big","bug"]
```

### 匹配字母表中的字母

在`字符集`中，你可以使用`连字符`（`-`）来定义要匹配的字符范围。例如，要匹配小写字母`a`到`e`，你可以使用`[a-e]`。示例如下：

```javascript
let str="cat,bat,mat";
let testRegex=/[b-m]at/g;
str.match(testRegex);//Return ["bat","cat","mat"]
```

### 匹配字母表中的数字和字母

使用连字符（`-`）匹配字符范围并不仅限于字母。它还可以匹配一系列数字。示例如下：

```javascript
let str="Hello,2020";
let testRegex=/[hello0-2]/gi;
str.match(testRegex);//Return ["H", "e", "l", "l", "o", "2", "0", "2", "0"]
```

### 匹配单个未指定的字符

到目前为止，你已创建了一个你想要匹配的字符集合，但你也可以创建一个你不想匹配的字符集合。这些类型的字符集称为`否定字符集`。

要创建`否定字符集`，你需要在开始括号后面和不想匹配的字符前面放置`插入字符`（即`^`）。

例如，`/[^aeiou]/gi`匹配所有非元音字符。注意，字符`.`、`!`、`[`、`@`、`/`和空白字符等也会被匹配，该否定字符集仅排除元音字符。示例如下：

```javascript
let str="abcdefg";
let testRegex=/[^a-c]/g;
str.match(testRegex);//Return ["d", "e", "f", "g"]
```

### 匹配出现一次或多次的字符

有时，你需要匹配出现一次或者连续多次的的字符（或字符组）。你可以使用`+`符号来检查情况是否如此。记住，字符或匹配模式必须一个接一个地连续出现。

例如，`/a+/g`会在`"abc"`中匹配到一个匹配项，并且返回`["a"]`。因为`+`的存在，它也会在`"aabc"`中匹配到一个匹配项，然后返回`["aa"]`。

如果它是检查字符串`"abab"`，它将匹配到两个匹配项并且返回`["a", "a"]`，因为`a`字符不连续，在它们之间有一个`b`字符。最后，因为在字符串`"bcd"`中没有`"a"`，因此找不到匹配项。示例如下：

```javascript
let str="abaabaaabbba";
let testRegex=/a+/g;
str.match(testRegex);//Return ["a", "aa", "aaa", "a"]
```

### 匹配出现零次或多次的字符

上一次的挑战中使用了加号`+`来查找出现一次或多次的字符。还有一个选项可以匹配出现零次或多次的字符。

执行该操作的字符叫做`asterisk`或`star`，即`*`。示例如下：

```javascript
let str="haaaaaaaa";
let str1="hgggggggg";
let textRegex=/ha*/;
str.match(textRegex);//Return ["haaaaaaaa"]
str1.match(textRegex);//Return ["h"]
```

### 用惰性匹配来查找字符

在正则表达式中，`贪婪`匹配会匹配到符合正则表达式匹配模式的字符串的最长可能部分，并将其作为匹配项返回。另一种方案称为`懒惰`匹配，它会匹配到满足正则表达式的字符串的最小可能部分。

你可以将正则表达式`/t[a-z]*i/`应用于字符串`"titanic"`。这个正则表达式是一个以`t`开始，以`i`结束，并且中间有一些字母的匹配模式。

正则表达式默认是`贪婪`匹配，因此匹配返回为`["titani"]`。它会匹配到适合该匹配模式的最大子字符串。

但是，你可以使用`?`字符来将其变成`懒惰`匹配。调整后的正则表达式`/t[a-z]*?i/`匹配字符串`"titanic"`返回`["ti"]`。

```javascript
let str="different";
let textRegex=/d[a-z]*e/;
let textRegex1=/d[a-z]*?e/;
str.match(textRegex);//Return ["differe"]
str.match(textRegex1);//Return ["diffe"]
```

### 在狩猎中找到一个或多个罪犯

群罪犯逃出监狱逃跑，但你不知道有多少人。但是，你知道他们和其他人在一起时会保持紧密联系。你有责任立刻找到所有的罪犯。

这里有一个示例来回顾如何做到这一点：

当字母`z`在一行中出现一次或连续多次时，正则表达式`/z+/`会匹配到它。它会在以下所有字符串中找到匹配项：

```javascript
"z"
"zzzzzz"
"ABCzzzz"
"zzzzABC"
"abczzzzzzzzzzzzzzzzzzzzzabc"
```

但是它不会在以下字符串中找到匹配项，因为它们中没有字母`z`：

```javascript
""
"ABC"
"abcabc"
```

编写一个`贪婪`正则表达式，在一组其他人中匹配到一个或多个罪犯。罪犯由大写字母`C`表示

```javascript
// example crowd gathering
let crowd = 'P1P2P3P4P5P6CCCP7P8P9';

let reCriminals = /./; // 修改这一行

let matchedCriminals = crowd.match(reCriminals);
console.log(matchedCriminals);
```

示例答案：

```javascript
// example crowd gathering
let crowd = 'P1P2P3P4P5P6CCCP7P8P9';

let reCriminals = /C+/; // 修改这一行

let matchedCriminals = crowd.match(reCriminals);
console.log(matchedCriminals);
```

### 匹配字符串的开头

你使用`字符集`中的`插入`符号（`^`）来创建一个`否定字符集`，形如`[^thingsThatWillNotBeMatched]`。在`字符集`之外，插入`^`符号用于字符串的开头搜寻匹配模式。

```javascript
let str="Hello,World";
let textRegex=/^Hello/;
let textRegex1=/^World/;
textRegex.test(str);//true
textRegex1.test(str);//false
```

### 匹配字符串的末尾

你可以使用正则表达式的`美元`符号`$`来搜寻字符串的结尾。

```javascript
let str="hello,world";
let str1="wold,hello";
let textRegex=/world$/;
textRegex.test(str);//true
textRegex.test(str1);//false
```

### 匹配所有的字母和数字

使用字符类，你可以使用`[a-z]`搜寻字母表中的所有字母。这种字符类是很常见的，它有一个缩写，但这个缩写也包含额外的字符。

JavaScript 中与字母表匹配的最接近的字符类是`\w`，这个缩写等同于`[A-Za-z0-9_]`。它不仅可以匹配大小写字母和数字，注意，它还会匹配下划线字符（`_`）。

```javascript
let str="Hello_World2020";
let testRegex=/\w+/;
str.match(testRegex);//Return ["Hello_World2020"]
```

### 匹配除了字母和数字的所有符号

你可以使用`\W`搜寻和`\w`相反的匹配模式。注意，相反匹配模式使用大写字母。此缩写与`[^A-Za-z0-9_]`是一样的

```javascript
let str="hello,World!";
let testRegex=/\W/g;
str.match(testRegex);//Return [",","!"]
```

### 匹配所有数字

查找数字字符的缩写是`\d`，注意是小写的`d`。这等同于字符类`[0-9]`，它查找 0 到 9 之间任意数字的单个字符。

```javascript
let str="0123hello";
let testRegex=/\d/g;
str.match(testRegex);//Return ["0","1","2","3"]
```

### 匹配所有非数字

查找非数字字符的缩写是`\D`。这等同于字符串`[^0-9]`，它查找不是 0 - 9 之间数字的单个字符。

```javascript
let str="hello2020world";
let testRegex=/\D/g;
str.match(testRegex);//Return ["h", "e", "l", "l", "o", "w", "o", "r", "l", "d"]
```

### 限制可能的用户名

你需要检查数据库中的所有用户名。以下是用户在创建用户名时必须遵守的一些简单规则。

1) 用户名中的数字必须在最后，且数字可以有零个或多个。

2) 用户名字母可以是小写字母和大写字母。

3) 用户名长度必须至少为两个字符。两位用户名只能使用字母。

修改正则表达式`userCheck`以适合上面列出的约束。

```javascript
let username = "JackOfAllTrades";
let userCheck = /change/; // 修改这一行
let result = userCheck.test(username);
```

示例答案：

```javascript
let username = "JackOfAllTrades";
let username1 = "Mike666";
let username2 = "KK";
let userCheck = /^[a-z]([0-9][0-9]+|[a-z]+[\d]*)$/i; // 修改这一行
userCheck.test(username);//false
userCheck.test(username1);//true
userCheck.test(username2);//true
```

### 匹配空白字符

你可以使用`\s`搜寻空格，其中`s`是小写。此匹配模式不仅匹配空格，还匹配回车符、制表符、换页符和换行符，你可以将其视为与`[\r\t\f\n\v]`类似。

```javascript
let str="hello hello hello ";
let testRegex=/\s/g;
str.match(testRegex);//Return  [" ", " ", " "]
```

### 匹配非空白字符

使用`\S`搜寻非空白字符，其中`S`是大写。此匹配模式将不匹配空格、回车符、制表符、换页符和换行符。你可以认为这类似于字符类`[^\r\t\f\n\v]`。

```javascript
let str="h h h h h";
let testRegex=/\S/g;
str.match(testRegex);//Return ["h", "h", "h", "h", "h"]
```

### 指定匹配的上限和下限

你使用加号`+`查找一个或多个字符，使用星号`*`查找零个或多个字符。这些都很方便，但有时你需要匹配一定范围的匹配模式。

你可以使用`数量说明符`指定匹配模式的上下限。数量说明符与花括号（`{`和`}`）一起使用。你可以在花括号之间放两个数字，这两个数字代表匹配模式的上限和下限。

```javascript
let str="haaakk";
let testRegex=/ha{1,3}/;
str.match(testRegex));//Return ["haaa"]
str.match(/ha{1,2}/);//Return ["haa"]
```

### 只指定匹配的下限

你可以使用带有花括号的`数量说明符`来指定匹配模式的上下限。但有时候你只想指定匹配模式的下限而不需要指定上限。

为此，在第一个数字后面跟一个逗号即可

```javascript
let str="haaaaa";
let str1="haaaaaaaa";
let testRegex=/ha{3,}/;
str.match(testRegex);//Return ["haaaaa"]
str1.match(testRegex);//Return ["haaaaaaaa"]
```

### 指定匹配的确切数量

要指定一定数量的匹配模式，只需在大括号之间放置一个数字。

```javascript
let str="helllllllo";
let testRegex=/hel{3}/;
str.match(testRegex);//Return ["helll"]
```

### 检查全部或无

有时，你想要搜寻的匹配模式可能有不确定是否存在的部分。尽管如此，你还是想检查它们。

为此，你可以使用问号`?`指定可能存在的元素。这将检查前面的零个或一个元素。你可以将此符号视为前面的元素是可选的

例如，美式英语和英式英语略有不同，你可以使用问号来匹配两种拼写

```javascript
let american = "color";
let british = "colour";
let rainbowRegex= /colou?r/;
rainbowRegex.test(american); // Returns true
rainbowRegex.test(british); // Returns true
```

### 正向先行断言和负向先行断言

`先行断言`是告诉 JavaScript 在字符串中向前查找的匹配模式。当你想要在同一个字符串上搜寻多个匹配模式时，这可能非常有用。

有两种`先行断言`：`正向先行断言`和`负向先行断言`。

`正向先行断言`会查看并确保搜索匹配模式中的元素存在，但实际上并不匹配。正向先行断言的用法是`(?=...)`，其中`...`就是需要存在但不会被匹配的部分。

另一方面，`负向先行断言`会查看并确保搜索匹配模式中的元素不存在。负向先行断言的用法是`(?!...)`，其中`...`是你希望不存在的匹配模式。如果负向先行断言部分不存在，将返回匹配模式的其余部分

```javascript
let quit = "qu";
let noquit = "qt";
let quRegex= /q(?=u)/;
let qRegex = /q(?!u)/;
quit.match(quRegex); // Returns ["q"]
noquit.match(qRegex); // Returns ["q"]
```

`先行断言`的更实际用途是检查一个字符串中的两个或更多匹配模式。这里有一个简单的密码检查器，密码规则是 3 到 6 个字符且至少包含一个数字：

```javascript
let password = "abc123";
let checkPass = /(?=\w{3,6})(?=\D*\d)/;
checkPass.test(password); // Returns true
```

### 使用捕获组重用模式

一些你所搜寻的匹配模式会在字符串中出现多次，手动重复该正则表达式太浪费了。有一种更好的方法可以指定何时在字符串中会有多个重复的子字符串。

你可以使用`捕获组`搜寻重复的子字符串。括号`(`和`)`可以用来匹配重复的子字符串。你只需要把重复匹配模式的正则表达式放在括号中即可。

要指定重复字符串将出现的位置，可以使用反斜杠（`\`）后接一个数字。这个数字从 1 开始，随着你使用的每个捕获组的增加而增加。这里有一个示例，`\1`可以匹配第一个组。

下面的示例匹配任意两个被空格分割的单词：

```javascript
let repeatStr = "regex regex";
let repeatRegex = /(\w+)\s\1/;
repeatRegex.test(repeatStr); // Returns true
repeatStr.match(repeatRegex); // Returns ["regex regex", "regex"]
```

在字符串上使用`.match()`方法将返回一个数组，其中包含它匹配的字符串及其捕获组

### 使用捕获组搜索和替换

搜索功能是很有用的。但是，当你的搜索也执行更改（或替换）匹配文本的操作时，搜索功能就会显得更加强大。

可以使用字符串上`.replace()`方法来搜索并替换字符串中的文本。`.replace()`的输入首先是你想要搜索的正则表达式匹配模式，第二个参数是用于替换匹配的字符串或用于执行某些操作的函数。

```javascript
let wrongText = "The sky is silver.";
let silverRegex = /silver/;
wrongText.replace(silverRegex, "blue");
// Returns "The sky is blue."
```

你还可以使用美元符号（`$`）访问替换字符串中的捕获组。

```javascript
"Code Camp".replace(/(\w+)\s(\w+)/, '$2 $1');
// Returns "Camp Code"
```

### 删除开头和结尾的空白

编写一个正则表达式并使用适当的字符串方法删除字符串开头和结尾的空格。

```javascript
let hello = "   Hello, World!  ";
let wsRegex = /^\s+|\s+$/g; 
let result = hello.replace(wsRegex, "");
```