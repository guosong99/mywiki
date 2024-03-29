[TOC]

# 〇、简单写个序言
- 主要针对嵌入式软件工程师总结常用的vim无插件使用技巧
- 主要是总结常用的操作技巧，不常用的少
- 高频操作总结都是我日常工作用的比较频繁的，系统归纳下
- 尤其日常出差到客户那里，vim都是无插件版，所以有必要熟练操作技巧

# 一、高频操作总结
# 二、日常操作总结
## 1.四个模式
（1）一般模式（--NORMAL--）：命令模式，以下3个模式的切换也是在这里中转（按Esc回到normal![tiger](E:\wiki\mywiki\mydocs\docs\images\tiger.png)）；可移动光标、删除字符、复制粘贴



（2）插入模式（--INSERT--）：可编辑，按下i  I  o  O  a  A  r  R  s  S 均可进入此模式，编辑完成后，按Esc回到normal模式

```
i I是insert     （在光标所在字符前或光标所在行首插入）
a A是append（在光标所在字符后或光标所在行尾插入）
o O是open   （在光标所在行的下面或上面open一新行开始插入)
s S 是substitute (删除光标所在的字符或行，并开始插入)
r R是replace   （替换光标所在的字符  或  进入插入替代模式，将光标后面的字符都替换）
```
（3）末行模式：按下：  /  ？ 任何一个进入此模式；可查找、读取、保存、替换、离开vim、显示行号等操作
（4）可视模式（--VISUAL--）：可以进行块操作，按下v V ctrl-v进入，v选择单位是一个字符，V选择单位是一行，ctrl-v选择单位是方块。
## 2.移动
### 2.1 基本移动
normal模式下的基本移动
```
w → 将光标移动到下一个word的首字符上；  e → 将光标移动到下一个单词的结尾  b → 将光标移动到前一个word的首字符上；（单词默认是以空格或分号分隔的）
W → 到将光标移动下一个字符串的首字符上；E → 将光标移动到下一个字符串的结尾 B → 到将光标移动前一个字符串的首字符上；(字符串默认以空格分隔，指数字、字母、下划线组成的字符串)
```

```
0 → 数字零，到行头
^ → 到本行第一个不是空格的位置
$ → 到本行行尾
% → 到光标所在这对括号的另外一个，括号匹配
gg → 首行
G → 最后一行
h j k l  左 下 上 右(强例推荐使用其移动光标)
```
**高频使用场景:**

- a.修改行中某个变量名 先移把光标移动：w and b 、W and B （或者如果本行太长可用下文的搜索功能）到目的单词
- b.修改缩进，跳到行头^
- c.查看函数或类的完整或者变量作用域%
- d.切分屏幕之后，跳转不同窗口：ctrl+w+(h or j or k or l)
- e.左下上右移动（h、j、k、l）
- f.删除到末尾:d$ 删除到开头: d^

### 2.2 标记
简记：标记是为了更好地查找，normal模式下：
```mx``` meaning: mark x, x is the name of mark;
```'x``` meaning: go to the position of x mark

**高频使用场景：**
在函数中看到调用其他函数，你想去看怎么定义的，你看完之后要回来，那么先标记一下，然后在跳回来。
### 2.3 语法相关的跳转
normal模式下：
```gd``` 意思： go to definition
先按 ```[``` 再按 ```ctrl+d``` 跳转到#define处
先按 ```[``` 再按 ```ctrl+i``` 跳转到函数、变量和#define
注意：语言支持不太良好, 大家可以试试所用的语言
### 2.4 快速翻页
normal模式下：
```
ctrl-u 向上翻半页
ctrl-d 向下翻半页
ctrl-b 返回上一页
ctrl-f 向前下一页
Ctrl + e #向下滚动一行
Ctrl + y #向上滚动一行
```
## 3.动作操作指令
### 3.1 文本编辑
normal模式下：
```
d 删除光标下的字符并复制到剪切板；D 删除光标所在位置一直到行尾，并复制;dd 删除当前行并复制（剪切）；d$删除到本行末尾。
p 粘贴到光标所在字符之后；P 粘贴到光标所在字符之前。
y 复制光标所在字符；Y 复制一行（即 yy ）。
r 替代光标下的字符；R 进入替代模式，将后面的字符都替代。
x 剪切一个字符。
s S 是substitute (删除光标所在的字符或行，并开始插入)
u 撤销上次操作；ctrl-r 对撤销的撤销；U 一次性撤销对一整行的所有操作。
cw 剪切当前光标所在字符及后面字符直到不为字母或下划线为止，并进入插入模式，Esc后可以p粘贴
cc 剪切当前光标所在行，并进入插入模式，Esc后p可粘贴行
c1 剪切1个字符并进入插入模式；
c2 剪切2个字符并进入插入模式；

```
### 3.2 搜索
normal模式下：
```
* 向下搜索当前光标所在的单词，找到就跳到下一个单词（全文查找）
# 向上搜索当前光标所在的单词，找到就跳到下一个单词
f 向光标位置之后查找一个字符；F 向光标位置之前查找一个字符 (仅限当前行)
t 向光标位置之后查找一个字符,并跳到目标字符前面；T类似
```
末行模式下：
```
/word  向下全文搜索word代表字符，n 向下搜；N 向上搜
？word 向上全文搜索word代表字符，n 向上搜；N 向下搜（方向反着来）
```
```
/text #正向查找text，按n健查找下一个，按N健查找前一个。
?text #逆向查找text，按n健查找下一个，按N健查找前一个。
%  #查找配对的 {，[，(
#vim中有一些特殊字符在查找时需要转义　　.*[]^%/?~$
#查找很长的词，如果一个词很长，键入麻烦，可以将光标移动到该词上，按*或#键即可以该单词进行搜索，相当于/搜索。而#命令相当于?搜索。
:set hlsearch　　高亮搜索结果，所有结果都高亮显示，而不是只显示一个匹配。
:set nohlsearch　　关闭高亮搜索显示
:nohlsearch　　关闭当前的高亮显示，如果再次搜索或者按下n或N键，则会再次高亮。
:set incsearch　　逐步搜索模式，对当前键入的字符进行搜索而不必等待键入完成。
:set wrapscan　　重新搜索，在搜索到文件头或尾时，返回继续搜索，默认开启。
:set ignorecase　　忽略大小写的查找
:set noignorecase　　不忽略大小写的查找
:set ic 忽略大小写
:set noic 取消忽略大小写
:set hls 匹配项高亮显示
:set is 显示部分匹配
```
### 3.3 单独成型
```.``` 重复刚才的操作
```~``` 转换大小写

- 可以对变量首字母改变大小写
- 可以结合下文提供的命令的选择一个字符串（变量），然后再改变整个字符串（变量）的大小写。比如：宏定义

```=``` 自动格式化

- 对当前行用== （连按=两次）, 或对多行用n==（n是自然数）表示自动缩进从当前行起的下面n行
- 或者进入可视行模式选择一些行后再=进行格式化，相当于一般IDE里的code format。
- 使用gg=G可对整篇代码进行排版。
### 3.4 撤销和恢复
- u undo撤销上一步的操作，命令可以组合，例如Nu N是任意一个整数，表示撤销N步操作，以下类同。
- U 恢复当前行（即一次撤销对当前行的全部操作）
- ctr+r control+redo 恢复上一步被撤销的操作
- CTRL-R 回退前一个命令
### 3.5 文本替换
末行模式下输入替换命令： :[range]s/pattern/string/[flags]

pattern 就是要被替換掉的字串，可以用 regexp 來表示。
string 將 pattern 由 string 所取代。
[range] 有以下一些取值：
```c
无      默认为光标所在的行
.       光标所在当前的行
N       第N行
$       最后一行
'a      标记a所在的行（之前要使用ma做过标记）
.+1     当前光标所在行的下面一行
$-1     倒数第二行，可以对某一行加减某个数值来确定取得相对的行
22,33   第22～33行
1,$     第1行 到 最后一行
1,.     第1行 到 当前行
.,$     当前行 到 最后一行
'a,'b   标记a所在的行 到 标记b所在的行（之前要使用ma和mb做过标记）
%       所有行（与 1,$ 等价）
?str?   从当前位置向上搜索，找到的第一个str所在的行 （其中str可以是任何字符串或者正则表达式）
/str/   从当前位置向下搜索，找到的第一个str所在的行（其中str可以是任何字符串或者正则表达式）
```
注意，上面的所有用于range的表示方法都可以通过 +、- 操作来设置相对偏移量。
[flags]有以下一些取值：
```
g	对指定范围内的所有匹配项（global）进行替换
c	在替换前请求用户确认（confirm）
e	忽略执行过程中的错误
i	ignore 不分大小写
无	只对指定范围内的第一个匹配项进行替换
```
注意：上面的所有flags都可以组合起来使用，比如 gc 表示对指定范围内的 所有匹配项进行替换，并且在每一次替换之前都会请用户确认。
**高频操作:**
```
:10,20s/from/to/g   对第10行到第20行的内容进行替换。
:1,$s/from/to/g     对第一行到最后一行的内容进行替换（即全部文本）
:1,.s/from/to/g     对第一行到当前行的内容进行替换。
:.,$s/from/to/g     对当前行到最后一行的内容进行替换。
:'a,'bs/from/to/g   对标记a和b之间的行（含a和b所在的行）进行替换，其中a和b是之前用m命令所做的标记。
替换所有行的内容：:%s/from/to/g
```
## 4.动作的重复
normal模式下，任意一个动作都可以重复
### 4.1 N的使用
Nyy从当前行算起向下拷贝N行
Ndd从当前行算起向下删除N行
Ngg跳到第N行
dNw删除从当前光标开始到第N个单词前（不包含空白，即删除N-1个单词)
yNe拷贝从当前光标到第N个单词末尾（注意： yy=1yy dd=1dd）
d$删除到本行末尾
重复前一个命令： N. （N表示重复的次数）
### 4.2 点（.）的使用
待续~~~
## 5.区块选择
注：中括号内容为可选项
normal模式下：[ctr + ] v + (h or j or k or l)  即进入 可视VISUAL模式(块操作模式)
**高频使用场景**

- [ctr + ] v 选中某些行的行头之后 再按= 效果：代码格式自动调整
- [ctr + ] v 选中某些行的行头之后 再按I再按注释的符号（比如：//）最后按ESC 效果：选中的这些行全部注释了 多行快速注释
- [ctr + ] v 选中某些行的行头之后 再按A再按注释的内容 最后按 ESC（比如：//这是测试代码） 效果：选中的这些行的行尾全部注释上//这是测试代码 多行快速注释
- [ctr + ] v 选中某些行的行头的注释（比如：//）之后 再按d 最后按ESC 效果：选中的这些行全部注释删除了 多行快速删除注释
- [ctr + ] v 选中某些区块之后，再按上文动作的按键实现区域操作
## 6.组合的强大
操作光标所在的一个word。默认上来说，一个word（单词串）由字母，数字和下划线组成
normal模式下：
```
动作 + 移动 [+重复次数]
```
前面已经已经大量使用组合，这里继续：
```
c1或c2  剪切1个或2个字符，并进入插入模式,esc后可粘贴
cw或c1w  改变当前光标位置开始的第一个word，并进入插入模式
c2w     改变当前光标位置开始的第一个word+非word字串,并进入插入模式
c3w     改变当前光标位置开始的第一个word+非word字串+第二个word，并进入插入模式
c3w     改变当前光标位置开始的第一个word+非word字串+第二个word+第二个非word串，并进入插入模式
caw     改变当前光标所在的整个word，并进入插入模式
d1或d2  删除1个或2个字符，不进入插入模式，可p粘贴删除的字符(但要注意光标停留位置)
dw或d1w 删除光标位置开始的word，不进入插入模式
d2w或d3w或d4w 同c2w/c3w/c4w类似，但不进入插入模式
daw     删除光标所在的整个word，不进入插入模式
yw或y1w  从当前光标位置开始复制word
y1或y2   从光标位置开始复制字符1个或2个
yaw     复制光标所在位置的整个word
d/word	从当前光标处向下删除到‘word’之前（'word'保留）
d?word	从当前光标处向上删除到‘word’之前（‘word’也删掉）
```
```
dtc	向后删除直到第一个'c'之前
dfc	向后删除直到第一个'c'之后
```
```
bve 操作当前光标所在的一个变量或word，配合c/d/y/p/P操作使用
```
## 7.自动补全
在insert模式下直接按： 最常用的补全
```
ctrl + n    补全，同时按住ctrl+通过n向下选择
ctrl + p    补全，同时按住ctrl+通过p向上选择    
```
智能补全
```
待续~~~~
```

## 8.切分屏幕
- 打开文件时就切分好
vim -O file1.c file2.c 垂直分屏打开两个文件
vim -o file1.c file2.c 水平分屏打开两个文件
vim -O5 file1.c file2.c file3.c file4.c file5.c垂直分屏打开5个文件
- 切分命令，normal模式下，输入
    ```:vs```(说明：vertically split 纵向切分屏幕）
    ```:sp```(说明：split 横向切分屏幕，即默认的切分方式）
    ```:vs```file2.txt 垂直打开文件file2.txt,又不失原来的编辑文件
- 屏幕相互跳转
ctr + w + h/j/k/l   窗口跳转到左/下/上/右边
ctrl+ww  顺序依次跳转窗口
- 调整切分窗口的大小
（1）ctrl+```w```+``` =``` 等分窗口
（2）在normal模式下输入```:resize -N``` 或```:resize +N```,明确指定窗口减少或增加N行
- 关闭窗口
- 分隔窗口选项
    ```：[n] split(vsplit)  [++opt]  [+cmd]  [file]```
    
    ```
    n   为vim指定在新窗口中显示的行数，且新窗口的大小刚好容纳该行数，新窗口位于画面顶端
    opt  传递vim选项信息给新的窗口会话（请注意，它的前面必须加上两个加号）
    cmd 传入欲在新窗口中执行的命令（请注意，它的前面必须加上一个加号）
    file  指定在新窗口中编辑的文件
    ```
    ：sview  filename  以只读的方式水平分割打开一个新窗口
    ：sfind  [++opt]  [+cmd]  [file]  和split的运作方式相似，但在path中寻找filename，如果vim未找到文件则不显示
## 9.tab窗口
多标签切换的功能相当于多窗口，虽然vim有多文件编辑功能，但总不如这个方便 用法：normal模式下，
```
:tabnew [++opt选项] ［＋cmd］ 文件  //建立对指定文件新的tab标签
:tabnew file1.txt //对文件file1.txt建立标签，文件补全用tab，选择文件用tab切换
:tabc 关闭当前的tab 同 :q
:tabo 关闭其他的tab
:tabs 查看所有打开的tab
:tabe file.txt 在标签页中打开文件file.txt
:tabp 前一个tab窗口
:tabn 后一个tab窗口
gt或gT 可以直接在tab之间切换。
:help table 可以查看tab其他用法
```
## 10.目录
normal模式下：
```
:Te 以tab窗口形式显示当前目录 然后可进行切换目录、打开某个文件
:!ls 这种是vim调用shell命令的方式:!+shell命令（不是以tab窗口形式显示当前目录）
```
## 11.成对符号的内容操作
以下命令可以对标点内的内容进行操作：
```c
ci' ci" ci( ci[ ci{ ci<     分别change这些配对标点符号中的文本内容,进入插入模式，光标在配对符号同一行即可不必在符号内
di' di" di(或dib di{或diB   分别删除这些配对标点符号中的文本内容，需将光标移到配对符号内
yi' yi" yi( yi[ yi{ yi<     分别复制这些配对标点符号中的文本内容，光标在配对符号同一行即可不必在符号内
vi' vi" vi( vi[ vi{ vi<     分别选中这些配对标点符号中的文本内容，需先将光标移到配对符号内
```
注：（1）将把上面的 i 改成 a 可以同时操作配对标点和配对标点内的内容：（2）尽量将光标移动到配对符号内部操作
**高频操作**
要操作的文本：111"222"333，将光标移到"222"的任何一个字符处输入命令
```c
di",文本会变成： 111""333
若输入命令 da" ,文本会变成： 111333
```
## 12.剪贴板
### 12.1 简单复制和粘贴
vim提供十几个剪贴板，它们的名字分别为0、1、2、…、9、a等。使用:reg命令，可以查看各个粘贴板里的内容。
在vim中简单用y只是复制到某个粘贴板里，同样用p粘贴的也是这个粘贴板里的内容。
### 12.2 复制和粘贴到指定剪贴板
- 要将vim的内容复制到某个粘贴板，normal模式下，选择要复制的内容，然后按```"Ny```完成复制，其中N为粘贴板号.例如要把内容复制到粘贴板a，选中内容后按```"ay```就可以了。
- 要将vim某个粘贴板里的内容粘贴进来，normal模式下按```"Np```，其中N为粘贴板号。

### 12.3 系统剪贴板
normal模式下输入```:reg```,查看vim支持的剪切板
星号(*)和加号(+)粘贴板是系统粘贴板。在windows系统下， (空)和 + 剪贴板是相同的。
*剪贴板的一个作用是，在vim的一个窗口选中的内容，可以在vim的另一个窗口取出。
（1）复制到系统剪贴板
```c
"*y     将选中内容复制到系统*号剪切板
"+y     将选中内容复制到系统+号剪切板，在visual模式下选中内容
"+Nyy   复制N行到系统剪切板
```
（2）剪切到系统剪贴板
```html
    "+dd
```
（3）从系统剪贴板粘贴到vim
```html
normal模式下：
"*p
"+p  比ctrl-v好用
```

## 13. vim编码
(1)Vim 可以很好的编辑各种字符编码的文件:包括UCS-2、UTF-8、Unicode等编码方式。
(2)四个字符编码选项，encoding、fileencoding、fileencodings、termencoding (取值请参考 Vim ```:help encoding-names```)
```
encoding: Vim 内部使用的字符编码方式。
包括 Vim 的buffer (缓冲区) 、 菜单文本、 消息文本等。默认是根据你的locale选择.用户手册上建议只在.vimrc中改变它的值，事实上似乎也只有在.vimrc中改变它的值才有意义。你可以用另外一种编码来编辑和保存文件，如你的vim的encoding为utf-8,所编辑的文件采用cp936编码,vim会自动将读入的文件转成utf-8(vim的能读懂的方式），而当你写入文件时,又会自动转回成cp936（文件的保存编码).
```
```
fileencoding: Vim 中当前编辑的文件的字符编码方式。
Vim 保存文件时也会将文件保存为这种字符编码方式 (不管是否新文件都如此)。
```
```
fileencodings: Vim会自动探测编码设置项
启动时会按照它所列出的字符编码方式逐一探测即将打开的文件的字符编码方式，并且将 fileencoding 设置为最终探测到的字符编码方式。因此最好将Unicode 编码方式放到这个列表的最前面，将拉丁语系编码方式 latin1 放到最后面。
```
```
termencoding: Vim 所工作的终端 (或者 Windows 的 Console 窗口) 的字符编码方式
如果vim所在的term与vim编码相同，则无需设置。如其不然，你可以用vim的termencoding选项将自动转换成term的编码.这个选项在 Windows 下对我们常用的 GUI 模式的 gVim 无效，而对 Console 模式的Vim 而言就是 Windows 控制台的代码页，并且通常我们不需要改变它。 好了，解释完了这一堆容易让新手犯糊涂的参数，我们来看看 Vim 的多字符编码方式支持是如何工作的。
```
- Vim 启动，根据 .vimrc 中设置的 encoding 的值来设置 buffer、菜单文本、消息文的字符编码方式。
- 读取需要编辑的文件，根据 fileencodings 中列出的字符编码方式逐一探测该文件编码方式。并设置 fileencoding 为探测到的，看起来是正确的 (注1) 字符编码方式。
- 对比 fileencoding 和 encoding 的值，若不同则调用 iconv 将文件内容转换为encoding 所描述的字符编码方式，并且把转换后的内容放到为此文件开辟的 buffer 里，此时我们就可以开始编辑这个文件了。注意，完成这一步动作需要调用外部的 iconv.dll(注2)，你需要保证这个文件存在于 $VIMRUNTIME 或者其他列在 PATH 环境变量中的目录里。
- 编辑完成后保存文件时，再次对比 fileencoding 和 encoding 的值。若不同，再次调用 iconv 将即将保存的 buffer 中的文本转换为 fileencoding 所描述的字符编码方式，并保存到指定的文件中。同样，这需要调用 iconv.dll由于 Unicode 能够包含几乎所有的语言的字符，而且 Unicode 的 UTF-8 编码方式又是非常具有性价比的编码方式 (空间消耗比 UCS-2 小)，因此建议 encoding 的值设置为utf-8。这么做的另一个理由是 encoding 设置为 utf-8 时，Vim 自动探测文件的编码方式会更准确 (或许这个理由才是主要的 ;)。我们在中文 Windows 里编辑的文件，为了兼顾与其他软件的兼容性，文件编码还是设置为 GB2312/GBK 比较合适，因此 fileencoding 建议设置为 chinese (chinese 是个别名，在 Unix 里表示 gb2312，在 Windows 里表示cp936，也就是 GBK 的代码页)。
- 对于fedora来说，vim的设置一般放在/etc/vimrc文件中，不过，建议不要修改它。可以修改~/.vimrc文件（默认不存在，可以自己新建一个），写入所希望的设置。

我的.vimrc文件如下:
```
:set encoding=utf-8
:set fileencodings=ucs-bom,utf-8,cp936
:set fileencoding=gb2312
:set termencoding=utf-8
```
其中，fileencoding配置可以设置utf-8，但是我的mp3好像不支持utf-8编码，所以干脆，我就设置为gb2312了。现在搞定了，不管是vi中还是mp3上都可以显示无乱码的.txt文件了。

## 14.个人的配置
本人无插件使用过程中的配置很短，写在vim的配置文件.vimrc里， 配置是使用vim script进行配置的，它有自己的一套语法，详细请点击vim Script
```
set number;display number
set mouse=a; setting smart mouse
set hlsearch ;high light search
set tabstop=4 ; setting tab width 4 letters
set shiftwidth=4; setting new line incident width
set noexpandtab; tab doesn't expand to space
;set list ;display manipulator, example： \n \t \r ......
set encoding=utf-8
set fileencodings=ucs-bom,utf-8,cp936
set fileencoding=gb2312
set termencoding=utf-8
```
## 15.前进和后退功能
 vim 中使用 `Ctrl-O` 执行后退，使用 `Ctrl-I` 执行前进
 (详见 :help CTRL-O :help CTRL-I :help jump-motions) 
Ctrl + o #跳转回之前的位置
Ctrl + i #返回跳转之前的位置

## 16.vim比较文件
### 16.1启动方法
首先保证系统中的diff命令是可用的。Vim的diff模式是依赖于diff命令的。
```
vimdiff file1 file2
```
```
vim -d file1 file2
```
如果已在 Vim 中，你可以用三种方式进入比较模式，只介绍一种：
```
:diffs[plit] {filename}
:vert diffsplit another_filename 这个垂直比较会高频使用
```
### 16.2跳转到差异
有两条命令可用于在跳转到差异文所在的位置:
`[c` 反向跳转至上一处更改的开始。计数前缀使之重复执行相应次。
`]c` 正向跳转至下一个更改的开始。计数前缀使之重复执行相应次。
如果不存在光标可以跳转到的更改，将产生错误。
### 16.3合并
比较目的就是合并差异，直接使用以下自带命令或者麻烦的办法：手动从一个窗口拷贝至另一个窗口。
```
:[range]diffg[et] [bufspec]
    用另一个缓冲区来修改当前的缓冲区，消除不同之处。除非只有另外一个比较模式下的缓冲区， [bufspec] 必须存在并指定那个缓冲区。如果 [bufspec] 指定的是当前缓冲区， 则为空动作。 [range] 可以参考下面。

:[range]diffpu[t] [bufspec]
    用当前缓冲区来修改另一个缓冲区，消除不同之处。
[count]do   
    同 ":diffget"，但没有范围。"o" 表示 "obtain" (不能用"dg"，因为那可能是 "dgg" 的开始！)。
dp
    同 ":diffput"，但没有范围。注意 不适用于可视模式。给出的 [count] 用作 ":diffput" 的 [bufspec] 参数。
    
当没有给定 [range] 时，受影响的仅是当前光标所处位置或其紧上方的差异文本。
当指定 [range] 时，Vim 试图仅改动它指定的行。不过，当有被删除的行时，这不总有效。
参数 [bufspec] 可以是缓冲区的序号，匹配缓冲区名称或缓冲区名称的一部分的模式。
例如:
        :diffget                使用另一个进入比较模式的缓冲区
        :diffget 3              使用 3 号缓冲区
        :diffget v2             使用名字同 "v2" 匹配的缓冲区，并进入比较模式(例如，"file.c.v2")
```
### 16.4更新比较和撤销修改
（1）比较基于缓冲区的内容。如果在载入文件后你做过改动，需要不时使用 `:diffupdate[!]`。因为并非所有改动都能自动更新。包含`!` 时，Vim 会检查文件是否被外部改变而需要重新载入。对每个被改变的文件给出提示。
（2）如果希望撤销修改，可以和平常用vim编辑一样，直接进入normal模式下按u但是要注意一定要将光标移动到需要撤销修改的文件窗口中。
### 16.5上下文的展开和查看
比较和合并文件的时候经常需要结合上下文来确定最终要采取的操作。Vimdiff 缺省是会把不同之处上下各 6 行的文本都显示出来以供参考。其他的相同的文本行被自动折叠。如果希望修改缺省的上下文行数，可以这样设置：
```
:set diffopt=context:3
```
### 16.6多个文件的退出
对多个文件同时进行操作
比如同时退出：`:qa` （quit all）
如果希望保存全部文件：`:wa` （write all）
保存全部文件，然后退出：`:wqa` （write, then quit all）
如果退出时不希望保存任何操作的结果：`:qa!` （force to quit all）

### 16.7 vimdiff 详细请参考
```
vim下 :help diff
vimdiff doc
```
## 17 vim命令行的保存、离开等命令：
`:w` 将编辑的数据写入硬盘文件中。
`:w!` 若文件属性为“只读”，强制写入该文件。但能否写入还由对该文件的文件权限有关。
`:q`保存后离开。若为“:wq！”则强制保存后离开。
`:w[文件名]` 将编辑的数据保存为另一个文件。
`:r[文件名]` 在编辑的数据中读入另一个文件的内容加到光标所在行后面。
`:n1,n2 w[文件名]` 将n1行到n2行的内容保存到另一个文件。
`:!command` 暂时离开vi到命令行模式下执行command的显示结果。
`ZZ` 若文件未改动，则直接离开；若已改动则保存后离开。
`:set num/nonum` 显示/取消行号。
## 18 VIM的宏
宏的使用非常强大，前往vim 中，宏的使用
## 19 文件操作
```
vim file #打开单个文件
vim file1 file2 file3 ... #同时打开多个文件
:open file #在vim窗口中打开一个新文件
:split file #在新窗口中打开文件
:bn #切换到下一个文件
:bp #切换到上一个文件
:args #查看当前打开的文件列表，当前正在编辑的文件会用[]括起来。
:e ftp://192.168.10.76/abc.txt #打开远程文件，比如ftp或者share folder
:e \\qadrive\test\1.txt
```
## 20 可视模式操作

## 21 



# 三、参考资料汇总
1.VIM中文帮助文件http://vimcdoc.sourceforge.net/doc/help.html
2.https://www.linuxsong.org/2010/09/vim-quick-select-copy-delete/
3.vim无插件使用https://snaildove.github.io/2016/01/20/vim_without_widgets/#vim比较文件