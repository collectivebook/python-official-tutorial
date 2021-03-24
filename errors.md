  8\. 错误和异常 — Python 3.10.0a6 文档                   @media only screen { table.full-width-table { width: 100%; } }   

### 导航

*   [索引](https://docs.python.org/zh-cn/3/genindex.html "总目录")
*   [模块](https://docs.python.org/zh-cn/3/py-modindex.html "Python 模块索引") |
*   [下一页](classes.md "9. 类") |
*   [上一页](inputoutput.md "7. 输入与输出") |
*   ![](https://docs.python.org/zh-cn/3/_static/py.png)
*   [Python](https://www.python.org/) »
*   [3.10.0a6 Documentation](https://docs.python.org/zh-cn/3/index.html) »
*   [Python 教程](index.md) »
*   8\. 错误和异常
*      
    
    $('.inline-search').show(0); |

# 8\. 错误和异常[¶](#errors-and-exceptions "永久链接至标题")

至此，本教程还没有深入介绍过错误信息，但如果您试着输入过本教程前文中的例子，应该已经看到过一些错误信息。目前，（至少）有两种不同错误：_句法错误_ 和 _异常_。

## 8.1. 句法错误[¶](#syntax-errors "永久链接至标题")

句法错误又称解析错误，它是学习 Python 时最常见的错误：

\>>> while True print('Hello world')
  File "<stdin>", line 1
    while True print('Hello world')
                   ^
SyntaxError: invalid syntax

解析器会复现句法错误的那行代码，并用一个小“箭头”指向行里检测到的第一个错误。错误是由箭头 _上方_ 的 token 引发的（或至少是在这里检测出的）：本例中，在 [`print()`](https://docs.python.org/zh-cn/3/library/functions.html#print "print") 函数中检测到错误，因为，在它前面缺少冒号（`':'`） 。错误信息中还会输出文件名与行号，在使用脚本文件时，就能知道去哪里查错。

## 8.2. 异常[¶](#exceptions "永久链接至标题")

即使语句或表达式在语法上是正确的，但在尝试执行时，它仍可能会引发错误。 在执行时检测到的错误被称为\*异常\*，异常不一定会导致严重后果：你将很快学会如何在Python程序中处理它们。 但是，大多数异常并不会被程序处理，此时会显示如下所示的错误信息:

\>>> 10 \* (1/0)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: division by zero
\>>> 4 + spam\*3
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'spam' is not defined
\>>> '2' + 2
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: Can't convert 'int' object to str implicitly

错误信息的最后一行告诉我们程序遇到了什么类型的错误。异常有不同的类型，而其类型名称将会作为错误信息的一部分中打印出来：上述示例中的异常类型依次是：[`ZeroDivisionError`](https://docs.python.org/zh-cn/3/library/exceptions.html#ZeroDivisionError "ZeroDivisionError")， [`NameError`](https://docs.python.org/zh-cn/3/library/exceptions.html#NameError "NameError") 和 [`TypeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#TypeError "TypeError")。作为异常类型打印的字符串是发生的内置异常的名称。对于所有内置异常都是如此，但对于用户定义的异常则不一定如此（虽然这是一个有用的规范）。标准的异常类型是内置的标识符（而不是保留关键字）。

这一行的剩下的部分根据异常类型及其原因提供详细信息。

错误消息的开头部分以堆栈回溯的形式显示发生异常的上下文。 通常它会包含列出源代码行的堆栈回溯；但是，它将不会显示从标准输入读取的行。

[内置异常](https://docs.python.org/zh-cn/3/library/exceptions.html#bltin-exceptions) 列出了内置异常和它们的含义。

## 8.3. 处理异常[¶](#handling-exceptions "永久链接至标题")

可以编写处理所选异常的程序。请看下面的例子，它会要求用户一直输入，直到输入的是一个有效的整数，但允许用户中断程序（使用 Control\-C 或操作系统支持的其他操作）；请注意用户引起的中断可以通过引发 [`KeyboardInterrupt`](https://docs.python.org/zh-cn/3/library/exceptions.html#KeyboardInterrupt "KeyboardInterrupt") 异常来指示。:

\>>> while True:
...     try:
...         x \= int(input("Please enter a number: "))
...         break
...     except ValueError:
...         print("Oops!  That was no valid number.  Try again...")
...

[`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 语句的工作原理如下：

*   首先，执行 _try 子句_ （[`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 和 [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except) 关键字之间的（多行）语句）。
    
*   如果没有异常发生，则跳过 _except 子句_ 并完成 [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 语句的执行。
    
*   If an exception occurs during execution of the [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) clause, the rest of the clause is skipped. Then, if its type matches the exception named after the [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except) keyword, the _except clause_ is executed, and then execution continues after the try/except block.
    
*   If an exception occurs which does not match the exception named in the _except clause_, it is passed on to outer [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) statements; if no handler is found, it is an _unhandled exception_ and execution stops with a message as shown above.
    

A [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) statement may have more than one _except clause_, to specify handlers for different exceptions. At most one handler will be executed. Handlers only handle exceptions that occur in the corresponding _try clause_, not in other handlers of the same `try` statement. An _except clause_ may name multiple exceptions as a parenthesized tuple, for example:

... except (RuntimeError, TypeError, NameError):
...     pass

A class in an [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except) clause is compatible with an exception if it is the same class or a base class thereof (but not the other way around --- an _except clause_ listing a derived class is not compatible with a base class). For example, the following code will print B, C, D in that order:

class B(Exception):
    pass

class C(B):
    pass

class D(C):
    pass

for cls in \[B, C, D\]:
    try:
        raise cls()
    except D:
        print("D")
    except C:
        print("C")
    except B:
        print("B")

Note that if the _except clauses_ were reversed (with `except B` first), it would have printed B, B, B --- the first matching _except clause_ is triggered.

The last _except clause_ may omit the exception name(s), to serve as a wildcard. Use this with extreme caution, since it is easy to mask a real programming error in this way! It can also be used to print an error message and then re-raise the exception (allowing a caller to handle the exception as well):

import sys

try:
    f \= open('myfile.txt')
    s \= f.readline()
    i \= int(s.strip())
except OSError as err:
    print("OS error: {0}".format(err))
except ValueError:
    print("Could not convert data to an integer.")
except:
    print("Unexpected error:", sys.exc\_info()\[0\])
    raise

The [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) ... [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except) statement has an optional _else clause_, which, when present, must follow all _except clauses_. It is useful for code that must be executed if the _try clause_ does not raise an exception. For example:

for arg in sys.argv\[1:\]:
    try:
        f \= open(arg, 'r')
    except OSError:
        print('cannot open', arg)
    else:
        print(arg, 'has', len(f.readlines()), 'lines')
        f.close()

使用 `else` 子句比向 [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 子句添加额外的代码要好，因为它避免了意外捕获非 `try` ... `except` 语句保护的代码引发的异常。

发生异常时，它可能具有关联值，也称为异常 _参数_ 。参数的存在和类型取决于异常类型。

The _except clause_ may specify a variable after the exception name. The variable is bound to an exception instance with the arguments stored in `instance.args`. For convenience, the exception instance defines `__str__()` so the arguments can be printed directly without having to reference `.args`. One may also instantiate an exception first before raising it and add any attributes to it as desired.

\>>> try:
...     raise Exception('spam', 'eggs')
... except Exception as inst:
...     print(type(inst))    \# the exception instance
...     print(inst.args)     \# arguments stored in .args
...     print(inst)          \# \_\_str\_\_ allows args to be printed directly,
...                          \# but may be overridden in exception subclasses
...     x, y \= inst.args     \# unpack args
...     print('x =', x)
...     print('y =', y)
...
<class 'Exception'>
('spam', 'eggs')
('spam', 'eggs')
x = spam
y = eggs

如果异常有参数，则它们将作为未处理异常的消息的最后一部分（'详细信息'）打印。

Exception handlers don't just handle exceptions if they occur immediately in the _try clause_, but also if they occur inside functions that are called (even indirectly) in the _try clause_. For example:

\>>> def this\_fails():
...     x \= 1/0
...
\>>> try:
...     this\_fails()
... except ZeroDivisionError as err:
...     print('Handling run-time error:', err)
...
Handling run-time error: division by zero

## 8.4. 触发异常[¶](#raising-exceptions "永久链接至标题")

[`raise`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#raise) 语句支持强制触发指定的异常。例如：

\>>> raise NameError('HiThere')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: HiThere

[`raise`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#raise) 唯一的参数就是要触发的异常。这个参数必须是异常实例或异常类（派生自 [`Exception`](https://docs.python.org/zh-cn/3/library/exceptions.html#Exception "Exception") 的类）。如果传递的是异常类，将通过调用没有参数的构造函数来隐式实例化：

raise ValueError  \# shorthand for 'raise ValueError()'

如果你需要确定是否引发了异常但不打算处理它，则可以使用更简单的 [`raise`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#raise) 语句形式重新引发异常

\>>> try:
...     raise NameError('HiThere')
... except NameError:
...     print('An exception flew by!')
...     raise
...
An exception flew by!
Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
NameError: HiThere

## 8.5. 异常链[¶](#exception-chaining "永久链接至标题")

[`raise`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#raise) 语句允许可选的 [`from`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#from) 子句，它启用了链式异常。 例如:

\# exc must be exception instance or None.
raise RuntimeError from exc

这在要转换异常时很有用。例如：

\>>> def func():
...     raise ConnectionError
...
\>>> try:
...     func()
... except ConnectionError as exc:
...     raise RuntimeError('Failed to open database') from exc
...
Traceback (most recent call last):
  File "<stdin>", line 2, in <module>
  File "<stdin>", line 2, in func
ConnectionError

The above exception was the direct cause of the following exception:

Traceback (most recent call last):
  File "<stdin>", line 4, in <module>
RuntimeError: Failed to open database

Exception chaining happens automatically when an exception is raised inside an [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except) or [`finally`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#finally) section. This can be disabled by using `from None` idiom:

\>>> try:
...     open('database.sqlite')
... except IOError:
...     raise RuntimeError from None
...
Traceback (most recent call last):
  File "<stdin>", line 4, in <module>
RuntimeError

异常链机制详见 [内置异常](https://docs.python.org/zh-cn/3/library/exceptions.html#bltin-exceptions)。

## 8.6. 用户自定义异常[¶](#user-defined-exceptions "永久链接至标题")

程序可以通过创建新的异常类来命名它们自己的异常（有关Python 类的更多信息，请参阅 [类](classes.md#tut-classes)）。异常通常应该直接或间接地从 [`Exception`](https://docs.python.org/zh-cn/3/library/exceptions.html#Exception "Exception") 类派生。

可以定义异常类，它可以执行任何其他类可以执行的任何操作，但通常保持简单，只提供一些属性，这些属性允许处理程序为异常提取有关错误的信息。 在创建可能引发多个不同错误的模块时，通常的做法是为该模块定义的异常创建基类，并为不同错误条件创建特定异常类的子类:

class Error(Exception):
    """Base class for exceptions in this module."""
    pass

class InputError(Error):
    """Exception raised for errors in the input.

 Attributes:
 expression -- input expression in which the error occurred
 message -- explanation of the error
 """

    def \_\_init\_\_(self, expression, message):
        self.expression \= expression
        self.message \= message

class TransitionError(Error):
    """Raised when an operation attempts a state transition that's not
 allowed.

 Attributes:
 previous -- state at beginning of transition
 next -- attempted new state
 message -- explanation of why the specific transition is not allowed
 """

    def \_\_init\_\_(self, previous, next, message):
        self.previous \= previous
        self.next \= next
        self.message \= message

大多数异常都定义为名称以“Error”结尾，类似于标准异常的命名。

许多标准模块定义了它们自己的异常，以报告它们定义的函数中可能出现的错误。有关类的更多信息，请参见 [类](classes.md#tut-classes) 章节。

## 8.7. 定义清理操作[¶](#defining-clean-up-actions "永久链接至标题")

[`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 语句有另一个可选子句，用于定义必须在所有情况下执行的清理操作。例如:

\>>> try:
...     raise KeyboardInterrupt
... finally:
...     print('Goodbye, world!')
...
Goodbye, world!
KeyboardInterrupt
Traceback (most recent call last):
  File "<stdin>", line 2, in <module>

如果存在 [`finally`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#finally) 子句，则 `finally` 子句将作为 [`try`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#try) 语句结束前的最后一项任务被执行。 `finally` 子句不论 `try` 语句是否产生了异常都会被执行。 以下几点讨论了当异常发生时一些更复杂的情况：

*   如果在执行 `try` 子句期间发生了异常，该异常可由一个 [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except) 子句进行处理。 如果异常没有被某个 `except` 子句所处理，则该异常会在 `finally` 子句执行之后被重新引发。
    
*   异常也可能在 `except` 或 `else` 子句执行期间发生。 同样地，该异常会在 `finally` 子句执行之后被重新引发。
    
*   如果在执行 `try` 语句时遇到一个 [`break`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#break), [`continue`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#continue) 或 [`return`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#return) 语句，则 `finally` 子句将在执行 `break`, `continue` 或 `return` 语句之前被执行。
    
*   如果 `finally` 子句中包含一个 `return` 语句，则返回值将来自 `finally` 子句的某个 `return` 语句的返回值，而非来自 `try` 子句的 `return` 语句的返回值。
    

例如

\>>> def bool\_return():
...     try:
...         return True
...     finally:
...         return False
...
\>>> bool\_return()
False

一个更为复杂的例子:

\>>> def divide(x, y):
...     try:
...         result \= x / y
...     except ZeroDivisionError:
...         print("division by zero!")
...     else:
...         print("result is", result)
...     finally:
...         print("executing finally clause")
...
\>>> divide(2, 1)
result is 2.0
executing finally clause
\>>> divide(2, 0)
division by zero!
executing finally clause
\>>> divide("2", "1")
executing finally clause
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 3, in divide
TypeError: unsupported operand type(s) for /: 'str' and 'str'

正如你所看到的，[`finally`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#finally) 子句在任何情况下都会被执行。 两个字符串相除所引发的 [`TypeError`](https://docs.python.org/zh-cn/3/library/exceptions.html#TypeError "TypeError") 不会由 [`except`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#except) 子句处理，因此会在 `finally` 子句执行后被重新引发。

在实际应用程序中，[`finally`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#finally) 子句对于释放外部资源（例如文件或者网络连接）非常有用，无论是否成功使用资源。

## 8.8. 预定义的清理操作[¶](#predefined-clean-up-actions "永久链接至标题")

某些对象定义了在不再需要该对象时要执行的标准清理操作，无论使用该对象的操作是成功还是失败，清理操作都会被执行。 请查看下面的示例，它尝试打开一个文件并把其内容打印到屏幕上。:

for line in open("myfile.txt"):
    print(line, end\="")

这个代码的问题在于，它在这部分代码执行完后，会使文件在一段不确定的时间内处于打开状态。这在简单脚本中不是问题，但对于较大的应用程序来说可能是个问题。 [`with`](https://docs.python.org/zh-cn/3/reference/compound_stmts.html#with) 语句允许像文件这样的对象能够以一种确保它们得到及时和正确的清理的方式使用。:

with open("myfile.txt") as f:
    for line in f:
        print(line, end\="")

执行完语句后，即使在处理行时遇到问题，文件 _f_ 也始终会被关闭。和文件一样，提供预定义清理操作的对象将在其文档中指出这一点。

### [目录](https://docs.python.org/zh-cn/3/contents.html)

*   [8\. 错误和异常](#)
    *   [8.1. 句法错误](#syntax-errors)
    *   [8.2. 异常](#exceptions)
    *   [8.3. 处理异常](#handling-exceptions)
    *   [8.4. 触发异常](#raising-exceptions)
    *   [8.5. 异常链](#exception-chaining)
    *   [8.6. 用户自定义异常](#user-defined-exceptions)
    *   [8.7. 定义清理操作](#defining-clean-up-actions)
    *   [8.8. 预定义的清理操作](#predefined-clean-up-actions)

#### 上一个主题

[7\. 输入与输出](inputoutput.md "上一章")

#### 下一个主题

[9\. 类](classes.md "下一章")

### 本页

*   [提交 Bug](https://docs.python.org/zh-cn/3/bugs.html)
*   [显示源代码](https://github.com/python/cpython/blob/master/Doc/tutorial/errors.rst)

### 导航

*   [索引](https://docs.python.org/zh-cn/3/genindex.html "总目录")
*   [模块](https://docs.python.org/zh-cn/3/py-modindex.html "Python 模块索引") |
*   [下一页](classes.md "9. 类") |
*   [上一页](inputoutput.md "7. 输入与输出") |
*   ![](https://docs.python.org/zh-cn/3/_static/py.png)
*   [Python](https://www.python.org/) »
*   [3.10.0a6 Documentation](https://docs.python.org/zh-cn/3/index.html) »
*   [Python 教程](index.md) »
*   8\. 错误和异常
*      
    
    $('.inline-search').show(0); |

© [版权所有](https://docs.python.org/zh-cn/3/copyright.html) 2001-2021, Python Software Foundation.  
This page is licensed under the Python Software Foundation License Version 2.  
Examples, recipes, and other code in the documentation are additionally licensed under the Zero Clause BSD License.  
See History and License for more information.  
  
The Python Software Foundation is a non-profit corporation. [Please donate.](https://www.python.org/psf/donations/)  
  
最后更新于 3月 19, 2021. [Found a bug](https://docs.python.org/3/bugs.html)?  
Created using [Sphinx](https://www.sphinx-doc.org/) 3.2.1.
