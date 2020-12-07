# lab12

    本节目标：
     1. 理解指针的基础知识 
     2. 理解局部变量和全局变量的概念与使用
 
## 获取及提交lab

获取：通过 https://github.com/C-FUDAN-2020/lab12 获取。

提交物：将你完成源代码文件作为 lab12 的提交物。

提交：将提交物文档命名为学号_姓名 （如20302010000_王明），提交至超星学习通对应的作业中。

截止时间：北京时间 2020年12月13日 23:59:59

#### 指针是C的灵魂，没有学会指针就相当于没有学过C！
#### 指针是C的灵魂，没有学会指针就相当于没有学过C！
#### 指针是C的灵魂，没有学会指针就相当于没有学过C！
#### （重要的事情说3遍，提醒自己，好好学习，思考）

    指针为什么重要？
    （1）.快速的传递数据，减少内存的使用
    （2）.可以使函数返回一个以上的值
    （3）.可以直接访问物理硬件
    （4）.可以方便的处理字符串
    （5）.是理解面向对象语言中"引用"功能的基础
    （6）.可以表示一些复杂的数据结构

### 1、指针的定义

指针就是一个变量，用来存放地址的变量，利用它可以找到该地址位置的内存单元。

`指针 & 指针变量是不同的`

e.g:普通变量a的地址是1000H，可以称a的指针是1000H 但是绝对不能说a的指针变量是1000H。指针是一个操作受限的非负整数：比如2个地址相乘是没有意的 故不能做乘法操作，所以说指针是受限的。

### 2、指针变量的声明

    int *a; ///定义了一个整形的指针变量a
    char *b;///定义了一个字符型指针变量b
    int *c,d;///不会报错，但是相当于定义了一个整型的指针变量c和整型变量d


### 3、指针运算符

*号代表取值运算符，后边跟着的一定是一个指针型的变量。&号代表取地址运算符，后边跟着的一定是一个数值型的变量（此处的数值类型取决于你定义的数据类型）。

    int a=10,b=20;///定义a，b两个整形变量数值分别为10,20
    int * pa,* pb;  ///定义两个整型的指针变量pa，pb
    pa = &a;pb = &b;
    /**关于取地址运算符的应用，我们取a这个整型变量的地址，赋给pa，
    同理取b这个整型变量的地址，赋给pb，
    现在pa对应的就是a这个值的门牌号*/
    printf("%d\n",* pa + * pb);
    /**关于取值运算符的应用，我们取pa这个地址存的值10（原来a的值）
    加上pb这个地址存的值20（原来b的值），输出30;
    */
    
关于跟指针有关的相关运算，切记等号左右两边数据类型一定要保持一致，即左边是指针右边必是指针，左边是数值，右边必是数值；比如 int * pa;int a; 我定义了pa这个指针以及a这个数值。

在运算中，pa 代表地址，a代表数值，* pa代表数值，&a代表地址，&pa，* a以及等号两边类型不同均会报错。

### 4、指针与数组

要理解数组与指针的关系，就首先要理解数组在在内存中储存方式，数组是顺序储存结构，就相当于对于a[10]这个数组，a[0]的地址(门牌号)为100，那么a[1]的门牌号就是101，a[2]就是102，以此类推。

那么我们理解了数组的储存方式，就可以看看数组跟指针有什么关系；

我们可以定义一个int型的* a，此时，a代表的是a[0]在内存中的地址，* a就表示a[0]的值。由顺序结构可知 a+1 为a[1]的地址，则* (a+1)表示a[1]的值，以此类推。

        int *a; ///定义了一个整型的指针变量，可看做a数组第一个值的地址，即a[0]的地址
        for(int i=0;i<10;i++)
        {
        *(a+i) = i;
           /**目的，将a[0]~a[9]分别赋值为0~9；
              数组的每个地址就相当于a+i，赋值就要用取值运算符对改地址存的值进行改变；
              即 *(a+i) = i;*/
        }
        for(int i=0;i<10;i++)
        {
        printf("%d\n",a[i]);
          /同样可以用a[i]的形式操作数组；
        }
### 5、指针与字符串

用字符数组指向字符串和用字符指针指向的字符串的区别

如：char  * str="OK"; 与 char a[]="OK";

* str 是指针变量，可多次赋值；a是指向数组的变量，数组大小固定。

* 类型、大小不同。str 是指针，a 是数组。
           
* a 的元素可重新赋值，不能通过 str 间接修改字符串常量的值。


在助教给出的生命游戏的PJ中有这样一段函数代码，请同学们思考，对比字符数组和字符指针的区别，代码中的字符数组char buff[BUFFLEN]是否可任意用字符指针替代呢？下面的代码要保证正常运行应该做何修改呢？

           
           Grid on_run(Grid grid)
        {
           Grid current = grid;
           char buff[BUFFLEN];
           while (true) 
         {
            usleep(200000);
            system("clear");
            printf("输入回车键暂停游戏\n");
            current = on_gerenate(current);
            if (_kbhit())
           {
            // 获取回车键返回的值（无效值，需要舍弃）
            fgets(buff, BUFFLEN, stdin);
            printf("输入 '%s' 停止生命游戏\nrun%s", EXIT, INPUT_HEAD);
            // 清空缓冲区
            fflush(stdin);
            fgets(buff, BUFFLEN, stdin);
            system("clear");
            if (strncmp(buff, EXIT, strlen(EXIT)) == 0)
              {
                break;
              }
           }
         }
         return current;
        }


*经典的例子加深对指针的理解：互换2个数字(之前使用的是普通变量，现在使用指针&函数)*

    #include <stdio.h>

    void swap(int p,int q)
    {
      int t;
      t = p;
      p = q;
      q = t;
      return;
    }//swap 不能完成互换，只是互换了形参的值 主函数中的实参值并未互换 

    void swap1(int *p,int *q)
    {
      int *t;
      t = p;
      p = q;
       q = t;
     }//swap1 不能完成 a b的值互换，只是互换指针变量 

    void swap2(int *p,int *q)
    {
      int t;
      t = *p;//*p =a ,*q=b
      *p = *q;
      *q = t;
     }//swap2 互换成功 

    int main(void)
    {
      int a,b;
      a = 5;
      b = 9;
      swap(a,b);
      printf("a = %d,b = %d\n",a,b);
      swap1(&a,&b);
      printf("a = %d,b = %d\n",a,b);
      swap2(&a,&b);
      printf("a = %d,b = %d\n",a,b);
      return 0;
    }

 输出结果：
 
 a = 5,b = 9 
 
 a = 5,b = 9 
 
 a = 9,b = 5 

 *总结：思考：printf 为什么不能放在被调函数中？
 题目的要求是：互换a b的值，而非被调函数的值互换。*

 *测试结果：*
 
 *1.swap只是被调函数的形参值互换了，主函数中的实盘并没有互换。*
 
 *2.swap1只是互换a b地址的存储位置，并没有互换a b地址中的值。*
 
 *3.swap2为什么会成功？原因很简单哦。swap2的功能是把a b地址中的值互换了。简单说：a b是被划分出来的2个静态地址。5，9是存放在地址中的值。swap2功能是把2个地址中的5 9互换，一旦地址中的值达到互换，即a b的值完成了互换。*[1]




#### 编写一个函数（参数用指针）将一个3×3矩阵转置。
        
### 6、局部变量与全局变量

定义在函数内部的变量称为局部变量（Local Variable），它的作用域仅限于函数内部， 离开该函数后就是无效的，再使用就会报错。例如：

    int f1(int a)
    {
      int b,c;  //a,b,c仅在函数f1()内有效
      return a+b+c;
    }
    int main()
    {
      int m,n;  //m,n仅在函数main()内有效
    return 0;
    }
    
*几点说明：*

*1) 在 main 函数中定义的变量也是局部变量，只能在 main 函数中使用；同时，main 函数中也不能使用其它函数中定义的变量。main 函数也是一个函数，与其它函数地位平等。*

*2) 形参变量、在函数体内定义的变量都是局部变量。实参给形参传值的过程也就是给局部变量赋值的过程。*

*3) 可以在不同的函数中使用相同的变量名，它们表示不同的数据，分配不同的内存，互不干扰，也不会发生混淆。*

*4) 在语句块中也可定义变量，它的作用域只限于当前语句块。*[2]

在所有函数外部定义的变量称为全局变量（Global Variable），它的作用域默认是整个程序，也就是所有的源文件，包括 .c 和 .h 文件。例如：

    int a, b;  //全局变量
    void func1()
    {
          //TODO:
     }
    float x,y;  //全局变量
    int func2(){
          //TODO:
     }
    int main(){
         //TODO:
      return 0;
     }
a、b、x、y 都是在函数外部定义的全局变量。C语言代码是从前往后依次执行的，由于 x、y 定义在函数 func1() 之后，所以在 func1() 内无效；而 a、b 定义在源程序的开头，所以在 func1()、func2() 和 main() 内都有效。

局部变量和全局变量的综合示例

【示例1】输出变量的值：
        
    #include <stdio.h>
    int n = 10;  //全局变量
    void func1()
    {
     int n = 20;  //局部变量
     printf("func1 n: %d\n", n);
    }
     void func2(int n)
     {
     printf("func2 n: %d\n", n);
    }
    void func3(){
    printf("func3 n: %d\n", n);
    }
    int main()
    {
      int n = 30;  //局部变量
      func1();
      func2(n);
      func3();
      //代码块由{}包围
     {
        int n = 40;  //局部变量
        printf("block n: %d\n", n);
      }
      printf("main n: %d\n", n);
      return 0;
     }

运行结果：

func1 n: 20

func2 n: 30

func3 n: 10

block n: 40

main n: 30

*代码中虽然定义了多个同名变量 n，但它们的作用域不同，在内存中的位置（地址）也不同，所以是相互独立的变量，互不影响，不会产生重复定义（Redefinition）错误。*

*1) 对于 func1()，输出结果为 20，显然使用的是函数内部的 n，而不是外部的 n；func2() 也是相同的情况。当全局变量和局部变量同名时，在局部范围内全局变量被“屏蔽”，不再起作用。或者说，变量的使用遵循就近原则，如果在当前作用域中存在同名变量，就不会向更大的作用域中去寻找变量。*

*2) func3() 输出 10，使用的是全局变量，因为在 func3() 函数中不存在局部变量 n，所以编译器只能到函数外部，也就是全局作用域中去寻找变量 n。*

*3) 由{ }包围的代码块也拥有独立的作用域，printf() 使用它自己内部的变量 n，输出 40。*

*4) C语言规定，只能从小的作用域向大的作用域中去寻找变量，而不能反过来，使用更小的作用域中的变量。对于 main() 函数，即使代码块中的 n 离输出语句更近，但它仍然会使用 main() 函数开头定义的 n，所以输出结果是 30。*[2]

【示例2】根据长方体的长宽高求它的体积以及三个面的面积。
     
    #include <stdio.h>
    int s1, s2, s3;  //面积
    int vs(int a, int b, int c)
    {
       int v;  //体积
       v = a * b * c;
       s1 = a * b;
       s2 = b * c;
       s3 = a * c;
       return v;
    }
    int main(){
      int v, length, width, height;
      printf("Input length, width and height: ");
      scanf("%d %d %d", &length, &width, &height);
      v = vs(length, width, height);
      printf("v=%d, s1=%d, s2=%d, s3=%d\n", v, s1, s2, s3);
      return 0;
    }
   
运行结果：

Input length, width and height: 10 20 30↙

v=6000, s1=200, s2=600, s3=300

根据题意，我们希望借助一个函数得到三个值：体积 v 以及三个面的面积 s1、s2、s3。遗憾的是，C语言中的函数只能有一个返回值，我们只能将其中的一份数据，也就是体积 v 放到返回值中，而将面积 s1、s2、s3 设置为全局变量。全局变量的作用域是整个程序，在函数 vs() 中修改 s1、s2、s3 的值，能够影响到包括 main() 在内的其它函数。


### 7、相关链接
[1][https://blog.csdn.net/weixin_33755847/article/details/91669585](https://blog.csdn.net/weixin_33755847/article/details/91669585)

[2][https://blog.csdn.net/weixin_30871905/article/details/98729009](https://blog.csdn.net/weixin_30871905/article/details/98729009)

