# 容器
## 容器基本功能与分类
### 一、标准容器

`容器是存储其他对象(其元素)的集合的持有者对象。`
它们作为类模板实现,这使得作为元素支持的类型具有极大的灵活性。
容器管理其元素的存储空间,并提供成员函数直接或通过`迭代器(iterator)`(具有指针类似属性的引用对象)访问它们。<br><br>
容器复制在编程中非常常用的结构:`动态数组(矢量)`、`队列(队列)`、`堆栈(堆栈)`、`堆(优先级_队列)`、`链接列表(列表)`、`树 (集)`, `关联数组 (映射)` ...<br><br>
许多容器具有多个共同的成员功能,并且共享功能。决定为特定需求使用哪种类型的容器通常不仅取决于容器提供的功能,还取决于其某些成员的效率(复杂性)。对于序列容器尤其如此,在插入/删除元素和访问它们之间提供了不同的复杂权衡。<br><br>
    堆栈、队列和优先级队列作为容器适配器实现。容器适配器不是完整的容器类,而是提供特定接口的类,它依赖于容器类之一(如deque或列表)的对象来处理元素。 基础容器的 封装方式使其元素由容器适配器的成员访问,而不受使用的基础容器类的影响。<br><br>

设`S`表示一种容器类型`(例如vector<int>)`，`s1`和`s2`都是`S`类型实例，容器支持基本功能如下:<br>
* S s1     
容器都有一个默认构造函数，用于构造一个没有任何元素的空容器,其元素可在后续插入。
* s1 op s2  
这里op可以是`==,!=,<,<=,>,>=`之一，他会对两个容器之间元素按字典序进行比较
* s1.begin()  
返回指向s1第一个元素的迭代器
* s1.end()  
返回指向s1最后一个元素的下一个位置的迭代器
* s1.clear()  
将容器s1内容清空
* s1.empty()   
返回一个`bool`值，表示s1容器是否为空。
>当为以下情况时返回`true`<br>
>"" (空字符串)<br>
>0 (作为整数的0)<br>
>0.0 (作为浮点数的0)<br>
>"0" (作为字符串的0)<br>
>NULL<br>
>FALSE<br>
>array() (一个空数组)<br>
>$var; (一个声明了，但是没有值的变量)<br>

### 二、顺序容器
         STL中包含的顺序容器包括`向量(vector)`、`双端队列(deque)`和`列表(list)`,在逻辑上可以看作是一个
         长度可以扩展的数组,容器中的元素都线性排列。程序员可随意决定每个元素在容器中的位置，可以随时向指
         定位置插入新元素和删除已有的元素。
  

#### 一、向量 vector 
         vector 可以看做是动态的数组。
```c++
vector<int>vec;

vec.push_back(2);//尾部插入数字2,即 vec[0]=2

vec.push_back(4);//尾部插入数字4,即 vec[1]=4

int Size = vec.size();//容器中存放数字的个数

cout<< vec[1] <<endl;//访问第二个数字，即4


for(int i = 0; i < vec.size(); ++ i)//按照下标遍历元素,此时vec[0]=2  vec[1]=4
    cout<< vec[i] << " ";
cout<<endl;


vector<int>::iterator it;//按照迭代器遍历元素

for(it = vec.begin(); it != vec.end(); ++ it)
    cout<< *it <<" ";
cout<<endl;

 
vec.insert(vec.begin() + 1, 6);//在第二个位置上插入元素6，即vec[1]=6

vec.erase(vec.begin() + 1);//删除第二个位置上的元素

vec.clear();//把容器中的元素全部清除

//vector-----------------

   vector<int>v;

   v.erase(v.begin() + 2);//删除第2个元素，从0开始计数

   v.erase(v.begin() + 1, v.begin() + 5);//删除第1到第5个元素

   sort(v.begin(), v.end());//元素排序

   //sort(v.begin(), v.end(), cmp);//自定义排序规则，cmp函数自定义

   reverse(v.begin(), v.end());
   
//vector-----------------

```
>>另外也可以定义二维动态数组即vector<int>vec[2];也就是两个容器，用它可以很方便的保存有向图的邻接表,即vec[i]中存放的是与第i个顶点相邻的顶点（从顶点i出发），.其操作只要把上述代码中的vec改成vec[i] 就可以.
    
#### 二、队列 queue

         队列，又称为伫列（queue），是先进先出（FIFO, First-In-First-Out）的线性表。在具体应用中通常
         用链表或者数组来实现。队列只允许在后端（称为rear）进行插入操作，在前端（称为front）进行删除操作。 
         队列的操作方式和堆栈类似，唯一的区别在于队列只允许新数据在后端进行添加。 

```c++

queue<int>que;//队列que,存放int型数据

que.push(3);//将3入队列

que.push(2);//将2入队列

que.pop();//队首3出队列

int Front = que.front();//获取队首元素

int Size = que.size();//队列中元素个数

bool isEmpty = que.empty(); //是否为空

queue<T>que;  // T是存放数据的类型，可以是int, double等，也可以是自定义的结构体类型.


//deque-------------双端队列

   push_back()方法在尾部插入元素，不断扩张队列

   push_front()和insert()在首部和中间位置插入元素，只是将原位置上的元素值覆盖，不会增加新元素

   deque<int> d;

   d.push_back(1);

   d.push_back(2);

   d.push_back(3);

   d.insert(d.begin() + 1, 88);

   cout << d[0] << d[1] << d[2] <<endl; //输出 1 88 3

   d.pop_front();//头部删除元素

   d.pop_back();//尾部删除元素

   d.erase(d.begin() + 1);
   
//deque-------------双端队列

```
* 优先队列 priority_queue 

   >优先队列也是一种队列，只不过不同的是，优先队列的出队顺序是按照优先级来的；在有些情况下，可能需要
   找到元素集合中的最小或者最大元素，可以利用优先队列ADT来完成操作，优先队列ADT是一种数据结构，它支
   持插入和删除最小值操作(返回并删除最小元素)或删除最大值操作(返回并删除最大元素);这些操作等价于
   队列的`queue`和`dequeue`操作,区别在于,对于优先队列,元素进入队列的顺序可能与其被操作的顺序不同,
   作业调度是优先队列的一个应用实例,它根据优先级的高低而不是先到先服务的方式来进行调度;如果最小键值
   元素拥有最高的优先级，那么这种优先队列叫作升序优先队列(即总是先删除最小的元素),类似的,如果最大键
   值元素拥有最高的优先级,那么这种优先队列叫作降序优先队列（即总是先删除最大的元素）.
   
```c++
//示例

const int len = 5;

int a[len] = {3, 5, 9, 6, 2};

priority_queue<int> q;

for(int i = 0; i < len; ++ i)
    q.push(a[i]);
    
for(int i = 0; i < len; ++ i)
{
    cout<< q.top() <<endl;
    q.pop();
}

//输出为 : 9 6 5 3 2
```
   

     


# 迭代器
         迭代器是一种检查容器内元素并遍历元素的数据类型。C++更趋向于使用迭代器而不是下标操作，因为标准库为每一种
         标准容器（如vector）定义了一种迭代器类型，而只用少数容器（如vector）支持下标操作访问容器元素。
## 一、定义和初始化
每种容器都定义了自己的迭代器类型，如vector:
```c++
vector<int>::iterator    iter;    //定义一个名为iter的变量
```
每种容器都定义了一对名为begin和en的函数，用于返回迭代器。下面对迭代器进行初始化操作：
```c++
vector<int>    ivec;
vector<int>::iterator    iter1=ivec.bengin();    //将迭代器iter1初始化为指向ivec容器的第一个元素
vector<int>::iterator   iter2=ivec.end();    //将迭代器iter2初始化为指向ivec容器的最后一个元素的下一个位置
```
>注意end并不指向容器的任何元素，而是`指向容器的最后元素的下一位置`，称为超出末端迭代器。如果vector为空，则begin
>返回的迭代器和end返回的迭代器相同。一旦向上面这样定义和初始化，就相当于把该迭代器和容器进行了某种关联，就像把一
>个指针初始化为指向某一空间地址一样。
## 二、常用操作
下面列出了迭代器的常用运算操作：
```c++
*iter                //对iter进行解引用，返回迭代器iter指向的元素的引用
iter->men            //对iter进行解引用，获取指定元素中名为men的成员。等效于(*iter).men
++iter                //给iter加1，使其指向容器的下一个元素
iter++
--iter                //给iter减1，使其指向容器的前一个元素
iter--
iter1==iter2        //比较两个迭代器是否相等，当它们指向同一个容器的同一个元素或者都指向同同一个容器的超出末端的下一个位置时，它们相等 
iter1!=iter2
```
假设已经声明一个vector<int>的ivec容器，下面用迭代器来遍历ivec容器，把其每个元素重置为0：
```c++
for(vector<int>::iterator iter=ivec.begin();iter!=ivec.end();++iter)
        *iter=0;
```

vector 和 deque 容器的迭代器提供额外的运算
```c++
iter + n
iter - n
//在迭代器上加（减）整数值 n，将产生指向容器中前面（后面）第 n个元素的迭代器。新计算出来的迭代器必须指向容器中的元素或超出容器末端的下一位置
iter1 +=iter2
iter1 -=iter2
//这里迭代器加减法的复合赋值运算：将 iter1 加上或减去 iter2 的运算结果赋给 iter1
iter1 -iter2
//两个迭代器的减法，其运算结果加上右边的迭代器即得左边的迭代器。这两个迭代器必须指向同一个容器中的元素或超出容器末端的下一位置只适用于 vector 和 deque 容器
iter + n
iter - n
//在迭代器上加（减）整数值 n，将产生指向容器中前面（后面）第 n个元素的迭代器。新计算出来的迭代器必须指向容器中的元素或超出容器末端的下一位置
>, >=,<, <=
//迭代器的关系操作符。当一个迭代器指向的元素在容器中位于另一个迭代器指向的元素之前，则前一个迭代器小于后一个迭代器。关系操作符的两个迭代器必须指向同一个容器中的元素或超出容器末端的下一位置只适用于 vector 和 deque 容器
```
    
## 三、迭代器const_iterator
每种容器还定义了一种名为const_iterator的类型。该类型的迭代器只能读取容器中的元素，不能用于改变其值。之前的例子中，普通的迭代器可以对容器中的元素进行解引用并修改，而const_iterator类型的迭代器只能用于读不能进行重写。例如可以进行如下操作:<br>
```c++
for(vector<int>::const_iterator iter=ivec.begin();iter!=ivec.end();++iter)
     cout<<*iter<<endl;       //合法，读取容器中元素值

for(vector<int>::const_iterator iter=ivec.begin();iter!=ivec.end();++iter)
    *iter=0;        //不合法，不能进行写操作
```
const_iterator和const  iterator是不一样的，后者对迭代器进行声明时，必须对迭代器进行初始化，并且一旦初始化后就不能修改其值。这有点像常量指针和指针常量的关系。例如：
```c++
vector<int>    ivec(10);
const    vector<int>::iterator    iter=ivec.begin();
*iter=0;    //合法，可以改变其指向的元素的值
++iter;    //不合法，无法改变其指向的位置
```
