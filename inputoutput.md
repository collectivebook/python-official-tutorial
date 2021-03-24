  7\. 输入与输出 — Python 3.10.0a6 文档                   @media only screen { table.full-width-table { width: 100%; } }   

### 导航

*   [索引](https://docs.python.org/zh-cn/3/genindex.html "总目录")
*   [模块](https://docs.python.org/zh-cn/3/py-modindex.html "Python 模块索引") |
*   [下一页](errors.md "8. 错误和异常") |
*   [上一页](modules.md "6. 模块") |
*   ![](https://docs.python.org/zh-cn/3/_static/py.png)
*   [Python](https://www.python.org/) »
*   [3.10.0a6 Documentation](https://docs.python.org/zh-cn/3/index.html) »
*   [Python 教程](index.md) »
*   7\. 输入与输出
*      
    
    $('.inline-search').show(0); |

# 7\. 输入与输出[¶](#input-and-output "永久链接至标题")

程序输出有几种显示方式；数据既可以输出为人类可读的形式，也可以写入文件备用。本章探讨一些可用的方式。

## 7.1. 更复杂的输出格式[¶](#fancier-output-formatting "永久链接至标题")

至此，我们已学习了两种写入值的方法：_表达式语句_ 和 [`print()`](https://docs.python.org/zh-cn/3/library/functions.html#print "print") 函数。第三种方法是使用文件对象的 `write()` 方法；标准输出文件称为 `sys.stdout`。详见标准库参考。

对输出格式的控制不只是打印空格分隔的值，还需要更多方式。格式化输出有以下几种方法。

*   使用 [格式化字符串字面值](#tut-f-strings) ，要在字符串开头的引号或三引号前添加 `f` 或 `F` 。在此字符串中，可以在 `{` 和 `}` 字符之间输入引用的变量或字面值的 Python 表达式。
    
    \>>> year \= 2016
    \>>> event \= 'Referendum'
    \>>> f'Results of the {year} {event}'
    'Results of the 2016 Referendum'
    
*   字符串的 [`str.format()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.format "str.format") 方法需要更多的手动操作。该方法仍使用 `{` 和 `}` 标记要替换的变量的位置，该方法还支持详细的格式化指令，但需要提供格式化信息。
    
    \>>> yes\_votes \= 42\_572\_654
    \>>> no\_votes \= 43\_132\_495
    \>>> percentage \= yes\_votes / (yes\_votes + no\_votes)
    \>>> '{:-9} YES votes {:2.2%}'.format(yes\_votes, percentage)
    ' 42572654 YES votes  49.67%'
    
*   最后，还可以用字符串切片和合并完成各种字符串处理操作，创建任何想要的排版布局。字符串类型还支持将字符串按给定列宽进行填充，这些方法也很有用。
    

如果不需要花哨的输出，只想快速显示变量以进行调试，可以用 [`repr()`](https://docs.python.org/zh-cn/3/library/functions.html#repr "repr") 或 [`str()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str "str") 函数把值转化为字符串。

[`str()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str "str") 函数返回适于人类阅读的值，[`repr()`](https://docs.python.org/zh-cn/3/library/functions.html#repr "repr") 则生成适于解释器读取的值（如果没有等效的语法，则强制执行 [`SyntaxError`](https://docs.python.org/zh-cn/3/library/exceptions.html#SyntaxError "SyntaxError")）。对于没有适合人类阅读展示结果的对象， [`str()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str "str") 返回与 [`repr()`](https://docs.python.org/zh-cn/3/library/functions.html#repr "repr") 一样的值。一般情况下，数字、列表或字典等结构的值，使用这两个函数输出的展现形式是一样的。字符串则不同，有两种不同的展现形式。

示例如下：

\>>> s \= 'Hello, world.'
\>>> str(s)
'Hello, world.'
\>>> repr(s)
"'Hello, world.'"
\>>> str(1/7)
'0.14285714285714285'
\>>> x \= 10 \* 3.25
\>>> y \= 200 \* 200
\>>> s \= 'The value of x is ' + repr(x) + ', and y is ' + repr(y) + '...'
\>>> print(s)
The value of x is 32.5, and y is 40000...
\>>> \# The repr() of a string adds string quotes and backslashes:
... hello \= 'hello, world\\n'
\>>> hellos \= repr(hello)
\>>> print(hellos)
'hello, world\\n'
\>>> \# The argument to repr() may be any Python object:
... repr((x, y, ('spam', 'eggs')))
"(32.5, 40000, ('spam', 'eggs'))"

[`string`](https://docs.python.org/zh-cn/3/library/string.html#module-string "string: Common string operations.") 模块包含一个叫 [`Template`](https://docs.python.org/zh-cn/3/library/string.html#string.Template "string.Template") 的类，提供了另一种将值替换为字符串的方法。该类使用 `$x` 占位符，并用字典的值进行替换，但这种方式对格式控制的支持比较有限。

### 7.1.1. 格式化字符串字面值[¶](#formatted-string-literals "永久链接至标题")

[格式化字符串字面值](https://docs.python.org/zh-cn/3/reference/lexical_analysis.html#f-strings) （简称为 f-字符串）在字符串前添加前缀 `f` 或 `F`，通赤 `{expression}` 的形式输入表达式，从而把 Python 表达式的值包含在字符串内。

格式说明符在表达式后面，是可选的，该说明符可以更好地控制值的格式化方式。下例将 pi 舍入到小数点后三位：

\>>> import math
\>>> print(f'The value of pi is approximately {math.pi:.3f}.')
The value of pi is approximately 3.142.

在 `':'` 后传递整数，为该字段设置最小字符宽度。这种操作常用于列对齐：

\>>> table \= {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 7678}
\>>> for name, phone in table.items():
...     print(f'{name:10} ==> {phone:10d}')
...
Sjoerd     ==>       4127
Jack       ==>       4098
Dcab       ==>       7678

下述修饰符用于在格式化前转换值。 `'!a'` 应用 [`ascii()`](https://docs.python.org/zh-cn/3/library/functions.html#ascii "ascii") ，`'!s'` 应用 [`str()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str "str")，`'!r'` 应用 [`repr()`](https://docs.python.org/zh-cn/3/library/functions.html#repr "repr")：

\>>> animals \= 'eels'
\>>> print(f'My hovercraft is full of {animals}.')
My hovercraft is full of eels.
\>>> print(f'My hovercraft is full of {animals!r}.')
My hovercraft is full of 'eels'.

有关格式规范的参考，详见参考指南 [格式规格迷你语言](https://docs.python.org/zh-cn/3/library/string.html#formatspec)。

### 7.1.2. 字符串 format() 方法[¶](#the-string-format-method "永久链接至标题")

[`str.format()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.format "str.format") 方法的基本用法如下所示：

\>>> print('We are the {} who say "{}!"'.format('knights', 'Ni'))
We are the knights who say "Ni!"

花括号和其中的字符（称为格式字段）将替换为传递给 [`str.format()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.format "str.format") 方法的对象。花括号中的数字可用来表示传递给 [`str.format()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.format "str.format") 方法的对象的位置。

\>>> print('{0} and {1}'.format('spam', 'eggs'))
spam and eggs
\>>> print('{1} and {0}'.format('spam', 'eggs'))
eggs and spam

如果在 [`str.format()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.format "str.format") 方法中使用关键字参数，则使用参数的名称引用它们的值。:

\>>> print('This {food} is {adjective}.'.format(
...       food\='spam', adjective\='absolutely horrible'))
This spam is absolutely horrible.

位置和关键字参数可以任意组合:

\>>> print('The story of {0}, {1}, and {other}.'.format('Bill', 'Manfred',
 other='Georg'))
The story of Bill, Manfred, and Georg.

如果你有一个非常长的格式字符串，你不想把它拆开，那么你最好是按名称而不是按位置引用变量来进行格式化。 这可以通过简单地传递字典并使用方括号 `'[]'` 访问键来完成。

\>>> table \= {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
\>>> print('Jack: {0\[Jack\]:d}; Sjoerd: {0\[Sjoerd\]:d}; '
...       'Dcab: {0\[Dcab\]:d}'.format(table))
Jack: 4098; Sjoerd: 4127; Dcab: 8637678

这也可以通过使用 '\*\*' 符号将 table 作为关键字参数传递。

\>>> table \= {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
\>>> print('Jack: {Jack:d}; Sjoerd: {Sjoerd:d}; Dcab: {Dcab:d}'.format(\*\*table))
Jack: 4098; Sjoerd: 4127; Dcab: 8637678

这在与内置函数 [`vars()`](https://docs.python.org/zh-cn/3/library/functions.html#vars "vars") 结合使用时非常有用，它会返回包含所有局部变量的字典。

例如，下面几行代码生成一组整齐的列，其中包含给定的整数和它的平方以及立方:

\>>> for x in range(1, 11):
...     print('{0:2d} {1:3d} {2:4d}'.format(x, x\*x, x\*x\*x))
...
 1   1    1
 2   4    8
 3   9   27
 4  16   64
 5  25  125
 6  36  216
 7  49  343
 8  64  512
 9  81  729
10 100 1000

关于使用 [`str.format()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.format "str.format") 进行字符串格式化的完整概述，请参阅 [格式字符串语法](https://docs.python.org/zh-cn/3/library/string.html#formatstrings) 。

### 7.1.3. 手动格式化字符串[¶](#manual-string-formatting "永久链接至标题")

这是同一个平方和立方的表，手动格式化的:

\>>> for x in range(1, 11):
...     print(repr(x).rjust(2), repr(x\*x).rjust(3), end\=' ')
...     \# Note use of 'end' on previous line
...     print(repr(x\*x\*x).rjust(4))
...
 1   1    1
 2   4    8
 3   9   27
 4  16   64
 5  25  125
 6  36  216
 7  49  343
 8  64  512
 9  81  729
10 100 1000

（注意每列之间的一个空格是通过使用 [`print()`](https://docs.python.org/zh-cn/3/library/functions.html#print "print") 的方式添加的：它总是在其参数间添加空格。）

字符串对象的 [`str.rjust()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.rjust "str.rjust") 方法通过在左侧填充空格来对给定宽度的字段中的字符串进行右对齐。类似的方法还有 [`str.ljust()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.ljust "str.ljust") 和 [`str.center()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.center "str.center") 。这些方法不会写入任何东西，它们只是返回一个新的字符串，如果输入的字符串太长，它们不会截断字符串，而是原样返回；这虽然会弄乱你的列布局，但这通常比另一种方法好，后者会在显示值时可能不准确（如果你真的想截断，你可以添加一个切片操作，例如 `x.ljust(n)[:n]` 。）

还有另外一个方法，[`str.zfill()`](https://docs.python.org/zh-cn/3/library/stdtypes.html#str.zfill "str.zfill") ，它会在数字字符串的左边填充零。它能识别正负号:

\>>> '12'.zfill(5)
'00012'
\>>> '-3.14'.zfill(7)
'-003.14'
\>>> '3.14159265359'.zfill(5)
'3.14159265359'

### 7.1.4. 旧的字符串格式化方法[¶](#old-string-formatting "永久链接至标题")

% 运算符（求余）也可用于字符串格式化。 给定 `'string' % values`，则 `string` 中的 `%` 实例会以零个或多个 `values` 元素替换。 此操作通常被称为字符串插值。 例如:

\>>> import math
\>>> print('The value of pi is approximately %5.3f.' % math.pi)
The value of pi is approximately 3.142.

可在 [printf 风格的字符串格式化](https://docs.python.org/zh-cn/3/library/stdtypes.html#old-string-formatting) 部分找到更多信息。

## 7.2. 读写文件[¶](#reading-and-writing-files "永久链接至标题")

[`open()`](https://docs.python.org/zh-cn/3/library/functions.html#open "open") 返回一个 [file object](https://docs.python.org/zh-cn/3/glossary.html#term-file-object)，最常用的有两个参数： `open(filename, mode)`。

\>>> f \= open('workfile', 'w')

第一个参数是包含文件名的字符串。第二个参数是另一个字符串，其中包含一些描述文件使用方式的字符。_mode_ 可以是 `'r'` ，表示文件只能读取，`'w'` 表示只能写入（已存在的同名文件会被删除），还有 `'a'` 表示打开文件以追加内容；任何写入的数据会自动添加到文件的末尾。`'r+'` 表示打开文件进行读写。_mode_ 参数是可选的；省略时默认为 `'r'`。

通常文件是以 _text mode_ 打开的，这意味着从文件中读取或写入字符串时，都会以指定的编码方式进行编码。如果未指定编码格式，默认值与平台相关 (参见 [`open()`](https://docs.python.org/zh-cn/3/library/functions.html#open "open"))。在mode 中追加的 `'b'` 则以 _binary mode_ 打开文件：现在数据是以字节对象的形式进行读写的。这个模式应该用于所有不包含文本的文件。

在文本模式下读取时，默认会把平台特定的行结束符 (Unix 上的 `\n`, Windows 上的 `\r\n`) 转换为 `\n`。在文本模式下写入时，默认会把出现的 `\n` 转换回平台特定的结束符。这样在幕后修改文件数据对文本文件来说没有问题，但是会破坏二进制数据例如 `JPEG` 或 `EXE` 文件中的数据。请一定要注意在读写此类文件时应使用二进制模式。

在处理文件对象时，最好使用 [`with`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#with) 关键字。 优点是当子句体结束后文件会正确关闭，即使在某个时刻引发了异常。 而且使用 `with` 相比等效的 [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try)\-[`finally`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#finally) 代码块要简短得多:

\>>> with open('workfile') as f:
...     read\_data \= f.read()

\>>> \# We can check that the file has been automatically closed.
\>>> f.closed
True

如果你没有使用 [`with`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#with) 关键字，则你应当调用 `f.close()` 来关闭文件并立即释放它所使用的任何系统资源。

警告

调用 `f.write()` 时未使用 `with` 关键字或未调用 `f.close()` **可能** 导致 `f.write()` 的参数没有完全写入到磁盘，即使程序是正常退出的。

通过 [`with`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#with) 语句或者调用 `f.close()` 关闭文件对象后，尝试使用该文件对象将自动失败。:

\>>> f.close()
\>>> f.read()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: I/O operation on closed file.

### 7.2.1. 文件对象的方法[¶](#methods-of-file-objects "永久链接至标题")

本节中剩下的例子将假定你已创建名为 `f` 的文件对象。

要读取文件内容，请调用 `f.read(size)`，它会读取一些数据并将其作为字符串（在文本模式下）或字节串对象（在二进制模式下）返回。 _size_ 是一个可选的数值参数。 当 _size_ 被省略或者为负数时，将读取并返回整个文件的内容；如果文件的大小是你的机器内存的两倍就会出现问题。 当取其他值时，将读取并返回至多 _size_ 个字符（在文本模式下）或 _size_ 个字节（在二进制模式下）。 如果已到达文件末尾，`f.read()` 将返回一个空字符串 (`''`)。

\>>> f.read()
'This is the entire file.\\n'
\>>> f.read()
''

`f.readline()` 从文件中读取一行；换行符（`\n`）留在字符串的末尾，如果文件不以换行符结尾，则在文件的最后一行省略。这使得返回值明确无误；如果 `f.readline()` 返回一个空的字符串，则表示已经到达了文件末尾，而空行使用 `'\n'` 表示，该字符串只包含一个换行符。:

\>>> f.readline()
'This is the first line of the file.\\n'
\>>> f.readline()
'Second line of the file\\n'
\>>> f.readline()
''

要从文件中读取行，你可以循环遍历文件对象。这是内存高效，快速的，并简化代码:

\>>> for line in f:
...     print(line, end\='')
...
This is the first line of the file.
Second line of the file

如果你想以列表的形式读取文件中的所有行，你也可以使用 `list(f)` 或 `f.readlines()`。

`f.write(string)` 会把 _string_ 的内容写入到文件中，并返回写入的字符数。:

\>>> f.write('This is a test\\n')
15

在写入其他类型的对象之前，需要先把它们转化为字符串（在文本模式下）或者字节对象（在二进制模式下）:

\>>> value \= ('the answer', 42)
\>>> s \= str(value)  \# convert the tuple to string
\>>> f.write(s)
18

`f.tell()` 返回一个整数，给出文件对象在文件中的当前位置，表示为二进制模式下时从文件开始的字节数，以及文本模式下的意义不明的数字。

要改变文件对象的位置，请使用 `f.seek(offset, whence)`。 通过向一个参考点添加 _offset_ 来计算位置；参考点由 _whence_ 参数指定。 _whence_ 的 0 值表示从文件开头起算，1 表示使用当前文件位置，2 表示使用文件末尾作为参考点。 _whence_ 如果省略则默认值为 0，即使用文件开头作为参考点。

\>>> f \= open('workfile', 'rb+')
\>>> f.write(b'0123456789abcdef')
16
\>>> f.seek(5)      \# Go to the 6th byte in the file
5
\>>> f.read(1)
b'5'
\>>> f.seek(\-3, 2)  \# Go to the 3rd byte before the end
13
\>>> f.read(1)
b'd'

在文本文件（那些在模式字符串中没有 `b` 的打开的文件）中，只允许相对于文件开头搜索（使用 `seek(0, 2)` 搜索到文件末尾是个例外）并且唯一有效的 _offset_ 值是那些能从 `f.tell()` 中返回的或者是零。其他 _offset_ 值都会产生未定义的行为。

文件对象有一些额外的方法，例如 `isatty()` 和 `truncate()` ，它们使用频率较低；有关文件对象的完整指南请参阅库参考。

### 7.2.2. 使用 [`json`](https://docs.python.org/zh-cn/3/library/json.html#module-json "json: Encode and decode the JSON format.") 保存结构化数据[¶](#saving-structured-data-with-json "永久链接至标题")

字符串可以很轻松地写入文件并从文件中读取出来。数字可能会费点劲，因为 `read()` 方法只能返回字符串，这些字符串必须传递给类似 [`int()`](https://docs.python.org/zh-cn/3/library/functions.html#int "int") 的函数，它会接受类似 `'123'` 这样的字符串并返回其数字值 123。当你想保存诸如嵌套列表和字典这样更复杂的数据类型时，手动解析和序列化会变得复杂。

Python 允许你使用称为 [JSON (JavaScript Object Notation)](http://json.org) 的流行数据交换格式，而不是让用户不断的编写和调试代码以将复杂的数据类型保存到文件中。名为 [`json`](https://docs.python.org/zh-cn/3/library/json.html#module-json "json: Encode and decode the JSON format.") 的标准模块可以采用 Python 数据层次结构，并将它们转化为字符串表示形式；这个过程称为 _serializing_ 。从字符串表示中重建数据称为 _deserializing_ 。在序列化和反序列化之间，表示对象的字符串可能已存储在文件或数据中，或通过网络连接发送到某个远程机器。

注解

JSON格式通常被现代应用程序用于允许数据交换。许多程序员已经熟悉它，这使其成为互操作性的良好选择。

如果你有一个对象 `x` ，你可以用一行简单的代码来查看它的 JSON 字符串表示:

\>>> import json
\>>> json.dumps(\[1, 'simple', 'list'\])
'\[1, "simple", "list"\]'

[`dumps()`](https://docs.python.org/zh-cn/3/library/json.html#json.dumps "json.dumps") 函数的另一个变体叫做 [`dump()`](https://docs.python.org/zh-cn/3/library/json.html#json.dump "json.dump") ，它只是将对象序列化为 [text file](https://docs.python.org/zh-cn/3/glossary.html#term-text-file) 。因此，如果 `f` 是一个 [text file](https://docs.python.org/zh-cn/3/glossary.html#term-text-file) 对象，我们可以这样做:

json.dump(x, f)

要再次解码对象，如果 `f` 是一个打开的以供阅读的 [text file](https://docs.python.org/zh-cn/3/glossary.html#term-text-file) 对象:

x \= json.load(f)

这种简单的序列化技术可以处理列表和字典，但是在JSON中序列化任意类的实例需要额外的努力。 [`json`](https://docs.python.org/zh-cn/3/library/json.html#module-json "json: Encode and decode the JSON format.") 模块的参考包含对此的解释。

参见

[`pickle`](https://docs.python.org/zh-cn/3/library/pickle.html#module-pickle "pickle: Convert Python objects to streams of bytes and back.") - 封存模块

与 [JSON](#tut-json) 不同，_pickle_ 是一种允许对任意复杂 Python 对象进行序列化的协议。因此，它为 Python 所特有，不能用于与其他语言编写的应用程序通信。默认情况下它也是不安全的：如果数据是由熟练的攻击者精心设计的，则反序列化来自不受信任来源的 pickle 数据可以执行任意代码。

### [目录](https://docs.python.org/zh-cn/3/contents.html)

*   [7\. 输入与输出](#)
    *   [7.1. 更复杂的输出格式](#fancier-output-formatting)
        *   [7.1.1. 格式化字符串字面值](#formatted-string-literals)
        *   [7.1.2. 字符串 format() 方法](#the-string-format-method)
        *   [7.1.3. 手动格式化字符串](#manual-string-formatting)
        *   [7.1.4. 旧的字符串格式化方法](#old-string-formatting)
    *   [7.2. 读写文件](#reading-and-writing-files)
        *   [7.2.1. 文件对象的方法](#methods-of-file-objects)
        *   [7.2.2. 使用 `json` 保存结构化数据](#saving-structured-data-with-json)

#### 上一个主题

[6\. 模块](modules.md "上一章")

#### 下一个主题

[8\. 错误和异常](errors.md "下一章")

### 本页

*   [提交 Bug](https://docs.python.org/zh-cn/3/bugs.html)
*   [显示源代码](https://github.com/python/cpython/blob/master/Doc/tutorial/inputoutput.rst)

### 导航

*   [索引](https://docs.python.org/zh-cn/3/genindex.html "总目录")
*   [模块](https://docs.python.org/zh-cn/3/py-modindex.html "Python 模块索引") |
*   [下一页](errors.md "8. 错误和异常") |
*   [上一页](modules.md "6. 模块") |
*   ![](https://docs.python.org/zh-cn/3/_static/py.png)
*   [Python](https://www.python.org/) »
*   [3.10.0a6 Documentation](https://docs.python.org/zh-cn/3/index.html) »
*   [Python 教程](index.md) »
*   7\. 输入与输出
*      
    
    $('.inline-search').show(0); |

© [版权所有](https://docs.python.org/zh-cn/3/copyright.html) 2001-2021, Python Software Foundation.  
This page is licensed under the Python Software Foundation License Version 2.  
Examples, recipes, and other code in the documentation are additionally licensed under the Zero Clause BSD License.  
See History and License for more information.  
  
The Python Software Foundation is a non-profit corporation. [Please donate.](https://www.python.org/psf/donations/)  
  
最后更新于 3月 19, 2021. [Found a bug](https://docs.python.org/3/bugs.html)?  
Created using [Sphinx](https://www.sphinx-doc.org/) 3.2.1.
