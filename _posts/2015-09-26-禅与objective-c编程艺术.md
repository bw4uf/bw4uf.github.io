#禅与Objective-C编程艺术
##条件语句
1、给条件语句体加大括号

示例：

    if (!error){
         return success;
    }

条件语句体一定要用大括号括起来，即使是只有一行内容。

2、不要使用尤达表达式

示例：

    if ([myValue isEqual:@42]){
         ....
    }
不要使用尤达表达式。尤达表达式是指，拿一个常量去和变量比较。这样是不对的，正确的方式应该像示例中拿变量去和常量比较。

3、使用!作为对象为空的判断方式

示例：

    if(someObject){ ...
    if(!someObject){ ...
    if(![someObject booValue]){ ...
    
不要拿对象和`YES`进行比较，因为`YES`是1，而`BOOL`是char类型的，是8位的。而如果使用

    if(myValue == nil){ ...
    
这样的条件判断，万一错写成

    if(myValue = nil){ ...
把判断条件误写成赋值语句，编译是不会报错的，这样就很难检查出错误来。

4、黄金大道

示例：

    - (void)someMethod{
      if(![someOther boolValue]){
          return;
      }
      //Do something important
    }
不要嵌套`if`语句，把do something放到条件语句体里，多个return语句也OK，这样可以避免Cyclomatic(循环)复杂性，并且让代码更加容易阅读。因为方法的重要部分没有嵌套在分支上，所以可以很清楚地找到相关的代码。

5、复杂的表达式

就像一个很长的viewDidLoad方法需要拆分出多个方法一样，当你有一个复杂的if子句时，你应该把它们提取出来赋给一个BOOL变量，这样可以让逻辑更清楚，而且让每个子句的意义体现出来。

6、错误处理

示例：

    NSError *error = nil;
    if(![self trySomethingWithError:&error]){
        //Handle Error
    }
当方法返回一个错误参数的引用的时候，检查返回值，而不是错误的变量。

##命名

1、遵守Apple的命名约定，使用长的、描述性的方法和变量名

2、小心不要将`nil`放到NSArray和NSDictionary中，这样会导致Crash。

##类

1、类名

类名应加上三个大写字母作为前缀，这样做是为了减少Objective-C没有命名空间带来的问题。

2、我们常见的[[NSObject alloc] init]表达式。这里体现了Objective-C的一个特性叫`两步创建`。这意味着申请分配内存和初始化是两个分离的操作。

* `alloc`表示对象分配内存，这个过程涉及分配足够的可用内存来保存对象，写入`isa`指针，初始化retain的技术，并且初始化所有实例变量。

* `init`是表示初始化对象，这意味着把对象放到了一个可用的状态。这通常是指把对象的实例变量赋给了可用的值。

3、Designated and Secondary Initializers（指定初始化和二次初始化）
示例：

    @implemention HELEvent
    
    - (instancetype)initWithTitle:(NSString *)title
 	        			    	date:(NSDate *)date
 	   			    	location:(CLLocation *)location
    {
        self = [super init];
        if(self){
            _title = title;
            _date = date;
            _location = location;
        }
        return self;
    }
    
    - (instancetype)initWithTitle:(NSString *)title
 	        			    	date:(NSDate *)date
    {
        return [self initWithTitle:title date:date 
           location nil];
    }
    
    @end
    
designated初始化方法提供所有的参数，secondary初始化方法是一个或者多个，并且提供一个或者更多的默认参数来调用designated初始化方法。

创建子类的时候，你希望提供你自己的初始化函数，那么你应该遵守三个步骤来保证正确性。

 * 定义你的designated initializer，确保调用了父类的designated initializer。
 * 重写父类的designated initializer，并在其中调用你的新的designated initializer。
 * 为新的designated initializer写文档。
（PDF中介绍了参考的苹果开发者网站上的文档，可以去看官方是如何解释的）

4、instancetype

根据clang的定义，`id`可以被编译器提升到`instancetype`。在`alloc`或者`init`中，强烈建议对所有返回类的实例的类方法和实例方法使用`instancetype`类型。

5、class cluster（类簇）

class cluster是Apple对抽象工厂设计模式的称呼。一个经典的例子是如果你有为iPad和iPhone写的一样的UIViewController子类，但是在不同的设备上有不同的行为。（我的理解就是在抽象工厂方法里面由条件语句判断执行不同类的创建和初始化）

    @implementation HELPhotoViewController
    - (id)initWithPhotos:(NSArray *)photos
    {
        if([self isMemberOfClass:HELPhotoViewController.class]){
            self = nil;
            if([UIDevice isPad]){
                self = [[HELPhotoViewController_iPad alloc] initWithPhotos:photos];
            }
            else{
                self = [[HELPhotoViewController_iPhone alloc] initWithPhotos:photos];
            }
            return self;
        }
        return [super initWithNibName:nil bundle:nil];
    }
    
    @end

6、Categories（分类）

我们应该在category方法前加上自己的小写前缀以及下划线，比如`- (id)hel_myCategoryMethod`,这是苹果推荐的写法。

示例：

    @interface NSDate(HELTimeExtensions)
    - (NSString *)hel_timeAgoShort;
    @end

##美化代码
1、空格

缩进使用4个空格，永远不要使用tab键。

##对象间的通讯
1、Blocks

示例代码：

    - (void)downloadObjectsAtPath:(NSString *)path
                       completion:(void(^)(NSArray *objects,NSError *error))completion;

在定义一个这样的接口的时候，使用block作为接口的最后一个参数。把需要提供的数据和错误信息整合到一个单独的block中，比分别提供成功和失败的block要好。

2、关于Blocks

* block是在栈上创建的
* block可以复制到堆上
* block有自己的私有的栈变量（以及指针）的常量复制
* 可变的栈上的变量和指针必须用__block关键字声明

如果block没有在其他地方被保持，那么它会随着栈生存并且当栈帧返回时消失。当在栈上的时候，一个block对访问的任何内容不会有影响。如果block需要在栈帧返回的时候存在，它们需要明确地被复制到堆上，这样，block会像其他Cocoa对象一样增加引用计数。当它们被复制的时候，它会带着它们的捕获作用域一起，retain它们所有引用的对象。如果一个block指向一个栈变量或者指针，那么这个block初始化的时候它会有一份声明为const的副本，所以对它们赋值是没用的。当一个block被复制后，`__block`声明的栈变量的引用被复制到堆里，复制之后栈上的以及产生的堆上的block都会引用这个堆上的变量。



#附：本文md格式编辑注意点
1、空一行，行首四个空格，可以实现程序格式

    NSLog("hello");

2、字符串前后加上英文的 ` (同esc下方的~键)，可以使字符串高亮
     
     `高亮状态`
     
3、空一行，*后面空一格，可以使行首添加一个黑点

* 一个黑点
    * 空四格的是白点

4、尖括号里面一个s，其后面内容会被划掉，<s>效果就像这样</s>
用结束标签的写法可以终断这种效果。


5、首尾行三个英文格式的```中间段的内容可以实现程序格式

```
NSLog("hello");
```






