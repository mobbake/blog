---
title: yaml 语法
date: 2017-09-25 10:27:55
tags: yaml
categories: 知识储备
---
#### 搭建hexo博客时经常要配置yml文件，于是搜一些yaml语法文档，做一些总结

### 语法规则 

它的基本语法规则如下：

- 大小写敏感

- 使用缩进表示层级关系

- 缩进时不允许使用 Tab 键，只允许使用空格

- 缩进的空格数目不重要，只要相同层级的元素左侧对齐即可


### 语法学习

`NOTE:`YAML 文件没有强制后缀名，只要内容格式对，解析器就能解析成功，和后缀无关。

#### 支持的数据格式：

1.对象：键值对的集合，又称映射(mapping) / 哈希（hashes）/ 字典(dictionary)

2.数组: 一组按次序排列的值，又称序列(sequence) / 列表(list)

3.纯量(scalars)：单个的，不可再分的值

以下分别介绍这三种数据格式

### 对象

对象的一组键值对，是用冒号结构来表示

`animal: pets`

转为JavaScript

`{ animal: 'pets' }`

fYAML也支持另一种写法，将所有的键值对写成一个行内对象

`hash: { name: steve, foo: bar }`

转为JavaScript

`{ hash: { name: 'steve', foo: 'bar'}}`

### 数组

一组连词线开头的行，构成一个数组
```
- Cat
- Dog
- Goldfish
```
转为JavaScript

`[ 'Cat', 'Dog', 'Goldfish' ]`

数据的子结构也是一个数组，可以在该项下面缩进空格来表示层级关系
```
-
  - Cat
  - Dog
  - Goldfish
```
转为JavaScript

`[ [ 'Cat', 'Dog', 'Goldfish'] ]`

数组也可以采用行内表示法

animal: [Cat, Dog]

转为JavaScript

{ animal: ['Cat', 'Dog']}

### 复合结构

对象和数组可以结合使用，形成复合结构
```
languages:
  - Ruby
  - Perl
  - Python
websites:
  YAML: yaml.org
  Ruby: ruby-lang.org
  Python: python.org
  Perl: user.perl.org
```
转为JavaScript
```
{
  languages: [ 'Ruby', 'Perl', 'Python'],
  websites:
  {
    YAML: 'yaml.org',
    Ruby: 'ruby-lang.org',
    Python: 'python.org',
    Perl: 'user.perl.org'
  }
}
```
### 纯量

纯量是最基本的、不可再分的值。 以下数据类型都是javaScript的纯量。

 - 字符串
 - 布尔值
 - 整数
 - 浮点数
 - null
 - 时间
 - 日期

数值直接以字面量的形式表示

`number: 12.30`

转为JavaScript

`{ number: 12.30 }`

布尔值以true 和false 来表示

`isSet: true`

转为JavaScript

`{ isSet: true }`

null用 ~ 表示

`parent: ~`

转为JavaScript

`{ parent: null }`

时间用 ISO8601 格式

`iso8601: 2001-12-14t21:59:43.10-05:00`

转为JavaScript

`{ iso8601: new Date('2001-12-14t21:59:43.10-05:00') }`

日期采用复合 ISO8601 格式的年、月、日表示

`date: 1976-12-20`

转为JavaScript

`{ date: new Date('1976-12-20') }`

**fYAML 允许使用两个感叹号，强制转换数据类型**
```
e: !!str 123
f: !!str true
```
转为JavaScript

`{ e: '123', f: 'true'}`

### 字符串

字符串是最常见，也是最复杂的一种数据类型。 字符串默认不适用引号表示。

`str : 这是一行字符串`

转为JavaScript

`{ str: '这是一行字符串'}`

如果字符串之间存在空格或其他特殊字符，需放在单引号之中。

`str: '内容: 字符串'`

转为JavaScript

`{ str: '内容: 字符串'}`

*单引号和双引号都可以使用，双引号不会对特殊字符进行转义。*
```
s1: '内容\n字符串'
s2: "内容\n字符串"
```
转为JavaScript

`{ s1: '内容\\n字符串', s2: '内容\n字符串'}`

单引号之中如果还有单引号，必须连续使用两个单引号进行转义

`str: 'labor''s day'`

转为JavaScript

`{ str: 'labor\'s day'}`

字符串可以写成多行，从第二行开始，必须有一个单空格缩进。换行符会被转为空格。
```
str: 这是一段
  多行
  字符串
```
转为JavaScript

`{ str: '这是一段 多行 字符串'}`

多行字符串可以采用 | 保留换行符，也可以使用 > 折叠换行。
```
this: |
  Foo
  Bar
that: >
  Foo
  Bar
```
转为JavaScript

`{ this: 'Foo\nBar\n', that:'Foo Bar\n' }`

“ + ” 表示保留文字块末尾的换行，-表示删除字符串末尾的换行。
```
s1: |
      Foo

s2: |+
    Foo

s3: |-
    Foo
```
转为JavaScript

`{ s1: 'Foo\n', s2: 'Foo\n\n\n', s3:'Foo' }`

字符串之中可以插入 HTML 标记
```
message: |

    <p style="color: red">
        段落
    </p>
```
转为JavaScript

`{ message: '\n<p style="color: red">\n 段落\n</p>\n' }`

### 引用

锚点 & 和别名 * , 可以用来引用
```
defaults: &defaults
    adapter: postgres
    host: localhost

development:
   database: myapp_development,
   <<: *defaults

test:
    database: myapp_test,
    <<: *defaults
```

相当于

```
defaults: 
    adapter: postgres
    host: localhost

development:
    database: myapp_development,
    adapter: postgres
    host: localhost

test:
    database: myapp_test,
    adapter: postgres
    host: localhost
```

&用来建立锚点（defaults），<<表示合并到当前数据，*用来引用锚点。

下面另外一个例子

```
- &showell Steve 
- Clark 
- Brian 
- Oren 
- *showell
```

转为JavaScript

`[ 'Steve', 'Clark', 'Brian', 'Oren', 'Steve' ]`

函数和正则表达式的转换

这是fjs-yaml库特有的功能，可以把函数和正则表达式转为字符串
```
#exmaple.yml
fn: function() { return 1 }
reg: /test/
```
解析上面的yml文件代码如下:
```
var yaml = require('js-yaml');
var fs = require('fs');
try{
    var doc = yaml.load(
        fs.readFileSync('./example.yml', 'utf8')
   );
} catch(e){
    console.warn(e);
}
```
从javaScript对象还原到yaml代码如下：
```
var yaml = require('js-yaml');
var fs = require('fs');
var obj = {
    fn: function() { return 1 },
    reg: /test/
 }

try{
    fs.writeFileSync('./exmaple.js', yama.dump(obj), 'utf8')
} catch(e) {
    console.log(e);
}
```
>参考链接
- [YAML 语言教程](http://www.ruanyifeng.com/blog/2016/07/yaml.html?f=tt)
- [YAML 1.2 规格](http://www.yaml.org/spec/1.2/spec.html)