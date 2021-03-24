  Python 教程 — Python 3.10.0a6 文档                   @media only screen { table.full-width-table { width: 100%; } }   

### 导航

*   [索引](https://docs.python.org/zh-cn/3/genindex.html "总目录")
*   [模块](https://docs.python.org/zh-cn/3/py-modindex.html "Python 模块索引") |
*   [下一页](appetite.md "1. 课前甜点") |
*   [上一页](https://docs.python.org/zh-cn/3/whatsnew/changelog.html "更新日志") |
*   ![](https://docs.python.org/zh-cn/3/_static/py.png)
*   [Python](https://www.python.org/) »
*   [3.10.0a6 Documentation](https://docs.python.org/zh-cn/3/index.html) »
*   Python 教程
*      
    
    $('.inline-search').show(0); |

# Python 教程[¶](#the-python-tutorial "永久链接至标题")

Python 是一种易于学习又功能强大的编程语言。它提供了高效的高级数据结构，还能简单有效地面向对象编程。Python 优雅的语法和动态类型，以及解释型语言的本质，使它成为多数平台上写脚本和快速开发应用的理想语言。

Python 解释器及丰富的标准库，提供了适用于各个主要系统平台的源码或机器码，这些可以到 Python 官网 [https://www.python.org/](https://www.python.org/) 免费获取，并可自由地分发。许多免费的第三方 Python 模块、程序、工具和它们的文档，也能在这个网站上找到对应内容或链接。

Python 解释器易于扩展，可以使用 C 或 C++（或者其他可以通过 C 调用的语言）扩展新的功能和数据类型。Python 也可用于可定制化软件中的扩展程序语言。

这个教程非正式地介绍了 Python 语言和系统的基本概念和功能。最好在阅读的时候准备一个 Python 解释器进行练习。所有的例子都是相互独立的，所以这个教程也可以离线阅读。

有关标准的对象和模块，请参阅 [Python 标准库](https://docs.python.org/zh-cn/3/library/index.html#library-index)。[Python 语言参考手册](https://docs.python.org/zh-cn/3/reference/index.html#reference-index) 提供了更正式的语言定义。想要编写 C 或者 C++ 扩展可以参考 [扩展和嵌入 Python 解释器](https://docs.python.org/zh-cn/3/extending/index.html#extending-index) 和 [Python/C API 参考手册](https://docs.python.org/zh-cn/3/c-api/index.html#c-api-index)。另外还有不少书籍深入讲解 Python。

这个教程并没有完整地介绍每一个功能，甚至可能没有涉及全部的常用功能。这个教程只介绍 Python 中最值得注意的功能，也会让你体会到这个语言的风格特色。学习完这个教程，你将可以阅读和编写 Python 模块和程序，也可以开始学习 [Python 标准库](https://docs.python.org/zh-cn/3/library/index.html#library-index)。

[术语对照表](https://docs.python.org/zh-cn/3/glossary.html#glossary) 也很值得一读。

*   [1\. 课前甜点](appetite.md)
*   [2\. Python 解释器](interpreter.md)
    *   [2.1. 调用解释器](interpreter.md#invoking-the-interpreter)
        *   [2.1.1. 传入参数](interpreter.md#argument-passing)
        *   [2.1.2. 交互模式](interpreter.md#interactive-mode)
    *   [2.2. 解释器的运行环境](interpreter.md#the-interpreter-and-its-environment)
        *   [2.2.1. 源文件的字符编码](interpreter.md#source-code-encoding)
*   [3\. Python 速览](introduction.md)
    *   [3.1. Python 用作计算器](introduction.md#using-python-as-a-calculator)
        *   [3.1.1. 数字](introduction.md#numbers)
        *   [3.1.2. 字符串](introduction.md#strings)
        *   [3.1.3. 列表](introduction.md#lists)
    *   [3.2. 走向编程的第一步](introduction.md#first-steps-towards-programming)
*   [4\. 其他流程控制工具](controlflow.md)
    *   [4.1. `if` 语句](controlflow.md#if-statements)
    *   [4.2. `for` 语句](controlflow.md#for-statements)
    *   [4.3. `range()` 函数](controlflow.md#the-range-function)
    *   [4.4. 循环中的 `break`、`continue` 语句及 `else` 子句](controlflow.md#break-and-continue-statements-and-else-clauses-on-loops)
    *   [4.5. `pass` 语句](controlflow.md#pass-statements)
    *   [4.6. `match` Statements](controlflow.md#match-statements)
    *   [4.7. 定义函数](controlflow.md#defining-functions)
    *   [4.8. 函数定义详解](controlflow.md#more-on-defining-functions)
        *   [4.8.1. 默认值参数](controlflow.md#default-argument-values)
        *   [4.8.2. 关键字参数](controlflow.md#keyword-arguments)
        *   [4.8.3. 特殊参数](controlflow.md#special-parameters)
            *   [4.8.3.1. 位置或关键字参数](controlflow.md#positional-or-keyword-arguments)
            *   [4.8.3.2. 仅位置参数](controlflow.md#positional-only-parameters)
            *   [4.8.3.3. 仅限关键字参数](controlflow.md#keyword-only-arguments)
            *   [4.8.3.4. 函数示例](controlflow.md#function-examples)
            *   [4.8.3.5. 小结](controlflow.md#recap)
        *   [4.8.4. 任意实参列表](controlflow.md#arbitrary-argument-lists)
        *   [4.8.5. 解包实参列表](controlflow.md#unpacking-argument-lists)
        *   [4.8.6. Lambda 表达式](controlflow.md#lambda-expressions)
        *   [4.8.7. 文档字符串](controlflow.md#documentation-strings)
        *   [4.8.8. 函数注解](controlflow.md#function-annotations)
    *   [4.9. 小插曲：编码风格](controlflow.md#intermezzo-coding-style)
*   [5\. 数据结构](datastructures.md)
    *   [5.1. 列表详解](datastructures.md#more-on-lists)
        *   [5.1.1. 列表用作堆栈](datastructures.md#using-lists-as-stacks)
        *   [5.1.2. 列表作为队列使用](datastructures.md#using-lists-as-queues)
        *   [5.1.3. 列表推导式](datastructures.md#list-comprehensions)
        *   [5.1.4. 嵌套的列表推导式](datastructures.md#nested-list-comprehensions)
    *   [5.2. `del` 语句](datastructures.md#the-del-statement)
    *   [5.3. 元组和序列](datastructures.md#tuples-and-sequences)
    *   [5.4. 集合](datastructures.md#sets)
    *   [5.5. 字典](datastructures.md#dictionaries)
    *   [5.6. 循环的技巧](datastructures.md#looping-techniques)
    *   [5.7. 深入条件控制](datastructures.md#more-on-conditions)
    *   [5.8. 序列和其他类型的比较](datastructures.md#comparing-sequences-and-other-types)
*   [6\. 模块](modules.md)
    *   [6.1. 模块详解](modules.md#more-on-modules)
        *   [6.1.1. 以脚本方式执行模块](modules.md#executing-modules-as-scripts)
        *   [6.1.2. 模块搜索路径](modules.md#the-module-search-path)
        *   [6.1.3. “已编译的” Python 文件](modules.md#compiled-python-files)
    *   [6.2. 标准模块](modules.md#standard-modules)
    *   [6.3. `dir()` 函数](modules.md#the-dir-function)
    *   [6.4. 包](modules.md#packages)
        *   [6.4.1. 从包中导入 \*](modules.md#importing-from-a-package)
        *   [6.4.2. 子包参考](modules.md#intra-package-references)
        *   [6.4.3. 多目录中的包](modules.md#packages-in-multiple-directories)
*   [7\. 输入与输出](inputoutput.md)
    *   [7.1. 更复杂的输出格式](inputoutput.md#fancier-output-formatting)
        *   [7.1.1. 格式化字符串字面值](inputoutput.md#formatted-string-literals)
        *   [7.1.2. 字符串 format() 方法](inputoutput.md#the-string-format-method)
        *   [7.1.3. 手动格式化字符串](inputoutput.md#manual-string-formatting)
        *   [7.1.4. 旧的字符串格式化方法](inputoutput.md#old-string-formatting)
    *   [7.2. 读写文件](inputoutput.md#reading-and-writing-files)
        *   [7.2.1. 文件对象的方法](inputoutput.md#methods-of-file-objects)
        *   [7.2.2. 使用 `json` 保存结构化数据](inputoutput.md#saving-structured-data-with-json)
*   [8\. 错误和异常](errors.md)
    *   [8.1. 句法错误](errors.md#syntax-errors)
    *   [8.2. 异常](errors.md#exceptions)
    *   [8.3. 处理异常](errors.md#handling-exceptions)
    *   [8.4. 触发异常](errors.md#raising-exceptions)
    *   [8.5. 异常链](errors.md#exception-chaining)
    *   [8.6. 用户自定义异常](errors.md#user-defined-exceptions)
    *   [8.7. 定义清理操作](errors.md#defining-clean-up-actions)
    *   [8.8. 预定义的清理操作](errors.md#predefined-clean-up-actions)
*   [9\. 类](classes.md)
    *   [9.1. 名称和对象](classes.md#a-word-about-names-and-objects)
    *   [9.2. Python 作用域和命名空间](classes.md#python-scopes-and-namespaces)
        *   [9.2.1. 作用域和命名空间示例](classes.md#scopes-and-namespaces-example)
    *   [9.3. 初探类](classes.md#a-first-look-at-classes)
        *   [9.3.1. 类定义语法](classes.md#class-definition-syntax)
        *   [9.3.2. 类对象](classes.md#class-objects)
        *   [9.3.3. 实例对象](classes.md#instance-objects)
        *   [9.3.4. 方法对象](classes.md#method-objects)
        *   [9.3.5. 类和实例变量](classes.md#class-and-instance-variables)
    *   [9.4. 补充说明](classes.md#random-remarks)
    *   [9.5. 继承](classes.md#inheritance)
        *   [9.5.1. 多重继承](classes.md#multiple-inheritance)
    *   [9.6. 私有变量](classes.md#private-variables)
    *   [9.7. 杂项说明](classes.md#odds-and-ends)
    *   [9.8. 迭代器](classes.md#iterators)
    *   [9.9. 生成器](classes.md#generators)
    *   [9.10. 生成器表达式](classes.md#generator-expressions)
*   [10\. 标准库简介](stdlib.md)
    *   [10.1. 操作系统接口](stdlib.md#operating-system-interface)
    *   [10.2. 文件通配符](stdlib.md#file-wildcards)
    *   [10.3. 命令行参数](stdlib.md#command-line-arguments)
    *   [10.4. 错误输出重定向和程序终止](stdlib.md#error-output-redirection-and-program-termination)
    *   [10.5. 字符串模式匹配](stdlib.md#string-pattern-matching)
    *   [10.6. 数学](stdlib.md#mathematics)
    *   [10.7. 互联网访问](stdlib.md#internet-access)
    *   [10.8. 日期和时间](stdlib.md#dates-and-times)
    *   [10.9. 数据压缩](stdlib.md#data-compression)
    *   [10.10. 性能测量](stdlib.md#performance-measurement)
    *   [10.11. 质量控制](stdlib.md#quality-control)
    *   [10.12. 自带电池](stdlib.md#batteries-included)
*   [11\. 标准库简介 —— 第二部分](stdlib2.md)
    *   [11.1. 格式化输出](stdlib2.md#output-formatting)
    *   [11.2. 模板](stdlib2.md#templating)
    *   [11.3. 使用二进制数据记录格式](stdlib2.md#working-with-binary-data-record-layouts)
    *   [11.4. 多线程](stdlib2.md#multi-threading)
    *   [11.5. 日志](stdlib2.md#logging)
    *   [11.6. 弱引用](stdlib2.md#weak-references)
    *   [11.7. 用于操作列表的工具](stdlib2.md#tools-for-working-with-lists)
    *   [11.8. 十进制浮点运算](stdlib2.md#decimal-floating-point-arithmetic)
*   [12\. 虚拟环境和包](venv.md)
    *   [12.1. 概述](venv.md#introduction)
    *   [12.2. 创建虚拟环境](venv.md#creating-virtual-environments)
    *   [12.3. 使用pip管理包](venv.md#managing-packages-with-pip)
*   [13\. 接下来？](whatnow.md)
*   [14\. 交互式编辑和编辑历史](interactive.md)
    *   [14.1. Tab 补全和编辑历史](interactive.md#tab-completion-and-history-editing)
    *   [14.2. 默认交互式解释器的替代品](interactive.md#alternatives-to-the-interactive-interpreter)
*   [15\. 浮点算术：争议和限制](floatingpoint.md)
    *   [15.1. 表示性错误](floatingpoint.md#representation-error)
*   [16\. 附录](appendix.md)
    *   [16.1. 交互模式](appendix.md#interactive-mode)
        *   [16.1.1. 错误处理](appendix.md#error-handling)
        *   [16.1.2. 可执行的Python脚本](appendix.md#executable-python-scripts)
        *   [16.1.3. 交互式启动文件](appendix.md#the-interactive-startup-file)
        *   [16.1.4. 定制模块](appendix.md#the-customization-modules)

#### 上一个主题

[更新日志](https://docs.python.org/zh-cn/3/whatsnew/changelog.html "上一章")

#### 下一个主题

[1\. 课前甜点](appetite.md "下一章")

### 本页

*   [提交 Bug](https://docs.python.org/zh-cn/3/bugs.html)
*   [显示源代码](https://github.com/python/cpython/blob/master/Doc/tutorial/index.rst)

### 导航

*   [索引](https://docs.python.org/zh-cn/3/genindex.html "总目录")
*   [模块](https://docs.python.org/zh-cn/3/py-modindex.html "Python 模块索引") |
*   [下一页](appetite.md "1. 课前甜点") |
*   [上一页](https://docs.python.org/zh-cn/3/whatsnew/changelog.html "更新日志") |
*   ![](https://docs.python.org/zh-cn/3/_static/py.png)
*   [Python](https://www.python.org/) »
*   [3.10.0a6 Documentation](https://docs.python.org/zh-cn/3/index.html) »
*   Python 教程
*      
    
    $('.inline-search').show(0); |

© [版权所有](https://docs.python.org/zh-cn/3/copyright.html) 2001-2021, Python Software Foundation.  
This page is licensed under the Python Software Foundation License Version 2.  
Examples, recipes, and other code in the documentation are additionally licensed under the Zero Clause BSD License.  
See History and License for more information.  
  
The Python Software Foundation is a non-profit corporation. [Please donate.](https://www.python.org/psf/donations/)  
  
最后更新于 3月 19, 2021. [Found a bug](https://docs.python.org/3/bugs.html)?  
Created using [Sphinx](https://www.sphinx-doc.org/) 3.2.1.
