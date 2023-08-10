# c-p79-C-4-
C语言学习笔记 p79C语言预处理（4）
#include(stdio.h>
int mian()
{
      int a=10;
      int b=a+1;//1
      int b=++a;//2 给b赋11时，a也是11
      return 0;
}


宏的副作用
宏的参数在第一次用完可能会对后面的程序有影响
#define MAX(X,Y) ((X)>(Y)?(X):(Y))//结果为真则输出X，结果为假则输出Y
//带有副作用的宏参数使用起来一定要小心，尽量避免使用
// 注：宏的参数不是算好替换进去的，而是直接替换进去的
int main()
{
      int a=10;
      int b=11;
      int max=MAX(a++,b++);
      //int max=((a++)>(b++)?(a++):(b++));
      
      printf("%d\n",max);//12
      printf("%d\n",a);//11
      printf("%d\n",b);//13
      return 0;
}



//函数
int Max(int x,int y)
{
      return (x>y?x:y);
}
//宏
#define MAX(X,Y) ((X)>(Y)?(X):(Y))

int main()
{
      int a=10;
      int b=20;
      int max=MAX(a,b);
      printf("max=%d\n",max);
      max=MAX(a,b);
      printf("max=%d\n",max);
      return 0;
}
1.函数得调用和返回都有开销，效率可能较低，而宏没有，宏在预处理阶段就完成了替换
2.宏没有类型

宏相对于函数的劣势
1。一份宏定义的代码插入到程序中。除非宏比较短，否则可能大幅度增加1程序的长度
2.宏没法调试，宏在预处理阶段就不是宏了，调试出来的代码和看到的代码不是一个代码
3.宏与类型无关所以不够严谨
4.宏可能会带来运算符优先级的问题，导致程序容易出错


#define SIZEOF(type) sizeof(type)
int main()
{
      int ret=SIZEOF(int);
      printf("%d\n",ret);
      return 0;
}


#define MALLOC(num,type) (type*)malloc(num*sizeof(type))
int main()
{
      int p=(int*)malloc(10*sizeof(int));
      
      int * p=MALLOC(10,int);
      return 0;
}


函数与宏的对比
1.函数长度：函数代码在那里，要用去访问就可以了，不会增加代码长度
2.宏执行速度更快
3.宏有操作符优先级问题，建议写宏多写括号
4.宏有带有副作用的参数更可能会影响代码，而函数只在传参时求值一次，结果容易控制
5.宏与参数类型无关
6.宏不方便调试，宏在调试的时候已经不是宏了
7.宏不能递归



命名约定：
一般来说，宏和函数用法很相似，所以宏一般都用大写，函数都用小写

#undef:
用于移除一个宏指令
#deine MAX 100
int main()
{
      printf("MAX=%d\n",MAX);
      #undef MAX
      printf("MAX=%d\n",MAX);//这里会把未标识的警告
      return 0;
}

