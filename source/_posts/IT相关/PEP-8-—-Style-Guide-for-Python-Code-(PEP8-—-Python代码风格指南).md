---
title: PEP-8-—-Style-Guide-for-Python-Code-(PEP8-—-Python代码风格指南)
date: {{ date }}
tags:
categories: 
permalink:
---

# 前言

本篇文章是对[Python官网](https://www.python.org/dev/peps/pep-0008/)上的代码风格指南的翻译和注解。虽然网上已经有很多类似的翻译了，我还是希望通过自己进行翻译的方式加深对指南的理解。本文更多注重于内容的翻译，所以没有特别多的辞藻修饰，文中若有疏漏和不妥之处，欢迎大家批评指正。本文没有完全翻译结束，近期会慢慢完善。



| PEP: | 8 |
---- | ---
| Title: | Style Guide for Python Code |
| Author: | Guido van Rossum , Barry Warsaw , Nick Coghlan |
| Status: | Active |
| Type: | Process |
| Created: | 05-Jul-2001 |
| Post-History: | 05-Jul-2001, 01-Aug-2013 |


# Introduction 介绍

This document gives coding conventions for the Python code comprising the standard library in the main Python distribution. Please see the companion informational PEP describing style guidelines for the C code in the C implementation of Python [[1]](https://www.python.org/dev/peps/pep-0008/#id8). 

本文介绍的Python编程规范适用于Python主发行版中标准库。对于在Python中应用C代码的编程规范，请参见相关PEP风格指南。

This document and [PEP 257](https://www.python.org/dev/peps/pep-0257) (Docstring Conventions) were adapted from Guido’s original Python Style Guide essay, with some additions from Barry’s style guide [[2]](https://www.python.org/dev/peps/pep-0008/#id9).

本文及PEP257（Docsring 规范）改编自Guido的Python风格介绍指南原文，并增添了Barry的风格指南的相关内容。

This style guide evolves over time as additional conventions are identified and past conventions are rendered obsolete by changes in the language itself.

本风格指南随着时间不断发展，因为新的规范被认可而过时的规范会随着语言自身的变化而被废弃。

Many projects have their own coding style guidelines. In the event of any conflicts, such project-specific guides take precedence for that project.

许多项目有它们自己的代码风格指南。当本文档和它们有冲突时，应优先使用该项目的特定指南。

# A Foolish Consistency is the Hobgoblin of Little Minds 盲目的一致性是头脑简单的妖怪

[注:标题出自艾默生的《Self-Reliance》]

One of Guido’s key insights is that code is read much more often than it is written. The guidelines provided here are intended to improve the readability of code and make it consistent across the wide spectrum of Python code. As [PEP 20](https://www.python.org/dev/peps/pep-0020) says, “Readability counts”.

Guido的主要洞见之一是，代码被读的次数远多于被写的次数。本文提供的指南旨在提高代码的可读性并使浩瀚的Python代码保持一致性。

A style guide is about consistency. Consistency with this style guide is important. Consistency within a project is more important. Consistency within one module or function is the most important.

风格指南讲的是一致性。和本指南保持一致很重要。在项目内保持一致更重要。而在同一个模块或函数内保持一致性是最重要的。

However, know when to be inconsistent — sometimes style guide recommendations just aren’t applicable. When in doubt, use your best judgment. Look at other examples and decide what looks best. And don’t hesitate to ask!

然而，要明白什么时候需要不一致 — 有时风格指南的推荐就是没法用。 如果你有所怀疑，则使用你的最佳判断。参考一下其他的例子并决定怎么看起来最好。并且，别犹豫，尽管问。

In particular: do not break backwards compatibility just to comply with this PEP!

特别的：不要仅仅为了遵守这篇PEP指南而破坏代码的向后兼容性。

Some other good reasons to ignore a particular guideline:

其他可以忽略某个指南的好理由：

1.  When applying the guideline would make the code less readable, even for someone who is used to reading code that follows this PEP. 如果使用该指南会降低代码的可读性，甚至对那些习惯于使用本PEP指南的人。
2.  To be consistent with surrounding code that also breaks it (maybe for historic reasons) — although this is also an opportunity to clean up someone else’s mess (in true XP style). 为了与周围没有遵守该指南的代码保持一致（也许由于历史原因）–尽管这也许是个清理别人混乱代码的机会。
3.  Because the code in question predates the introduction of the guideline and there is no other reason to be modifying that code. 该代码的编写早于指南并且没有特殊原因需要修改这个代码。
4.  When the code needs to remain compatible with older versions of Python that don’t support the feature recommended by the style guide. 当代码需要与不支持风格指南中推荐的特征的早期Python版本保持兼容性时。

# Code lay-out 代码布局

## Indentation 缩进

Use 4 spaces per indentation level. 

每个缩进级别使用4个空格

Continuation lines should align wrapped elements either vertically using Python’s implicit line joining inside parentheses, brackets and braces, or using a *hanging indent*[[7]](https://www.python.org/dev/peps/pep-0008/#fn-hi). When using a hanging indent the following should be considered; there should be no arguments on the first line and further indentation should be used to clearly distinguish itself as a continuation line.

连续行需要对齐其所包含的元素，或者垂直的使用Python的隐式缩进，对齐圆括号、方括号及花括号，或者使用悬挂缩进。当使用悬挂缩进时，需考虑以下因素：第一行不应包含参数，后续的行应该增加一级缩进：

Yes 正确:

# Aligned with opening delimiter. 
# 和开放的符号对齐（隐式缩进）
foo = long_function_name(var_one, var_two,
                         var_three, var_four)

# More indentation included to distinguish this from the rest.
# 使用更多的缩进以便与后面的代码区分（悬挂缩进）
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)

# Hanging indents should add a level.
# 悬挂缩进需要增加一级缩进
foo = long_function_name(
    var_one, var_two,
    var_three, var_four)
</pre>

No 错误:

<pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;"># Arguments on first line forbidden when not using vertical alignment.
# 如果不使用垂直对齐（隐式缩进），第一行禁止使用参数
foo = long_function_name(var_one, var_two,
    var_three, var_four)

# Further indentation required as indentation is not distinguishable.
# （悬挂缩进）需要进一步缩进以便与后续代码（print）进行区分
def long_function_name(
    var_one, var_two, var_three,
    var_four):
    print(var_one)
</pre>

The 4-space rule is optional for continuation lines.

对于连续的行，4-空格 规则不是强制的。

Optional 可选方案（此处2-空格）:

<pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;"># Hanging indents *may* be indented to other than 4 spaces.
foo = long_function_name(
  var_one, var_two,
  var_three, var_four)
</pre>

When the conditional part of an <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">if</tt>-statement is long enough to require that it be written across multiple lines, it’s worth noting that the combination of a two character keyword (i.e. <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">if</tt>), plus a single space, plus an opening parenthesis creates a natural 4-space indent for the subsequent lines of the multiline conditional. This can produce a visual conflict with the indented suite of code nested inside the <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">if</tt>-statement, which would also naturally be indented to 4 spaces. This PEP takes no explicit position on how (or whether) to further visually distinguish such conditional lines from the nested suite inside the <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">if</tt>-statement. Acceptable options in this situation include, but are not limited to: 

当if语句中的条件部分长到需要使用多行时，不值得结合使用一个2字母的关键字（比如 if）、一个空格以及开放的括号独占一行，然后（多）缩进4个空格开始后续的条件语句。由于if语句内部本身要缩进4个空格，再次缩进会造成视觉上的冲突。本PEP没有明确指出怎么（或者是否）要进一步在视觉上区分这些条件部分及if-语句内嵌套的部分。在这种情况下可接受的选择包括但不限于以下几种：

<pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;"># No extra indentation.
# 无额外缩进
if (this_is_one_thing and
    that_is_another_thing):
    do_something()

# Add a comment, which will provide some distinction in editors
# 添加一个注释，由其提供编辑器内的区分
# supporting syntax highlighting.
if (this_is_one_thing and
    that_is_another_thing):
    # Since both conditions are true, we can frobnicate.
    do_something()

# Add some extra indentation on the conditional continuation line.
# 在条件部分的连续行增加额外缩进
if (this_is_one_thing
        and that_is_another_thing):
    do_something()
</pre>

(Also see the discussion of whether to break before or after binary operators below.)

（也参见下边关于在二元运算符之前或之后换行的讨论）

The closing brace/bracket/parenthesis on multiline constructs may either line up under the first non-whitespace character of the last line of list, as in:

横跨多行的大括号/方括号/括号可以要么闭合于最后一行的第一个非空格元素，如下：

<pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">my_list = [
    1, 2, 3,
    4, 5, 6,
    ]
result = some_function_that_takes_arguments(
    'a', 'b', 'c',
    'd', 'e', 'f',
    )
</pre>

or it may be lined up under the first character of the line that starts the multiline construct, as in:

或者与这个多行结构的开始行的第一个字符对齐，如下：

<pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">my_list = [
    1, 2, 3,
    4, 5, 6,
]
result = some_function_that_takes_arguments(
    'a', 'b', 'c',
    'd', 'e', 'f',
)
</pre>

## Tabs or Spaces? 制表符还是空格？

Spaces are the preferred indentation method.

推荐使用空格进行缩进。

Tabs should be used solely to remain consistent with code that is already indented with tabs.

制表符仅在需要与已经使用制表符进行缩进的代码保持一致时才使用。

Python 3 disallows mixing the use of tabs and spaces for indentation.

Python 3 不允许在缩进时混合使用制表符和空格。

Python 2 code indented with a mixture of tabs and spaces should be converted to using spaces exclusively.

Python 2 代码中本来混合使用制表符和空格进行缩进的，需要全部转换为使用空格进行缩进。

When invoking the Python 2 command line interpreter with the <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">-t</tt> option, it issues warnings about code that illegally mixes tabs and spaces. When using <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">-tt</tt> these warnings become errors. These options are highly recommended!

当使用 -t 选项运行Python 2 代码时，会对非法混用制表符和空格的代码进行警告。 当使用 -tt 选项时，这些警告会变成报错。非常推荐使用这些选项。

## Maximum Line Length 每行最大长度

Limit all lines to a maximum of 79 characters.

每行的最大长度限定于79字符。

For flowing long blocks of text with fewer structural restrictions (docstrings or comments), the line length should be limited to 72 characters.

对于含有较少结构限制的连续大块文字（docstrings或者注释），行的长度应该限定于72字符。

Limiting the required editor window width makes it possible to have several files open side-by-side, and works well when using code review tools that present the two versions in adjacent columns.

对编辑器窗口的宽度进行限定后可以并排打开若干文件，并且便于使用代码检查工具时在相邻的两列展示不同的版本。

The default wrapping in most tools disrupts the visual structure of the code, making it more difficult to understand. The limits are chosen to avoid wrapping in editors with the window width set to 80, even if the tool places a marker glyph in the final column when wrapping lines. Some web based tools may not offer dynamic line wrapping at all.

大部分工具的默认换行功能会破坏代码的可视化结构，从而使代码更加难以理解。选择上述代码长度的限制是为了避免编辑窗口宽度为80字符时的自动换行，尽管工具会自动换行时候的最后一列设置一个标记。有些基于网页的工具也许根本就不提供自动换行功能。

Some teams strongly prefer a longer line length. For code maintained exclusively or primarily by a team that can reach agreement on this issue, it is okay to increase the nominal line length from 80 to 100 characters (effectively increasing the maximum length to 99 characters), provided that comments and docstrings are still wrapped at 72 characters.

有些团队强烈推荐较长的代码行长度。如果完全或者主要负责维护代码的队伍对此达成一致，那么将代码行长度从80提高到100字符也是可以的（有效的将最大行长度提高的99字符），同时应该确保注释和docstring仍然在72字符处换行。

The Python standard library is conservative and requires limiting lines to 79 characters (and docstrings/comments to 72).

Python的标准库是保守的并且要求行长度限定为最大79字符（并且docstrings和注释最大72字符）。

The preferred way of wrapping long lines is by using Python’s implied line continuation inside parentheses, brackets and braces. Long lines can be broken over multiple lines by wrapping expressions in parentheses. These should be used in preference to using a backslash for line continuation.

比较推荐的续行方式是在Python的圆括号、方括号和大括号内进行隐式续行。括号中的较长代码行可以折成多行。这种换行方式比使用反斜杠进行续行更受推荐。

Backslashes may still be appropriate at times. For example, long, multiple <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">with</tt>-statements cannot use implicit continuation, so backslashes are acceptable:

<pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">有时使用反斜杠也比较合适。比如，在较长的多行with语句中，不能使用隐式续行的时候，反斜杠也是可以接受的：
with open('/path/to/some/file/you/want/to/read') as file_1, \
     open('/path/to/some/file/being/written', 'w') as file_2:
    file_2.write(file_1.read())
</pre>

(See the previous discussion on multiline if-statements for further thoughts on the indentation of such multiline <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">with</tt>-statements.)

（查看之前讨论的多行if语句深入思考对这种多行with语句的缩进。）

Another such case is with <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">assert</tt> statements.

另一种类似情况是对assert语句。

Make sure to indent the continued line appropriately.

确保对连续的行进行合适的缩进。

## Should a line break before or after a binary operator? 应该在二元运算符之前还是之后换行？

For decades the recommended style was to break after binary operators. But this can hurt readability in two ways: the operators tend to get scattered across different columns on the screen, and each operator is moved away from its operand and onto the previous line. Here, the eye has to do extra work to tell which items are added and which are subtracted:

几十年来推荐的风格是在二元运算符之后换行。但是这有可能在两方面影响可读性：运算符会漫布于屏幕上不同的行，另外运算符远离它的算子并且成为较前一行。这样，眼睛就必须弄明白哪些项被加，哪些项被减：

<pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;"># No: operators sit far away from their operands
# 不要：运算符远离他们的算子
income = (gross_wages +
          taxable_interest +
          (dividends - qualified_dividends) -
          ira_deduction -
          student_loan_interest)
</pre>

To solve this readability problem, mathematicians and their publishers follow the opposite convention. Donald Knuth explains the traditional rule in his *Computers and Typesetting* series: “Although formulas within a paragraph always break after binary operations and relations, displayed formulas always break before binary operations” [[3]](https://www.python.org/dev/peps/pep-0008/#id10).

为了解决这个可读性问题，数学家和出版人追从相反的约定。Donald Knuth在他的*Computers and Typesetting*系列中解释了传统的原则: 尽管一段之内的公式常在二元运算符和关系之换行，展示出来的公式常常在二元运算符之前换行。

Following the tradition from mathematics usually results in more readable code:

根据数学家的传统常常可以得到更具可读性的代码：

<pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;"># Yes: easy to match operators with operands
# 正确：便于连接运算符和算子 
income = (gross_wages
          + taxable_interest
          + (dividends - qualified_dividends)
          - ira_deduction
          - student_loan_interest)
</pre>

In Python code, it is permissible to break before or after a binary operator, as long as the convention is consistent locally. For new code Knuth’s style is suggested.

在Python代码中，在二元运算符之前或者之后进行换行都是允许的，只要该约定保持一致性即可。对于新的代码，推荐使用Knuth的风格。

## Blank Lines 空行

Surround top-level function and class definitions with two blank lines.

使用两个空行来分隔最高级的函数和类的定义。

Method definitions inside a class are surrounded by a single blank line.

使用一个空行来分隔一个类之中的方法定义。

Extra blank lines may be used (sparingly) to separate groups of related functions. Blank lines may be omitted between a bunch of related one-liners (e.g. a set of dummy implementations).

额外的空行也许可以（谨慎地）用于分隔不同的某组相关的函数。在一系列单行代码之间（比如一系列dummy）可以省略空行。

Use blank lines in functions, sparingly, to indicate logical sections.

在函数中（谨慎的）使用空行来区分不同的逻辑块。

Python accepts the control-L (i.e. ^L) form feed character as whitespace; Many tools treat these characters as page separators, so you may use them to separate pages of related sections of your file. Note, some editors and web-based code viewers may not recognize control-L as a form feed and will show another glyph in its place.

Python接受control-L (即 ^L)作为空格；许多工具把这些作为分页符，因此你可以用它们来对文件中的相关块进行分页。注意，有些编辑器和基于网页的代码浏览器也许不把control-L识别为换页符，它们也许会被显示为其他符号。 

## Source File Encoding 源文件编码

Code in the core Python distribution should always use UTF-8 (or ASCII in Python 2).

Python核心发行版中的代码应该保持使用UTF-8（或者Python2使用ASCII）。

Files using ASCII (in Python 2) or UTF-8 (in Python 3) should not have an encoding declaration.

使用ASCII（Python 2）和UTF-8 （Python 3）的文件不需要编码声明。

In the standard library, non-default encodings should be used only for test purposes or when a comment or docstring needs to mention an author name that contains non-ASCII characters; otherwise, using <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">\x</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">\u</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">\U</tt>, or <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">\N</tt> escapes is the preferred way to include non-ASCII data in string literals.

在标准库中，非默认的编码应该仅用于测试目的或者当注释或docstring需要提及含有非ASCII字符的作者名字时；否则，推荐使用<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">\x</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">\u</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">\U</tt> 和 <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">\N</tt> 等转义符是表达字符串中的非ASCII数据。

For Python 3.0 and beyond, the following policy is prescribed for the standard library (see [PEP 3131](https://www.python.org/dev/peps/pep-3131)): All identifiers in the Python standard library MUST use ASCII-only identifiers, and SHOULD use English words wherever feasible (in many cases, abbreviations and technical terms are used which aren’t English). In addition, string literals and comments must also be in ASCII. The only exceptions are (a) test cases testing the non-ASCII features, and (b) names of authors. Authors whose names are not based on the Latin alphabet (latin-1, ISO/IEC 8859-1 character set) MUST provide a transliteration of their names in this character set.

对于Python 3.0以上的版本，标准库遵循以下原则（参见 [PEP 3131](https://www.python.org/dev/peps/pep-3131)）：标准库中的所有标识符都**必须**仅使用ASCII标识符，并且在任何可能的情况下**应该**使用英语（在很多情况下，缩写和技术名词不是英语）。此外，字符串和注释也必须是ASCII，仅有两种例外情况（a）测试情况下进行非ASCII特征进行测试， （b）作者名字。当作者的名字不是基于拉丁字母时（latin-1, ISO/IEC 8859-1 character set），作者**必须**提供他们名字的拉丁字符音译。

Open source projects with a global audience are encouraged to adopt a similar policy.

鼓励面向全世界开源的项目使用类似原则。

## Imports

*   Imports should usually be on separate lines, e.g.: 通常Imports应该在单独的一行，比如：

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">Yes: import os
         import sys

    No:  import sys, os
    </pre>

    It’s okay to say this though: 尽管如此，如下语句也可以：

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">from subprocess import Popen, PIPE
    </pre>

*   Imports are always put at the top of the file, just after any module comments and docstrings, and before module globals and constants. Imports语句总是在文件的最顶端，仅在模块注释和docstring之后，并且在全局模块和常量之前：

    Imports should be grouped in the following order: Imports应该按以下顺序进行分组：

    1.  standard library imports 标准库imports
    2.  related third party imports 相关第三方 imports
    3.  local application/library specific imports 本地应用和库的特定imports

    You should put a blank line between each group of imports. 你应该在每组之间加入空行。

*   Absolute imports are recommended, as they are usually more readable and tend to be better behaved (or at least give better error messages) if the import system is incorrectly configured (such as when a directory inside a package ends up on <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">sys.path</tt>): 推荐使用绝对imports，因为如果import系统正确配置的话（比如包内的路径以sys.path），通常来说使用绝对imports更加具有可读性而且表现更好 （至少会提供更好的报错信息）

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">import mypkg.sibling
    from mypkg import sibling
    from mypkg.sibling import example
    </pre>

    However, explicit relative imports are an acceptable alternative to absolute imports, especially when dealing with complex package layouts where using absolute imports would be unnecessarily verbose: 然而，除了绝对imports之外，详尽的相对imports也是可以接受的，特别是当使用复杂的包时当绝对imports变得不必要的冗长的时候，

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">from . import sibling
    from .sibling import example
    </pre>

    Standard library code should avoid complex package layouts and always use absolute imports. 标准库代码应该避免复杂的包并且始终使用绝对imports。

    Implicit relative imports should *never* be used and have been removed in Python 3. 不明确的相对引用应该*从不*被使用，并且在Python 3中已经被移除。

*   When importing a class from a class-containing module, it’s usually okay to spell this: 当从一个含有类的模块中import一个类的时候，以下语句也可以：

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">from myclass import MyClass
    from foo.bar.yourclass import YourClass
    </pre>

    If this spelling causes local name clashes, then spell them 如果以下拼写造成了本地变量名冲突的话，则使用：

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">import myclass
    import foo.bar.yourclass
    </pre>

    and use “myclass.MyClass” and “foo.bar.yourclass.YourClass”. 并且用 “myclass.MyClass” 和 “foo.bar.yourclass.YourClass”

*   Wildcard imports (<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">from <module> import *</tt>) should be avoided, as they make it unclear which names are present in the namespace, confusing both readers and many automated tools. There is one defensible use case for a wildcard import, which is to republish an internal interface as part of a public API (for example, overwriting a pure Python implementation of an interface with the definitions from an optional accelerator module and exactly which definitions will be overwritten isn’t known in advance). 应该避免使用通配符import， (<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">from <module> import *</tt>)，因为会造成命名空间中的名称不清晰，给读者和许多自动化工具造成困扰。在一种情况下可以使用通配符import，也就是当把一个内部接口作为一个公共API重新发布的时候（比如，通过一个可选加速器模块覆盖一个纯Python实现的接口，并且哪些定义会被覆盖提前并不能预知。）

    When republishing names this way, the guidelines below regarding public and internal interfaces still apply. 当这样重复发布名称时，以下关于公共和内部接口的指南依然适用。

## Module level dunder names 模块层dunder名称

Module level “dunders” (i.e. names with two leading and two trailing underscores) such as <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__all__</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__author__</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__version__</tt>, etc. should be placed after the module docstring but before any import statements *except*<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">from __future__</tt> imports. Python mandates that future-imports must appear in the module before any other code except docstrings.

模块层的“dunders” （即名称中含有两个前和两个后下划线）比如 <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__all__</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__author__</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__version__ 等，应该放置于模块的文档说明之后但是在任何除了<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">from __future__ imports之外的import语句之前。Python要求future-imports必须比除了文档说明之外的任何代码更早出现在模块。</tt></tt>

For example: 例如：

<pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">"""This is the example module.

This module does stuff.
"""

from __future__ import barry_as_FLUFL

__all__ = ['a', 'b', 'c']
__version__ = '0.1'
__author__ = 'Cardinal Biggles'

import os
import sys
</pre>

# String Quotes 字符串引用

In Python, single-quoted strings and double-quoted strings are the same. This PEP does not make a recommendation for this. Pick a rule and stick to it. When a string contains single or double quote characters, however, use the other one to avoid backslashes in the string. It improves readability.

在Python中，单引号字符串和双引号字符串是相同的。本PEP没有对此进行推荐。可以自选一个并且保持一致。然而，如果一个字符串含有单引号或者双引号，使用另一个来避免反斜线。这可以提高可读性。

For triple-quoted strings, always use double quote characters to be consistent with the docstring convention in [PEP 257](https://www.python.org/dev/peps/pep-0257).

对于三引号，总是使用双引号字符以便与 [PEP 257](https://www.python.org/dev/peps/pep-0257)中的文档说明的约定保持一致。

# Whitespace in Expressions and Statements 表达式和语句中的空格

## Pet Peeves

Avoid extraneous whitespace in the following situations:

避免在如下情况使用无关的空格：

*   Immediately inside parentheses, brackets or braces. 括号，方括号和大括号中直接的空格。

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">Yes: spam(ham[1], {eggs: 2})
    No:  spam( ham[ 1 ], { eggs: 2 } )
    </pre>

*   Between a trailing comma and a following close parenthesis. 在尾随逗号和结束括号之间。

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">Yes: foo = (0,)
    No:  bar = (0, )
    </pre>

*   Immediately before a comma, semicolon, or colon: 直接在逗号、分号和冒号之前。

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">Yes: if x == 4: print x, y; x, y = y, x
    No:  if x == 4 : print x , y ; x , y = y , x
    </pre>

*   However, in a slice the colon acts like a binary operator, and should have equal amounts on either side (treating it as the operator with the lowest priority). In an extended slice, both colons must have the same amount of spacing applied. Exception: when a slice parameter is omitted, the space is omitted. 然而，在切片中冒号类似于二元运算符，应该在其两边使用相同数量的空格（把它作为拥有最低优先级的运算符）。在扩展切片中，两个冒号必须有相同的空格。特殊情况：如果一个切片参数被省略了，空格也省略。

    Yes:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">ham[1:9], ham[1:9:3], ham[:9:3], ham[1::3], ham[1:9:]
    ham[lower:upper], ham[lower:upper:], ham[lower::step]
    ham[lower+offset : upper+offset]
    ham[: upper_fn(x) : step_fn(x)], ham[:: step_fn(x)]
    ham[lower + offset : upper + offset]
    </pre>

    No:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">ham[lower + offset:upper + offset]
    ham[1: 9], ham[1 :9], ham[1:9 :3]
    ham[lower : : upper]
    ham[ : upper]
    </pre>

*   Immediately before the open parenthesis that starts the argument list of a function call: 直接在一个函数的开始括号之前。

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">Yes: spam(1)
    No:  spam (1)
    </pre>

*   Immediately before the open parenthesis that starts an indexing or slicing: 直接在一个索引或者切片的开始括号之前。

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">Yes: dct['key'] = lst[index]
    No:  dct ['key'] = lst [index]
    </pre>

*   More than one space around an assignment (or other) operator to align it with another. 为了对齐其他参数而使用多于一个空格。

    Yes:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">x = 1
    y = 2
    long_variable = 3
    </pre>

    No:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">x             = 1
    y             = 2
    long_variable = 3
    </pre>

## Other Recommendations 其他推荐

*   Avoid trailing whitespace anywhere. Because it’s usually invisible, it can be confusing: e.g. a backslash followed by a space and a newline does not count as a line continuation marker. Some editors don’t preserve it and many projects (like CPython itself) have pre-commit hooks that reject it. 避免在任何地方使用尾空格。因为它是不可见的，这会造成困扰：比如一个反斜杠后面跟了一个空格因此新的一行不被认为是新行。有些编辑器不确保其正确运行，许多项目（比如CPython本身）有pre-commit hooks可以拒绝此类编译。

*   Always surround these binary operators with a single space on either side: assignment (<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">=</tt>), augmented assignment (<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">+=</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">-=</tt>etc.), comparisons (<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">==</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;"><</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">></tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">!=</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;"><></tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;"><=</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">>=</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">in</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">not in</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">is</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">is not</tt>), Booleans (<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">and</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">or</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">not</tt>). 总是在这些二元运算符两侧使用单独空格：等号（=），增量赋值负号 (<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">+=</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">-=</tt>etc.), 比较符号(<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">==</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;"><</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">></tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">!=</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;"><></tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;"><=</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">>=</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">in</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">not in</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">is</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">is not</tt>), 布尔运算符(<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">and</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">or</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">not</tt>).

*   If operators with different priorities are used, consider adding whitespace around the operators with the lowest priority(ies). Use your own judgment; however, never use more than one space, and always have the same amount of whitespace on both sides of a binary operator. 如果使用不同优先级的运算符，考虑给低优先级的运算符增加空格。自行判断，然而，永远不要使用多于一个空格，并且总是在二元运算符的两侧使用相同数量的空格。

    Yes:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">i = i + 1
    submitted += 1
    x = x*2 - 1
    hypot2 = x*x + y*y
    c = (a+b) * (a-b)
    </pre>

    No:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">i=i+1
    submitted +=1
    x = x * 2 - 1
    hypot2 = x * x + y * y
    c = (a + b) * (a - b)
    </pre>

*   Don’t use spaces around the <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">=</tt> sign when used to indicate a keyword argument or a default parameter value.不要在用于定义函数关键字默认值的等号两侧使用空格。

    Yes:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">def complex(real, imag=0.0):
        return magic(r=real, i=imag)
    </pre>

    No:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">def complex(real, imag = 0.0):
        return magic(r = real, i = imag)
    </pre>

*   Function annotations should use the normal rules for colons and always have spaces around the <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">-></tt> arrow if present. (See[Function Annotations](https://www.python.org/dev/peps/pep-0008/#function-annotations) below for more about function annotations.) 函数annotations 应该使用平常的冒号规则并且如果使用 <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">-> 的话需要配合空格。</tt>

    Yes:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">def munge(input: AnyStr): ...
    def munge() -> AnyStr: ...
    </pre>

    No:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">def munge(input:AnyStr): ...
    def munge()->PosInt: ...
    </pre>

*   When combining an argument annotation with a default value, use spaces around the <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">=</tt> sign (but only for those arguments that have both an annotation and a default). 当同时使用annotation和默认值的时候，给等号两侧加上空格 （但是只给同时有annotation和默认值的等号加空格）。

    Yes:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">def munge(sep: AnyStr = None): ...
    def munge(input: AnyStr, sep: AnyStr = None, limit=1000): ...
    </pre>

    No:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">def munge(input: AnyStr=None): ...
    def munge(input: AnyStr, limit = 1000): ...
    </pre>

*   Compound statements (multiple statements on the same line) are generally discouraged. 通常不推荐使用混合语句（同一行多个语句）。

    Yes:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">if foo == 'blah':
        do_blah_thing()
    do_one()
    do_two()
    do_three()
    </pre>

    Rather not:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">if foo == 'blah': do_blah_thing()
    do_one(); do_two(); do_three()
    </pre>

*   While sometimes it’s okay to put an if/for/while with a small body on the same line, never do this for multi-clause statements. Also avoid folding such long lines! 尽管有时可以将if/for/while和一小部分语句放在同一行，永远不要将含有多语句的指令放在同一行。同时也避免折叠这样的很长的行 [注：我理解是避免从这样比较长的行的某一部分进行折叠]。

    Rather not最好不要:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">if foo == 'blah': do_blah_thing()
    for x in lst: total += x
    while t < 10: t = delay()
    </pre>

    Definitely not 绝对不要:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">if foo == 'blah': do_blah_thing()
    else: do_non_blah_thing()

    try: something()
    finally: cleanup()

    do_one(); do_two(); do_three(long, argument,
                                 list, like, this)

    if foo == 'blah': one(); two(); three()</pre>

# When to use trailing commas

Trailing commas are usually optional, except they are mandatory when making a tuple of one element (and in Python 2 they have semantics for the <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">print</tt> statement). For clarity, it is recommended to surround the latter in (technically redundant) parentheses.

尾逗号通常是可选的，仅在建立一个元素的tuple时尾逗号是必须的（在Python 2中它们对于print语句是有语义的）。准确的说，推荐使用（冗余的）括号把字母括起来。

Yes 正确:

<pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">FILES = ('setup.cfg',)
</pre>

OK, but confusing 可行但是容易混淆:

<pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">FILES = 'setup.cfg',
</pre>

When trailing commas are redundant, they are often helpful when a version control system is used, when a list of values, arguments or imported items is expected to be extended over time. The pattern is to put each value (etc.) on a line by itself, always adding a trailing comma, and add the close parenthesis/bracket/brace on the next line. However it does not make sense to have a trailing comma on the same line as the closing delimiter (except in the above case of singleton tuples).

当尾逗号是冗余的时候，它们常常在使用版本控制系统时有用，或者当一个由数值、语句或者导入的项组成的列表需要随着时间不断扩展的时候。这个布局可以把每个数值（等等）单独放在一行，并加上尾逗号以及在下一行加上闭合括号/方括号/大括号。然而，不建议将尾逗号和闭合括号放在同一行（除了前边说的单元素tuple的情况）。

Yes 正确:

<pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">FILES = [
    'setup.cfg',
    'tox.ini',
    ]
initialize(FILES,
           error=True,
           )
</pre>

No 错误:

<pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">FILES = ['setup.cfg', 'tox.ini',]
initialize(FILES, error=True,)
</pre>

# Comments 注释

Comments that contradict the code are worse than no comments. Always make a priority of keeping the comments up-to-date when the code changes!

错误的注释还不如没有注释。总是在改变代码时一并更新注释。

Comments should be complete sentences. The first word should be capitalized, unless it is an identifier that begins with a lower case letter (never alter the case of identifiers!).

注释应该是完整的橘子。第一个单词需要大写首字母，除非是有一个由小写字母开头的标识符（不要改变标识符的大小写）。

Block comments generally consist of one or more paragraphs built out of complete sentences, with each sentence ending in a period.

注释块通常由一到多段完整的句子组成，每个句子由句号结尾。

You should use two spaces after a sentence-ending period in multi- sentence comments, except after the final sentence.

除了最后一句外，在多个句子组成的注释的每个句末的句号后边使用2个空格。

When writing English, follow Strunk and White.

如果注释为英语，根据Strunk and White的语法规则。

Python coders from non-English speaking countries: please write your comments in English, unless you are 120% sure that the code will never be read by people who don’t speak your language.

对于非英语国家的编程员：请用英语书写注释，除非你120%的确定这个代码永远不会被不懂你母语的人读到。

## Block Comments 注释块

Block comments generally apply to some (or all) code that follows them, and are indented to the same level as that code. Each line of a block comment starts with a <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">#</tt> and a single space (unless it is indented text inside the comment).

注释块通常应用于紧随它的部分（或者所有）代码，并且他们应该和这些代码有相同的缩进。注释块的每一行由 <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;"># 和一个空格开始（除非是注释中已经缩进的文字）</tt>

Paragraphs inside a block comment are separated by a line containing a single <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">#</tt>.

注释块内部的各段由一个单个的 <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;"># 进行分隔。</tt>

## Inline Comments 行内注释

Use inline comments sparingly.

小心地使用行内注释。

An inline comment is a comment on the same line as a statement. Inline comments should be separated by at least two spaces from the statement. They should start with a # and a single space.

行内注释是指与指令在同一行的注释。行内注释需要与指令至少相隔两个空格。他们应该由一个#和一个空格开始。

Inline comments are unnecessary and in fact distracting if they state the obvious. Don’t do this:

行内注释不必要，而且事实上很让人闹心，如果它们只是陈述明显的事实。不要像这样：

<pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">x = x + 1                 # Increment x
</pre>

But sometimes, this is useful:

但是有时候也是有用的：

<pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">x = x + 1                 # Compensate for border

[注：个人觉得这个自己把握，不需要用行内注释说明运算本身的作用，而可以用行内注释说明这行指令的潜在意图，尤其是一些特殊的意图和想法。对于有些想法，也许过了一段时间再看代码就不明白为什么当时要这么做了，那就应该注释下来。]</pre>

## Documentation Strings 文档字符串

Conventions for writing good documentation strings (a.k.a. “docstrings”) are immortalized in [PEP 257](https://www.python.org/dev/peps/pep-0257).

关于怎么写好文档字符串（a.k.a. “docstrings”）的约定详见 [PEP 257](https://www.python.org/dev/peps/pep-0257)。

*   Write docstrings for all public modules, functions, classes, and methods. Docstrings are not necessary for non-public methods, but you should have a comment that describes what the method does. This comment should appear after the <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">def</tt> line. 为所有的公共模块、函数和方法写文档字符串。对于非公共的方法，文档字符串不是必须的，但是你应该有一个描述这个方法的注释。这个注释应该出现在def行下方。

*   [PEP 257](https://www.python.org/dev/peps/pep-0257) describes good docstring conventions. Note that most importantly, the <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">"""</tt> that ends a multiline docstring should be on a line by itself, e.g.:   [PEP 257](https://www.python.org/dev/peps/pep-0257) 阐述了好的文档字符串的相关约定。注意最重要的是，<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">用以结束一个多行的文档字符串的<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">"""</tt>应该自成一行，比如：</tt>

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">"""Return a foobang

    Optional plotz says to frobnicate the bizbaz first.
    """  [注：第一个<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">"""开始了一段文档字符串，可以不自成一行。但是第二个<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">"""用以结束文档字符串，因此必须自成一行。</tt></tt>]</pre>

*   For one liner docstrings, please keep the closing <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">"""</tt> on the same line. 对于一样的文档字符串，请把用以结束的<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">"""写在同一行。</tt>

# Naming Conventions 命名约定

The naming conventions of Python’s library are a bit of a mess, so we’ll never get this completely consistent — nevertheless, here are the currently recommended naming standards. New modules and packages (including third party frameworks) should be written to these standards, but where an existing library has a different style, internal consistency is preferred.

Python的命名约定有些混乱， 所以我们从没就这点达成完全的一致 — 虽然如此，这有些目前推荐的命名标准。 新的模块和包 （包括第三方框架）应该遵从这些标准，但是对于已经存在的具有不同风格的库，建议保持内部的一致性。

## Overriding Principle 首要原则

Names that are visible to the user as public parts of the API should follow conventions that reflect usage rather than implementation.

对用户可见的API的公共部分的命名应该反映它的用途而不是其实现。

## Descriptive: Naming Styles 描述：命名风格

There are a lot of different naming styles. It helps to be able to recognize what naming style is being used, independently from what they are used for.

现存很多不同的命名风格。如果能不依赖于它们的用途而分辨出使用了哪种命名风格，会很有帮助。

The following naming styles are commonly distinguished:

通常可以区分如下命名风格：

*   <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">b</tt> (single lowercase letter) 单个小写字母

*   <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">B</tt> (single uppercase letter) 单个大写字母

*   <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">lowercase 小写字母</tt>

*   <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">lower_case_with_underscores 带下划线的小写字母</tt>

*   <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">UPPERCASE 大写字母</tt>

*   <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">UPPER_CASE_WITH_UNDERSCORES 带下划线的大写字母</tt>

*   <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">CapitalizedWords</tt> (or CapWords, or CamelCase — so named because of the bumpy look of its letters [[4]](https://www.python.org/dev/peps/pep-0008/#id11)). This is also sometimes known as StudlyCaps.单词首字母大写 （或者叫CapWord， 或者CamelCase — 这样叫是因为看起来像驼峰 [[4]](https://www.python.org/dev/peps/pep-0008/#id11)）。这种方法有时也叫StudlyCaps. 

    Note: When using acronyms in CapWords, capitalize all the letters of the acronym. Thus HTTPServerError is better than HttpServerError.

    注意：当在CapWords中使用缩写的时候，缩写的所有字母需要大写。 因此HTTPServerError 好于 HttpServerError。

*   <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">mixedCase</tt> (differs from CapitalizedWords by initial lowercase character!) 混合方式（不同于CapitalizedWords中默认为小写字母）

*   <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">Capitalized_Words_With_Underscores</tt> (ugly!) 单词首字母大写加下划线（难看！）

There’s also the style of using a short unique prefix to group related names together. This is not used much in Python, but it is mentioned for completeness. For example, the <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">os.stat()</tt> function returns a tuple whose items traditionally have names like <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">st_mode</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">st_size</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">st_mtime</tt> and so on. (This is done to emphasize the correspondence with the fields of the POSIX system call struct, which helps programmers familiar with that.)

也有一种风格是使用一个短的前缀将相关的名称分组。这种方法在Python中不常用，为了完整起见提及一下。例如，os.stat()函数返回一个tuple，这个tuple的元素传统上命名为<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">st_mode</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">st_size</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">st_mtime等。（这样做是为了强调与POSIX系统调用结构之间的关联，藉此帮助程序员对它熟悉。）</tt>

The X11 library uses a leading X for all its public functions. In Python, this style is generally deemed unnecessary because attribute and method names are prefixed with an object, and function names are prefixed with a module name.

X11库使用X作为它所有公共函数的开头。在Python中，这种风格通常不是很必要，因为属性和方法都已经有了对象的前缀，而函数名有模块名作为前缀。

In addition, the following special forms using leading or trailing underscores are recognized (these can generally be combined with any case convention):

补充一下，如下特殊格式可以使用开头或结尾的下划线（这些可以和所有的上述约定结合使用）

*   <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">_single_leading_underscore</tt>: weak “internal use” indicator. E.g. <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">from M import *</tt> does not import objects whose name starts with an underscore.

*   单下划线开头: “内部使用”的弱标识。比如，<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">from M import * 不能import名字以下划线开头的对象</tt>

*   <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">single_trailing_underscore_</tt>: used by convention to avoid conflicts with Python keyword, e.g.

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">Tkinter.Toplevel(master, class_='ClassName')</pre>

*   <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;"><tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">单下划线结尾：</tt>用于避免与Python关键字的约定，比如Tkinter.Toplevel(master, class_='ClassName')</pre>

*   <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__double_leading_underscore</tt>: when naming a class attribute, invokes name mangling (inside class FooBar, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__boo</tt> becomes<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">_FooBar__boo</tt>; see below). 

*   双下划线开头：当命名一个类的属性时，触发命名修饰（在FooBar类之内，<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__boo</tt> 成为<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">_FooBar__boo；见下方</tt>）

*   <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__double_leading_and_trailing_underscore__</tt>: “magic” objects or attributes that live in user-controlled namespaces. E.g. <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__init__</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__import__</tt> or <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__file__</tt>. Never invent such names; only use them as documented.
*   双下划线开头双下划线结尾：“魔术”对象或者属性，存在于用户控制的命名空间。例如<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__init__</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__import__</tt> 或者 <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__file__。永远不要自己创造这样的名称；请按照文档说明进行使用。</tt>

## Prescriptive: Naming Conventions

### [Names to Avoid](https://www.python.org/dev/peps/pep-0008/#id38)

Never use the characters ‘l’ (lowercase letter el), ‘O’ (uppercase letter oh), or ‘I’ (uppercase letter eye) as single character variable names.

In some fonts, these characters are indistinguishable from the numerals one and zero. When tempted to use ‘l’, use ‘L’ instead.

### [ASCII Compatibility](https://www.python.org/dev/peps/pep-0008/#id39)

Identifiers used in the standard library must be ASCII compatible as described in the [policy section](https://www.python.org/dev/peps/pep-3131/#policy-specification) of [PEP 3131](https://www.python.org/dev/peps/pep-3131).

### [Package and Module Names](https://www.python.org/dev/peps/pep-0008/#id40)

Modules should have short, all-lowercase names. Underscores can be used in the module name if it improves readability. Python packages should also have short, all-lowercase names, although the use of underscores is discouraged.

When an extension module written in C or C++ has an accompanying Python module that provides a higher level (e.g. more object oriented) interface, the C/C++ module has a leading underscore (e.g. <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">_socket</tt>).

### [Class Names](https://www.python.org/dev/peps/pep-0008/#id41)

Class names should normally use the CapWords convention.

The naming convention for functions may be used instead in cases where the interface is documented and used primarily as a callable.

Note that there is a separate convention for builtin names: most builtin names are single words (or two words run together), with the CapWords convention used only for exception names and builtin constants.

### [Type variable names](https://www.python.org/dev/peps/pep-0008/#id42)

Names of type variables introduced in [PEP 484](https://www.python.org/dev/peps/pep-0484) should normally use CapWords preferring short names: <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">T</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">AnyStr</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">Num</tt>. It is recommended to add suffixes <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">_co</tt> or <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">_contra</tt> to the variables used to declare covariant or contravariant behavior correspondingly. Examples:

<pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">from typing import TypeVar

VT_co = TypeVar('VT_co', covariant=True)
KT_contra = TypeVar('KT_contra', contravariant=True)
</pre>

### [Exception Names](https://www.python.org/dev/peps/pep-0008/#id43)

Because exceptions should be classes, the class naming convention applies here. However, you should use the suffix “Error” on your exception names (if the exception actually is an error).

### [Global Variable Names](https://www.python.org/dev/peps/pep-0008/#id44)

(Let’s hope that these variables are meant for use inside one module only.) The conventions are about the same as those for functions.

Modules that are designed for use via <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">from M import *</tt> should use the <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__all__</tt> mechanism to prevent exporting globals, or use the older convention of prefixing such globals with an underscore (which you might want to do to indicate these globals are “module non-public”).

### [Function and variable names](https://www.python.org/dev/peps/pep-0008/#id45)

Function names should be lowercase, with words separated by underscores as necessary to improve readability.

Variable names follow the same convention as function names.

mixedCase is allowed only in contexts where that’s already the prevailing style (e.g. threading.py), to retain backwards compatibility.

### [Function and method arguments](https://www.python.org/dev/peps/pep-0008/#id46)

Always use <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">self</tt> for the first argument to instance methods.

Always use <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">cls</tt> for the first argument to class methods.

If a function argument’s name clashes with a reserved keyword, it is generally better to append a single trailing underscore rather than use an abbreviation or spelling corruption. Thus <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">class_</tt> is better than <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">clss</tt>. (Perhaps better is to avoid such clashes by using a synonym.)

### [Method Names and Instance Variables](https://www.python.org/dev/peps/pep-0008/#id47)

Use the function naming rules: lowercase with words separated by underscores as necessary to improve readability.

Use one leading underscore only for non-public methods and instance variables.

To avoid name clashes with subclasses, use two leading underscores to invoke Python’s name mangling rules.

Python mangles these names with the class name: if class Foo has an attribute named <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__a</tt>, it cannot be accessed by <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">Foo.__a</tt>. (An insistent user could still gain access by calling <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">Foo._Foo__a</tt>.) Generally, double leading underscores should be used only to avoid name conflicts with attributes in classes designed to be subclassed.

Note: there is some controversy about the use of __names (see below).

### [Constants](https://www.python.org/dev/peps/pep-0008/#id48)

Constants are usually defined on a module level and written in all capital letters with underscores separating words. Examples include <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">MAX_OVERFLOW</tt> and <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">TOTAL</tt>.

### [Designing for inheritance](https://www.python.org/dev/peps/pep-0008/#id49)

Always decide whether a class’s methods and instance variables (collectively: “attributes”) should be public or non-public. If in doubt, choose non-public; it’s easier to make it public later than to make a public attribute non-public.

Public attributes are those that you expect unrelated clients of your class to use, with your commitment to avoid backward incompatible changes. Non-public attributes are those that are not intended to be used by third parties; you make no guarantees that non-public attributes won’t change or even be removed.

We don’t use the term “private” here, since no attribute is really private in Python (without a generally unnecessary amount of work).

Another category of attributes are those that are part of the “subclass API” (often called “protected” in other languages). Some classes are designed to be inherited from, either to extend or modify aspects of the class’s behavior. When designing such a class, take care to make explicit decisions about which attributes are public, which are part of the subclass API, and which are truly only to be used by your base class.

With this in mind, here are the Pythonic guidelines:

*   Public attributes should have no leading underscores.

*   If your public attribute name collides with a reserved keyword, append a single trailing underscore to your attribute name. This is preferable to an abbreviation or corrupted spelling. (However, notwithstanding this rule, ‘cls’ is the preferred spelling for any variable or argument which is known to be a class, especially the first argument to a class method.)

    Note 1: See the argument name recommendation above for class methods.

*   For simple public data attributes, it is best to expose just the attribute name, without complicated accessor/mutator methods. Keep in mind that Python provides an easy path to future enhancement, should you find that a simple data attribute needs to grow functional behavior. In that case, use properties to hide functional implementation behind simple data attribute access syntax.

    Note 1: Properties only work on new-style classes.

    Note 2: Try to keep the functional behavior side-effect free, although side-effects such as caching are generally fine.

    Note 3: Avoid using properties for computationally expensive operations; the attribute notation makes the caller believe that access is (relatively) cheap.

*   If your class is intended to be subclassed, and you have attributes that you do not want subclasses to use, consider naming them with double leading underscores and no trailing underscores. This invokes Python’s name mangling algorithm, where the name of the class is mangled into the attribute name. This helps avoid attribute name collisions should subclasses inadvertently contain attributes with the same name.

    Note 1: Note that only the simple class name is used in the mangled name, so if a subclass chooses both the same class name and attribute name, you can still get name collisions.

    Note 2: Name mangling can make certain uses, such as debugging and <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__getattr__()</tt>, less convenient. However the name mangling algorithm is well documented and easy to perform manually.

    Note 3: Not everyone likes name mangling. Try to balance the need to avoid accidental name clashes with potential use by advanced callers.

## [Public and internal interfaces](https://www.python.org/dev/peps/pep-0008/#id50)

Any backwards compatibility guarantees apply only to public interfaces. Accordingly, it is important that users be able to clearly distinguish between public and internal interfaces.

Documented interfaces are considered public, unless the documentation explicitly declares them to be provisional or internal interfaces exempt from the usual backwards compatibility guarantees. All undocumented interfaces should be assumed to be internal.

To better support introspection, modules should explicitly declare the names in their public API using the <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__all__</tt> attribute. Setting <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__all__</tt> to an empty list indicates that the module has no public API.

Even with <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__all__</tt> set appropriately, internal interfaces (packages, modules, classes, functions, attributes or other names) should still be prefixed with a single leading underscore.

An interface is also considered internal if any containing namespace (package, module or class) is considered internal.

Imported names should always be considered an implementation detail. Other modules must not rely on indirect access to such imported names unless they are an explicitly documented part of the containing module’s API, such as <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">os.path</tt> or a package’s <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__init__</tt> module that exposes functionality from submodules.

# [Programming Recommendations](https://www.python.org/dev/peps/pep-0008/#id51)

*   Code should be written in a way that does not disadvantage other implementations of Python (PyPy, Jython, IronPython, Cython, Psyco, and such).

    For example, do not rely on CPython’s efficient implementation of in-place string concatenation for statements in the form <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">a += b</tt> or <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">a = a + b</tt>. This optimization is fragile even in CPython (it only works for some types) and isn’t present at all in implementations that don’t use refcounting. In performance sensitive parts of the library, the <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">''.join()</tt> form should be used instead. This will ensure that concatenation occurs in linear time across various implementations.

*   Comparisons to singletons like None should always be done with <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">is</tt> or <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">is not</tt>, never the equality operators.

    Also, beware of writing <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">if x</tt> when you really mean <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">if x is not None</tt> — e.g. when testing whether a variable or argument that defaults to None was set to some other value. The other value might have a type (such as a container) that could be false in a boolean context!

*   Use <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">is not</tt> operator rather than <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">not ... is</tt>. While both expressions are functionally identical, the former is more readable and preferred.

    Yes:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">if foo is not None:
    </pre>

    No:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">if not foo is None:
    </pre>

*   When implementing ordering operations with rich comparisons, it is best to implement all six operations (<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__eq__</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__ne__</tt>,<tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__lt__</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__le__</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__gt__</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__ge__</tt>) rather than relying on other code to only exercise a particular comparison.

    To minimize the effort involved, the <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">functools.total_ordering()</tt> decorator provides a tool to generate missing comparison methods.

    [PEP 207](https://www.python.org/dev/peps/pep-0207) indicates that reflexivity rules *are* assumed by Python. Thus, the interpreter may swap <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">y > x</tt> with <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">x < y</tt>, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">y >= x</tt>with <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">x <= y</tt>, and may swap the arguments of <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">x == y</tt> and <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">x != y</tt>. The <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">sort()</tt> and <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">min()</tt> operations are guaranteed to use the <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;"><</tt> operator and the <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">max()</tt> function uses the <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">></tt> operator. However, it is best to implement all six operations so that confusion doesn’t arise in other contexts.

*   Always use a def statement instead of an assignment statement that binds a lambda expression directly to an identifier.

    Yes:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">def f(x): return 2*x
    </pre>

    No:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">f = lambda x: 2*x
    </pre>

    The first form means that the name of the resulting function object is specifically ‘f’ instead of the generic ‘<lambda>’. This is more useful for tracebacks and string representations in general. The use of the assignment statement eliminates the sole benefit a lambda expression can offer over an explicit def statement (i.e. that it can be embedded inside a larger expression)

*   Derive exceptions from <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">Exception</tt> rather than <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">BaseException</tt>. Direct inheritance from <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">BaseException</tt> is reserved for exceptions where catching them is almost always the wrong thing to do.

    Design exception hierarchies based on the distinctions that code *catching* the exceptions is likely to need, rather than the locations where the exceptions are raised. Aim to answer the question “What went wrong?” programmatically, rather than only stating that “A problem occurred” (see [PEP 3151](https://www.python.org/dev/peps/pep-3151) for an example of this lesson being learned for the builtin exception hierarchy)

    Class naming conventions apply here, although you should add the suffix “Error” to your exception classes if the exception is an error. Non-error exceptions that are used for non-local flow control or other forms of signaling need no special suffix.

*   Use exception chaining appropriately. In Python 3, “raise X from Y” should be used to indicate explicit replacement without losing the original traceback.

    When deliberately replacing an inner exception (using “raise X” in Python 2 or “raise X from None” in Python 3.3+), ensure that relevant details are transferred to the new exception (such as preserving the attribute name when converting KeyError to AttributeError, or embedding the text of the original exception in the new exception message).

*   When raising an exception in Python 2, use <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">raise ValueError('message')</tt> instead of the older form <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">raise ValueError, 'message'</tt>.

    The latter form is not legal Python 3 syntax.

    The paren-using form also means that when the exception arguments are long or include string formatting, you don’t need to use line continuation characters thanks to the containing parentheses.

*   When catching exceptions, mention specific exceptions whenever possible instead of using a bare <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">except:</tt> clause.

    For example, use:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">try:
        import platform_specific_module
    except ImportError:
        platform_specific_module = None
    </pre>

    A bare <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">except:</tt> clause will catch SystemExit and KeyboardInterrupt exceptions, making it harder to interrupt a program with Control-C, and can disguise other problems. If you want to catch all exceptions that signal program errors, use <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">except Exception:</tt> (bare except is equivalent to <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">except BaseException:</tt>).

    A good rule of thumb is to limit use of bare ‘except’ clauses to two cases:

    1.  If the exception handler will be printing out or logging the traceback; at least the user will be aware that an error has occurred.
    2.  If the code needs to do some cleanup work, but then lets the exception propagate upwards with <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">raise</tt>. <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">try...finally</tt>can be a better way to handle this case.
*   When binding caught exceptions to a name, prefer the explicit name binding syntax added in Python 2.6:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">try:
        process_data()
    except Exception as exc:
        raise DataProcessingFailedError(str(exc))
    </pre>

    This is the only syntax supported in Python 3, and avoids the ambiguity problems associated with the older comma-based syntax.

*   When catching operating system errors, prefer the explicit exception hierarchy introduced in Python 3.3 over introspection of <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">errno</tt> values.

*   Additionally, for all try/except clauses, limit the <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">try</tt> clause to the absolute minimum amount of code necessary. Again, this avoids masking bugs.

    Yes:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">try:
        value = collection[key]
    except KeyError:
        return key_not_found(key)
    else:
        return handle_value(value)
    </pre>

    No:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">try:
        # Too broad!
        return handle_value(collection[key])
    except KeyError:
        # Will also catch KeyError raised by handle_value()
        return key_not_found(key)
    </pre>

*   When a resource is local to a particular section of code, use a <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">with</tt> statement to ensure it is cleaned up promptly and reliably after use. A try/finally statement is also acceptable.

*   Context managers should be invoked through separate functions or methods whenever they do something other than acquire and release resources. For example:

    Yes:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">with conn.begin_transaction():
        do_stuff_in_transaction(conn)
    </pre>

    No:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">with conn:
        do_stuff_in_transaction(conn)
    </pre>

    The latter example doesn’t provide any information to indicate that the <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__enter__</tt> and <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">__exit__</tt> methods are doing something other than closing the connection after a transaction. Being explicit is important in this case.

*   Be consistent in return statements. Either all return statements in a function should return an expression, or none of them should. If any return statement returns an expression, any return statements where no value is returned should explicitly state this as <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">return None</tt>, and an explicit return statement should be present at the end of the function (if reachable).

    Yes:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">def foo(x):
        if x >= 0:
            return math.sqrt(x)
        else:
            return None

    def bar(x):
        if x < 0:
            return None
        return math.sqrt(x)
    </pre>

    No:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">def foo(x):
        if x >= 0:
            return math.sqrt(x)

    def bar(x):
        if x < 0:
            return
        return math.sqrt(x)
    </pre>

*   Use string methods instead of the string module.

    String methods are always much faster and share the same API with unicode strings. Override this rule if backward compatibility with Pythons older than 2.0 is required.

*   Use <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">''.startswith()</tt> and <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">''.endswith()</tt> instead of string slicing to check for prefixes or suffixes.

    startswith() and endswith() are cleaner and less error prone. For example:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">Yes: if foo.startswith('bar'):
    No:  if foo[:3] == 'bar':
    </pre>

*   Object type comparisons should always use isinstance() instead of comparing types directly.

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">Yes: if isinstance(obj, int):

    No:  if type(obj) is type(1):
    </pre>

    When checking if an object is a string, keep in mind that it might be a unicode string too! In Python 2, str and unicode have a common base class, basestring, so you can do:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">if isinstance(obj, basestring):
    </pre>

    Note that in Python 3, <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">unicode</tt> and <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">basestring</tt> no longer exist (there is only <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">str</tt>) and a bytes object is no longer a kind of string (it is a sequence of integers instead)

*   For sequences, (strings, lists, tuples), use the fact that empty sequences are false.

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">Yes: if not seq:
         if seq:

    No: if len(seq):
        if not len(seq):
    </pre>

*   Don’t write string literals that rely on significant trailing whitespace. Such trailing whitespace is visually indistinguishable and some editors (or more recently, reindent.py) will trim them.

*   Don’t compare boolean values to True or False using <tt class="docutils literal" style="box-sizing: border-box; margin: 0px; padding: 0px;">==</tt>.

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">Yes:   if greeting:
    No:    if greeting == True:
    Worse: if greeting is True:
    </pre>

## [Function Annotations](https://www.python.org/dev/peps/pep-0008/#id52)

With the acceptance of [PEP 484](https://www.python.org/dev/peps/pep-0484), the style rules for function annotations are changing.

*   In order to be forward compatible, function annotations in Python 3 code should preferably use [PEP 484](https://www.python.org/dev/peps/pep-0484) syntax. (There are some formatting recommendations for annotations in the previous section.)

*   The experimentation with annotation styles that was recommended previously in this PEP is no longer encouraged.

*   However, outside the stdlib, experiments within the rules of [PEP 484](https://www.python.org/dev/peps/pep-0484) are now encouraged. For example, marking up a large third party library or application with [PEP 484](https://www.python.org/dev/peps/pep-0484) style type annotations, reviewing how easy it was to add those annotations, and observing whether their presence increases code understandability.

*   The Python standard library should be conservative in adopting such annotations, but their use is allowed for new code and for big refactorings.

*   For code that wants to make a different use of function annotations it is recommended to put a comment of the form:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;"># type: ignore
    </pre>

    near the top of the file; this tells type checker to ignore all annotations. (More fine-grained ways of disabling complaints from type checkers can be found in [PEP 484](https://www.python.org/dev/peps/pep-0484).)

*   Like linters, type checkers are optional, separate tools. Python interpreters by default should not issue any messages due to type checking and should not alter their behavior based on annotations.

*   Users who don’t want to use type checkers are free to ignore them. However, it is expected that users of third party library packages may want to run type checkers over those packages. For this purpose [PEP 484](https://www.python.org/dev/peps/pep-0484) recommends the use of stub files: .pyi files that are read by the type checker in preference of the corresponding .py files. Stub files can be distributed with a library, or separately (with the library author’s permission) through the typeshed repo [[5]](https://www.python.org/dev/peps/pep-0008/#id12).

*   For code that needs to be backwards compatible, type annotations can be added in the form of comments. See the relevant section of [PEP 484](https://www.python.org/dev/peps/pep-0484) [[6]](https://www.python.org/dev/peps/pep-0008/#id13).

## [Variable annotations](https://www.python.org/dev/peps/pep-0008/#id53)

[PEP 526](https://www.python.org/dev/peps/pep-0526) introduced variable annotations. The style recommendations for them are similar to those on function annotations described above:

*   Annotations for module level variables, class and instance variables, and local variables should have a single space after the colon.

*   There should be no space before the colon.

*   If an assignment has a right hand side, then the equality sign should have exactly one space on both sides.

*   Yes:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">code: int

    class Point:
        coords: Tuple[int, int]
        label: str = '<unknown>'
    </pre>

*   No:

    <pre class="literal-block" style="box-sizing: border-box; margin: 0px; padding: 0px; overflow: auto; font-family: Menlo, Monaco, Consolas, &quot;Courier New&quot;, monospace; font-size: 13px; display: block; line-height: 1.42857; color: rgb(51, 51, 51); word-break: break-all; word-wrap: break-word; background-color: rgb(245, 245, 245); border: 1px solid rgb(204, 204, 204); border-radius: 4px;">code:int  # No space after colon
    code : int  # Space before colon

    class Test:
        result: int=0  # No spaces around equality sign
    </pre>

*   Although the [PEP 526](https://www.python.org/dev/peps/pep-0526) is accepted for Python 3.6, the variable annotation syntax is the preferred syntax for stub files on all versions of Python (see [PEP 484](https://www.python.org/dev/peps/pep-0484) for details).

Footnotes

<colgroup style="box-sizing: border-box; margin: 0px; padding: 0px;"><col style="box-sizing: border-box; margin: 0px; padding: 0px;"></colgroup>
| [[7]](https://www.python.org/dev/peps/pep-0008/#id3) | *Hanging indentation* is a type-setting style where all the lines in a paragraph are indented except the first line. In the context of Python, the term is used to describe a style where the opening parenthesis of a parenthesized statement is the last non-whitespace character of the line, with subsequent lines being indented until the closing parenthesis. |

# [References](https://www.python.org/dev/peps/pep-0008/#id54)

<colgroup style="box-sizing: border-box; margin: 0px; padding: 0px;"><col style="box-sizing: border-box; margin: 0px; padding: 0px;"></colgroup>
| [[1]](https://www.python.org/dev/peps/pep-0008/#id1) | [PEP 7](https://www.python.org/dev/peps/pep-0007), Style Guide for C Code, van Rossum |

<colgroup style="box-sizing: border-box; margin: 0px; padding: 0px;"><col style="box-sizing: border-box; margin: 0px; padding: 0px;"></colgroup>
| [[2]](https://www.python.org/dev/peps/pep-0008/#id2) | Barry’s GNU Mailman style guide [http://barry.warsaw.us/software/STYLEGUIDE.txt](http://barry.warsaw.us/software/STYLEGUIDE.txt) |

<colgroup style="box-sizing: border-box; margin: 0px; padding: 0px;"><col style="box-sizing: border-box; margin: 0px; padding: 0px;"></colgroup>
| [[3]](https://www.python.org/dev/peps/pep-0008/#id4) | Donald Knuth’s *The TeXBook*, pages 195 and 196. |

<colgroup style="box-sizing: border-box; margin: 0px; padding: 0px;"><col style="box-sizing: border-box; margin: 0px; padding: 0px;"></colgroup>
| [[4]](https://www.python.org/dev/peps/pep-0008/#id5) | [http://www.wikipedia.com/wiki/CamelCase](http://www.wikipedia.com/wiki/CamelCase) |

<colgroup style="box-sizing: border-box; margin: 0px; padding: 0px;"><col style="box-sizing: border-box; margin: 0px; padding: 0px;"></colgroup>
| [[5]](https://www.python.org/dev/peps/pep-0008/#id6) | Typeshed repo [https://github.com/python/typeshed](https://github.com/python/typeshed) |

<colgroup style="box-sizing: border-box; margin: 0px; padding: 0px;"><col style="box-sizing: border-box; margin: 0px; padding: 0px;"></colgroup>
| [[6]](https://www.python.org/dev/peps/pep-0008/#id7) | Suggested syntax for Python 2.7 and straddling code [https://www.python.org/dev/peps/pep-0484/#suggested-syntax-for-python-2-7-and-straddling-code](https://www.python.org/dev/peps/pep-0484/#suggested-syntax-for-python-2-7-and-straddling-code) |

# [Copyright](https://www.python.org/dev/peps/pep-0008/#id55)

This document has been placed in the public domain.

Source: [https://github.com/python/peps/blob/master/pep-0008.txt](https://github.com/python/peps/blob/master/pep-0008.txt)

其他翻译版本：

[http://nanshu.wang/post/2015-07-04/](http://nanshu.wang/post/2015-07-04/)

[https://lizhe2004.gitbooks.io/code-style-guideline-cn/content/python/python-pep8.html](https://lizhe2004.gitbooks.io/code-style-guideline-cn/content/python/python-pep8.html)

[https://alvinzhu.xyz/2017/10/07/python-pep-8/](https://alvinzhu.xyz/2017/10/07/python-pep-8/)
