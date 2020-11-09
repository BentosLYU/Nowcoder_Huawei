# 牛客网刷题笔记
## 序言和计划
* 总题量：108
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
## 入门和简单难度
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
## DAY 2

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
x+y+z=100
\end{cases}
(x,y,z\in N)$$

求x,y,z所有整数解得组合

----
## DAY 3
### Q15: 日期转换天数
题目描述:
```
根据输入的日期，计算是这一年的第几天。。
测试用例有多组，注意循环输入
```

输入
```
输入多行，每行空格分割，分别是年，月，日
```

输出
```
成功:返回outDay输出计算后的第几天;
失败:返回-1
```

我的答案:
```python
while True:
    try:
        year, month, day = input().split(' ')
        year = int(year)
        month = int(month)
        day = int(day)
        leapflag = False
        if year%4 == 0 and year%100 != 0:
            leapflag = True
        if month > 12 or day > 31:
            print(-1)
            break
        elif month in [4,6,9,11] and day > 30:
            print(-1)
            break
        elif month in [1,3,5,7,8,10,12] and day > 31:
            print(-1)
            break
        elif month == 2:
            if leapflag == True and day > 29:
                print(-1)
                break
            elif leapflag == False and day > 28:
                print(-1)
                break
        month_list = [31,28,31,30,31,30,31,31,30,31,30,31]
        actual_day = sum(month_list[0:month - 1]) + day
        if leapflag == True:
            print(actual_day + 1)
        else:
            print(actual_day)
    except:
        print(-1)
        break
```

别人的答案:
```python
while True:
    try:
        y,m,d = map(int, input().split())
        month = [31,28,31,30,31,30,31,31,30,31,30,31]
        days = sum(month[:(m-1)])+d
        if m >2 and (y % 4 ==0 and y%100 !=0 or y%400 ==0):
            days +=1
        print(days)
    except:
        break
```

**解题思路**
   1. 判断闰年,如果是闰年则天数加1.
   2. 还需判断输入是否合法,但讨论区的代码并没有加入这个功能,说明测试集中的日期都是符合格式且正常的
~~本题过于基础确实没什么好写的~~

----

### Q16: 参数解析
题目描述:
```
在命令行输入如下命令：
xcopy /s c:\ d:\，
各个参数如下： 
参数1：命令字xcopy 
参数2：字符串/s
参数3：字符串c:\
参数4: 字符串d:\
请编写一个参数解析程序，实现将命令行各个参数解析出来。
 
解析规则： 
1.参数分隔符为空格 
2.对于用“”包含起来的参数，如果中间有空格，不能解析为多个参数。比如在命令行输入xcopy /s “C:\program files” “d:\”时，参数仍然是4个，第3个参数应该是字符串C:\program files，而不是C:\program，注意输出参数时，需要将“”去掉，引号不存在嵌套情况。
3.参数不定长 
4.输入由用例保证，不会出现不符合要求的输入 
```

输入:
```
输入一行字符串，可以有空格
```

输出:
```
输出参数个数，分解后的参数，每个参数都独占一行
```

我的答案:
```python
while True:
    try:
        s = input().split(' ')
        print(len(s))
        for cmd in s:
            print(cmd)
    except:
        break
```

思路:~~过于基础没什么好说的了~~

----

### Q17: 寻找最大公共字符串长度

题目描述:
```
题目标题：
计算两个字符串的最大公共字串的长度，字符不区分大小写
详细描述：
接口说明
原型：
int getCommonStrLength(char * pFirstStr, char * pSecondStr);
输入参数：
     char * pFirstStr //第一个字符串
     char * pSecondStr//第二个字符串
```

输入:
```
输入两个字符串
```

输出:
```
输出一个整数
```

我的答案:
```python
while True:
    try:
        s1 = input().lower()
        s2 = input().lower()
        max_length = 0
        for i in range(len(s1)):
            for j in range(len(s2)):
                word = s1[i: i+j+1]
                if word in s2 and len(word) > max_length:
                    max_length = len(word)
        print(max_length)
    except:
        break
```

思路:

**1.因为不区分大小写,所以在匹配之前应该全部转换为统一的大写或者小写**
2.遍历两个字符串, 记录每次尝试匹配的字符串长度+1,知道找到最大值

-----
### Q18: 尼科彻斯定理

题目描述:
```
验证尼科彻斯定理，即：任何一个整数m的立方都可以写成m个连续奇数之和。
例如：
1^3=1
2^3=3+5
3^3=7+9+11
4^3=13+15+17+19
输入一个正整数m（m≤100），将m的立方写成m个连续奇数之和的形式输出。
本题含有多组输入数据。
```

输入:
```
一个整数
```

输出:
```
一个表达式字符串
```

我的答案:
```python
while True:
    try:
        m = int(input())
        x0 = str(m *(m - 1) + 1)
        out_list = [x0]
        for i in range(1,m):
            out_list.append(str(int(x0) + 2*i))
        print('+'.join(out_list))
    except:
        break
```

思路:
1. 关键在找到多项式的规律,直接将数学表达式写出来就行了

-----

### Q18: 二维数组操作判断

题目描述:
```
有一个数据表格为二维数组（数组元素为int类型），行长度为ROW_LENGTH,列长度为COLUMN_LENGTH。对该表格中数据的操作可以在单个单元内，也可以对一个整行或整列进行操作，操作包括交换两个单元中的数据；插入某些行或列。
请编写程序，判断对表格的各种操作是否合法。
详细要求:

1.数据表规格的表示方式为“行*列”, 数据表元素的位置表示方式为[行,列]，行列均从0开始编号
2.数据表的最大规格为9行*9列，对表格进行操作时遇到超出规格应该返回错误
3.插入操作时，对m*n表格，插入行号只允许0~m，插入列号只允许0~n。超出范围应该返回错误
4.只需记录初始表格中数据的变化轨迹，查询超出初始表格的数据应返回错误
例如:  初始表格为4*4，可查询的元素范围为[0,0]~[3,3]，假设插入了第2行，数组变为5*4，查询元素[4,0]时应该返回错误
```
输入:
```
输入数据按下列顺序输入：
1 表格的行列值
2 要交换的两个单元格的行列值
3 输入要插入的行的数值
4 输入要插入的列的数值
5 输入要获取运动轨迹的单元格的值
```

输出:
```
输出按下列顺序输出：
1 初始化表格是否成功，若成功则返回0， 否则返回-1
2 输出交换单元格是否成功
3 输出插入行是否成功
4 输出插入列是否成功
5 输出要查询的运动轨迹的单元查询是否成功
```

我的答案:
```python
while True:
    try:
        row, col = map(int, input().split(' '))
        if row > 9 or row < 0 or col > 9 or col < 0:
            print(-1)
        else:
            print(0)
        swap_row1, swap_col1, swap_row2, swap_col2 = map(int, input().split(' '))
        if swap_row1 >= row or swap_row2 >= row or swap_col1 >= col or swap_col2 >= col:
            print(-1)
        elif swap_row1 == swap_row2 and swap_col1 == swap_col2:
            print(-1)
        else:
            print(0)
        insert_row = int(input())
        if insert_row >= row or insert_row < 0 or row + 1 > 9:
            print(-1)
        else:
            print(0)
        insert_col = int(input())
        if insert_col >= col or insert_col < 0 or col + 1 > 9:
            print(-1)
        else:
            print(0)
        trace_row, trace_col = map(int, input().split(' '))
        if trace_row >= row or trace_col >= col:
            print(-1)
        else:
            print(0)
    except:
        break
```

思路:
~~没什么思路按照题目描述硬做出来就行了~~

-----
### Q19: 统计大写字母个数

题目描述:
```
找出给定字符串中大写字符(即'A'-'Z')的个数
接口说明
原型：int CalcCapital(String str);
返回值：int
```

输入:
```
输入一个String数据
```

输出:
```
输出string中大写字母的个数
```

我的答案:
```python
while True:
    try:
        s = str(input())
        n = 0
        for i in s:
            if i.isupper() is True:
                n += 1
        print(n)
    except:
        break
```

思路:
比较基础,python的字符操作还是非常方便的,有下面几个常用的函数可以参考:
函数   | 功能
:----|:----
字符串.isalnum() | 所有字符都是数字或者字母，为真返回 Ture，否则返回 False。 
字符串.isalpha()  | 所有字符都是字母，为真返回 Ture，否则返回 False。 
字符串.isdigit()   |  所有字符都是数字，为真返回 Ture，否则返回 False。 
字符串.islower()   | 所有字符都是小写，为真返回 Ture，否则返回 False。 
字符串.isupper()  | 所有字符都是大写，为真返回 Ture，否则返回 False。 
字符串.istitle()   |   所有单词都是首字母大写，为真返回 Ture，否则返回 False。 
字符串.isspace()  | 所有字符都是空白字符，为真返回 Ture，否则返回 False。

----

### Q20: 寻找最长回文子串的长度
题目描述:
```
Catcher 是MCA国的情报员，他工作时发现敌国会用一些对称的密码进行通信，比如像这些ABBA，ABA，A，123321，但是他们有时会在开始或结束时加入一些无关的字符以防止别国破解。比如进行下列变化 ABBA->12ABBA,ABA->ABAKK,123321->51233214　。因为截获的串太长了，而且存在多种可能的情况（abaaab可看作是aba,或baaab的加密形式），Cathcer的工作量实在是太大了，他只能向电脑高手求助，你能帮Catcher找出最长的有效密码串吗？
（注意：记得加上while处理多个测试用例）
```

输入:
```
一个字符串
```

输出:
```
字符串内含有最长回文(密码)的长度
```

我的答案:
```python
def solution(s):
    if s==s[::-1]: #如果整个字符串都是回文则不用进行遍历,直接输出字符串的长度,不浪费时间
        return len(s)
    m = 0
    #初始化最长回文长度为0
    for i in range(len(s)):
    #从第一个字符开始遍历字符串
        if i-m>=1 and s[i-m-1:i+1]==s[i-m-1:i+1][::-1]:
        #判断目前将要判定字符串是奇数长度还是偶数长度,分别进行判断
            m+=2
        if i-m>=0 and s[i-m:i+1]==s[i-m:i+1][::-1]:
            m+=1
    return m
while True:
    try:
        s = str(input())
        if s: #如果s为空,则不输出!!!!(这里有坑)
            print(solution(s))
    except:
        break
```

思路:
题目描述看起来复杂,但是本质上就是寻找字符串中所包含的**最长的回文的长度**
基础部分--每增加一个字母,回文最大长度只可能+1(奇对称)或者+2(偶对称)
因此,从头扫描字符串,以每个字符串开头分别增加新的字符, 判断增加字符后的内容是否为回文, 如果目前其长度为奇数(i - m) = 1, 则+2, 反之+1

### Q21: 求最大连续bit数
题目描述:
```
功能: 求一个byte数字对应的二进制数字中1的最大连续数，例如3的二进制为00000011，最大连续2个1 
输入: 一个byte型的数字   
输出: 无     
返回: 对应的二进制数字中1的最大连续数
```

输入:
```
一个byte数
```

输出:
```
数的二进制中最长连续'1'的个数
```

我的答案:
```python
while True:
    try:
        num = int(input())
        binum = bin(num)
        s = str(binum)
        m = 0
        for i in range(len(s)):
            if '1' * i in s and i > m:
                m = i
        print(m)
    except:
        break
```

思路:
遍历一长度为i的'1'的字符串在数中是否存在,i的最大值为数值二进制的长度

----
### Q22: 密码强度等级

题目描述:
```
密码按如下规则进行计分，并根据不同的得分为密码进行安全等级划分。
一、密码长度:
5 分: 小于等于4 个字符
10 分: 5 到7 字符
25 分: 大于等于8 个字符
二、字母:
0 分: 没有字母
10 分: 全都是小（大）写字母
20 分: 大小写混合字母
三、数字:
0 分: 没有数字
10 分: 1 个数字
20 分: 大于1 个数字
四、符号:
0 分: 没有符号
10 分: 1 个符号
25 分: 大于1 个符号
五、奖励:
2 分: 字母和数字
3 分: 字母、数字和符号
5 分: 大小写字母、数字和符号
最后的评分标准:
>= 90: 非常安全
>= 80: 安全（Secure）
>= 70: 非常强
>= 60: 强（Strong）
>= 50: 一般（Average）
>= 25: 弱（Weak）
>= 0:  非常弱

对应输出为：
VERY_SECURE

SECURE,

VERY_STRONG,

STRONG,

AVERAGE,

WEAK,

VERY_WEAK,


请根据输入的密码字符串，进行安全评定。
注：
字母：a-z, A-Z
数字：-9
符号包含如下： (ASCII码表可以在UltraEdit的菜单view->ASCII Table查看)
!"#$%&'()*+,-./     (ASCII码：x21~0x2F)
:;<=>?@             (ASCII<=><=><=><=><=>码：x3A~0x40)
[\]^_`              (ASCII码：x5B~0x60)
{|}~                (ASCII码：x7B~0x7E)
接口描述：

Input Param 
String pPasswordStr:    密码，以字符串方式存放。
Return Value
根据规则评定的安全等级。


public static Safelevel GetPwdSecurityLevel(String pPasswordStr)
{
/*在这里实现功能*/
return null;
}
```

输入:
```
一个字符串
```

输出:
```
打印密码等级
```

我的答案:
```python
def strnum(s):
    DigitNum = 0
    UpperNum = 0
    LowerNum = 0
    OtherNum = 0
    for i in s:
        if i.isdigit():
            DigitNum = DigitNum + 1
        elif i.isalpha() and i.isupper():
            UpperNum += 1
        elif i.isalpha() and i.islower():
            LowerNum += 1
        else:
            OtherNum += 1
    return (DigitNum, UpperNum, LowerNum, OtherNum)

def secure_score(s):
    score = 0
    #score for length
    if len(s) <= 4:
        len_score = 5
    elif len(s) >= 8:
        len_score = 25
    else:
        len_score = 10
    
    DigitNum, UpperNum, LowerNum, OtherNum = strnum(s)
    
    #score for letter
    if UpperNum + LowerNum == 0:
        letter_score = 0
    elif UpperNum == 0 or LowerNum == 0:
        letter_score = 10
    else:
        letter_score = 20
    
    #score for digit
    if DigitNum == 0:
        digit_score = 0
    elif DigitNum == 1:
        digit_score = 10
    else:
        digit_score = 20
    
    #score for others
    if OtherNum == 0:
        other_score = 0
    elif OtherNum == 1:
        other_score = 10
    else:
        other_score = 25
    
    #extra score
    if DigitNum != 0 and UpperNum != 0 and LowerNum != 0 and OtherNum != 0:
        extra_score = 5
    elif DigitNum != 0 and UpperNum != 0 and LowerNum == 0 and OtherNum != 0:
        extra_score = 3
    elif DigitNum != 0 and UpperNum == 0 and LowerNum != 0 and OtherNum != 0:
        extra_score = 3
    elif DigitNum != 0 and UpperNum + LowerNum != 0 and OtherNum == 0:
        extra_score = 2
    else:
        extra_score = 0
    total_score = len_score + letter_score + digit_score + other_score + extra_score
    return (total_score)

while True:
    try:
        password = str(input())
        score = secure_score(password)
        if score >= 90:
            print('VERY_SECURE')
        elif score >= 80 and score <90:
            print('SECURE')
        elif score >=70 and score <80:
            print('VERY_STRONG')
        elif score >= 60 and score <70:
            print('STRONG')
        elif score >= 50 and score <60:
            print('AVERAGE')
        elif score >= 25 and score <50:
            print('WEAK')
        else:
            print('VERY_WEAK')
    except:
        break
```

别人的答案:
```python
while True:
    try:
        str_data = input().strip()
        num, up_char, low_char, other, score = 0, 0, 0, 0, 0

        for data in str_data:
            if data.isdigit():
                num += 1
            elif data.isalpha():
                if data.lower() == data:
                    low_char += 1
                else:
                    up_char += 1
            else:
                other += 1
        if len(str_data) < 5:
            score += 5
        elif len(str_data) < 8:
            score += 10
        else:
            score += 25
        if up_char==0 and low_char==0:
            pass
        elif (up_char==0 and low_char!=0) or (up_char!=0 and low_char==0):
            score += 10
        else:
            score += 20
        if num == 0:
            pass
        elif num == 1:
            score += 10
        else:
            score += 20
        if other == 0:
            pass
        elif other == 1:
            score += 10
        else:
            score += 25
        if num != 0 and (up_char+low_char) != 0 and other==0:
            score += 2
        elif num != 0 and up_char != 0 and low_char != 0 and other!=0:
            score += 5
        elif num != 0 and (up_char+low_char) != 0 and other!=0:
            score += 3
        if score >=90:
            print('VERY_SECURE')
        elif score >=80:
            print('SECURE')
        elif score >= 70:
            print('VERY_STRONG')
        elif score >= 60:
            print('STRONG')
        elif score >= 50:
            print('AVERAGE')
        elif  score>=25:
            print('WEAK')
        else:
            print('VERY_WEAK')
    except:
        break
```

思路:
没什么技巧,硬分类就行了

-----
## DAY 4
### Q23 棋盘走法

题目描述
```
请编写一个函数（允许增加子函数），计算n x m的棋盘格子（n为横向的格子数，m为竖向的格子数）沿着各自边缘线从左上角走到右下角，总共有多少种走法，要求不能走回头路，即：只能往右和往下走，不能往左和往上走。
输入描
```

输入:
```
两个正整数
```

输出:
```
整数结果
```

我的答案:
```python
def UniquePath(m, n):
    if m == 1 or n == 1:
        return 1
    result = [[0 for i in range(n)]] * m
    for i in range(m):
        result[i][0] = 1
    for i in range(n):
        result[0][i] = 1
    for i in range(1, m):
        for j in range(1, n):
            result[i][j] = result[i - 1][j] + result[i][j - 1]
    return result[m - 1][n - 1]

while True:
    try:
        print(UniquePath(*map(lambda c: int(c)+1, input().split())))
    except:
        break
```

思路:
这是典型的一个动态规划问题,通过找到动态规划的表格和状态转移方程的表述,可以遍历所有可能的最优方案来得到结果.详细算法参考*算法图解,第八章*
**本体的主要思路来源于牛客网讨论区**

动态规划是最优算法的一个重要部分,之后的联系中肯定会大量地涉及.应该将注意力更多地放在对<算法图解>这本书的解释上

---
### Q23: 等差数列

题目描述:
```
功能:等差数列 2，5，8，11，14。。。。
输入:正整数N >0
输出:求等差数列前N项和
返回:转换成功返回 0 ,非法输入与异常返回-1
本题为多组输入，请使用while(cin>>)等形式读取数据
```

输入:
```
输入一个正整数。
```

输出:
```
输出一个相加后的整数。
```

我的答案:
```python
while True:
    try:
        N = int(input())
        i = 0
        M = 0
        if N > 0:
            while i < N:
                M += 2 + i*3
                i += 1
        print(M)
    except:
        break
```

思路:
比较基础,就不用解释了

----

### Q24:字符逆序

题目描述:
```
将一个字符串str的内容颠倒过来，并输出。str的长度不超过100个字符。 如：输入“I am a student”，输出“tneduts a ma I”。
输入参数：

inputString：输入的字符串

返回值：

输出转换好的逆序字符串
```

输入:
```
输入一个字符串，可以有空格
```

输出:
```
输出逆序的字符串
```

我的答案:
```python
while True:
    try:
        print(str(input())[::-1])
    except:
        break
```

思路:
对于python来说是送分题,不过多赘述

----
### Q25: 最小公倍数

题目描述:
```
正整数A和正整数B 的最小公倍数是指 能被A和B整除的最小的正整数值，设计一个算法，求输入A和B的最小公倍数。
```

输入:
```
输入两个正整数A和B。
```

输出:
```
输出A和B的最小公倍数。
```

我的答案:
```python
def find_gcd(M, N):
    while M%N != 0:
        Res = M%N
        M = N
        N = Res
    return N

while True:
    try:
        A, B = map(int, input().split(' '))
        print(int(A * B / find_gcd(A,B)))
    except:
        break
```

思路:
非常经典的一个算法题,关键点在于使用辗转相除法的得到最大公约数之后里用

$最大公约数 = 整数A * 整数B / 最小公倍数(A, B)$

这个式子来得到最终答案

----
## 中等难度
### Q26: 进制转换

题目描述:
```
写出一个程序，接受一个十六进制的数，输出该数值的十进制表示。
```

输入:
```
输入一个十六进制的数值字符串。注意：一个用例会同时有多组输入数据，请参考帖子https://www.nowcoder.com/discuss/276处理多组输入的问题。
```

输出:
```
输出该数值的十进制字符串。不同组的测试用例用\n隔开。
```

我的答案:
```python
while True:
    try:
        print(str(int(input(), 16)))
    except:
        break
```

思路:
对于python来说只需要一行就可以进行进制转换,但我认为这个这个答案虽然能通过,但并非所有情况都能使用,这其中涉及到*大数问题*,但碍于时间限制,这次并不展开讨论,如果后面有类似题目再深入进行思考

### Q27: 质数因子
题目描述:
```
功能:输入一个正整数，按照从小到大的顺序输出它的所有质因子（重复的也要列举）（如180的质因子为2 2 3 3 5 ）
最后一个数后面也要有空格
```

输入:
```
输入一个long型整数
```

输出:
```
按照从小到大的顺序输出它的所有质数的因子，以空格隔开。最后一个数后面也要有空格。
```

我的答案:
```python
while True:
    try:
        N = int(input())
        div = []
        while N > 1:
            for i in range(2, N + 1):
                if N % i == 0:
                    N = int(N / i )
                    if N == 1:
                        div.append(i)
                    else:
                        div.append(i)
                    break
        for i in div:
            print(i, end = ' ')
    except:
        break
```

思路:
类似于辗转相除法,每次用新的商来除以新的质数.

-----
### Q28 合并记录表

题目描述:
```
数据表记录包含表索引和数值（int范围的整数），请对表索引相同的记录进行合并，即将相同索引的数值进行求和运算，输出按照key值升序进行输出。
```

输入:
```
先输入键值对的个数
然后输入成对的index和value值，以空格隔开
```

输出:
```
输出合并后的键值对（多行）
```

我的答案:
```python
while True:
    try:
        num = int(input())
        dict = {}
        for i in range(num):
            m, n = map(int, input().split())
            if m in dict:
                dict[m] += n
            else:
                dict[m] = n
        for i in sorted(dict.keys()):
            print(i, dict[i])
    except:
        break
```

思路:
关键点在于输入的判断和对字典的排序,如果输入的index已经重复则值相加,否则加入新的key和value

----

## DAY 5
### 提取不重复的整数

题目描述:
```
输入一个int型整数，按照从右向左的阅读顺序，返回一个不含重复数字的新的整数。
```

输入:
```
输入一个int
```

输出:
```
按照从右到左的阅读顺序,返回一个不含重复数字的新的整数
```

我的答案:
```python
while True:
    try:
        num = str(int(input()))[::-1]
        rev = []
        for i in num:
            if i not in rev:
                rev.append(i)
        print(int(''.join(rev)))
    except:
        break
```

思路:
比较无脑,逆序然后逐个比较,有就丢掉,没有就加入新的list,然后把新的list组合成字符串后输出

别人的答案:
```python
a = input()[::-1]
print("".join(sorted(set(a),key=a.index)))
```

思路:
用到了python中的`set()`函数来进行去重, 效率更高, 但需要注意的是, 直接使用set()函数会改变列表的顺序,所以还要使用`sorted()`函数来重新排列
