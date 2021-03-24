  6\. 模块 — Python 3.10.0a6 文档                   @media only screen { table.full-width-table { width: 100%; } }   

### 导航

*   [索引](https://docs.python.org/zh-cn/3/genindex.html "总目录")
*   [模块](https://docs.python.org/zh-cn/3/py-modindex.html "Python 模块索引") |
*   [下一页](inputoutput.md "7. 输入与输出") |
*   [上一页](datastructures.md "5. 数据结构") |
*   ![](https://docs.python.org/zh-cn/3/_static/py.png)
*   [Python](https://www.python.org/) »
*   [3.10.0a6 Documentation](https://docs.python.org/zh-cn/3/index.html) »
*   [Python 教程](index.md) »
*   6\. 模块
*      
    
    $('.inline-search').show(0); |

# 6\. 模块[¶](#modules "永久链接至标题")

退出 Python 解释器再次进入时，会丢失之前定义的函数和变量。因此，编写较长程序时，建议用文本编辑器代替解释器，执行文件中的输入内容，这就是编写 _脚本_ 。随着程序越来越长，为了方便维护，最好把一个脚本拆分成多个文件。还一种情况，不同程序使用同一个函数时，不用每次把函数复制到各个程序。

为实现这些需求，Python 把各种定义存入一个文件，在脚本或解释器的交互式实例中使用。这个文件就是 _模块_ ；模块中的定义可以 _导入_ 到其他模块或 _主_ 模块（在顶层和计算器模式下，执行脚本中可访问的变量集）。

模块是包含 Python 定义和语句的文件。其文件名是模块名加后缀名 `.py` 。在模块内部，通过全局变量 `__name__` 可以获取模块名（即字符串）。例如，用文本编辑器在当前目录下创建 `fibo.py` 文件，输入以下内容：

\# Fibonacci numbers module

def fib(n):    \# write Fibonacci series up to n
    a, b \= 0, 1
    while a < n:
        print(a, end\=' ')
        a, b \= b, a+b
    print()

def fib2(n):   \# return Fibonacci series up to n
    result \= \[\]
    a, b \= 0, 1
    while a < n:
        result.append(a)
        a, b \= b, a+b
    return result

现在，进入 Python 解释器，用以下命令导入该模块：

\>>> import fibo

这项操作不直接把 `fibo` 函数定义的名称导入到当前符号表，只导入模块名 `fibo` 。要使用模块名访问函数：

\>>> fibo.fib(1000)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987
\>>> fibo.fib2(100)
\[0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89\]
\>>> fibo.\_\_name\_\_
'fibo'

如果经常使用某个函数，可以把它赋值给局部变量：

\>>> fib \= fibo.fib
\>>> fib(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377

## 6.1. 模块详解[¶](#more-on-modules "永久链接至标题")

模块包含可执行语句及函数定义。这些语句用于初始化模块，且仅在 import 语句 _第一次_ 遇到模块名时执行。[1](#id2) (文件作为脚本运行时，也会执行这些语句。)

模块有自己的私有符号表，用作模块中所有函数的全局符号表。因此，在模块内使用全局变量时，不用担心与用户定义的全局变量发生冲突。另一方面，可以用与访问模块函数一样的标记法，访问模块的全局变量，`modname.itemname`。

可以把其他模块导入模块。按惯例，所有 [`import`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#import) 语句都放在模块（或脚本）开头，但这不是必须的。导入的模块名存在导入模块的全局符号表里。

[`import`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#import) 语句有一个变体，可以直接把模块里的名称导入到另一个模块的符号表。例如：

\>>> from fibo import fib, fib2
\>>> fib(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377

这段代码不会把模块名导入到局部符号表里（因此，本例没有定义 `fibo`）。

还有一种变体可以导入模块内定义的所有名称：

\>>> from fibo import \*
\>>> fib(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377

这种方式会导入所有不以下划线（`_`）开头的名称。大多数情况下，不要用这个功能，这种方式向解释器导入了一批未知的名称，可能会覆盖已经定义的名称。

注意，一般情况下，不建议从模块或包内导入 `*`， 因为，这项操作经常让代码变得难以理解。不过，为了在交互式编译器中少打几个字，这么用也没问题。

模块名后使用 `as` 时，直接把 `as` 后的名称与导入模块绑定。

\>>> import fibo as fib
\>>> fib.fib(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377

与 `import fibo` 一样，这种方式也可以有效地导入模块，唯一的区别是，导入的名称是 `fib`。

[`from`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#from) 中也可以使用这种方式，效果类似：

\>>> from fibo import fib as fibonacci
\>>> fibonacci(500)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377

注解

为了保证运行效率，每次解释器会话只导入一次模块。如果更改了模块内容，必须重启解释器；仅交互测试一个模块时，也可以使用 [`importlib.reload()`](https://docs.python.org/zh-cn/3/library/importlib.html#importlib.reload "importlib.reload")，例如 `import importlib; importlib.reload(modulename)`。

### 6.1.1. 以脚本方式执行模块[¶](#executing-modules-as-scripts "永久链接至标题")

可以用以下方式运行 Python 模块：

python fibo.py <arguments\>

这项操作将执行模块里的代码，和导入模块一样，但会把 `__name__` 赋值为 `"__main__"`。 也就是把下列代码添加到模块末尾：

if \_\_name\_\_ \== "\_\_main\_\_":
    import sys
    fib(int(sys.argv\[1\]))

既可以把这个文件当脚本使用，也可以用作导入的模块， 因为，解析命令行的代码只有在模块以 “main” 文件执行时才会运行：

$ python fibo.py 50
0 1 1 2 3 5 8 13 21 34

导入模块时，不运行这些代码：

\>>> import fibo
\>>>

这种操作常用于为模块提供便捷用户接口，或用于测试（把模块当作执行测试套件的脚本运行）。

### 6.1.2. 模块搜索路径[¶](#the-module-search-path "永久链接至标题")

导入 `spam` 模块时，解释器首先查找名为 spam 的内置模块。如果没找到，解释器再从 [`sys.path`](https://docs.python.org/zh-cn/3/library/sys.html#sys.path "sys.path") 变量中的目录列表里查找 `spam.py` 文件。[`sys.path`](https://docs.python.org/zh-cn/3/library/sys.html#sys.path "sys.path") 初始化时包含以下位置：

*   输入脚本的目录（或未指定文件时的当前目录）。
    
*   [`PYTHONPATH`](https://docs.python.org/zh-cn/3/using/cmdline.html#envvar-PYTHONPATH) （目录列表，与 shell 变量 `PATH` 的语法一样）。
    
*   默认安装目录。
    

注解

在支持 symlink 的文件系统中，输入脚本目录是在追加 symlink 后计算出来的。换句话说，包含 symlink 的目录并 **没有** 添加至模块搜索路径。

初始化后，Python 程序可以更改 [`sys.path`](https://docs.python.org/zh-cn/3/library/sys.html#sys.path "sys.path")。运行脚本的目录在标准库路径之前，置于搜索路径的开头。即，加载的是该目录里的脚本，而不是标准库的同名模块。 除非刻意替换，否则会报错。详见 [标准模块](#tut-standardmodules)。

### 6.1.3. “已编译的” Python 文件[¶](#compiled-python-files "永久链接至标题")

为了快速加载模块，Python 把模块的编译版缓存在 `__pycache__` 目录中，文件名为 `module._version_.pyc`，version 对编译文件格式进行编码，一般是 Python 的版本号。例如，CPython 的 3.3 发行版中，spam.py 的编译版本缓存为 `__pycache__/spam.cpython-33.pyc`。使用这种此命名惯例，可以实现 Python 不同发行版和不同版本的已编译模块共存。

Python 对比编译版本与源码的修改日期，查看它是否已过期，是否要重新编译，此过程完全自动化。此外，编译模块与平台无关，因此，可在不同架构系统之间共享相同的支持库。

Python 在两种情况下不检查缓存。其一，从命令行直接载入模块，只重新编译，不存储编译结果；其二，没有源模块，就不会检查缓存。为了支持无源文件（仅编译）发行版本， 编译模块必须在源目录下，并且绝不能有源模块。

给专业人士的一些小建议：

*   在 Python 命令中使用 [`-O`](https://docs.python.org/zh-cn/3/using/cmdline.html#cmdoption-O) 或 [`-OO`](https://docs.python.org/zh-cn/3/using/cmdline.html#cmdoption-OO) 开关，可以减小编译模块的大小。`-O` 去除断言语句，`-OO` 去除断言语句和 \_\_doc\_\_ 字符串。有些程序可能依赖于这些内容，因此，没有十足的把握，不要使用这两个选项。“优化过的”模块带有 `opt-` 标签，并且文件通常会一小些。将来的发行版或许会改进优化的效果。
    
*   从 `.pyc` 文件读取的程序不比从 `.py` 读取的执行速度快，`.pyc` 文件只是加载速度更快。
    
*   [`compileall`](https://docs.python.org/zh-cn/3/library/compileall.html#module-compileall "compileall: Tools for byte-compiling all Python source files in a directory tree.") 模块可以为一个目录下的所有模块创建 .pyc 文件。
    
*   本过程的细节及决策流程图，详见 [**PEP 3147**](https://www.python.org/dev/peps/pep-3147)。
    

## 6.2. 标准模块[¶](#standard-modules "永久链接至标题")

Python 附带了标准模块库，详见 Python 标准库参考手册（以下简称为“库参考”）。解释器中内置了一些模块，用于访问不属于语言核心的内置操作，其目的主要是为了提高运行效率，或访问系统调用等操作系统原语。这些模块的集合是依赖于底层平台的配置选项。例如，[`winreg`](https://docs.python.org/zh-cn/3/library/winreg.html#module-winreg "winreg: Routines and objects for manipulating the Windows registry. (Windows)") 模块仅供 Windows 使用。特别要注意内嵌到 Python 解释器中的模块 [`sys`](https://docs.python.org/zh-cn/3/library/sys.html#module-sys "sys: Access system-specific parameters and functions.")。变量 `sys.ps1` 和 `sys.ps2` 则用来定义主次提示的字符串：

\>>> import sys
\>>> sys.ps1
'>>> '
\>>> sys.ps2
'... '
\>>> sys.ps1 \= 'C> '
C> print('Yuck!')
Yuck!
C>

只有解释器用于交互模式时，才定义这两个变量。

变量 `sys.path` 是字符串列表，用于确定解释器的模块搜索路径。该变量以环境变量 [`PYTHONPATH`](https://docs.python.org/zh-cn/3/using/cmdline.html#envvar-PYTHONPATH) 提取的默认路径进行初始化，如未设置 [`PYTHONPATH`](https://docs.python.org/zh-cn/3/using/cmdline.html#envvar-PYTHONPATH)，则使用内置的默认路径。可以用标准列表操作修改该变量：

\>>> import sys
\>>> sys.path.append('/ufs/guido/lib/python')

## 6.3. [`dir()`](https://docs.python.org/zh-cn/3/library/functions.html#dir "dir") 函数[¶](#the-dir-function "永久链接至标题")

内置函数 [`dir()`](https://docs.python.org/zh-cn/3/library/functions.html#dir "dir") 用于查找模块定义的名称。返回结果是经过排序的字符串列表：

\>>> import fibo, sys
\>>> dir(fibo)
\['\_\_name\_\_', 'fib', 'fib2'\]
\>>> dir(sys)  
\['\_\_breakpointhook\_\_', '\_\_displayhook\_\_', '\_\_doc\_\_', '\_\_excepthook\_\_',
 '\_\_interactivehook\_\_', '\_\_loader\_\_', '\_\_name\_\_', '\_\_package\_\_', '\_\_spec\_\_',
 '\_\_stderr\_\_', '\_\_stdin\_\_', '\_\_stdout\_\_', '\_\_unraisablehook\_\_',
 '\_clear\_type\_cache', '\_current\_frames', '\_debugmallocstats', '\_framework',
 '\_getframe', '\_git', '\_home', '\_xoptions', 'abiflags', 'addaudithook',
 'api\_version', 'argv', 'audit', 'base\_exec\_prefix', 'base\_prefix',
 'breakpointhook', 'builtin\_module\_names', 'byteorder', 'call\_tracing',
 'callstats', 'copyright', 'displayhook', 'dont\_write\_bytecode', 'exc\_info',
 'excepthook', 'exec\_prefix', 'executable', 'exit', 'flags', 'float\_info',
 'float\_repr\_style', 'get\_asyncgen\_hooks', 'get\_coroutine\_origin\_tracking\_depth',
 'getallocatedblocks', 'getdefaultencoding', 'getdlopenflags',
 'getfilesystemencodeerrors', 'getfilesystemencoding', 'getprofile',
 'getrecursionlimit', 'getrefcount', 'getsizeof', 'getswitchinterval',
 'gettrace', 'hash\_info', 'hexversion', 'implementation', 'int\_info',
 'intern', 'is\_finalizing', 'last\_traceback', 'last\_type', 'last\_value',
 'maxsize', 'maxunicode', 'meta\_path', 'modules', 'path', 'path\_hooks',
 'path\_importer\_cache', 'platform', 'prefix', 'ps1', 'ps2', 'pycache\_prefix',
 'set\_asyncgen\_hooks', 'set\_coroutine\_origin\_tracking\_depth', 'setdlopenflags',
 'setprofile', 'setrecursionlimit', 'setswitchinterval', 'settrace', 'stderr',
 'stdin', 'stdout', 'thread\_info', 'unraisablehook', 'version', 'version\_info',
 'warnoptions'\]

没有参数时，[`dir()`](https://docs.python.org/zh-cn/3/library/functions.html#dir "dir") 列出当前定义的名称：

\>>> a \= \[1, 2, 3, 4, 5\]
\>>> import fibo
\>>> fib \= fibo.fib
\>>> dir()
\['\_\_builtins\_\_', '\_\_name\_\_', 'a', 'fib', 'fibo', 'sys'\]

注意，该函数列出所有类型的名称：变量、模块、函数等。

[`dir()`](https://docs.python.org/zh-cn/3/library/functions.html#dir "dir") 不会列出内置函数和变量的名称。这些内容的定义在标准模块 [`builtins`](https://docs.python.org/zh-cn/3/library/builtins.html#module-builtins "builtins: The module that provides the built-in namespace.") 里：

\>>> import builtins
\>>> dir(builtins)  
\['ArithmeticError', 'AssertionError', 'AttributeError', 'BaseException',
 'BlockingIOError', 'BrokenPipeError', 'BufferError', 'BytesWarning',
 'ChildProcessError', 'ConnectionAbortedError', 'ConnectionError',
 'ConnectionRefusedError', 'ConnectionResetError', 'DeprecationWarning',
 'EOFError', 'Ellipsis', 'EnvironmentError', 'Exception', 'False',
 'FileExistsError', 'FileNotFoundError', 'FloatingPointError',
 'FutureWarning', 'GeneratorExit', 'IOError', 'ImportError',
 'ImportWarning', 'IndentationError', 'IndexError', 'InterruptedError',
 'IsADirectoryError', 'KeyError', 'KeyboardInterrupt', 'LookupError',
 'MemoryError', 'NameError', 'None', 'NotADirectoryError', 'NotImplemented',
 'NotImplementedError', 'OSError', 'OverflowError',
 'PendingDeprecationWarning', 'PermissionError', 'ProcessLookupError',
 'ReferenceError', 'ResourceWarning', 'RuntimeError', 'RuntimeWarning',
 'StopIteration', 'SyntaxError', 'SyntaxWarning', 'SystemError',
 'SystemExit', 'TabError', 'TimeoutError', 'True', 'TypeError',
 'UnboundLocalError', 'UnicodeDecodeError', 'UnicodeEncodeError',
 'UnicodeError', 'UnicodeTranslateError', 'UnicodeWarning', 'UserWarning',
 'ValueError', 'Warning', 'ZeroDivisionError', '\_', '\_\_build\_class\_\_',
 '\_\_debug\_\_', '\_\_doc\_\_', '\_\_import\_\_', '\_\_name\_\_', '\_\_package\_\_', 'abs',
 'all', 'any', 'ascii', 'bin', 'bool', 'bytearray', 'bytes', 'callable',
 'chr', 'classmethod', 'compile', 'complex', 'copyright', 'credits',
 'delattr', 'dict', 'dir', 'divmod', 'enumerate', 'eval', 'exec', 'exit',
 'filter', 'float', 'format', 'frozenset', 'getattr', 'globals', 'hasattr',
 'hash', 'help', 'hex', 'id', 'input', 'int', 'isinstance', 'issubclass',
 'iter', 'len', 'license', 'list', 'locals', 'map', 'max', 'memoryview',
 'min', 'next', 'object', 'oct', 'open', 'ord', 'pow', 'print', 'property',
 'quit', 'range', 'repr', 'reversed', 'round', 'set', 'setattr', 'slice',
 'sorted', 'staticmethod', 'str', 'sum', 'super', 'tuple', 'type', 'vars',
 'zip'\]

## 6.4. 包[¶](#packages "永久链接至标题")

包是一种用“点式模块名”构造 Python 模块命名空间的方法。例如，模块名 `A.B` 表示包 `A` 中名为 `B` 的子模块。正如模块可以区分不同模块之间的全局变量名称一样，点式模块名可以区分 NumPy 或 Pillow 等不同多模块包之间的模块名称。

假设要为统一处理声音文件与声音数据设计一个模块集（“包”）。声音文件的格式很多（通常以扩展名来识别，例如：`.wav`， `.aiff`， `.au`），因此，为了不同文件格式之间的转换，需要创建和维护一个不断增长的模块集合。为了实现对声音数据的不同处理（例如，混声、添加回声、均衡器功能、创造人工立体声效果），还要编写无穷无尽的模块流。下图以分级文件系统形式展示这个包的架构：

sound/                          Top-level package
      \_\_init\_\_.py               Initialize the sound package
      formats/                  Subpackage for file format conversions
              \_\_init\_\_.py
              wavread.py
              wavwrite.py
              aiffread.py
              aiffwrite.py
              auread.py
              auwrite.py
              ...
      effects/                  Subpackage for sound effects
              \_\_init\_\_.py
              echo.py
              surround.py
              reverse.py
              ...
      filters/                  Subpackage for filters
              \_\_init\_\_.py
              equalizer.py
              vocoder.py
              karaoke.py
              ...

导入包时，Python 搜索 `sys.path` 里的目录，查找包的子目录。

Python 只把含 `__init__.py` 文件的目录当成包。这样可以防止以 `string` 等通用名称命名的目录，无意中屏蔽出现在后方模块搜索路径中的有效模块。 最简情况下，`__init__.py` 只是一个空文件，但该文件也可以执行包的初始化代码，或设置 `__all__` 变量，详见下文。

还可以从包中导入单个模块，例如：

import sound.effects.echo

这段代码加载子模块 `sound.effects.echo` ，但引用时必须使用子模块的全名：

sound.effects.echo.echofilter(input, output, delay\=0.7, atten\=4)

另一种导入子模块的方法是 ：

from sound.effects import echo

这段代码还可以加载子模块 `echo` ，并且不加包前缀也可以使用。因此，可以按如下方式使用：

echo.echofilter(input, output, delay\=0.7, atten\=4)

另一种变体是直接导入所需的函数或变量：

from sound.effects.echo import echofilter

同样，这样也会加载子模块 `echo`，但可以直接使用函数 `echofilter()`：

echofilter(input, output, delay\=0.7, atten\=4)

注意，使用 `from package import item` 时，item 可以是包的子模块（或子包），也可以是包中定义的函数、类或变量等其他名称。`import` 语句首先测试包中是否定义了 item；如果未在包中定义，则假定 item 是模块，并尝试加载。如果找不到 item，则触发 [`ImportError`](https://docs.python.org/zh-cn/3/library/exceptions.html#ImportError "ImportError") 异常。

相反，使用 `import item.subitem.subsubitem` 句法时，除最后一项外，每个 item 都必须是包；最后一项可以是模块或包，但不能是上一项中定义的类、函数或变量。

### 6.4.1. 从包中导入 \*[¶](#importing-from-a-package "永久链接至标题")

使用 `from sound.effects import *` 时会发生什么？理想情况下，该语句在文件系统查找并导入包的所有子模块。这项操作花费的时间较长，并且导入子模块可能会产生不必要的副作用，这种副作用只有在显式导入子模块时才会发生。

唯一的解决方案是提供包的显式索引。[`import`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#import) 语句使用如下惯例：如果包的 `__init__.py` 代码定义了列表 `__all__`，运行 `from package import *` 时，它就是用于导入的模块名列表。发布包的新版本时，包的作者应更新此列表。如果包的作者认为没有必要在包中执行导入 \* 操作，也可以不提供此列表。例如，`sound/effects/__init__.py` 文件包含以下代码：

\_\_all\_\_ \= \["echo", "surround", "reverse"\]

即，`from sound.effects import *` 将导入 `sound` 包中的这三个命名子模块。

如果没有定义 `__all__`，`from sound.effects import *` 语句 _不会_ 把包 `sound.effects` 中所有子模块都导入到当前命名空间；该语句只确保导入包 `sound.effects` （可能还会运行 `__init__.py` 中的初始化代码），然后，再导入包中定义的名称。这些名称包括 `__init__.py` 中定义的任何名称（以及显式加载的子模块），还包括之前 [`import`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#import) 语句显式加载的包里的子模块。请看以下代码：

import sound.effects.echo
import sound.effects.surround
from sound.effects import \*

本例中，执行 `from...import` 语句时，将把 `echo` 和 `surround` 模块导入至当前命名空间，因为，它们是在 `sound.effects` 包里定义的。（该导入操作在定义了 `__all__` 时也有效。）

虽然，可以把模块设计为用 `import *` 时只导出遵循指定模式的名称，但仍不提倡在生产代码中使用这种做法。

记住，使用 `from package import specific_submodule` 没有任何问题！ 实际上，除了导入模块使用不同包的同名子模块之外，这种方式是推荐用法。

### 6.4.2. 子包参考[¶](#intra-package-references "永久链接至标题")

包中含有多个子包时（与示例中的 `sound` 包一样），可以使用绝对导入引用兄弟包中的子模块。例如，要在模块 `sound.filters.vocoder` 中使用 `sound.effects` 包的 `echo` 模块时，可以用 `from sound.effects import echo` 导入。

还可以用 import 语句的 `from module import name` 形式执行相对导入。这些导入语句使用前导句点表示相对导入中的当前包和父包。例如，相对于 `surround` 模块，可以使用：

from . import echo
from .. import formats
from ..filters import equalizer

注意，相对导入基于的是当前模块名。由于，主模块名是 `"__main__"` ，因此，Python 应用程序的主模块必须始终使用绝对导入。

### 6.4.3. 多目录中的包[¶](#packages-in-multiple-directories "永久链接至标题")

包还支持特殊属性 [`__path__`](https://docs.python.org/zh-cn/3/reference/import.html#path__ "__path__")。该属性初始化为在包的 `__init__.py` 文件中的代码执行前所在的目录名列表。这个变量可以修改，但这样做会影响将来搜索包中模块和子包的操作。

虽然，这个功能不常用，但可用它扩展包中的模块集。

脚注

[1](#id1)

实际上，函数定义也是“可执行”的“语句”；模块级函数定义执行时，把函数名导入至模块的全局符号表。

### [目录](https://docs.python.org/zh-cn/3/contents.html)

*   [6\. 模块](#)
    *   [6.1. 模块详解](#more-on-modules)
        *   [6.1.1. 以脚本方式执行模块](#executing-modules-as-scripts)
        *   [6.1.2. 模块搜索路径](#the-module-search-path)
        *   [6.1.3. “已编译的” Python 文件](#compiled-python-files)
    *   [6.2. 标准模块](#standard-modules)
    *   [6.3. `dir()` 函数](#the-dir-function)
    *   [6.4. 包](#packages)
        *   [6.4.1. 从包中导入 \*](#importing-from-a-package)
        *   [6.4.2. 子包参考](#intra-package-references)
        *   [6.4.3. 多目录中的包](#packages-in-multiple-directories)

#### 上一个主题

[5\. 数据结构](datastructures.md "上一章")

#### 下一个主题

[7\. 输入与输出](inputoutput.md "下一章")

### 本页

*   [提交 Bug](https://docs.python.org/zh-cn/3/bugs.html)
*   [显示源代码](https://github.com/python/cpython/blob/master/Doc/tutorial/modules.rst)

### 导航

*   [索引](https://docs.python.org/zh-cn/3/genindex.html "总目录")
*   [模块](https://docs.python.org/zh-cn/3/py-modindex.html "Python 模块索引") |
*   [下一页](inputoutput.md "7. 输入与输出") |
*   [上一页](datastructures.md "5. 数据结构") |
*   ![](https://docs.python.org/zh-cn/3/_static/py.png)
*   [Python](https://www.python.org/) »
*   [3.10.0a6 Documentation](https://docs.python.org/zh-cn/3/index.html) »
*   [Python 教程](index.md) »
*   6\. 模块
*      
    
    $('.inline-search').show(0); |

© [版权所有](https://docs.python.org/zh-cn/3/copyright.html) 2001-2021, Python Software Foundation.  
This page is licensed under the Python Software Foundation License Version 2.  
Examples, recipes, and other code in the documentation are additionally licensed under the Zero Clause BSD License.  
See History and License for more information.  
  
The Python Software Foundation is a non-profit corporation. [Please donate.](https://www.python.org/psf/donations/)  
  
最后更新于 3月 19, 2021. [Found a bug](https://docs.python.org/3/bugs.html)?  
Created using [Sphinx](https://www.sphinx-doc.org/) 3.2.1.
