# 牛客网刷题笔记
## 序言和计划
* 总题量：200
* 分布：

    | 难易度 | 数量 |
    |------|----|
    | 入门  | 2  |
    | 简单  | 25 |
    | 中等  | 41 |
    | 困难  | 32 |
    | 极难  | 8  |

    **刷题计划：**
  * Phase1（入门+简单+中等）: 每日七题，*吃透，挖透，弄明白原理*
  * Phase2（困难+极难）: 每日五题，*弄懂算法类别，抄透，抄熟*
------
目录
[toc]
------
## DAY 1
### Q1: 进制转换
题目描述

```
输入一个int型的正整数，计算出该int型数据在内存中存储时1的个数。
```

输入描述:
```
输入一个整数（int类型）
```
输出描述:
```
这个数转换成2进制后，输出1的个数
```
我的答案：
```python
num = int(input())
bi_num = bin(num)
print(bi_num.count('1'))
```
别人的答案：
```python
while True
    try:
        print(bin(int(input)).count('1'))
    except:
        break
```
**关键点：**
1、bin（）十进制转二进制转换函数，同理有oct(), hex(), str()等类型转换函数
*都是十进制转X进制，如果实现任意进制转换套娃即可，如下表:*

|      | 二进制        | 八进制           | 十进制            | 十六进制           |
|------|---------------|---------------|----------------|----------------|
| 二进制  | \             | bin(int(x,8)) | bin(int(x,10)) | bin(int(x,16)) |
| 八进制  | oct(int(x,2)) | \             | oct(int(x,10)) | oct(int(x,16)) |
| 十进制  | str(int(x,2)) | str(int(x,8)) | \              | str(int(x,16)) |
| 十六进制 | hex(int(x,2)) | hex(int(x,8)) | hex(int(x,10)) | \              |

2、转换后利用`count()`函数进行对某个字符串/数字的计数功能

**我的不足:**

没有使用`try`，`break`等函数来确保输入数字的类型错误不会发生

**PS**
    另外，如果不使用内置函数进行进制转换，还可以根据取余数的算法
    `quotinent, remiander = divmod(dividend, divisor)`
    来手动做~~好像有点画蛇添足~~
    (详见：[用Python实现进制转换，这一篇教程就够了](https://juejin.im/post/6844903930200064014))

----

### Q2:取近似数 ###

题目描述：
```
写出一个程序，接受一个正浮点数值，输出该数值的近似整数值。如果小数点后数值大于等于5,向上取整；小于5，则向下取整。
```
输入：
```
输入一个正浮点数值
```
输出：
```
输出该数值的近似整数
```
我的答案：
```python
from math import floor
print(int(floor(float(input()) + 0.5 )))
```
比较容易犯的错误：
```
print(round( float( input() ) ))
```
*这个地方的错误点在于，对于python3的内置*‘round()’*函数，其功能并非我们熟知的四舍五入，在一个整数恰好被均分的时候，python会返回其最接近的偶数，而并非向上取整*
([python3官方文档对于round函数的解释](https://docs.python.org/3/library/functions.html#round))
例子：
```python
number1 = 4.5
print(round(number1)) --> 4
number2 = 5.5
print(round(number2)) --> 6
```
此外，除了round函数本身的问题外，python的浮点数（或者说**计算机存储浮点数的方式**）都会导致误差的出现，在进行精确计算时应该使用`Decimal()`函数进行类型限制

----

### Q3：数字颠倒
题目描述：
```
输入一个整数，将这个整数以字符串的形式逆序输出
程序不考虑负数的情况，若数字含有0，则逆序形式也含有0，如输入为100，则输出为001
```
输入：
```
输入一个int整数
```
输出：
```
将这个整数以字符串的形式逆序输出
```
我的答案：
```python
print(str(input())[::-1])
```
另外的答案：
```python
s = str(input())
print(''.join(reversed(s)))
```
**关键点：**
1、python内置的列表倒置操作[::-1]
2、python内置字符串操作`.join(reversed())`

### Q4：字符串倒置
题目描述：
```
写出一个程序，接受一个字符串，然后输出该字符串反转后的字符串。（字符串长度不超过1000）
```
输入：
```
输入N个字符
```
输出：
```
输出该字符串反转后的字符串
```
* 和上一题同理，略过

----
### Q5: 汽水瓶
题目描述：
```
有这样一道智力题：“某商店规定：三个空汽水瓶可以换一瓶汽水。小张手上有十个空汽水瓶，她最多可以换多少瓶汽水喝？”答案是5瓶，方法如下：先用9个空瓶子换3瓶汽水，喝掉3瓶满的，喝完以后4个空瓶子，用3个再换一瓶，喝掉这瓶满的，这时候剩2个空瓶子。然后你让老板先借给你一瓶汽水，喝掉这瓶满的，喝完以后用3个空瓶子换一瓶满的还给老板。如果小张手上有n个空汽水瓶，最多可以换多少瓶汽水喝
```
输入：
```
输入文件最多包含10组测试数据，每个数据占一行，仅包含一个正整数n（1<=n<=100），表示小张手上的空汽水瓶数。n=0表示输入结束，你的程序不应当处理这一行。
```
输出：
```
对于每组测试数据，输出一行，表示最多可以喝的汽水瓶数。如果一瓶也喝不到，输出0。
```
例子：
输入

```
3
10
81
0
```
输出

```
1
5
40
```
我的答案：
```python
while True:
    try: 
        n = int(input())
        if n == 0:
            break
        exchanged = 0
        while n > 2:
            exchanged = exchanged + n//3
            n = n%3 + n//3
        if n == 2:
            exchanged += 1
        print(exchanged)
    except:
        break
```
思路：问题的直接解法是一个递归的除法，每次余数和商相加得到新的被除数，累加每次得到的新的商就是，如果最后商为2，则总数+1，其他则不加
别人的解法：
```python
while True:
    try:
        a=int(input())
        if a !=  0:
            print(a//2)   
    except:
        break
```
思路：解法非常的巧妙，最后一句描述 __这时候剩2个空瓶子。然后你让老板先借给你一瓶汽水，喝掉这瓶满的，喝完以后用3个空瓶子换一瓶满的还给老板__ 暗示，其实本质上每两个瓶子就可以换一个，所以直接`n//2`就可以了

-----

### Q6: 统计每个月兔子数量

  问题描述

```
  有一只兔子，从出生后第3个月起每个月都生一只兔子，小兔子长到第三个月后每个月又生一只兔子，假如兔子都不死，问每个月的兔子总数为多少？
  本题有多组数据。
```

输入:

```
输入int型表示month
```

输出：

```
输出兔子总数int型
```

我的答案:

```python
def febonacci(n):
    if n <= 0:
        return 0
    elif n == 1:
        return 1
    else:
        return febonacci(n-1) + febonacci(n-2)
while True:
    try:
        month = int(input())
        print(febonacci(month))
    except:
        break
```
* 思路
  这是个典型的斐波那契数列问题，对于斐波那契数列，其递推公式为`f(n) = f(n-1) + f(n-2)`，因此，利用递推函数就可以快速写出
别人的答案

```pyhton
while True:
    try:
        month=int(input())
        a,b=1,0
        for i in range(month):
            a,b=b,a+b
        print(b)
    except:
        break
```
* 不同处:
同样是利用了递推的算法，但他的速度明显快于我的算法，其主要原因是我自己定义了一个函数来计算斐波那契数列的每一项，每次都要重新调用，从而浪费了大量的运算时间
**PS:**
有关斐波那契数列，还可以直接写出通项公式来计算

参考：[斐波那契数列四种python表示法](https://blog.csdn.net/FontThrone/article/details/78429771)

----

### Q7: 算术表达式
题述：
```
实现四则远算
```

输入:
```
算术表达式
```

输出:
```
计算结果
```
例子:
```
input:
3+2*{1+2*[-4/(8-6)+7]}

output:
25
```

我的答案:
```python
equation = input()
equation = equation.replace('[','(')
equation = equation.replace(']',')')
equation = equation.replace('{','(')
equation = equation.replace('}',')')
print(eval(equation))
```
python的思路比较简单,只需要将表达式的中括号和大括号进行替换即可

**关键点:**
 1. replace函数的使用
 2. eval()函数的使用

其他的答案:

`大同小异不再列出`

----

### Q8:杨辉三角的变形
题述:
```
1
1  1  1
1  2  3  2  1
1  3  6  7  6  3  1
1  4  10 16 19  16 10  4  1
以上三角形的数阵，第一行只有一个数1，以下每行的每个数，是恰好是它上面的数，左上角数到右上角的数，3个数之和（如果不存在某个数，认为该数就是0）。
求第n行第一个偶数出现的位置。如果没有偶数，则输出-1。例如输入3,则输出2，输入4则输出3。

输入n(n <= 1000000000)
本题有多组输入数据，输入到文件末尾，请使用while(cin>>)等方式读入
```

输入:
```
输入一个int整数
```
输出:
```
一个int值
```

我的代码：
```python
while True:
    try:
        n = int(input())
        if n == 1 or n ==2:
            print(-1)
        elif n%2 == 1:
            print(2)
        elif (n - 2)%4 == 0:
            print(4)
        else:
            print(3)
    except:
        break
```
实际上,这种方法比较投机取巧,通过观察10行三角数列的奇偶性来做出总结,发现在第二行之后,奇数行往往都是第二个数为偶数,而偶数行分为两种情况,分别作出`if`来进行输出

**缺点:**
这样的的方法显然不具有普适性,而且太过于投机取巧.接下来将进行比较传统的解法

```python
N_current = [1]
n = 1
required_row = int(input())
while n < required_row:
    N_temp = N_current
    N_temp.insert(0,0)
    N_temp.insert(0,0)
    N_temp.append(0)
    N_temp.append(0)
    N_next = []
    for i in range(len(N_temp) - 2):
        N_next.append(N_temp[i] + N_temp[i+1] + N_temp[i+2])
    N_current = N_next
    n += 1
        
print(N_current)
```

主要思想是利用递归和补零,但这种'传统的方法'实际上并不符合题目要求,因为原题暗示:

`输入n(n <= 1000000000)`

意味着不能使用递归或者循环(或者不能是这样的方法,最好的办法是找到规律只记录前面若干的数字,发现偶数就停止计算)

总体来说,这题的解法非常的巧妙,<font color = red>对数列的观察比思考出合理的算法更加重要</font>

------
## Day 2

### Q9: 表达式求值
题目描述:
```
给定一个字符串描述的算术表达式，计算出结果值。

输入字符串长度不超过100，合法的字符包括”+, -, *, /, (, )”，”0-9”，字符串内容的合法性及表达式语法的合法性由做题者检查。本题目只涉及整型计算。
```

输入:
```
算术表达式
```

输出:
```
计算结果
```

<font color = red>和Q7解法类似,不再赘述</font>
我的解法:

```py
while True:
    try:
        equation = str(input()).strip()
        print(eval(equation))
    except:
        break
```

----

### Q10: 完全数计算
题目描述:
```
完全数（Perfect number），又称完美数或完备数，是一些特殊的自然数。
它所有的真因子（即除了自身以外的约数）的和（即因子函数），恰好等于它本身。
例如：28，它有约数1、2、4、7、14、28，除去它本身28外，其余5个数相加，1+2+4+7+14=28。s
输入n，请输出n以内(含n)完全数的个数。计算范围, 0 < n <= 500000
本题输入含有多组样例。
```

输入:
```
一个数字n
```

输出:
```
输出不超过n的完全数的个数
```

我的代码:
```python
def perfect_num(num):
    if num == 1 or num == 0:
        return False
    divisor_list = []
    for i in range(num):
        if num%(i+1) == 0:
            divisor_list.append(i+1)
    del divisor_list[-1]
    if sum(divisor_list) == num:
        return True
    else:
        return False

while True:
    try:
        n = int(input())
        pnum = 0
        for i in range(n):
            if perfect_num(i + 1) == True:
                pnum += 1
        print(pnum)
    except:
        break
```

别人的解法(比较合理的):
```python
def checkprime(num):
    if num==1:
        return False
    list1=[]
    for i in range(2,num):
        if num%i==0:
            list1.append(i)
    if not list1:
        return True
    else:
        return False

while True:
    try:
        n=int(input())
        res=[]
        for i in range(1,n+1):
            if (2**i-1)*2**(i-1)>n:
                break
            elif checkprime(i) and checkprime(2**i-1):
                res.append((2**i-1)*2**(i-1))
        print(len(res))
    except:
        break
```

解题思路:
这个题目可以用比较常规的解法来通过,但是我们可以注意到,题目描述中,`计算范围, 0 < n <= 500000`, 而我的算法的时间复杂度为$O(n^2)$,显然是非常消耗计算资源,因此,为了更快的计算满足计算需求,就有了两种思路:
    ~~1. 通过提前计算好500000以内所有完美数的个数,分类直接输出答案~~
    **就我本人而言,是十分不认同这种解法的,因为这其实就是直接print答案到系统里,可算是是一种作弊**~~然而牛客里时间靠前的都是做么做的,没办法,最快嘛~~
    2. 通过数学推导,得到完美数的通项公式来进行验证
    这种方法即是我在上面贴出来的`别人的代码`的思路,通过`欧几里得-欧拉推论`可知,当$2^P-1$是一个质数时,$2^P(2^P-1)$即为完美数.
    因此,题目的解法就可以从遍历0到n的所有数字变成了预先计算好0~500,000的所有完美数来进行简化
    参考:[Euclid–Euler theorem](https://en.wikipedia.org/wiki/Euclid–Euler_theorem)

-----

### Q11:放苹果
题目描述:
```
把m个同样的苹果放在n个同样的盘子里，允许有的盘子空着不放，问共有多少种不同的分法？（用K表示）5，1，1和1，5，1 是同一种分法。
数据范围：0<=m<=10，1<=n<=10。
本题含有多组样例输入。
```

输入:
```
两个整数
```

```
一个整数
```

我的答案:
```python
def PutApple(apple,plate):
    if apple == 0:
        return 1
    elif plate == 1:
        return 1
    elif apple < plate:
        return PutApple(apple, apple)
    elif apple >= plate:
        return PutApple(apple, plate - 1) + PutApple(apple - plate, plate)
while True:
    try:
        M, N = map(int,input().split())
        print(PutApple(M, N))
    except:
        break
```

主要的思路:
这个题目最中心的思想就是递归,通过递归的逻辑来进行思考,具体可以分为以下四种情况开讨论:

```
- 设算法为PutApple(M,N)
1. 没有苹果或者只有一个盘子
2. 苹果数量小于盘子 --> 相当于M个苹果放到M个盘子 --> PutApple(M, M)
3. 苹果数量大于等于盘子, 计算下面的总和    
    --> 3.1 有空盘: 至少一个盘子是空的 --> PutApple(M, N-1)
    --> 3.2 没空盘: 相当于每个盘子先放一个 --> PutApple(M-N, N)
```
<font color = red>本题主要考察的是递归算法的运用, 解题思路非常的巧妙, 也对于逻辑思维能力有一定的要求, 可以作为递归算法的典型!
</font>

别人的答案:
`大同小异就不贴出来了`

----
### Q12: 查找输入整数二进制的1的个数
题目描述:
```
输入一个正整数，计算它在二进制下的1的个数。
注意多组输入输出！！！！！！
```

输入:
```
一个整数
```

输出:
```
整数二进制中1的个数
```

我的答案:
```python
while True:
    try:
        Num = int(input())
        Bi_Num = bin(Num)
        ones = str(Bi_Num).strip().count('1')
        print(ones)
    except:
        break
```

思路:
本题在python思路和Q1类似,不再赘述

----
### Q13: 

题目描述:
`有6条配置命令，它们执行的结果分别是：`

命令              |  执行 
:---------------:|:----------:
reset            | reset what
reset board      | board fault
board add        | where to add
board delete     | no board at all
reboot backplane | impossible
backplane abort  | install first
he he            | unknown command

```
注意：he he不是命令。
为了简化输入，方便用户，以“最短唯一匹配原则”匹配：
1、若只输入一字串，则只匹配一个关键字的命令行。例如输入：r，根据该规则，匹配命令reset，执行结果为：reset what；输入：res，根据该规则，匹配命令reset，执行结果为：reset what； 
2、若只输入一字串，但本条命令有两个关键字，则匹配失败。例如输入：reb，可以找到命令reboot backpalne，但是该命令有两个关键词，所有匹配失败，执行结果为：unknown command 
3、若输入两字串，则先匹配第一关键字，如果有匹配但不唯一，继续匹配第二关键字，如果仍不唯一，匹配失败。例如输入：r b，找到匹配命令reset board 和 reboot backplane，执行结果为：unkown command。
4、若输入两字串，则先匹配第一关键字，如果有匹配但不唯一，继续匹配第二关键字，如果唯一，匹配成功。例如输入：b a，无法确定是命令board add还是backplane abort，匹配失败。
5、若输入两字串，第一关键字匹配成功，则匹配第二关键字，若无匹配，失败。例如输入：bo a，确定是命令board add，匹配成功。
6、若匹配失败，打印“unknown command”
```

输入示例:
```
reset
reset board
board add
board delet
reboot backplane
backplane abort
```

输出示例:
```
reset what
board fault
where to add
no board at all
impossible
install first
```

我的答案:
```python
while True:
    try:
        cmd = input().split()
        cmd_dic1 = {'reset':'reset what'}
        cmd_dic2 = {'reset board': 'board fault',
                    'board add': 'where to add',
                    'board delete': 'no board at all',
                    'reboot backplane': 'impossible',
                    'backplane abort': 'install first'}
        unkcmd = 'unknown command'
        finding_flag = False
        if len(cmd) == 1:
            for key in cmd_dic1.keys():
                if cmd[0] in key[:len(cmd[0])]:
                    print(cmd_dic1[key])
                    finding_flag = True
            if not finding_flag:
                print(unkcmd)
        elif len(cmd) == 2:
            for key in cmd_dic2.keys():
                if cmd[0] in key[:len(cmd[0])] and cmd[1] in key.split()[1][:len(cmd[1])]:
                    print(cmd_dic2[key])
                    finding_flag = True
            if not finding_flag:
                print(unkcmd)
        else:
            print(unkcmd)
    except:
        break
```
*答案思路来源于牛客网评论区*

思路:
通过手动输入两个字典分别存放一个字符串的命令和两个字符串的命令和对应的返回值
优点                                  | 缺点
------------------------------------|-----------------------
具有拓展性,可以随时往里面加入新的命令 | 每个指令对应的返回值只能为一个(字典的特性)

-----
### Q14: 百钱买鸡

问题描述:
```
公元前五世纪，我国古代数学家张丘建在《算经》一书中提出了“百鸡问题”：鸡翁一值钱五，鸡母一值钱三，鸡雏三值钱一。百钱买百鸡，问鸡翁、鸡母、鸡雏各几何？
详细描述：
接口说明
原型：
int GetResult(vector &list)
输入参数：
        无
输出参数（指针指向的内存区域保证有效）：
    list  鸡翁、鸡母、鸡雏组合的列表
返回值：
     -1 失败     
     0 成功
```
输入:
```
任意整数开始运行
```

输出:
```
所有组合方式
```

我的答案:
```python
while True:
    try:
        start = input()
        total_money = 100  
        for x in range(0, int(total_money/5)):
            for y in range(1, int(total_money/3)):
                if 5 * x + 3 * y + 1/3 * (100 - x - y) == 100:
                    print(x, y, 100 - x - y)
    except:
        break
```
思路:
等同于解一个三元一次方程组,这里没有使用线性代数的方法来进行计算而是用循环来枚举得到解,这也可以算是计算机的方便之处了吧.
等同于:
$$\begin{cases}   
5x + 3y + \frac{1}{3}z = 100 \\
x+y+z=100 \\
\end{cases}
(x,y,z\in N)$$
求x,y,z所有整数解得组合
