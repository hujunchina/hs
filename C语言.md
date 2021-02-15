# 结构体

结构体中的函数必须为指针类型，与函数声明进行区分，若是指针函数，应再价格指针，如下图：

![image-20210124193352522](D:\markdown\IMG\image-20210124193352522.png)

# 指针

指针型的函数名和指针型的变量、结构体均存放在内存的堆中，程序执行完才释放内存；而一般的函数、变量、结构体存放在栈中，局部作用结束就会释放内存；

正确：![image-20210124194145635](D:\markdown\IMG\image-20210124194145635.png)

错误：![image-20210124194250154](D:\markdown\IMG\image-20210124194250154.png)

t[]和f[]为局部数组变量，放在栈区，执行完函数，释放掉内存，而函数返回值为char* (不能为char，否则返回的是数组与char类型不匹配)，指向t[]或f[]的地址，而地址里面的内容已经被清除，于是报错；

# goto语句

触发点，跳转到指定语句，该语句必须在方法及函数体内使用；

# 函数指针&指针函数

## 指针函数：

简单的来说，就是一个返回指针的函数，其本质是一个函数，而该函数的返回值是<u>一个指针</u>。

声明格式为：类型标识符 \*  函数名(参数表)

其返回值是一个 int 类型的指针，是一个地址。

注意：在调用指针函数时，需要一个同类型的指针来接收其函数的返回值。
不过也可以将其返回值定义为 void*类型，在调用的时候强制转换返回值为自己想要的类型。

## 函数指针：

其本质是一个指针变量，该指针指向这个函数。总结来说，函数指针就是指向函数的指针。
声明格式：类型说明符 (*函数名) (参数)

int (*fun)(int x,int y);

函数指针是需要把一个函数的地址赋值给它，有两种写法：

```
fun = &Function；
fun = Function;
取地址运算符&不是必需的，因为一个函数标识符就表示了它的地址，如果是函数调用，还必须包含一个圆括号括起来的参数表。
```

​      x = (*fun)(); x = fun();

## 定义不同

指针函数本质是一个函数，其返回值为指针。
函数指针本质是一个指针，其指向一个函数。

## 写法不同

指针函数：int* fun(int x,int y);
函数指针：int (*fun) (int x,int y);

可以简单粗暴的理解为，指针函数的*是属于数据类型的，而函数指针的星号是属于函数名的。
再简单一点，可以这样辨别两者：函数名带括号的就是函数指针，否则就是指针函数。

# 声明

声明是把特定标识符与计算机内存中的特定位置联系起来，变量声明和<u>函数声明</u>都是如此；

# 前缀和后缀

![image-20210130204800251](D:\markdown\IMG\image-20210130204800251.png)

![image-20210130205233446](D:\markdown\IMG\image-20210130205233446.png)

while(++shoe<18.5)，该测试条件相当于提供了一个鞋子尺码到 18的表。如果使用shoe++而不是++shoe，尺码表会增加到19，因为shoe会与18.5进行比较之后才递增，而不是先递增再比较。

# scanf输入前的&

![image-20210130210642382](D:\markdown\IMG\image-20210130210642382.png)

注意：scanf()只读取了Angela Plains中的Angela，它在遇到第1个空白（空格、制表符或换行符）时就不再读取输入。因此，scanf()在读取到Angela Plains之间的空格时就停止了。一般而言，根据%s转换说明，scanf()只会读取字符串中的一个单词，而不是一整句。C语言还有其他的输入函数（如：fgets()）,用于读取一般字符串。

strlen()不会将字符串末尾的空字符计入，sizeof运算符报告对声明的所有字节数统计，sizeof+变量，则不必须要sizeof()，若sizeof+类型，则需要sizeof(),例如：sizeof(int)。

scanf("%c", &cn)从输入中的第一个字符开始读取，scanf("  %c", &cn)从第一个非空白字符开始读取。

# 常量和C预处理器

## 符号常量

符号常量，#define NAME value   ,末尾不需要加“；”

## const限定符

const int MONTHS = 12;

# 副作用和序列点

副作用是对数据对象或文件的修改；序列点是程序执行的点，在该点上，所有的副作用都在进入下一步之前发生，语句的分号和任何一个完整表达式的结束都是序列点；

while(guests++ <10)

​	printf("%d \n",guests);

表达式guests++ <10是一个完整的表达式，所以printf中使用的guests递增之后的值。

# getchar()&&putchar()

getchar()和putchar()只处理字符，是预处理宏，不是真正的函数。

![image-20210131105954847](D:\markdown\IMG\image-20210131105954847.png)

# 字符测试函数

![image-20210131110539948](D:\markdown\IMG\image-20210131110539948.png)

![image-20210131110605792](D:\markdown\IMG\image-20210131110605792.png)

# 逻辑运算符、条件运算符

## 逻辑运算符

![image-20210131110924576](D:\markdown\IMG\image-20210131110924576.png)

### 优先级

！运算符的优先级很高，比乘法运算发优先级还高，与递增运算符的优先级相同，只比圆括号的优先级低。&&运算符的优先级比||运算符高，但是两者的优先级都比关系运算符低，比赋值运算符高。c保证逻辑表达式的求值顺序是从左往右，&&和||运算符都是序列点，所以整个程序在从一个运算对象执行到下一个运算对象之前，所有的副作用都会生效。

而且，C保证一旦发现某个元素让整个表达式无效，便立刻停止求值。

while(x++ <10 && x+y <20)

实际上，&&是一个序列点，这保证了在对<u>&&右侧的表达式求值之前，已经递增了x</u>。

## 条件运算符

x=(y<0)?-y:y;

在=和；之间的内容就是条件表达式，该语句的意思是“如果y小于0，那么x=-y；否则，x=y"。

cans += ((sq_feet % COVERAGE == 0)) ? 0: 1;

该语句把+=右侧的表达式的值加上cans，再赋值给cans。右侧表达式是一个条件表达式，根据sq_feet是否能被COVERAGE整除，其值为0或1.

# Switch && break  &&  continue

break语句可用于循环和switch语句中，而continue只能由于循环中，尽管如此，如果switch语句在一个循环中，continue便可作为switch语句中的一部分。这种情况下，就像在其他循环中一样，continue让程序跳出循环的剩余部分，包括switch语句的其他部分。

switch在圆括号中的测试表达式的值应该是一个整数值（包括char类型）。case标签必须是整数类型（包括char类型）的常量或整型常量表达式（即，表达式中只包含整型常量）。不能用变量作为case标签。

break语句让程序离开switch语句，跳至switch语句后面的下一条语句。如果没有break语句，就会从<u>匹配标签开始执行到switch末尾</u>（接下来的每个case都会执行）。

goto b；

b:XXXX；

# 函数

## 函数内存分配

程序执行过程中，函数若不被使用，则只是放在代码区，若被调用，在函数被调用的地方，给函数分配内存（无论是指针函数害还是函数指针被调用时，均给函数分配栈区的内存），注意：（1）指针函数；本质是一个函数，返回值是指针；调用这个指针函数时，为这个指针函数分配内存（<u>这个内存在栈区</u>），返回的指针，指向的内容在堆区；（2）函数指针；本质是一个指针，指向函数；调用这个函数指针时候，为这个函数指针分配内存（<u>这个内存在栈区</u>）。

函数与变量不一样，变量是有的分配在栈区，有的分配在堆区；而函数统一分配在栈区，是因为函数需要一步一步的执行，栈规定了一步一步执行，而堆区没有规定一步一步执行。

![img](D:\markdown\IMG\4bef2d84-c975-4e3f-b2f6-c2f49f2b807a.jpg)

## 带形参的函数定义、声明、被调用

### 定义带形式参数的函数

形式参数也是局部变量，属于函数私有，这意味着在其他函数中使用同名变量不会引起名称冲突。

void show_n_char(char ch, int num)

### 声明带形式参数的函数原型

（1）void show_n_char(char ch, int num)；

（2）void show_n_char(char, int)

在原型中使用变量名并没有实际创建变量，实际被调用时，在调用处创建变量并分配内存。

### 调用带形式参数的函数

形式参数是被调用函数中的变量，实际参数是主调函数赋给被调用函数的具体值，实际参数可以是变量、常量，甚至是更复杂的表达式，然后该值<u>被拷贝给</u>被调用函数相应的形式参数。

## return

（1）返回值不仅可以赋给变量，也可以被用作表达式的一部分；

（2）返回值不一定是变量的值，也可以是任意表达式的值；

（3）实际得到的返回值相当于把函数中指定的返回值赋给与函数类型相同的变量所得到的值；

（4）使用return的另一个作用是，终止函数并把控制返回给主调函数的下一条语句。

## 递归

待补充。。。

## Linux

假定linux系统安装了GNU C编译器GCC，假设文件file1.ch和文件file2.c是两个内含C函数的文件，下面的命令将编译两个文件并生成名为a.out的可执行文件：

gcc file1.c file2.c

另外还生成两个名为file1.o 和file2.o的目标文件。如果后来改动了file1.c，而file2.c不变，可以使用以下命令编译第一个文件，并与第二个文件的目标代码合并：

gcc file1.c file2.o

# 指针

指针是一个值为内存地址的变量（或数据对象），正如char类型变量的值是字符，int类型变量的值是整数，指针变量的值是地址。

ptr = & pooh; //把pooh的地址赋值给ptr

对于这条语句，我们说ptr指向pooh。ptr和&pooh的区别是ptr是变量，而&pooh是常量。或者说，ptr是可修改的左值，而&pooh是右值，还可以把ptr指向别处。

## 间接运算符：*

‘*’运算符有时也称为解引用运算符

地址运算符：&

后跟一个变量名时，&给出该变量的地址；

地址运算符：*

后跟一个指针名或地址时，*给出储存在指针指向地址上的值。

## 声明指针

pointer ptr; // 不能这样声明指针

为什么不能这样声明？因为声明指针变量时必须指定指针所指向变量的类型，因为不同的变量类型占用不同的存储空间，一些指针操作要求知道操作对象的大小。另外，程序必须知道储存在指定地址上的数据类型。long和float可能占用相同的存储空间，但是他们储存数字却大相径庭。

int *pi;

类型说明符表明了指针所指向对象的类型，星号*表明声明的变量时一个指针。int * pi ;声明的意思时pi时一个指针，*pi是int类型。

# 数组

## 初始化数组

数组通常被用来储存程序需要的数据；

(1)初始化方式1：

int power[8]={1,2,3,4,5,6,7,8};//在逗号和值之间可以使用空格。

(2)const 声明数组，方式2：

const int days[12]={31,28,31,30,31,30,31,31,30,31,30,31};

通过使用const声明和初始化数组，使数组为只读形式，这样，程序只能从数组中检索值，不能把新值写入数组。程序在运行过程中就不能修改该数组中的内容。

（3）初始化方式3：

int power[8]={1,2,3};

当初始化列表中的值少于数组元素个数时，编译器会把剩余的元素都初始化为0，也就是说，如果不初始化数组，数组元素和未初始化的普通变量一样，其中储存的都是垃圾值。如果初始化列表的项数多于数组元素个数，编译器会将其视为错误。

### 指定初始化器

int arr[6] = {[5] = 212}; //把arr[5]初始化为212

对于一般的初始化，在初始化一个元素后，未初始化的元素都会被设置为0.

变长数组：VLA

## 多维数组

float rain[5] [12];//内含5个数组元素的数组，每个数组元素内含12个float类型的元素。

理解该声明的一种方法是，先查看中间部分（粗体部分）：

float **rain[5]** [12];//rain是一个内含5个元素的数组

这说明数组rain有5个元素，至于每个元素的情况，要查看声明的其余部分（粗体部分）；

**float** rain[5] **[12]**;//一个内含12个float类型元素的数组

这说明每个元素的类型是float[12],也就是说，rain的每个元素本身都是一个内含12个float类型值的数组。

## 指针和数组

数组名是数组首元素的地址，如果flizny是一个数组，下面的语句成立：

flizny == &flizny[0];//数组名是该数组首元素的地址

flizny 和&flizny[0]都表示数组首元素的内存地址（&是地址运算符）。两者都是常量，在程序运行过程中，不会改变。

### 指针加

指针加1指的是增加一个存储单元，对数组而言，这意味着把加1后的地址是下一个元素的地址，而不是下一个字节的地址，这是为什么必须声明指针所指向对象类型的原因之一，只知道地址不够，因为计算机要知道储存对象需要多少个字节。

dates + 2 == &dates[2];//相同的地址

*（dates + 2 ）== dates[2];//相同的值

ar[n]的意思是*（ar+n）,可以认为 *（ar+n）的意思是“到内存的ar位置，然后移动n个单元，检索储存在那里的值”。

*（dates+2）和 *dates+2,间接运算符（ * ）的优先级高于 +，所以*dates+2相当于（ *dates）+2。

### 函数、数组和指针

total = sum(marbles); //可能的函数调用

记住，数组名是该数组首元素的地址，所以实际参数marbles是一个储存int类型值的地址，应把它赋给一个指针形式参数，即该参数是一个指向int的指针；

int sum(int *ar); //对应的函数原型

既然能使用指针表示数组名，也可以用数组名表示指针。

int sum(int *ar, int n)

{

​		int i;

​		int total = 0;

​		for (i=0; i<n; i++)

​				total += ar[i];//ar[i]和*（ar+i）相同

​		return total;

}

关于函数的形参，还有一点要注意。只有在<u>函数原型或函数定义头</u>中，才可以使用int ar[]代替int *ar;

int sum(int ar[], int n);

int *ar 形式和int ar[]形式都表示ar是一个指向int的指针。但是，int ar[]只能用于声明形式参数。

由于<u>函数原型</u>可以省略参数名，所以下面4种原型都是等价的：

int sum(int *ar, int n);

int sum(int *, int );

int sum(int ar[], int n);

int sum(int [], int );

但是，在函数定义中不能省略参数名。

int sum(int *ar, int n)

{

//其它代码

}

int sum(int ar[], int n)

{

//其它代码已省略

}

### 使用指针形参

函数处理数组，需要知道何时开始、何时结束。sum（）函数使用一个指针形参标识数组的开始，用一个整数形参表明待处理数组的元素个数，但是这并不是给函数传递必备信息的唯一方法；

还有一种方法是传递两个指针，第一个指针指明数组的开始处，第二个指针指明数组的结束处。

int main(void)
{
	int marbles[SIZE] = {20, 10, 5, 39, 4, 16, 19, 26, 31, 20};
	long answer;
	answer = sump(marbles, marbles + SIZE);//数组名也是指针
	printf("The total number of marbles is %ld.\n", answer); 
	return 0; 
	
}

int sump(int *start, int *end)
{
	int total = 0;
	while(start < end)
	{
		total += *start;//把数组元素的值加起来
		start++;        //让指针指向下一个元素 
	}
	return total; 
}

循环最后处理的一个元素是end所指向位置的前一个元素。这意味着end指向的位置实际上在数组最后一个元素的后面。C保证在给数组分配空间时，指向数组后面第一个位置的指针仍是有效的指针。

total += *start;一元运算符 * 和++的优先级相同，但结合律是从右往左，所以start++先求值，然后才是*start。

至于C语言，ar[i]和*（ar+1）这两个表达式都是等价的。无论ar是数组名还是指针变量，这两个表达式都没问题。但是，只有当ar是指针变量时，才能使用ar++这样的表达式。

### 解引用指针

千万不要解引用未初始化的指针，如下：

int * pt ; //未初始化的指针

*pt = 5;  //严重的错误

为何不行？第2行的意思是把5储存在pt指向的位置。但是pt未被初始化，其值是一个随机值。切记：创建一个指针时，系统只分配了储存指针本身的内存，并未分配储存数据的内存，因此，在使用指针之前，必须先用已分配的地址初始化它。

# const(保护数组中的数据)

函数使用中，传递数组必须使用指针，因为这样做效率高。如果一个函数按值传递数组，则必须分配足够的空间来储存原数组的副本，然后把原数组所有的数据拷贝至新的数组中。

编译器通常不会为普通的const只读变量分配存储空间，而是将它们保存在符号表中，这使得它成为一个编译期间的值，没有了存储与内存的操作，使得它的效率也高。const定义的只读变量从汇编的角度来看，只是给出了对应的内存地址，而不是像#define一样给出的是立即数，所以const定义的只读变量在程序运行过程中只有一份备份（因为它是全局的只读变量，存放在静态区），而#define定义的宏常量在内存中有若干个备份。#define宏是在预编译阶段进行替换，而const修饰的只读变量是在编译的时候确定其值。#define没有类型，而const修饰的只读变量具有特定的类型。

## 对形式参数使用const

如果函数的意图不是修改数组中的数据内容，那么在函数原型和函数定义中声明形式参数时应使用关键字const。

`int main(void)`
`{`
	`double dip[SIZE] = {20.0, 10.5, 5.78, 3.99, 4.26};`
	`printf("The original dip array:\n");`
	`show_array(dip, SIZE);`
	`mult_array(dip, SIZE, 2.5);`
	`printf("The dip array after calling mult_array():\n");`
	`show_array(dip, SIZE);`
	`return 0;` 	
`}`

`/*显示数组的内容*/`
`void show_array(const double ar[], int n)`
`{`
	`int i;`
	`for(i = 0; i< n; i++)`
		`printf("%8.3f",ar[i]);`
	`putchar('\n');`
 `}` 
`/*把数组的每个元素都乘以相同的值*/`
`void mult_array(double ar[], int n, double mult)   //数组也是指针，不会重新分配内存` 
`{`
	`int i;`
	`for(i=0;i<n;i++)`
		`ar[i] *=mult;//虽未有返回值return,但数组仍然被更新了。` 
 `}` 

## const其它内容

（1）const数组

​	const int days[5] ={31,28,31,30,31};//数组元素的值不能被改变

​	days[2] = 40;//编译器错误

（2）指向const的指针不能用于改变值

​	int days[5] ={31,28,31,30,31};

​	const double *pd = days;//pd指向数组的首元素

​	*pd  = 42;//不允许     指针表示法   表明不能使用pd来更改它所指向的值；

​	pd[2] = 222;//不允许  数组表示法

​	days[2] = 40;//允许

​	(3)把const数据的地址初始化为指向const的指针；

​	const int days[5] ={31,28,31,30,31};

​	const int *p = days;//OK

 **（4）汇总**

​	const int *p;//p可变，p指向的对象(值)不可变  ， 见（2）点

​	int const *p;//p可变，p指向的对象(值)不可变， 见（2）点

​    int  *  const  p;//p不可变，p指向的对象(值)可变

​	const int *const p;//指针p和p指向的对象都不可变

先忽略类型名（编译器解析的时候也是忽略类型名），我们看const离哪个近，“近水楼台先得月”，离谁近就修饰谁。

​	const ~~int~~ *p;       //const修饰 *p,p是指针； *p是指针指向的对象（值），不可变

​	~~int~~ const *p;		//const修饰 *p,p是指针； *p是指针指向的对象（值），不可变

​    ~~int~~  *  const  p;		//const修饰p，p不可变，p指向的对象(值)可变

​	const ~~int~~ *const p;		//前一个const修饰 *p，后一个const修饰p, 指针p和p指向的对象都不可变

### 修饰函数的返回值

const修饰符也可以修饰函数的返回值，返回值不可被改变，例如：

const int Fun(void);

在另一个链接文件中引用const只读变量：

extern const int i;//正确的声明

extern const int j =10;//错误，只读变量的值不能改变

## 指针和多维数组

int zippo[4] [2]; 	//内含int数组的数组

zippo是该数组首元素的地址，zippo的首元素是一个内含两个int值的数组，所以zippo是这个内含两个int值的数组的地址。

（1）因为zippo是数组首元素的地址，所以zippo的值和&zippo的值相同。而zippo[0]本身是一个内含两个整数的数组，所以zippo[0]和值和它首元素（一个整数）的地址（&zippo[0] [0]）相同。总而言之，zippo[0]是一个占用一个int大小对象的地址，而zippo是一个占用两个int大小对象的地址。

（2）给指针或地址加1，其值会增加对应类型大小的数值。zippo和zippo[0]不同，因为zippo指向的对象占用了两个int大小，而zippo[0]指向的对象只占用一个int大小，因此，zippo+1和zippo[0]+1的值不同。

（3）解引用一个指针（在指针前使用*运算符）或在数组名后使用带下标的[]运算符，得到引用对象代表的值。因为zippo[0]是该数组首元素zippo[0] [0]的地址，所以 *（zippo[0]）表示储存在zippo[0] [0]上的值（即一个int类型的值）。 **zippo与 *&zippo[0] [0]等价，地址的地址或指针的指针就是双重间接。

### 指向多维数组的指针

如何声明一个指针变量pz指向一个二维数组（如：zippo）？pz必须指向一个内含两个int类型值的数组，而不是指向一个int类型值，其声明如下：

int (* pz) [2]; 		//pz指向一个内含两个int类型值的数组

为什么要在声明中使用圆括号？因为[]的优先级高于 *。

int * pax[2];			//pax是一个内含两个指针元素的数组，每个元素都指向int的指针

由于[]优先级高，先与pax结合，所以pax成为一个内含两个元素的数组。然后 * 表示pax数组内含两个指针。最后int表示pax数组中的指针都指向int类型的值。因此，这行代码声明了两个指向int的指针。而前面有圆括号的版本，*先于pz结合，因此声明的是一个指向数组（内含两个int类型的值）的指针。

`int main(void)`
`{`
	`int zippo[4][2] = {{2,4},{6,8},{1,3},{5,7}};`
	`int (*pz)[2]; //指向二维数组的指针
	pz = zippo;
	printf("*pz[0] = %d\n",*pz[0]); //2
	printf("*(*(pz+2)+1) = %d\n", *(*(pz+2)+1));` //3
	`return 0;` 	
`}`

### 指针的兼容性

指针之间的赋值比数值类型之间的赋值要严格，例如：数值之间可以直接将int类型的值赋值给double类型的变量，而两个类型的指针不能这样；

int n = 5;  double x; 	int * p1 = &n;	double * pd = &x;	x = n;//隐式类型转换

pd = p1;//编译时错误

### 函数和多维数组

二维数组作为形参，声明函数的形参形式有：

void somefunction(int (*pt)[4]);

或，

void somefunction(int [] [4]);

### 变长数组（VLA）

数组的行数作为函数的形参，而列数却内置在函数体内，数组的维数必须是常量。变长数组必须是自动存储类别，这意味着无论在函数中声明还是作为函数形参声明，都不能使用static或extern存储类别说明符。而且，不能在声明中初始化它们。

注意：变长数组不能改变大小

变长数组中的“变”不是指可以修改已创建数组的大小。一旦创建了变长数组，它的大小则保持不变。这里的“变”指的是：在创建数组时，可以使用变量指定数组的维度。

声明一个带二维变长数组参数的函数，如下：

int sum2d(int rows, int clos, int ar[rows] [cols]);	//ar是一个变长数组（VAL）

注意前两个形参（rows和cols）用作第3个形参二维数组ar的两个维度。因为ar的声明要使用rows和cols，所以在形参列表中必须在声明ar之前先声明这两个形参。

int sum2d(int ar[rows] [cols], int rows, int clos);	//错误

### 复合字面量

(int []) {10, 20}  //复合字面量

因为复合字面量是匿名的，所以不能先创建然后再使用它，必须在创建的同时使用它。

# 字符串和字符串函数

## 1.表示字符串和字符串I/O

puts()和prinf()一样，都属于stdio.h系列的输入/输出函数。但是，与printf()不同的是，puts()函数只显示字符串，而且自动在显示的字符串末尾加上换行符。

### 1.1字符串字面量（字符串常量）

用双括号括起来的内容称为字符串字面量，也叫作字符串常量。如果字符串字面量之间没有间隔，或者用空白字符分隔，C会将其视为串联起来的字符串自字面量。

例如：char greeting[50] = "Hello, and "" how are"  "   you ""  today!";

等价于：char greeting[50] = "Hello, and how are you today!";

如果在字符串内部使用双引号，*必须在双引号前面加上一个反斜杠*（\）:

printf("\”Run ,spot, run! \ " exclaimed Dick. \n");

输出：”Run ,spot, run!"  exclaimed Dick. 

字符串常量属于静态存储类别（static storage class),这说明如果在函数中使用字符串常量，该*<u>字符串只会被储存一次，在整个程序的生命期内存在，即使函数被调用多次</u>*。用双引号括起来的内容被视为指向该字符串储存位置的指针，这类似于把数组名作为指向该数组位置的指针。

printf("%p", *"sapce farers");	//输出结果为:s

 *"sapce farers"表示该字符串所指向地址上储存的值，输出应该是字符串 *”space farers“的首字符/

### 1.2字符串数组和初始

定义字符串数组时，必须让编译器知道需要多少空间。一种方法时用足够空间的数组储存字符串，在下面的声明中，用指定的字符串初始化数组m1:

const char m1[40] = "Limit youself to one line's worth.";

const 表示不会更改这个字符串。

在指定数组大小时，要确保数组的元素个数至少比字符串长度多1（为了容纳空字符）。所有未被使用的元素都被自动初始化为0。

省略数组初始化声明中的大小，编译器会自动计算数组的大小：

const char m2[] = "If you can't think of anything, fake it.";

字符数组名和其他数组名一样，是该数组首元素的地址。因此，假设有下面的初始化：

char car[10] = "Tata";

那么下面的表达式都为真：

car = &car[0],	*car == 'T',	*(car+1) == car[1] == 'a'.

还可以使用指针表示法创建字符串：const char *pt1 = "Something is pointing at me.";

该声明和下面的声明几乎相同：

const char ar1[] = "Something is pointing at me.";

### 1.3数组和指针

数组形式和指针形式有何不同呢？以上面声明为例，数组形式（ar1[]）在计算机的内存中分配为一个内含29个元素带的数组，每个元素被初始化为字符串字面量对应的字符。通常，字符串都作为可执行文件的一部分储存在数据段中。当把程序载入到内存时，也载入了程序中的字符串，字符串储存在静态存储区（static memery）中，但是，程序在开始运行时才会为该数组分配内存。此时，才将字符串拷贝到数组中。注意：此时字符串有两个副本，一个是在静态内存中的字符串字面量，另一个是储存在ar1数组中的字符串。

***在数组形式中，ar1是地址常量***，不能更改ar1，如果改变了ar1，则意味着改变了数组的存储位置（即地址）。可以进行ar1+1这样的操作，标识数组的下一个元素，但是不允许进行++ar1这样的操作，递增运算符只能用于变量名前，不能用于常量。

***指针形式（*pt1）也使得编译器为字符串在静态存储区预留***29个元素的空间。另外，一旦开始执行程序，它会为指针变量留出一个储存位置，并把字符串的地址存储在指针变量中。该变量最初指向该字符串的首字符，但是它的值可以改变。因此，可以使用递增运算符。例如：++pt1将指向第2个字符。

字符串字面量被视为const数据。由于pt1指向这个const数据，所以应该把pt1声明为之指向const数据的指针。这意味着不能用pt1改变它所指向的数据，但仍然可以pt1的值。

总之，初始化数组把静态存储区的字符串拷贝到数组中，而初始化指针只把字符串的地址拷贝给指针。

### 1.4数组和指针的区别

两者的只要区别是：数组名heart是常量，而指针名head是变量。

（1）两者都可以使用数组表示法：

heart[i]; head[i]

（2）两者都能进行指针加法操作：

*(heart + i);  *(head + i)

但是只有指针表示法可以进行递增操作：

*(head++)

### 1.5字符串数组

`int main(void)`
`{`
	`const char *mytalents[LIM] = {`
	`"Adding numbers swiftly",`
	`"Multiplying accurately",`
	`"Stashing data",`
	`"Following instructions to the letter",`
	`"Understanding the C language"`
	`};`
	`char yourtalents[LIM][SLEN] ={`
	`"Walking in a straight line",`
	`"Sleeping",`
	`"Watching television",`
	`"Mailing letters",`
	`"Reading email"`
	`};`
	`int i;`
	`puts("Let's compare talents.");`
	`printf("%-36s %-24s\n", "My talents", "Your talnets");`
	`for(i =0; i < LIM; i++)`
		`printf("%-36s %-24s\n", mytalents[i], yourtalents[i]);`
	`printf("\nsizeof mytalnets: %zd, sizeof yourtalnets: %zd\n",sizeof(mytalents),sizeof(yourtalents));`
	`return 0;` 	
`}`

结果：

`Let's compare talents.`
`My talents                           Your talnets`
`Adding numbers swiftly               Walking in a straight line`
`Multiplying accurately               Sleeping`
`Stashing data                        Watching television`
`Following instructions to the letter Mailing letters`
`Understanding the C language         Reading email`

`sizeof mytalnets: 40, sizeof yourtalnets: 200`

两者都代表5个字符串。使用一个下标时都分别表示一个字符串，如mytalents[0]和yourtalents[0]；使用两个下标时都分别表示一个字符。

但是它们也有区别。mytalents数组是一个内含5个指针的数组，在我们的系统中共占用40字节。而yourtalents是一个内含5个数组的数组，每个数组内含40个char类型的值，共占用200个字节。mytalents中的指针指向初始化时所用的字符串字面量的位置，这些字符串字面量被储存在静态内存中；而yourtalents中的数组则储存着字符串字面量的副本，所以每个字符串都被储存了两次。此外，为字符串数组分配内存的使用率较低，yourtalents中的每个元素的大小必须相同，而且必须是储存最长字符串的大小。

## 2.字符串输入

如果想把一个字符串读入程序，首先必须预留储存该字符串的空间，然后用输入函数获取该字符串。

### 2.1分配空间

要做的第一件事就是分配空间，以储存稍后读入的字符串。这意味着必须要为字符串分配足够的空间。不要指望计算机在读取字符串时顺便计算它的长度，然后再分配空间。

char  *name;

scanf("%s", name);

虽然可能会通过编译，但是在读入name时，name可能会擦写掉程序中的数据或代码，从而导致程序异常中止。因为scanf()要把信息拷贝至擦拭农户指定的地址上，而此时该参数是个未初始化的指针，name可能会指向任何地方。

### 2.2输入函数

(1)gets()

在读取字符串时，scanf()和转换说明%s只能读取一个单词。可是在程序中要读取一整行输入，而不仅仅是一个单词。gets()函数简单以勇，它读取整行输入，直至遇到换行符，然后丢弃换行符，储存其余字符。

gets()唯一参数是words，它无法检查数组是否装得下输入行。gets()函数只知道数组的开始处，并不知道数组中有多少个元素。

如果输入的字符串过长，会导致缓冲区溢出（buffer overflow），即多余的字符超出了指定的目标空间。如果这些多余的字符只是占用了尚未使用的内存，就不会立即出现问题；如果它们擦写掉程序中的其他数据，会导致程序异常中止。

（2）gets()的替代品----->fgets()

fgets()函数通过第2个参数限制读入的字符数来解决溢出的问题。该函数专门设计用于处理文件输入，所以一般情况下可能不大好用。fgets()和gets()的区别如下。

1.fgets()函数的第2个参数指明了读入字符的最大数量。如果该参数的值是n，那么fgets()将读入n-1个字符，或者读到遇到的第一个换行符为止；

2.如果fgets()读到一个换行符，会把它储存在字符串中。这点于gets()不同，gets()会丢弃换行符；

3.fgets()第3个参数指明要读入的文件。

（3）gets_s()函数

gets_s()函数与fgets()类似，用一个参数限制读入的字符数，get_s(words, STLEN);

gets_s()函数与fgets()的区别如下：

1.gets_s()只从标准输入中读取数据，所以不需要第3个参数。

2.如果gets_s()读到换行符，会丢弃它而不是储存它。

3.如果gets_s()读到最大字符都没有读到换行符，会执行以下几步。首先把目标数组中的首字符设置为空字符，读取并丢弃随后的输入直至读到换行符或文件的结尾，然后返回空指针。接着，调用以来实现的“处理函数”，可能会中止或退出程序。

如果输入行太长会怎么样？使用gets()不安全，它会擦写现有数据，存在安全隐患。gets_s()函数很 安全，但是，如果不希望程序中止或退出，就要知道如何编写特殊的“处理函数”。另外，如果打算让程序继续运行，gets_s()会丢弃输入行的其余字符。由此可见，当输入太长，超过数组可容纳的字符数时，fgets()函数最容易使用，而且可以选择不同的处理方式。

## 3.字符串函数

### 3.1strlen()函数

strlen()函数用于统计字符串的长度，下面的函数可以缩短字符串的长度，其中用到了strlen():

`void fit(char *string, unsigned int size)`

`{`

​		`if(strlen(string) > size)`

​				`string[size] = '\0';`

`}`

该函数要改变字符串，所以函数头在声明形式参数string时没有使用const限定符。

### 3.2strcat()函数和strncat()函数

strcat()函数用于拼接字符串，函数接受两个字符串作为参数。该函数把第2个字符串的备份附加在第1个字符串末尾，并把拼接后形成的新字符串作为第1个字符串，第2个字符串不变，strcat()函数的类型是char *(即，指向char的指针)。strcat()函数返回第1个参数，即拼接第2个字符串后的第1个字符串的地址。

strcat()函数无法检查第1个数组是否能容纳第2个字符串。如果分配给第1个数组的空间不够大，多出来的字符溢出到相邻存储单元时就会出问题。

strncat()函数，该函数的第3个参数制定了最大添加字符数。例如：strncat(bugs, addon, 13)将把addon字符串的内容附加给bugs，在加到第13个字符或遇到空白字符时停止。因此，算上空白字符，bugs数组应该足够大，以容纳原始字符串、添加原始字符串在后面的13个字符和末尾的空字符。

### 3.3strcmp()函数和strncmp()

假设要把用户的相应与已存储的字符串作比较，该函数比较的是字符串内容，不是字符串的地址。

`#define SLZE 40`
`#define ANSWER "Grant"`

`char *s_gets(char *st, int n);`

`int main(void)`
`{`
	`char try[SLZE];`
	`puts("Who is buried in Grant's tomb");`
	`s_gets(try, SLZE);`
	`while(strcmp(try, ANSWER)!= 0)`
	`{`
		`puts("No, that's wrong. Try again.");`
		`s_gets(try, SLZE);`
	`}`
	`puts("That's right!");`
	`return 0;` 	
`}`

`char *s_gets(char *st, int n)`
`{`
	`char * ret_val;`
	`int i = 0;`
``	
	ret_val = fgets(st, n, stdin);
	if(ret_val)
	{
		while(st[i] != '\n' && st[i] != '\0')
			i++;
		if (st[i] == '\n')
			st[i] = '\0';
		else
			while(getchar() != '\n')
				continue;
	}
	return ret_val;
`}`

结果：

`Who is buried in Grant's tomb`
`your`
`No, that's wrong. Try again.`
`Grant`
`That's right!`

strncmp()函数比较字符串中的字符，直到发现不同的字符为止，这一过程可能会持续到字符串的末尾。而strncmp()函数在比较两个字符串时，可能比较到字符不同的地方，也可以只比较第3个参数指定的字符数。

### 3.4strcpy()函数和strncpy()函数

如果pt1和pt2都是指向字符串的指针，那么下面的语句拷贝的是字符串的地址而不是字符串本身：

pt2 = pt1;

如果希望拷贝整个字符串，要使用strcpy()函数。

char * str;

strcpy(str, "The C of Tramquility");

strcpy()把“The C of Tramquility”拷贝至str指向的地址上，但是str未被初始化，所以该字符串可能被拷贝到任意的地方！

总之，strcpy()接受两个字符串指针作为参数，可以把指向源字符串的第2个指针声明为指针、数组名或字符串常量；而指向源字符串副本的第1个指针应该指向一个数据对象（如：数组）且该对象有足够的空间储存源字符串的副本。记住，声明数组将分配储存数据的空间，而声明指针只储存一个地址的空间。

strcpy()的其他属性

strcpy()函数还有其他属性。第一，strcpy()的返回类型是char*，该函数返回的是第1个参数的值，即一个字符的地址。第二，第一个参数不必指向数组的开始。这个属性可用于拷贝数组的一部分。

ps = strpcpy(copy + 7, orig);

strcpy()和strcat()都有同样的问题，它们都不能检车目标空间是否能容纳源字符串的副本。拷贝字符串用strncpy()更安全。该函数的第三个参数指明可拷贝的最大字符数。

### 3.5sprintf()函数

sprintf()函数声明在stdio.h中，而不是在string.h中。该函数和printf()类似，但是他是把数据写入到字符串，而不是打印在显示器上。因此，该函数可以把多个元素组合成一个字符串。sprintf()的第一个参数是目标字符串的地址，其余参数和printf()相同，只不过sprintf()把组合后但字符串储存在数组formal中而不是显示在屏幕上。

# 存储类别、链接和内存管理

## 1.存储类别

程序员通过C的内存管理系统指定变量的作用域和生命期，实现对程序的控制。

C提供了多种不同的模型或存储类别（storage class）在内存中储存数据。从硬件方面来看，被储存的每个值都占用一定的物理内存，C语言把这样的一块内存称为对象（object）。对象可以存储一个或多个值。一个对象可能并未储存实际的值，但是它在储存适当的值时一定具有相应的大小（面向对象编程中的对象指的是类对象，其定义包括数据和允许对数据进行的操作，C不是面向对象的编程）。

从软件方面来看，程序需要一种方法访问对象。这可以通过声明变量来完成。

存储期：所谓存储期是指对象在内存中保留了多长时间。标识符用于访问对象，可以用作用域和链接描述标识符，标识符的作用域和链接表明了程序的哪些部分可以使用它。不同的存储类别具有不同的存储器、作用域和链接。

### 1.1作用域

作用域描述程序中可访问标识符的区域，一个C变量的作用域可以是块作用域、函数作用域、函数原型作用域或文件作用域。***块***是用一对花括号括起来的代码区域。例如，整个函数是一个块，函数中的任意复合语句也是一个块。定义在块中的变量具有块作用域（block scope），块作用域变量的可见范围是从定义处到包含该定义的块的末尾。**另外，虽然函数的形式参数声明在函数的左括号之前，但是它们也具有块作用域，属于函数体这个块。**所以到目前为止，我们使用的局部变量（包括函数的形式参数）都具有块的作用域。

#### 1.1.1块作用域

for (int i = 0; i < 10; i++)

​		printf("A  C99 feature : i = %d", i);

i的作用域仅限于for循环。

#### 1.1.2函数作用域

仅限于goto语句的标签，这意味着即使一个标签首次出现在函数的内层块中，它的作用域也延伸至整个函数。

#### 1.1.3函数原型作用域

int mighty(int mouse , double large);

函数原型作用域用于函数原型的形参名（变量名），函数原型作用域的范围是从形参定义处到原型声明结束。这意味着，编译器在处理函数原型中的形参时只关心它的类型，而形参名通常无关紧要。而且，即使有形参名，也不必与函数定义中的形参名相匹配。只有在变长数组中，形参名才有用。

void use_a_VLA(int n, int m, ar[n] [m]);//方括号中必须使用在函数原型中已声明的名称

#### 1.1.4文件作用域

变量的定义在函数的外面，具有文件作用域（file scope）。具有文件作用域的变量，从它的定义处到该定义所在的文件的末尾均可见。

`#include <stdio.h>`

`int units = 0;`

`void  critic(void);`

`int main(void)`

`{`

​		`...`

`}`

`void critic(void)`

`{`

​		`...`

`}`

这里的变量units具有文件作用域，main()和critic()函数都可以使用它（更准确地说，units具有外部链接文件作用域），由于这样的变量可用于多个函数，所以文件作用域变量也称为全局变量。

注意：翻译单元和文件

多个文件在编译器中可能以一个文件出现。例如，通常在源代码中包含一个或多个头文件，头文件会一次包含其它头文件，所以会包含多个单独的物理文件。但是，C预处理器实际上是用包含的头文件内容替换#include指令。所以，编译器源代码文件和所有的头文件都看成是一个包含信息的单独文件。这个文件被称为翻译单元，描述一个具有文件作用域的变量时，它的实际可见范围是整个翻译单元。如果程序由多个源代码文件组成，那么该程序也将由多个翻译单元组成。

### 1.2链接

C变量具有3种链接属性：外部链接、内部链接或无链接。具有块作用域、函数作用域或函数原型作用域的变量都是无链接变量。具有文件作用域的变量可以是外部链接或内部链接。外部链接变量可以用于多文件程序，内部链接变量只能用于一个**翻译单元？？？（编译器源代码文件和它所包含的头文件）。**

内部链接作用域简称为“文件作用域”，把外部链接的文件作用域简称为“全局作用域”或“程序员作用域”。

***如何知道文件作用域变量是内部链接还是外部链接？可以查看外部定义是否使用了存储类别说明符static:***

int giants = 5;	//文件作用域，外部链接

static int dodgers = 3;	//文件作用域，内部链接

### 1.3存储期

作用域和链接描述了标识符的可见性。存储期描述了通过这些标识符访问的对象的生存期，C对象有4种存储期：静态存储期、线程存储期、自动存储期、动态分配存储期。静态存储期在程序执行期间一直存在。

![image-20210213083609796](IMG/%E5%AD%98%E5%82%A8%E6%9C%9F)

具有自动存储期的变量，程序在进入该变量的声明所在块时才为其分配内存，在退出该块时释放之前分配的内存。如果未初始化，自动变量中是垃圾值。程序在编译时为具有静态存储期的变量分配内存，并在程序的运行过程中一直保留这块内存。如果未初始化，这样的变量会被设置为0。

#### 1.4块作用域的静态变量

静态变量（static variable）听起来自相矛盾，像是一个不可变的变量。实际上，静态的意思是该变量在内存中原地不动，并不是说它的值不变。具有文件作用域的变量自动具有静态存储期。这些变量和自动变量一样，具有相同的作用域，但是程序离开它们所在的函数后，这些变量不会消失。计算机在多次函数调用之间会记录它们的值。在块中（提供块作用域和无链接）以存储类别说明符static（提供静态存储期）声明这种变量。

### 1.5外部链接的静态变量

外部链接的静态变量具有文件作用域、外部链接和静态存储期。该类别有时称为外部存储类别（external storage class），属于该类别的变量称为外部变量（external）。当然，为了指出该函数使用了外部变量，可以在函数中用关键字extern再次声明。

extern char Coal；

## 2.分配内存：malloc()和free()

可以在程序运行时分配更多的内存，主要工具是malloc()函数。该函数接受一个参数：所需的内存字节数。malloc()函数会找到合适的空闲内存块，这样的内存是匿名的。也就是说，malloc()分配内存，但是不会为其赋名。然而，它确实返回动态分配内存块的首字节地址。因此，可以把该地址赋给一个指针变量，并使用指针访问这块内存。malloc()函数可用于返回指向数组的指针、指向结构的指针等，所以通常该函数的返回值会被强制转换为匹配的类型。然而，把指向void的指针赋给任意类型的指针完全不用考虑类型匹配的问题。如果malloc()分配内存失败，将返回空指针。

使用malloc()创建一个数组，除了用malloc()在程序运行时请求一块内存，还需要一个指针记录这块内存的位置。

double *ptd;

ptd = (double*)malloc(30 * sizeof(double));

以上代码为30个double类型的值请求内存空间，并设置ptd指向该位置。***注意，指针ptd被声明为指向一个double类型，而不是指向内含30个double类型值的块。***

现在，我们有3种创建数组的方法：

（1）声明数组时，用常量表达式表示数组的维度，用数组名访问数组的元素。可以用静态内存或自动内存创建这种数组。

（2）声明变长数组时，用变量表达式表示数组的维度，用数组名访问数组的元素。具有这种特性的数组只能在自动内存中创建。

（3）声明一个指针，调用malloc()，将其返回值赋给指针，使用指针访问数组的元素，该指针可以是静态的或自动的。

使用第2种和第3种方法可以自动创建动态数组（dynamic  array）。这种数组和普通数组不同，可以在程序运行时选择数组的大小和分配内存。

ptd = (double *)malloc(n * sizeof(double));

通常，malloc()要与free()配套使用。free()函数的参数是之前malloc()返回的地址，该函数释放之前malloc()分配的内存。因此，动态分配内存的存储期从调用malloc()分配内存到调用free()释放内存为止。每次调用malloc()分配内存给程序使用，每次调用free()把内存归还内存池中，这样便可重复使用这些内存。free()的参数应该是一个指针，指向由malloc()分配的一块内存。不能用free()释放通过其他方式（如：声明一个数组。）分配的内存，malloc()和free()的原型都在stdlib.h头文件中。

### 2.1动态内存分配和变长数组

变长数组（VLA）和调用malloc()在功能上有些重合。例如，两者都可用于创建在运行时确定大小的数组。不同的是，变长数组是自动存储类型，***因此，程序在离开变长数组定义所在的块时，变长数组占用的内存空间会被自动释放，***不必使用free()。另一方面，用malloc()创建的数组不必局限在一个函数内访问。例如，可以这样做：被调函数创建一个数组并返回指针，供主调函数访问，然后主调函数在末尾调用free()释放之前被调函数分配的内存。另外，free()所用的指针变量可以与malloc()的指针变量不同，但是两个指针必须储存相同的地址。但是，不能释放同一块内存两次。

对于多维数组而言，使用变长数组更为方便。malloc()也可以创建二维数组，但是语法比较繁琐。如果编译器不支持变长数组特性，就只能固定二维数组的维度。

int n =5;

int m = 6;

int ar2[n] [m];  //	变长数组

int (* p2) [6];		

int (* p3) [m]；//要求支持变长数组

p2 = (int (*)[6])malloc(n * 6 * sizeof(int));

p3 =  (int (*)[m])malloc(n * m * sizeof(int));//n*m数组（要求支持变长数组）

未使用的内存块分散在已使用的内存块之间，使用动态内存通常比使用栈内存慢。

# 文件输入/输出

文件用于储存程序、文档、数据、书信、表格、图形、照片、视频和许多其它种类的信息。

文件通常是在磁盘或固态硬盘上的一段已命名的存储区。

# 结构和其他数据形式

## 1.结构

结构声明描述了一个结构的组织布局。声明类似下面这样：

struct  book{

​		char title[MAXTITL];

​		char author[MAXAUTL];

​		float  value;

};

该声明描述了一个由两个字符数组和一个float类型变量组成的结构，该声明并未创建实际的数据对象，只描述了该对象由什么组成。

struct  book  library;

这把library声明为一个使用book结构布局的结构变量。

在结构声明中，用一对花括号括起来的是结构成员列表。可以把结构声明放在所有函数的外部，也可以放在一个函数定义的内部，如果把结构声明置于一个函数的内部，它的标记就只限于该函数内部使用，如果把结构声明置于函数的外部，那么该声明之后的所有函数都能使用它的标记。

### 1.1定义结构变量

结构有两层含义，一层含义是“结构布局”，结构布局告诉编译器如何表示数据，但是它并未让编译器为数据分配空间。下一步是创建一个结构变量。

struct  book  library;

编译器执行这行代码便创建了一个结构变量library。编译器使用book模板为该变量分配空间。在结构变量的声明中，struct  book 所起的作用相当于一般声明中的int或float，例如，可以定义两个struct  book类型的变量，或者甚至是struct  book类型结构的指针：

struct  book  doyle,  *ptbook;

struct {  / * 无结构标识符 * /

​		char title[MAXTITL];

​		char author[MAXAUTL];

​		float  value;

};

如果打算多次使用结构模板，就要使用带标记的形式，或者使用typedef。

### 1.2访问结构成员

如何访问结构中的成员？使用结构成员运算符-----点（.）访问结构中的成员。.比&的优先级高，因此&library.float 与&（library.float）一样。

结构的初始化器使用点运算和成员名（而不是方括号和下标）标识特定的元素。例如，只初始化book结构的value成员，可以这样做：

struct  book  surprise  =  {.value = 10.99};

可以按照任意顺序使用指定初始化器：

struct  book  gift = {

​		.value = 25.99,

​		.author = "James  Broadfool",

​		.title  =  "Rue for the Toad"

};

与数组类似，在指定初始化器后面的普通初始化器，为指定成员后面的成员提供初始值，另外，对特定成员的最后一次赋值才是它实际获得的值。

struct  book  gift = {

​		.value = 18.90,

​		.author = "James  Broadfool",

​		0.25

};

赋给value的值是0.25，因为它在结构声明中紧跟在author成员之后。新值0.25取代了之前的18.90。

### 1.3声明结构数组

struct  book  library[MAXBKS];

标识结构数组的成员：

library[2].value

library[2],title[4] //数组中library[2]元素的title成员的一个字符

### 1.4嵌套结构

在一个结构中包含另外一个结构（即嵌套结构）很方便。

`int main(void)`
`{`
	`struct guy fellow={`
		`{"Ewen", "Villard"`
		`},`
		`"grilled salmon",`
		`"personality coach",`
		`98112.00`
	`};`
	`printf("Dear %s, \n\n",fellow.handle.first);`
	`printf("%s%s.\n",msgs[0],fellow.handle.first);`
	`printf("%s%s\n",msgs[1],fellow.job);`
	`printf("%s\n",msgs[2]);`
	`printf("%s%s%s",msgs[3],fellow.favfood,msgs[4]);`
	`if (fellow.income > 150000.0)`
		`puts("!!");`
	`else if(fellow.income > 75000.0)`
		`puts("!");`
	`else`
		`puts(".");`	
	`return 0;` 	
`}`

`const char *msgs[5]=`
`{`
	`"Thank you for the wonderful evening,",`
	`"You certainly prove that a",`
	`" is a special kindof guy.We must get together",`
	`"over a delicious",`
	`" and have a few laughs"`
`};`

`struct names`
`{`
	`char first[LEN];`
	`char last[LEN];`
`};`

`struct guy`
`{`
	`struct names handle;`
	`char favfood[LEN];`
	`char job[LEN];`
	`float income;`
`};`

结构的声明，每个成员后面是‘；’，而结构的初始化，每个成员后面是‘，’。如何访问嵌套结构成员，需要使用两次点运算符。

## 2.指向结构的指针

为何要使用指向结构的指针？

（1）就像指向数组的指针比数组本身更容易操控一样，指向结构的指针通常比结构本身更容易操控；

（2）在一些早期的C实现中，结构不能作为参数传递给函数，但是可以传递指向结构的指针；

（3）即使能传递一个结构，传递指针通常更有效率；

（4）一些用于表示数据的结构中包含指向其他结构的指针。

`int main(void)`
`{`
	`struct guy fellow[2]={`
		`{{"Ewen", "Villard"},`
		`"grilled salmon",`
		`"personality coach",`
		`98112.00`
		`},`
		`{{"Rodney", "Swillbelly"},`
		`"tripe",`
		`"tabloid editor",`
		`432400.00`
		`}`
	`};`
	`struct guy *him;  //指向结构的指针
	printf("address #1: %p #2: %p\n", &fellow[0], &fellow[1]);
	him = &fellow[0];  //告诉编译器该指针指向何处
	printf("pointer #1: %p #2: %p\n", him, him+1);
	printf("him->income is $%.2f: (*him).income is $%.2f\n", him->income, (*him).income);`
	`him++;`
	`printf("him->favfood is %s: hime->handle.last is %s\n", him->favfood, him->handle.last);` 
	`return 0;` 	
`}`

结果：

`address #1: 000000000063FD60 #2: 000000000063FDB4`
`pointer #1: 000000000063FD60 #2: 000000000063FDB4`
`him->income is $98112.00: (*him).income is $98112.00`
`him->favfood is tripe: hime->handle.last is Swillbelly`

### 2.1声明和初始化结构指针

struct guy *him;

首先是关键字struct，其次是结构标记guy，然后是一个星号（*），其后跟着指针名。该声明并未创建一个新的结构，但是指针him现在可以指向任意现有的guy类型的结构，例如，如果barney是一个guy类型的结构，可以这样写：

him = &barney;

和数组不同的是，结构名并不是结构的地址，因此要在结构名前面加上&运算符。

在本例中，fellow是一个结构数组，这意味着fellow[0]是一个结构，所以，要让him指向fellow[0]，可以这样写：

him = &fellow[0];

### 2.2用指针访问成员

指针him指向结构变量fellow[0]，如何通过him获得fellow[0]的成员值？

方法1：使用->运算符。

如果him == &barney，那么him->income即是barney.income

如果him == &fellow[0]，那么him->income即是fellow[0].income

换句话说，->运算符后面的结构指针和.运算符后面的结构名工作方式相同（不能写成him.income，因为him不是结构名）。

方法2：如果him == &fellow[0]，那么*him == fellow[0]，因为&和 * 是一对互逆运算符。

fellow[0].income == (*him).income

必须要使用圆括号，因为.运算符比*运算符的优先级高。

## 3.向函数传递结构信息

程序员可以选择是传递结构本身，还是传递指向结构的指针，如果只关心结构中的某一部分，也可以把结构的成员作为参数。

### 3.1传递结构成员

只要结构成员是一个具有单个值的数据类型（即，int及其相关类型、char、float、double或指针），便可把它作为参数传递给接受该特定类型的函数。

### 3.2传递结构的地址

`int main(void)`
`{`
	`struct funds stan = {`
		`"Garlic-Melon Bank",`
		`4032.27,`
		`"Lucky's Savings and Loan",`
		`8543.94`
	`};` 
	`printf("Stan has a total of $.3f.\n", sum(&stan));`
	`return 0;` 	
`}`

`double sum(const struct funds * money)`
`{`
	`return(money->bankfund + money->savefund);`
`}`

结果：

`Stan has a total of $12576.210.`

sum()函数使用指针指向funds结构的指针（money）作为它的擦拭农户。把地址&stan传递给该函数，使得指针money指向结构stan。由于该函数不能改变指针所指向值的内容，所以把money声明为一个指向const的指针。

虽然该函数并未使用其它成员，但是而也可以访问他们。注意，必须使用&运算符来获取结构的地址，和数组名不同，结构名只是其地址的别名。

### 3.3传递结构

`int main(void)`
`{`
	`struct funds stan = {`
		`"Garlic-Melon Bank",`
		`4032.27,`
		`"Lucky's Savings and Loan",`
		`8543.94`
	`};` 
	`printf("Stan has a total of $.3f.\n", sum(&stan));`
	`return 0;` 	
`}`

`double sum(const struct funds moolah)`	//参数是一个结构
`{`
	`return(money->bankfund + money->savefund);`
`}`

结果：

`Stan has a total of $12576.210.`

与传递指针相比，调用sum()时，编译器根据funds模板创建了一个名为moolah的自动结构变量。然后，该结构的各成员被初始化为stan结构变量相应成员的值的副本。

### 3.4其他结构特性

可以把一个结构赋值给另外一个结构，但是数组不能这样做。如果n_data和o_data都是相同类型的结构，可以这样做：

o_data = n_data;

这条语句把n_data的每个成员的值都赋给o_data的相应成员，即使成员是数组，也能完成赋值。另外，还可以把一个结构初始化为相同类型的另一个结构：

struct names right_field = {"Ruthie", "George"};

struct names captain = right_field;	//把一个结构初始化为另一个结构

**函数不仅能把结构本身作为参数传递，还能把结构作为返回值返回。把结构作为函数参数可以把结构的信息传递给函数；把结构作为返回值的函数能把结构的信息从被掉函数传回主调函数。结构指针也允许这种双向通信，因此可以选择任一种方法来解决编程问题。**

`struct namect{`
	`char fname[NLEN];`
	`char lname[NLEN];`
	`int letters;`
`};`
`void getinfo(struct namect *);`
`void makeinfo(struct namect *);`
`void showinfo(const struct namect *);`
`int main(void)`
`{`
	`struct namect person;`
	`getinfo(&person);`
	`makeinfo(&person);`
	`showinfo(&person);`
	`return 0;` 	
`}`

`void getinfo(struct namect *pst)`
`{`
	`printf("Please enter your first name.\n");`
	`s_gets(pst->fname, NLEN);`
	`printf("Please enter your last name.\n");`
	`s_gets(pst->lname, NLEN);`
`}`

`void makeinfo(struct namect * pst)`
`{`
	`pst->letters = strlen(pst->fname)+strlen(pst->lname);`
`}`

`void showinfo(const struct namect * pst)`
`{`
	`printf("%s%s, your name contains %d letters.\n", pst->fname, pst->lname, pst->letters);`
`}`

`char *s_gets(char *st, int n)`
`{`
	`char * ret_val;`
	`char *find;`	

	ret_val = fgets(st, n, stdin);
	if(ret_val)
	{
		find = strchr(st,'\n');
		if(find)
			*find = '\0';
		else
			while(getchar()!= '\n')
				continue;
	}
	return ret_val;
`}`

结果：

Please enter your first name.
liu
Please enter your last name.
jihong
liujihong, your name contains 9 letters.

### 3.5结构和结构指针的选择

假设要编写一个与结构相关的函数，是用结构指针作为参数还是用结构作为参数和返回值？

把指针作为参数有两个优点：执行起来很快，只需要传递一个地址，缺点是无法保护数据。被调函数中的某些操作可能会意外影响原来结构中的数据。

把结构作为参数传递的优点是：函数处理的使原始的数据的副本，这保护了原始数据。另外，diamagnetic风格也更清除。缺点是：传递结构浪费时间和存储空间。尤其是把大型结构传递给函数，而它只使用结构中的一两个成员时特别浪费时间，这种情况下传递指针或只传递函数所需的成员更合理。

### 3.6结构中的字符数组和字符指针

#define LEN 20

struct  names{

​		char first[LEN];

​		char last[LEN];

};

struct  pnames{

​		char *first;

​		char *last;

};

struct names veep = {"Talia", "Summers"};

struct pnames treas = {"Brad", "Fallingjaw"};

以上代码均没有问题，也能正常运行，但是思考以下字符串被储存在何处。对于struct  names类型的结构变量veep，以上字符串储存在结构内部，结构总共要分配40字节储存型名。然而，对于struct  pnames类型的结构变量treas，以上字符串储存在编译器储存常量的地方。结构本身只储存了两个地址。struct pname结构不用为字符串分配任何存储空间。它使用的是储存在别处的字符串。简而言之，pnames结构变量中指针应该只用来在程序中管理哪些已分配和在别处分配的字符串。

struct  pnames  attorney;

scanf("%s", attorney.last); 	//未初始化的变量，可能导致程序崩溃

### 3.7结构、指针和malloc()

***如果使用malloc()分配内存并使用指针储存该地址，那么在结构中使用指针处理字符串就比较合理。这种方法的优点是，可以请求malloc()为字符串分配合适的存储空间。***

用指针代替数组

`struct namect{`
	`char *fname;`
	`char *lname;`
	`int letters;`
`};`

调用malloc()函数分配存储空间，并把字符串拷贝到新分配的存储空间中。

`void getinfo(struct namect *pst)`
`{`
	`char temp[SLEN];`
	`printf("Please enter your first name.\n");`
	`s_gets(temp,SLEN);`
	`//分配内存以储存名`
	`pst->fname = (char *)malloc(strlen(temp)+1);`
	`//把名拷贝到动态分配的内存中`
	`strcpy(pst->fname,temp);`
	`printf("Please enter your last name.\n");`
	`s_gets(temp,SLEN);`
	`pst->lname = (char *)malloc(strlen(temp)+1);`
	`strcpy(pst->lname,temp);`
`}`

***要理解这两个字符串都未存储在结构中，它们储存在malloc()分配的内存块中。然而，结构中储存着这两个字符串的地址，处理字符串的函数通常都要使用字符串的地址。***

代码：

`int main(void)`

`{`
	`struct namect person;`
	`getinfo(&person);`
	`makeinfo(&person);`
	`showinfo(&person);`
	`cleanup(&person);`
``	

	return 0; 	
`}`

`void getinfo(struct namect *pst)`
`{`
	`char temp[SLEN];`
	`printf("Please enter your first name.\n");`
	`s_gets(temp,SLEN);`
	`//分配内存以储存名`
	`pst->fname = (char *)malloc(strlen(temp)+1);`
	`//把名拷贝到动态分配的内存中`
	`strcpy(pst->fname,temp);`
	`printf("Please enter your last name.\n");`
	`s_gets(temp,SLEN);`
	`pst->lname = (char *)malloc(strlen(temp)+1);`
	`strcpy(pst->lname,temp);`
`}`

`void makeinfo(struct namect * pst)`
`{`
	`pst->letters = strlen(pst->fname)+strlen(pst->lname);`
`}`


`void showinfo(const struct namect * pst)`
`{`
	`printf("%s%s, your name contains %d letters.\n", pst->fname, pst->lname, pst->letters);`
`}`

`void cleanup(struct namect * pst)`
`{`
	`free(pst->fname);`
	`free(pst->lname);`
`}`
`double sum(const struct funds * money)`
`{`
	`return(money->bankfund + money->savefund);`
`}`

`char *s_gets(char *st, int n)`
`{`
	`char * ret_val;`
	`char *find;`
``	
	ret_val = fgets(st, n, stdin);
	if(ret_val)
	{
		find = strchr(st,'\n');
		if(find)
			*find = '\0';
		else
			while(getchar()!= '\n')
				continue;
	}
	return ret_val;
`}`

### 3.8复合字面量和结构

如果只需要一个临时结构值，复合字面量很好用。可以使用复合字面量创建一个数组作为函数的参数或赋值给另一个结构。如下：

（struct book){"The Idiot", "Fyodor Dostoyevsky", 6.99}

复合字面量在所有函数的外部，具有静态存存储期；如果复合字面量在块中，则具有自动存储期。复合字面量金额普通初始化列表的语法规则相同。

### 3.9伸缩型数组成员

伸缩型数组：第1个特性是，该数组不会立即存在；第2个特性是，使用这个伸缩型数组成员可以编写合适的代码，就好像它确实存在并具有所需数目的元素一样。

首先，声明一个伸缩型数组成员有如下规则：

（1）伸缩型数组成员必须是结构的最后的一个成员；

（2）结构中必须至少有一个成员；

（3）伸缩数组的声明类似于普通数组，只是它的方括号中是空的。

struct  flex

{

​		int count;

​		double average;

​		double scores[];		//伸缩型数组成员

}

声明一个struct flex类型的结构变量时，不能用scores做任何事，因为没有给这个数组预留存储空间。C99的意图并不是让声明struct flex类型的变量，而是希望你声明一个指向struct  flex类型的指针，然后用malloc()来分配足够的空间，以存储struct  flex类型结构的常规内容和伸缩型数组成员所需的额外空间。

struct flex *pf;	//声明一个指针

//请求未一个结构和一个数组分配存储空间

pf = malloc(sizeof(struct flex)+5*sizeof(double));

现在又足够的存储空间储存count 、average和一个内含5个double类型值的数组。可以使用指针访问这些成员：

pf->count = 5;

pf->scores[2] = 18.5;

带伸缩型数组成员的结构确实有一些特殊的处理要求。第一，不能用结构进行赋值或拷贝：

struct flex *pf1, *pf2;

*pf2 = *pf1;	//不要这样做

这样只能拷贝除伸缩型数组成员以外的其它成员，确实要拷贝，应使用memcpy()函数。

第二，不要以按值的方式把这种结构传递给结构。原因相同，按值传递一个参数于赋值类似。要把结构的地址传递给函数。

第三，不要使用带伸缩型数组成员的结构作为数组成员或另一个结构的成员。

### 3.10使用结构数组的函数

`int main(void)`
`{`
	`struct funds jones[N] =` 
	`{`
		`{`
			`"Garlic-Melon Bank",`
			`4032.27,`
			`"Lucky's Savings and Loan",`
			`8543.94`
		`},`
		`{`
			`"Honest Jack's Bank",`
			`3620.88,`
			`"Party Time Savings",`
			`3802.91`	
		`}` 
	`};`
	`printf("The Joneses have a total of $%.2f.\n", sum(jones, N));`
``	

	return 0; 	

`}`

`double sum(const struct funds money[], int n)`
`{`
	`double total;`
	`int i;`
	`for(i = 0, total = 0; i < n; i++)`
		`{`
			`total += money[i].bankfund + money[i].savefund;`
		`}`
	`return (total);`
`}`

结果：

The Joneses have a total of $20000.00.

数组名jones是该数组的地址，即该数组首元素的地址。因此，指针money的初始值相当于通过下面的表达式获得：

money = &jones[0];

下面是几个要点：

（1）可以把数组名作为数组中第1个结构的地址传递给函数；

（2）然后可以**用数组表示法访问数组中**的其它结构。注意下面的函数调用于使用数组名效果相同：

sum(&jones[0], N)

因jones和&jones[0]的地址相同，使用数组名是传递结构地址的一种间接的方法。

（3）由于sum()函数不能改变原始数据，所以该函数使用了限定符const。

## 4.把结构内容保存到文件中

由于结构可以储存不同类型的信息，所以它是构建数据库的重要工具。储存在一个结构中的整套信息被称为记录，单独的项被称为字段。

`int main(void)`
`{`
	`struct book library[MAXBKS];	//结构数组` 
	`int count = 0;`
	`int index, filecount;`
	`FILE *pbooks;`
	`int size = sizeof(struct book);`
	`if ((pbooks = fopen("book.txt", "a+")) == NULL)`
	`{`
		`fputs("Can't open book.txt file\n", stderr);`
		`exit(1);`
	`}`
	`rewind(pbooks);	//定位到文件开始`
	`while(count < MAXBKS && fread(&library[count],size,1,pbooks) ==1)` 
	`{`
		`if (count == 0)`
			`puts("Current contents of book.txt:");`
		`printf("%s by %s: $.2f\n", library[count].title, library[count].author, library[count].value);`
		`count++;`
	`}`
	`filecount = count;`
	`if(count == MAXBKS)`
	`{`
		`fputs("The book file is full.", stderr);`
		`exit(2);`
	`}`
	`puts("Please add new book titles.");`
	`puts("Press enter at the start of a line to stop.");`
	`while(count < MAXBKS && s_gets(library[count].title, MAXTITL)!= NULL && library[count].title[0] !='\0')`
	`{`
		`puts("Now enter the author.");`
		`s_gets(library[count].author, MAXAUTL);`
		`puts("Now enter the value.");`
		`scanf("%f", &library[count++].value);`
		`while(getchar() != '\n')`
			`continue;`
		`if(count < MAXBKS)`
			`puts("Enter the next title.");`
	`}`
	`if(count > 0)`
	`{`
		`puts("Here is the list of your books:");`
		`for(index = 0; index < count; index++)`
			`fprintf(pbooks, "%s by %s: $%.2f\n", library[index].title, library[index].author, library[index].value);`//文本文件
`//		fwrite(pbooks, "%s, ", &library[filecount], size, count - filecount, pbooks);`二进制文件
	`}`
	`else`
		`puts("No books?Too bad.\n");`
	`puts("Bye.\n");`
	`fclose(pbooks);`
	`return 0;` 	
`}`

## 5.联合简介

联合（union）是一种数据类型，它能在同一个内存空间中储存不同的数据类型（不是同时储存）。

创建联合和创建结构的方式相同，需要一个联合模板和联合变量。可以用一个步骤定义联合，也可以用联合标记分两步定义。下面是一个带标记的联合模板：

union hold{

​		int digit;

​		double bigf1;

​		char letter;

};

然而，声明的联合只能储存一个int类型的值或一个double类型的值或char类型的值。

union hold fit;

union hold save[10];

union hold *pu;

第1个声明创建了一个单独的联合变量fit。编译器分配足够的空间以便它能储存联合声明中占用最大字节的类型。本例中，占用空间最大的是double类型的数据。第2个声明创建了一个数组save，内含10个元素，每个元素都是8字节。第3个声明创建了一个指针，该指针变量储存hold类型联合变量的地址。

可以初始化联合，需要注意，联合只能储存一个值，这与结构不同。

联合的用法，在结构中储存与其成员有从属关系的信息。例如，假设用一个结构表示一辆汽车，如果汽车属于驾驶者，就要用一个结构成员来描述这个所有者。入宫汽车被租赁，那么需要一个成员来描述其租赁公司。

`struct owner{`

​		`char socsecurity[12];`

​		`....`

`};`

`struct leasecompany{`

​		`char name[40];`

​		`char headquarters[40];`

​		`....`

`};`

`union data{`

​		`struct ower owncar;`

​		`struct leasecompany leasecar;`

`};`

`struct car_data{`

​		`char make[15];`

​		`int status;	//私有为0，租赁为1`

​		`union data ownerinfo;`

`}；`

假设flits是car_data类型的结构变量，如果flits.status为0，程序将使用flits.ownerinfo.owncar.socsecurity，如果lits.status为1，程序则使用flits.ownerinfo.leasecar.name。

## 6.枚举类型

可以用枚举类型（enumerated type）声明符号名称来表示整型常量。

enum spectrum {red, orange, yellow, green, blue, violet};

enum spectrum color;

第1个声明创建了spetrum作为标记名，第2个声明使color作为该类型的变量。第1个声明中花括号内的标识符没聚了spectrum变量可能有的值。因此，color可能的值是red、orange、yellow等，这些符号常量被称为枚举符。

### 6.1enum常量

red = 0， orange = 1

red称为一个有名称的常量，代表整数0。类似地，其他标识符都是有名称的常量，分别代表1~5。只要是能使用整型常量的地方就可以使用枚举常量。例如，在声明数组时，可以用枚举常量表示数组的大小；在switch语句中，可以把枚举常量作为标签。

### 6.2默认值

默认情况下，枚举列表中的常量都被赋予0、1、2等。因此，下面的声明中nina的值时3：

enum kids {nippy, slats, skippy, nina, liz};

### 6.3赋值

在枚举声明中，可以为枚举常量指定整数值：

enum level {low = 100, medium = 500, high = 2000};

如果只给一个枚举常量赋值，没有对后面的枚举常量赋值，那么后面的常量会被赋予后续的值。例如，假设有如下的声明：

enum feline {cat, lynx = 10, puma ,tiger};

那么cat 的是0（默认），lynx、puma和tiger的值分别是10，11，12。

## 7.typedef简介

typedef工具是一个高级数据特性，利用typedef可以为某一类型自定义名称。这方面与define类似，但是两者有3处不同：

（1）与#define不同，typedef创建的符号名只受限于类型，不能用于值；

（2）typedef由编译器解释，不是预处理器。

（3）在其受限范围内，typedef比#define更灵活。

typedef unsigned char BYTE;

BYTE x, y[10], *z;

该定义的作用域取决于typedef定义所在的位置。如果定义在函数中，就具有局部作用域，受限于定于所在的函数。如果定义在函数的外面，就具有文件作用域。

用typedef来命名一个结构类型时，可以省略该结构的标签：

typedef struct {double x; double y;} rect;

假设这样使用typedef定义的类型名：

rect r1 = {3.0, 6.0};

rect r2;

r2 = r1；

这两个结构在声明时都没有标记，他们的成员完全相同，C认为这两个结构的类型相同，所以r1和r2间的赋值是有效操作。

使用typedef的第2个原因：typedef常用于给复杂的类型命名。例如：

typedef char (*FRPTC())[5];

把FRPTC声明为一个函数类型，该函数返回一个指针，该指针指向内含5个char类型元素的数组。

## 8.其它声明

理解*、[]和()的优先级：

1.数组名后面的[]和函数名后面的()具有相同的优先级，它们比*（解引用运算符）的优先级高，因此下面的声明risk是一个指针数组，不是指向数组的指针：

int *risks[10]; //声明一个内含10个元素的数组，每个元素都是一个指向int的指针

2.[]和()的优先级相同，由于都是从左到右结合，所以下面的声明中，在应用方括号之前，*先与rusks结合。因此，rusks是一个指向数组的指针，该数组内含10个int类型的元素：

int (*rusks)[10];//声明一个指向数组的指针，该数组内含10个int类型的值

3.[]和()都是从左到右结合。因此下面声明的goods是一个由12个内含50个int类型值的数组组成的二维数组，不是一个有50个内含12个int类型值的数组组成的二维数组：

int goods[12] [50];

把以上的规则用于下面的声明：

int *oof[3] [4];//声明一个3 *4的二维数组，该数组的每个元素都是指向int的指针

[3]比*优先级高，由于从左到右结合，所以[3]先与oof结合。因此，oof首先是一个内含3个元素的数组，然后再与[4]结合，所以oof的每个元素都是内含4个元素的数组。 *说明这些元素都是指针。最后，int表明这4个元素都是指向int的指针。简而言之，oof是一个3 * 4的二维数组，每个元素都是指向int的指针。编译器要为12个指针预留存储空间。

int (*uuf)[3] [4];//声明一个指向3 * 4二维数组的指针，该数组中内含int类型的值

圆括号使得*先与uuf结合，说明uuf是一个指针，所以uuf是一个指向3 * 4 的int类型二维数组的指针。编译器要为一个指针预留存储空间。

int (*uof[3])[4];//声明一个内含3个指针元素的数组，其中每个指针都指向一个内含4个int类型元素的数组

char * fump(int);	//指针函数本质是一个函数，其返回值为指针。

char (*frump)(int);	//函数指针本质是一个指针，其指向一个函数。

char (*flump[3])(int);	//内含3个指针的数组，每个指针指向返回类型为char的函数

typedef int arr5[5];

typedef arr5 * p_arr5;

typedef p_arr5 arrp10[10];

arr5 togs;	//togs是一个内含5个int类型值的数组

p_arr5 p2;	//p2是一个指向数组的指针，该数组内含5个int类型的值

arrp10 ap;	//ap是一个内含10个指针的数组，每个指针都指向一个内含5个int类型值的数组







































