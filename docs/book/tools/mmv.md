# mmv

分享者：乙文静

---

###### 更新时间：20241018 

在 Linux 中一次重命名多个文件

mmv 程序可在基于 Debian 的系统的默认仓库中使用。 要想在 Debian、Ubuntu、Linux Mint 上安装它，请运行以下命令：

$ sudo apt-get install mmv

 

我们假设你在当前目录中有以下文件。

$ ls

a1.txt a2.txt a3.txt

现在，你想要将所有以字母 “a” 开头的文件重命名为以 “b” 开头的。

$ mmv a\* b\#1

 

$ ls

b1.txt b2.txt b3.txt

所有以字母 “a” 开头的文件（即 a1.txt、a2.txt、a3.txt）都重命名为 b1.txt、b2.txt、b3.txt。

 

解释

在上面的例子中，第一个参数（a\*）是 “from” 模式，第二个参数是 “to” 模式（b\#1）。根据上面的例子，mmv 将查找任何以字母 “a” 开头的文件名，并根据第二个参数重命名匹配的文件，即 “to” 模式。我们可以使用通配符，例如用 *、? 和 [] 来匹配一个或多个任意字符。请注意，你必须转义使用通配符，否则它们将被 shell 扩展，mmv 将无法理解。

“to” 模式中的 #1 是通配符索引。它匹配 “from” 模式中的第一个通配符。 “to” 模式中的 #2 将匹配第二个通配符（如果有的话），依此类推。在我们的例子中，我们只有一个通配符（星号），所以我们写了一个 #1。并且，# 符号也应该被转义。此外，你也可以用引号括起模式。

修改前缀的名字

mmv all_nine_one_contig_gene_81_contig_mobile_merge_fin_\* all_hotspot_\#1_  ##改名字的同时还可以每个文件的末尾加上_

 

 

 

你甚至可以将具有特定扩展名的所有文件重命名为其他扩展名。例如，要将当前目录中的所有 .txt 文件重命名为 .doc 文件格式，只需运行：

 

$ mmv \*.txt \#1.doc

这是另一个例子。 我们假设你有以下文件。

 

$ ls

abcd1.txt abcd2.txt abcd3.txt

你希望在当前目录下的所有文件中将第一次出现的 “abc” 替换为 “xyz”。 你会怎么做呢？

 

很简单。

 

$ mmv '*abc*' '#1xyz#2'

请注意，在上面的示例中，模式被单引号括起来了。

 

让我们检查下 “abc” 是否实际上被替换为 “xyz”。

 

$ ls

xyzd1.txt xyzd2.txt xyzd3.txt

看到没？ 文件 abcd1.txt、abcd2.txt 和 abcd3.txt 已经重命名为 xyzd1.txt、xyzd2.txt 和 xyzd3.txt。

 

mmv 命令的另一个值得注意的功能是你可以使用 -n 选项打印输出而不是重命名文件，如下所示。

 

$ mmv -n a\* b\#1

a1.txt -> b1.txt

a2.txt -> b2.txt

a3.txt -> b3.txt

这样，你可以在重命名文件之前简单地验证 mmv 命令实际执行的操作。

 

有关更多详细信息，请参阅 man 页面。

 

$ man mmv
