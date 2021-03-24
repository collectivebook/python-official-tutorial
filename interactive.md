  14\. 交互式编辑和编辑历史 — Python 3.10.0a6 文档                   @media only screen { table.full-width-table { width: 100%; } }   

### 导航

*   [索引](https://docs.python.org/zh-cn/3/genindex.html "总目录")
*   [模块](https://docs.python.org/zh-cn/3/py-modindex.html "Python 模块索引") |
*   [下一页](floatingpoint.md "15. 浮点算术：争议和限制") |
*   [上一页](whatnow.md "13. 接下来？") |
*   ![](https://docs.python.org/zh-cn/3/_static/py.png)
*   [Python](https://www.python.org/) »
*   [3.10.0a6 Documentation](https://docs.python.org/zh-cn/3/index.html) »
*   [Python 教程](index.md) »
*   14\. 交互式编辑和编辑历史
*      
    
    $('.inline-search').show(0); |

# 14\. 交互式编辑和编辑历史[¶](#interactive-input-editing-and-history-substitution "永久链接至标题")

某些版本的 Python 解释器支持编辑当前输入行和编辑历史记录，类似 Korn shell 和 GNU Bash shell 的功能 。这个功能使用了 [GNU Readline](https://tiswww.case.edu/php/chet/readline/rltop.html) 来实现，一个支持多种编辑方式的库。这个库有它自己的文档，在这里我们就不重复说明了。

## 14.1. Tab 补全和编辑历史[¶](#tab-completion-and-history-editing "永久链接至标题")

在解释器启动的时候，补全变量和模块名的功能将 [自动打开](https://docs.python.org/zh-cn/3/library/site.html#rlcompleter-config)，以便在按下 Tab 键的时候调用补全函数。它会查看 Python 语句名称，当前局部变量和可用的模块名称。处理像 `string.a` 的表达式，它会求值在最后一个 `'.'` 之前的表达式，接着根据求值结果对象的属性给出补全建议。如果拥有 `__getattr__()` 方法的对象是表达式的一部分，注意这可能会执行程序定义的代码。默认配置下会把编辑历史记录保存在用户目录下名为 `.python_history` 的文件。在下一次 Python 解释器会话期间，编辑历史记录仍旧可用。

## 14.2. 默认交互式解释器的替代品[¶](#alternatives-to-the-interactive-interpreter "永久链接至标题")

Python 解释器与早期版本的相比，向前迈进了一大步；无论怎样，还有些希望的功能：如果能在编辑连续行时建议缩进（解析器知道接下来是否需要缩进符号），那将很棒。补全机制可以使用解释器的符号表。有命令去检查（甚至建议）括号，引号以及其他符号是否匹配。

一个可选的增强型交互式解释器是 [IPython](https://ipython.org/)，它已经存在了有一段时间，它具有 tab 补全，探索对象和高级历史记录管理功能。它还可以彻底定制并嵌入到其他应用程序中。另一个相似的增强型交互式环境是 [bpython](https://www.bpython-interpreter.org/)。

### [目录](https://docs.python.org/zh-cn/3/contents.html)

*   [14\. 交互式编辑和编辑历史](#)
    *   [14.1. Tab 补全和编辑历史](#tab-completion-and-history-editing)
    *   [14.2. 默认交互式解释器的替代品](#alternatives-to-the-interactive-interpreter)

#### 上一个主题

[13\. 接下来？](whatnow.md "上一章")

#### 下一个主题

[15\. 浮点算术：争议和限制](floatingpoint.md "下一章")

### 本页

*   [提交 Bug](https://docs.python.org/zh-cn/3/bugs.html)
*   [显示源代码](https://github.com/python/cpython/blob/master/Doc/tutorial/interactive.rst)

### 导航

*   [索引](https://docs.python.org/zh-cn/3/genindex.html "总目录")
*   [模块](https://docs.python.org/zh-cn/3/py-modindex.html "Python 模块索引") |
*   [下一页](floatingpoint.md "15. 浮点算术：争议和限制") |
*   [上一页](whatnow.md "13. 接下来？") |
*   ![](https://docs.python.org/zh-cn/3/_static/py.png)
*   [Python](https://www.python.org/) »
*   [3.10.0a6 Documentation](https://docs.python.org/zh-cn/3/index.html) »
*   [Python 教程](index.md) »
*   14\. 交互式编辑和编辑历史
*      
    
    $('.inline-search').show(0); |

© [版权所有](https://docs.python.org/zh-cn/3/copyright.html) 2001-2021, Python Software Foundation.  
This page is licensed under the Python Software Foundation License Version 2.  
Examples, recipes, and other code in the documentation are additionally licensed under the Zero Clause BSD License.  
See History and License for more information.  
  
The Python Software Foundation is a non-profit corporation. [Please donate.](https://www.python.org/psf/donations/)  
  
最后更新于 3月 19, 2021. [Found a bug](https://docs.python.org/3/bugs.html)?  
Created using [Sphinx](https://www.sphinx-doc.org/) 3.2.1.
