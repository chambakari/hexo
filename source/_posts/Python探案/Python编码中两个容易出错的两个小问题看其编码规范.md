---
title: Python编码中从容易出错的两个小问题中看其编码规范
date: 2014-09-21
tags: 
- Python
categories:
- Python探案
---

最近在写Python的一些小程序，由于没有系统地学习过Python的语法及编码风格，在编码规范上栽了几个跟头。先看看我遇到的这两个问题，接着引出Python的编码规范。  
### 缩进问题     
缩进是Python中最重要的，也是最容易出错的细节，这个对于每个初学者都要牢记于心并养成习惯，我的问题出在，从一个文本文档拷贝一段代码到一个IDE的时候，出现了如下的两个错误。 

    IndentationError: unindent does not match any outer indentation level 
    IndentationError:expected an indented block  
<!-- more -->  
这两个问题就是提醒你要缩进，但是我明明缩进了，为什么还不行，原因就是拷贝的代码的缩进是用空格，缩进不统一（用肉眼完全看不出来），另外一个就是IDE它本身加了一些功能让你方便写代码，像自动缩进，换行等，拷贝的代码本身也拷贝了文件的格式，所以拷贝过来的代码IDE不能识别，不知道为什么不能识别，按理说删除空格换成Tab就应该可以了，但是不管怎么弄都不行，后来就只得重新编写代码才解决这个问题。

### Python库import的导入顺序有讲究
库的导入有两种方式：  
1）并排导入：
    
    import module1,module2,module3.......  
2）顺序导入： 

    import module1  
    import module2  
    :  
    import moduleN  
显然第二种看着要清爽，但是由于Python库众多，什么库应该先导入，就非常有讲究。我的第二个问题就是这个。先来看看一个小例子：  
![](/image/importA.PNG)      
![](/image/importB.PNG)    
这上面导入的两个库的顺序不一样，完全出现不同的结果，可以看到，正确的版本是先导入第三方的库，在导入标准库，但是。。。但是Python的官方编码规范中要求的顺序是：     

- python 标准库模块
- python 第三方模块
- 应用程序自定义模块  

这就让人很匪夷所思了，这里先mark一下，以后遇到在进一步补上，但是我决定以后的做法是，用谁，谁最后导入，这里可能存在着覆盖的问题。  

好了，上面是我遇到的两个小问题，希望自己牢记，不要再犯同样的错误。关于Python的编码规范，更多的详见[Google的官方的风格指南:](http://zh-google-styleguide.readthedocs.org/en/latest/google-python-styleguide/python_style_rules/)  
其中，我挑几点记录一下：  
1、不要在行尾加分号  
2、一行太长，不要加\换行，这和C++这些不同，Python用()支持直接换行，如：  

    foo = long_function_name(  
    	var_one, var_two, var_three,  
    	var_four)  

3、括号内不要有空格，如：  

    Yes: spam(ham[1], {eggs: 2}, [])
    No： spam( ham[ 1 ], { eggs: 2 }, [ ] )  
4、一般'='或比较符号（'<''=''>'）两边我们都会加空格，但这里特别注意一下：  
当’=’用于指示关键字参数或默认参数值时, 不要在其两侧使用空格，如：  

    Yes: def complex(real, imag=0.0): return magic(r=real, i=imag)
    No:  def complex(real, imag = 0.0): return magic(r = real, i = imag)
5、一般在C、C++程序中我们都会这样写，看着舒服极了：  

    foo       = 1000  # comment
    long_name = 2     # comment that should not be aligned

    dictionary = {
        "foo"      : 1,
        "long_name": 2,
    }
但最好别这样写，这样写就行：  

    foo = 1000  # comment
    long_name = 2  # comment that should not be aligned

    dictionary = {
        "foo": 1,
        "long_name": 2,
    }
6、大部分.py文件不必以#!作为文件的开始. 根据 PEP-394 , 程序的main文件应该以 #!/usr/bin/python2或者 #!/usr/bin/python3开始.  
(#!)叫做Shebang(也叫Hashbang),一般在科学计算中，类Unix操作系统的程序载入器会分析Shebang后的内容，将这些内容作为解释器指令，并调用该指令, 并将载有Shebang的文件路径作为该解释器的参数. 例如, 以指令#!/bin/sh开头的文件在执行时会实际调用/bin/sh程序.)  
(#!)先用于帮助内核找到Python解释器, 但是在导入模块时, 将会被忽略. 因此只有被直接执行的文件中才有必要加入#!.  

7、使用文档字符串对模块、函数或方法进行注释，并在必要时增加行内注释，这一条决定着编写大型模块程序时，不会被搞得晕头转向，也不会让别人看自己程序时摸不清头脑。具体怎么做见下面这个模板即可。  

	def fetch_bigtable_rows(big_table, keys, other_silly_variable=None):
    """Fetches rows from a Bigtable.

    Retrieves rows pertaining to the given keys from the Table instance
    represented by big_table.  Silly things may happen if
    other_silly_variable is not None.

    Args:
        big_table: An open Bigtable Table instance.
        keys: A sequence of strings representing the key of each table row
            to fetch.
        other_silly_variable: Another optional variable, that has a much
            longer name than the other args, and which does nothing.

    Returns:
        A dict mapping keys to the corresponding table row data
        fetched. Each row is represented as a tuple of strings. For
        example:

        {'Serak': ('Rigel VII', 'Preparer'),
         'Zim': ('Irk', 'Invader'),
         'Lrrr': ('Omicron Persei 8', 'Emperor')}

        If a key from the keys argument is missing from the dictionary,
        then that row was not found in the table.

    Raises:
        IOError: An error occurred accessing the bigtable.Table object.
    """
    pass
8、如果一个类不继承自其他类，就应该显示地从object继承，嵌套类也一样，继承自 object 是为了使属性(properties)正常工作, 并且这样可以保护你的代码, 使其不受Python 3000的一个特殊的潜在不兼容性影响. 这样做也定义了一些特殊的方法, 这些方法实现了对象的默认语义, 包括 \_\_new\_\_, \_\_init\_\_, \_\_delattr\_\_, \_\_getattribute\_\_, \_\_setattr\_\_, \_\_hash\_\_, \_\_repr\_\_, and \_\_str\_\_ .如：  

	class SampleClass(object):
         pass


     class OuterClass(object):

         class InnerClass(object):
             pass


     class ChildClass(ParentClass):
         """Explicitly inherits from another class already."""

9、命名，这个应该是比较重要，好的命名在代码编写过程中，或是在后期调试，维护的过程中都会给人特别舒服的感觉。  
Tip：  

	module_name, package_name, ClassName, method_name, 
	ExceptionName, function_name, GLOBAL_VAR_NAME, 
	instance_var_name, function_parameter_name,
	local_var_name  
应该避免的名称
  
* 单字符名称, 除了计数器和迭代器.
* 包/模块名中的连字符(-)
* 双下划线开头并结尾的名称(Python保留, 例如\_\_init\_\_)

命名约定  

* 所谓”内部(Internal)”表示仅模块内可用, 或者, 在类内是保护或私有的.
* 用单下划线(_)开头表示模块变量或函数是protected的(使用import * from时不会包含).
* 用双下划线(__)开头的实例变量或方法表示类内私有.
* 将相关的类和顶级函数放在同一个模块里. 不像Java, 没必要限制一个类一个模块.
* 对类名使用大写字母开头的单词(如CapWords, 即Pascal风格), 但是模块名应该用小写加下划线的方式(如lower\_with\_under.py). 尽管已经有很多现存的模块使用类似于CapWords.py这样的命名, 但现在已经不鼓励这样做, 因为如果模块名碰巧和类名一致, 这会让人困扰.  

**Python 之父Guido推荐的规范**   
![](/image/Guido.PNG)  

10、即使是一个打算被用作脚本的文件, 也应该是可导入的. 并且简单的导入不应该导致这个脚本的主功能(main functionality)被执行, 这是一种副作用. 主功能应该放在一个main()函数中.

在Python中, pydoc以及单元测试要求模块必须是可导入的. 你的代码应该在执行主程序前总是检查 if \_\_name\_\_ == '\_\_main\_\_' , 这样当模块被导入时主程序就不会被执行.如：  

	def main():
      ...

	if __name__ == '__main__':
    	main()