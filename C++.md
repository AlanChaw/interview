* **一.变量**
    * 1）全局变量与static变量？（作用域、生存周期）
        > - 全局变量和 static 变量都存储在内存的静态存储区中，在未初始化时会被自动初始化为0，只会在程序开始运行时做唯一的一次初始化。生存周期直到程序结束。
        > - static 修饰的变量只能在其作用域内被访问（例如某个函数或某个文件中），而全局变量作用域是整个工程。static 全局变量也只能在本文件中访问。

    * 2）[static函数与普通函数的区别？](temp/C++.md#4static函数与普通函数的区别)
        > static 函数的作用域仅在当前文件，不能被其他文件所用。好处在于可以与其他文件定义相同的函数且不会冲突。

    * 3）两个文件中声明两个同名变量？（使用了与未使用extern？） 
        > 如果不加 extern 的话，这两个变量无关。使用 extern 的话被视为同一个变量。

    * 4）全局数组和局部数组的初始化？
        > 全局数组会自动被初始化为全0. 而局部数组将用随机值填充。

    * 5）[指针和引用的区别](https://www.nowcoder.com/ta/nine-chapter/review?page=11)？（代表意义、内存占用、初始化、指向是否可改、能否为空）
        > - 指针在本质上是存储地址的变量，而引用只是别名。指针可以指向其他地址，而引用一旦绑定某个对象则不可更改。
        > - 指针会占用内存区域（一般4bytes），而引用不会，它仅仅是别名。
        > - 在参数传递时，引用会做类型检查，而指针不会。
        > - 引用不能为空，指针可以为空。

    * 6）[C/C++中的强制转换](https://github.com/arkingc/note/blob/master/C++/EffectiveC++.md#%E6%9D%A1%E6%AC%BE27%E5%B0%BD%E9%87%8F%E5%B0%91%E5%81%9A%E8%BD%AC%E5%9E%8B%E5%8A%A8%E4%BD%9C)
        > - static_cast<> 强迫隐式转换，可以将 non-const 转为 const，但不能将 const 转为 non-const。可以将 int 转 double，将基类指针转为派生类指针，等等。
        > - const_cast<> 将 const 转为 non-const
        > - dynamic_cast<> 安全向下转型，用来决定某个对象是否归于某个继承体系中的某个类型，例如多态中将基类指针转为派生类指针以检验其类型。
        > - reinterpret_cast<> 低级转型。例如将 pointer-to-int 转为 int。比较少见。例如还可以将 pointer to address_in 转为 pointer to address

    * 7）[如何修改const变量、const与volatile](https://blog.csdn.net/heyabo/article/details/8745942)
        > - const volatile int a = 0; 实际上是未定义行为，很多编译器过不了，或者通过指针间接修改。
        > - volatile：一般是告诉编译器这个变量可能会发生其难以预料的修改，所以不要为它做缓存，哪怕刚刚读取过这个变量，每次读取 volatile 变量时都要去内存直接读取。

    * 8）静态类型获取与动态类型获取（[typeid](https://github.com/arkingc/llc/blob/master/cpp/RTTI/typeid.cpp#L4)、dynamic_cast:转换目标类型必须是引用类型）
        > - 只有句柄是引用或指针时，对象的动态类型和静态类型才有可能不同。静态类型是指该句柄声明为的类型，而动态类型是指其在执行过程中所指向的对象的真正类型。
        > - 动态类型是为动态绑定准备的，而且调用虚函数时才有意义，这样在可以运行期判断执行调用哪个版本的函数。而如果不是虚函数，则在编译期就能确定调用哪个版本。

    * 9）[如何比较浮点数大小？](https://blog.csdn.net/jk110333/article/details/8902707)（[直接使用==比较出现错误的例子](https://stackoverflow.com/questions/26261466/in-current-c-and-java-double-type-and-float-type-if-x-0-0-is-correct)）
        > - 设置一个较小的精度。然后比较两个数的差的绝对值是否小于这个小精度。

* **二.函数**
    * 1）重载（[参数必须不同(const修饰形参)](https://github.com/arkingc/llc/blob/master/cpp/overload/main.cpp#L9)、重载与作用域、继承中的重载\(using\)、重载与const成员函数） 
        > 函数重载要求函数名相同、作用域相同、参数必须不同，返回值不考察。const 和非 const 认为是不同版本。当传入参数是 const 时使用 const 版本，当传入参数非 const 时优先使用非 const 版本。
        > 在继承中，如果基类有多个版本的重载函数，而子类在自身定义中再次定义了该函数，那么基类的所有重载版本都会被隐藏。除非子类中声明： using Base::func;
    
    * 2) using
        > 说到 using，这里说一下using的几种用法。一是使用命名空间中的某个成员，二是使用整个命名空间，三是代替 typedef，四是在子类中使用基类的重载函数。

* **三.类**
    * 1）[面向对象的四大特征（封装、抽象、继承、多态）](面向对象的四大特性)

    * 2）[struct和class的区别？](https://blog.csdn.net/qq_37964547/article/details/81835488)
        > - struct 的成员默认是 public，class 成员默认是 private
        > - struct 默认是 public 继承，class 默认是 private 继承
        > - 在 c++ 中基本上是通用的，但是 struct 多用于具体的数据实体。而 class 多用于包含很多操作的对象。

    * 3）[访问权限说明符](temp/C++.md/#3访问控制说明符)？（目的是加强类的封装性）
        > - 类成员的访问权限说明符。 public 成员可以被外界访问，可以被派生类和友元访问。 protected 不能被外界访问，只能被派生类和友元访问。private 只能被友元访问，外界和派生类均不可访问。
        > - 继承时的访问权限说明符。 public 继承时，基类 public 成员成为派生类 public 成员，基类 protected 成员成为派生类 protected 成员。 protected 继承时，基类的 public 和 protected 成员都成为派生类的 protected 成员。 private 继承时，基类的 public 和 protected 成员都成为派生类的 protected 成员。  
        > - 实际上，基类的 private 成员无论如何不能被派生类继承和访问。上边两点并不冲突。

    * 4）类的静态成员（类类型的成员、定义时不能重复使用static、具有类内初始值的静态成员定义时不可再设初值）
        > - 想为静态成员变量赋类内初始值的话必须声明为 const，且不能再赋初值。
        > - static 可以被用来修饰类成员变量或成员函数。static修饰的类成员变量只有一份，被该类所有的对象共享，且无需借助该类的对象也能访问，想在类内声明处直接初始化的 static 必须是 const。 static 修饰的成员函数也无需借助该类对象访问，但没有 this 指针，只能访问 static 成员变量。

    * 5）构造函数相关
        - 有哪些构造函数（默认、委托、拷贝、转换、移动）
        - 合成的拷贝构造函数（默认行为？什么情况下不会合成？怎么解决？如果成员包含类内初始值，合成默认构造函数会使用该成员的类内初始值初始化该成员）
            > - 编译器合成的拷贝构造函数只提供浅拷贝，即逐字节的拷贝。
            > - 当类中有成员不支持拷贝，或显示声明了移动构造函数时，不会自动合成。（不可拷贝是指这个类自身或类中有成员的析构函数被删除或不可访问，或拷贝构造函数被删除或不可访问）

        - 拷贝构造函数（调用时机、合成版的行为、explict？、为何第一个参数必须是引用类型）
            > 调用时机：以一个现有对象初始化另一个对象时；函数的形参实参化时；函数返回类类型时。
            > explicit 用于禁止隐式类型转换。当存在仅接受一个参数的构造函数，且未声明为 explicit时，会被编译器认为是转换构造函数。
            > 先说为什么用引用，因为如果传值的话就会再多经历一次拷贝。而 const 是无所谓的，只是为了防止修改。

        - 移动拷贝构造函数（非拷贝而是窃取资源、与noexcept?、何时合成）
            > - 非拷贝而是窃取资源。但是只是对支持移动构造的对象会发生移动，不支持的部分（如基本类型）仅是拷贝。
            > - noexcept 的原因与析构函数也不能抛出异常的原因相似。因为在析构或移动的过程中，对象处于一种“半死不活”的状态，这时如果抛出异常很容易导致内存泄漏，或对象初始化到一半的状态。
            > - 只有当类未定义拷贝构造函数和析构函数时（也没删除析构函数），编译器才会自动合成。如果有类成员是 const 或者引用，也不会自动合成。

        - 可否通过对象或对象的引用(指针或引用)调用
            > - 不能。有些编译器好像可以，但是跟直接调用析构函数一样，都是只当做普通的成员函数。而且直接调用析构函数是很危险的，有可能导致堆内存二次释放。

    * 6）初始值列表（顺序、效率(内置类型不进行隐式初始化故无所谓,但..)、无默认构造函数的成员,const成员,
    引用成员必须通过初始值列表初始化）
        > - 顺序是按成员在类中出现的顺序进行，而不是按在初始化列表中的顺序，所以要注意不能拿还未初始化的成员去初始化其他成员。
        > - 内置类型无所谓。但对自定义类类型的对象，以及派生类对象的基类部分都会造成二次初始化，效率较低。
        > - 尤其是无默认构造函数的成员,const成员,引用成员必须通过初始值列表初始化

    * 7）赋值运算符相关
        - 拷贝赋值运算符（合成版的行为？、与delete？、自定义时要注意自赋值，参数与返回类型、大部分组合了拷贝构造函数与析构函数的工作）
            > 几乎与拷贝构造函数一样。可以 = delete 禁止重载。
            > 自定义时如果 rhs == this，则跳过
            > 返回值需要时一个自身类型的引用，从而可以实现串联赋值。

        - 阻止拷贝（某些对象应该独一无二(比方说人)、C++11前:private并且不定义(试图拷贝会报链接错误)，C++11:=delete [《Effective C++:条款6》](https://github.com/arkingc/note/blob/master/C++/EffectiveC++.md#%E6%9D%A1%E6%AC%BE06%E8%8B%A5%E4%B8%8D%E6%83%B3%E4%BD%BF%E7%94%A8%E7%BC%96%E8%AF%91%E5%99%A8%E8%87%AA%E5%8A%A8%E7%94%9F%E6%88%90%E7%9A%84%E5%87%BD%E6%95%B0%E5%B0%B1%E8%AF%A5%E6%98%8E%E7%A1%AE%E6%8B%92%E7%BB%9D)）

        - 移动赋值运算符（与noexcept？何时合成）
            > 与移动构造函数几乎一样，也应该是 noexcept，也是需要检测自赋值的情况。返回值应该是自身的引用。

        - 可以定义为成员或非成员函数，定义成成员函数时第一个操作数隐式绑定到this指针
            > 输入(>>)、输出运算符(<<)必须是非成员函数。从而能实现连续的输入或输出。

        - 不可重载的操作符有哪些？（?:，::）

    * 8）析构函数相关
        - 销毁过程的理解（delete会执行哪些操作？[逆序析构成员](https://github.com/arkingc/llc/blob/master/cpp/class/constructorANDdestructor/order.cpp#L1)）
            > delete 先执行析构函数，再使用 free() 释放内存。析构的过程是逆序的，先析构派生类对象的基类部分，自身成员按初始化顺序逆序销毁，最后析构自身（原因应该是因为是在栈空间中，先进后出，所以释放过程是逆序过程）。

        - 为什么析构函数中不能抛出异常？（不能是指“不应该”，C++本身并不禁止[《Effective C++:条款8》](https://github.com/arkingc/note/blob/master/C++/EffectiveC++.md#%E6%9D%A1%E6%AC%BE08%E5%88%AB%E8%AE%A9%E5%BC%82%E5%B8%B8%E9%80%83%E7%A6%BB%E6%9E%90%E6%9E%84%E5%87%BD%E6%95%B0)）
            > 不要让对象处于“半死不活”状态。如果析构执行一半去处理异常，可能使析构无法完成，导致内存泄漏。或者，对于 RAII 类，可能导致其中的连接永远无法被断开，锁永远无法解开等问题。

        - 如果析构函数中包含可能抛出异常的代码怎么办？（Effective C++:条款8》）
            > 直接吞掉异常（不是好方法）。或尝试将可能抛出异常的代码转移到析构函数以外。

        - 可否通过对象或对象的引用(指针或引用)调用
            > 可以。但只会当做普通成员函数执行。容易导致二次释放堆内存的问题。

        - 为什么将继承体系中基类的析构函数声明为虚函数？（[《Effective C++:条款7》](https://github.com/arkingc/note/blob/master/C++/EffectiveC++.md#%E6%9D%A1%E6%AC%BE07%E4%B8%BA%E5%A4%9A%E6%80%81%E5%9F%BA%E7%B1%BB%E5%A3%B0%E6%98%8Evirtual%E6%9E%90%E6%9E%84%E5%87%BD%E6%95%B0)）
            > 当实现多态性时，当派生类对象经基类句柄被删除，这时只有基类部分被删除，派生类部分会资源泄露。比较好的方法是，当且仅当类中有 virtual 函数时，就将析构函数也声明为 virtual.

        - 不应该将非继承体系中的类的虚函数声明为虚函数（[《Effective C++:条款7》](https://github.com/arkingc/note/blob/master/C++/EffectiveC++.md#%E6%9D%A1%E6%AC%BE07%E4%B8%BA%E5%A4%9A%E6%80%81%E5%9F%BA%E7%B1%BB%E5%A3%B0%E6%98%8Evirtual%E6%9E%90%E6%9E%84%E5%87%BD%E6%95%B0)）
            > 会扩大虚函数表，对象体积会增加。

        - 不应该继承析构函数非虚的类（[《Effective C++:条款7》](https://github.com/arkingc/note/blob/master/C++/EffectiveC++.md#%E6%9D%A1%E6%AC%BE07%E4%B8%BA%E5%A4%9A%E6%80%81%E5%9F%BA%E7%B1%BB%E5%A3%B0%E6%98%8Evirtual%E6%9E%90%E6%9E%84%E5%87%BD%E6%95%B0)，final防止继承）

        - [防止继承的方式](https://blog.twofei.com/672/)
            > final 就行了。。 别管那么多了。

        - 构造和析构函数中调用虚函数.
            > - 可以调用，但没有发生动态联编、即对虚函数的调用其实是实调用，也就是基类的版本。

    * 9）[删除的合成函数](https://github.com/arkingc/llc/blob/master/cpp/class/delete/README.md)（一般函数而言不想调用的话不定义就好）
        > 主要参见前边拷贝构造函数和移动构造函数那部分。

    * 10）继承相关
        - 继承体系中的构造、拷贝、析构顺序？
            > 构造时先构造最上层的基类部分，再逐级向下构造派生类部分，如果不在初始化列表中调用基类构造函数，会自动调用基类默认构造函数（但如果基类没有默认构造函数，则必须在初始化列表中调用基类构造函数初始化基类部分）； 拷贝时跟构造时的行为类似，也是会先构造最底层的基类，然后逐级向下；析构的顺序与构造顺序相反。

        - 继承中的名字查找（作用域嵌套、从子类到父类查找；[成员名字的处理](https://github.com/arkingc/note/blob/master/C++/C++%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B.md#%E5%90%8D%E7%A7%B0%E7%9A%84%E7%89%B9%E6%AE%8A%E5%A4%84%E7%90%86)）
            > - 名字查找先于参数检查。 编译器首先确定句柄的静态类型，然后从该静态类型对应的类开始查找，如果没有则向上一层从其直接基类开始查找，如果找遍整个继承体系中所有基类都没找到则报错。一旦找到，则进行常规类型检查，看本次调用是否合法。假如调用合法，编译器再看是否是虚函数，如果是则根据对象的动态类型调用相应的版本；如果不是虚函数则直接调用静态类型对应的版本。
            > - 如果派生类定义了基类同名函数，则基类所有重载版本会被隐藏，除非使用 using。


        - [成员函数体内、成员函数的参数列表的名字解析时机](https://github.com/arkingc/note/blob/master/C++/C++%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B.md#31-data-member%E7%9A%84%E7%BB%91%E5%AE%9A)（因此，务必将“内嵌的类型声明”放在class起始处）
            > 成员函数体内的名字解析直到类定义的大括号末尾才开始，所以在类的成员函数内可以随意使用其他成员的名字，不用担心未定义的问题。而成员函数的参数列表的名字解析是在参数第一次出现时就开始了，所以要将类内的 "typedef " 或 "using " 声明放到类起始处。


        - 同名名字隐藏（如何解决？(域作用符，从指示的类开始查找)、不同作用域无法重载、using的作用？除此之外呢？） 
            > 在函数名加上类名来定义，从而派生类不会隐藏基类同名函数。重载要求必须相同作用域才可以。

        - 虚继承（解决什么问题？(多继承中的子对象冗余)）
            > - 虚继承是在多重继承时出现的问题。如:类D继承自类B1、B2，而类B1、B2都继承自类A，因此在类D中两次出现类A中的变量和函数。为了节省内存空间，可以将B1、B2对A的继承定义为虚拟继承，而A就成了虚拟基类。
            > - 在虚拟继承情况下，基类子对象的布局是不同于普通继承的。因此，它需要多出一个指向基类子对象的指针。也就是说，其维护一个指向自身虚函数表的指针，也维护一个指向虚拟基类的虚函数指针。

        - 重载、覆盖、和隐藏
            > - 重载(overload)需要在相同的作用域中，也就是必须在同一个类中，重载只要求同名、同作用域、不同参数类型，不要求返回值和是否为虚函数。
            > - 覆盖(override)说的是派生类虚函数覆盖基类虚函数（要求virtual、名字和参数均相同）
            > - 隐藏(hide)，说的是派生类函数屏蔽了基类同名函数。当同名不同参数时，无论是否virtual，基类的所有重载版本都被隐藏；当同名同参数时，如果有 virtual 则基类对应函数被覆盖，否则基类所有版本被隐藏。

    * 11）多态的实现？
        > 使用虚函数表vtable。多态性是通过包含了三级指针的一种数据结构实现的。
        > - 第一级指针：虚函数表 vtable 中的函数指针，当调用虚函数时，这些指针指向实际执行的函数 (图中步骤 5 所对应的函数指针)。
        > - 第二级指针：当实例化具有一个或多个虚函数的类的对象时，编译器给这个对象附上一个指针，指向所属类的虚函数表(图中步骤 3 所对应的指针)。
        > - 第三级指针：接收虚函数调用的对象句柄(因为只有通过指针或引用才有动态类型，才能实现多态)

    * 12）[虚函数的实现原理？对类大小的影响？](https://www.cnblogs.com/malecrab/p/5572730.html)（vtbl是一个由函数指针组成的数组，无论pb指向哪种类型的对象，只要能够确定被调函数在虚函数中的偏移值，待运行时，能够确定具体类型，并能找到相应vptr，进一步能找出真正应该调用的函数）
        > - 虚函数调用时发生的指针间接引用(解引用)操作和内存访问都算作程序开销，从而增加程序执行时间，而且虚函数表和对象中的虚函数表指针也要占用额外内存。
        > - 在调用时，编译器首先确定句柄的静态类型，然后确定调用是否合法，再看是否是 virtual 函数，如果是则根据动态类型调用对应版本，如果不是则直接调用静态类型版本。

    * 13）为什么不要在构造、析构函数中调用虚函数？（子对象的base class构造期间，对象的类型是base class [《Effective C++:条款9》](https://github.com/arkingc/note/blob/master/C++/EffectiveC++.md#%E6%9D%A1%E6%AC%BE09%E7%BB%9D%E4%B8%8D%E5%9C%A8%E6%9E%84%E9%80%A0%E5%92%8C%E6%9E%90%E6%9E%84%E8%BF%87%E7%A8%8B%E4%B8%AD%E8%B0%83%E7%94%A8virtual%E5%87%BD%E6%95%B0)，[设置虚函数指针的时机](https://github.com/arkingc/note/blob/master/C++/C++%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B.md#vptr%E7%9A%84%E8%AE%BE%E7%BD%AE)）
        > - 在基类部分构造期间，如果基类构造函数中调用了虚函数，那么将只调用基类版本，不会调用派生类版本。

    * 14）[虚函数被覆盖？](https://github.com/arkingc/llc/blob/master/cpp/class/inheritance/virtual_function_hide.cpp#L1)
        > - 虚函数实现覆盖的原因是，派生类的在虚函数表中的虚函数指针覆盖了相应位置的派生类的虚函数指针。
        > - 也可以强行调用基类版本的虚函数，这时不会经过虚函数表，编译器会直接找到基类版本调用。

    * 15）virtual函数动态绑定，缺省参数值静态绑定（[《Effective C++:条款37》](https://github.com/arkingc/note/blob/master/C++/EffectiveC++.md#%E6%9D%A1%E6%AC%BE37%E7%BB%9D%E4%B8%8D%E9%87%8D%E6%96%B0%E5%AE%9A%E4%B9%89%E7%BB%A7%E6%89%BF%E8%80%8C%E6%9D%A5%E7%9A%84%E7%BC%BA%E7%9C%81%E5%8F%82%E6%95%B0%E5%80%BC)）
        > - 不要在虚函数中使用缺省参数。因为缺省参数是静态绑定的，派生类会直接使用基类的默认值，即使派生类定义了自己的。

    * 16）纯虚函数与抽象基类（[纯虚函数与虚函数、一般成员函数的选择](../C++/EffectiveC++.md#条款34区分接口继承和实现继承)）
        > - 永远不会实例化的类。通常在类的继承层次结构中作为基类，其派生类必须在这些类的对象实例化前定义那些"缺少的部分"。抽象类的目的是为其他类提供合适的基类。当基类实现一个函数是没有意义的，并且程序员希望在所有具体的派生类中实现这个函数时，就会用到纯虚函数。
        > - 纯虚函数: 通过声明类的一个或多个虚函数为纯虚函数，可以使一个类成为抽象类。一个纯虚函数是在声明时"初始化值为0"的函数
        > - 抽象类为类层次结构中的各种类 定义公共的通用接口。抽象类包含一个或多个纯虚函数，也可以有数据成员和具体的函数(包括构造函数和析构函数)，它们被派生类继承时都符合一般的继承规则。
        > - 虽然抽象基类不能实例化，但仍可用其句柄（指针或引用）实现多态性。

    * 17）静态类型与动态类型（引用是否可实现动态绑定）
        > - 静态类型：句柄本身的类型。动态类型：句柄所指对象的实际类型。
        > - 句柄可以是指针或引用。

    * 18）浅拷贝与深拷贝（安全性、行为像值的类与行为像指针的类）
        > - 浅拷贝，只是按字面值、按位一位一位拷贝。深拷贝会将对象中的指针所指对象也拷贝一份（申请新的堆上内存），从而避免了空悬指针问题。当对象中带有指针时必须用深拷贝。
        > - 三五法则： 
        >   - 有三个基本操作可以控制类的拷贝操作：拷贝构造函数、拷贝赋值运算符、以及析构函数。一个原则是：如果我们需要自定义一个析构函数，就也需要自定义两个拷贝函数。
        >   - 在 C++ 11中，又增加了移动语义，所以又增加了移动构造函数和移动赋值运算符，所以叫三五法则。
        > - 行为像值的类：对于每一个已经实例化的类的对象，对于每一个类管理的资源,当对象与对象之间进行复制操作的时候，每个对象都保存有一份副本，使得当有一个对象中对应的成员占有的空间被释放的时候，对应赋值过的对象中的相应成员不受影响。
        > - 行为像指针的类：底层数据共享，类似智能指针那样的行为，构造对象时引用计数++，析构时计数--。

    * 19）如何定义类内常量？（enum而不是static const [《Effective C++:条款2》](https://github.com/arkingc/note/blob/master/C++/EffectiveC++.md#%E6%9D%A1%E6%AC%BE02%E5%B0%BD%E9%87%8F%E4%BB%A5constenuminline%E6%9B%BF%E6%8D%A2define)）

    * 20）继承与组合(复合)之间如何选择？（[《Effective C++:条款38》](https://github.com/arkingc/note/blob/master/C++/EffectiveC++.md#%E6%9D%A1%E6%AC%BE38%E9%80%9A%E8%BF%87%E5%A4%8D%E5%90%88%E5%A1%91%E6%A8%A1%E5%87%BAhas-a%E6%88%96%E6%A0%B9%E6%8D%AE%E6%9F%90%E7%89%A9%E5%AE%9E%E7%8E%B0%E5%87%BA)）
        > - 组合，has-a，是类型间的一种关系，某种类型的对象含有另一种类型的对象。
        > - 继承，is-a，派生类具有基类的特征和基类的能力。

    * 21）private继承？（[《Effective C++:条款39》](https://github.com/arkingc/note/blob/master/C++/EffectiveC++.md#%E6%9D%A1%E6%AC%BE39%E6%98%8E%E6%99%BA%E8%80%8C%E5%AE%A1%E6%85%8E%E5%9C%B0%E4%BD%BF%E7%94%A8private%E7%BB%A7%E6%89%BF)）
        > - private继承下，基类的 public 和 protected 成员都会成为派生类的 private 成员。
        > - 不再满足 is-a 的关系。
        > - 如果一个类需要访问基类的protected成员，或需要重新定义其一个或多个virtual函数，那么使用private继承。

    * 22）[如何定义一个只能在堆上（栈上）生成对象的类？](https://www.nowcoder.com/questionTerminal/0a584aa13f804f3ea72b442a065a7618)
        > - 只能在堆上生成对象：将构造函数设为 private，这样就只能用 new 来分配内存。
        > - 只能在栈上生成对象：将 new 运算符设为私有，这样就只能用构造函数创建对象。

    * 23）[内联函数、构造函数、静态成员函数可以是虚函数吗？](https://www.nowcoder.com/ta/nine-chapter/review?page=24)
        > 都不可以。内联函数需要在编译阶段展开，而虚函数是运行时动态绑定的，编译时无法展开； 构造函数在进行调用时还不存在父类和子类的概念，父类只会调用父类的构造函数，子类调用子类 的，因此不存在动态绑定的概念；静态成员函数是以类为单位的函数，与具体对象无关，虚函数是 与对象动态绑定的，因此是两个不冲突的概念。
        
* **四.内存管理**
    * 1）[C++内存分区](../C++/内存分区.md)
        > - 堆、栈、全局（静态）存储区、常量存储区、代码区。
        > - 堆向上增长，栈向下增长。
        > - 栈内存由编译器自动分配，不存在碎片问题。堆内存由程序员手动分配，存在内存碎片问题。
        > - 堆内存一般比栈内存大很多。但栈内存分配效率较高。

    * 2）[new](https://github.com/arkingc/note/blob/master/C++/C++%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B.md#1new)和malloc的区别？（函数，运算符、类型安全、计算空间、步骤）
        > - 一个C一个C++。对于类类型，要使用new分配内存，new分配内存后会自动调用对象的构造函数。
        > - new是关键字而malloc是函数。malloc返回类型是 (void*)，需要手动转换，new不需要(内置类型转换和类型安全检查功能)。
        > - new会自动计算空间(内置了sizeof)，malloc需要用 sizeof 计算。

    * 3）[operator-new和operator-delete的实现](https://blog.csdn.net/hazir/article/details/21413833)
        ```cpp
        void *operator new(size_t);     //allocate an object
        void *operator delete(void *);    //free an object

        void *operator new[](size_t);     //allocate an array
        void *operator delete[](void *);    //free an array
        ```
        > - 它们是 C++ 标准库函数。这两个函数和 C 语言中的 malloc 和 free 函数有点像了，都是用来申请和释放内存的，并且 operator new 申请内存之后不对内存进行初始化，直接返回申请内存的指针。 所以在 new 时，会调用 operator new，delet 时会调用 operator delete，来分配和释放内存。STL提供三个重载版本，一个抛出异常(bad_alloc)，一个不抛出异常，一个用来做 placement new，在传入指针的地址上构建对象。

        > - 也就是说，new operator 是关键字。但是 operator new 是一个可以重载的操作符。在调用 new operator 时，分配内存这一步是由 operator new(sizeof A) 完成的，如果有重载版本则会执行重载版本。

    * 3）[new[]与delete[]？](../C++/C++对象模型.md#4针对数组的new语意)（步骤：如何分配内存，构建对象、如何析构与释放内存？[构造与析构](../C++/C++对象模型.md#3对象数组)）
        > - 用于分配和删除内置数组对象。需要成对出现。
        > - new[] 时先分配内存，然后逐个调用构造函数构造对象。delete[]时先逐个析构对象，再释放内存。
        > - 注意不要 typedef 数组类型，因为会忘记使用 delete[]

    * 4）new带括号和不带的区别？（无自定义构造函数时，不带括号的new只分配内存，带括号的new会初始化为0）

    * 5）new时内存不足？（[《Effective C++:条款49》](https://github.com/arkingc/note/blob/master/C++/EffectiveC++.md#%E6%9D%A1%E6%AC%BE49%E4%BA%86%E8%A7%A3new-handler%E7%9A%84%E8%A1%8C%E4%B8%BA)）(new-handler)
        > - 抛出 bad_alloc 异常
        > - 在抛出异常前，会执行用户传入的一个 new_handler 函数。通过 set_new_handler()传入函数指针来指定。

    * 6）[malloc](https://github.com/arkingc/note/blob/master/%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F/UNIX%E7%8E%AF%E5%A2%83%E9%AB%98%E7%BA%A7%E7%BC%96%E7%A8%8B.md#5%E5%AD%98%E5%82%A8%E7%A9%BA%E9%97%B4%E5%88%86%E9%85%8D)、[calloc](https://github.com/arkingc/note/blob/master/%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F/UNIX%E7%8E%AF%E5%A2%83%E9%AB%98%E7%BA%A7%E7%BC%96%E7%A8%8B.md#5%E5%AD%98%E5%82%A8%E7%A9%BA%E9%97%B4%E5%88%86%E9%85%8D)、[realloc](https://github.com/arkingc/note/blob/master/%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F/UNIX%E7%8E%AF%E5%A2%83%E9%AB%98%E7%BA%A7%E7%BC%96%E7%A8%8B.md#5%E5%AD%98%E5%82%A8%E7%A9%BA%E9%97%B4%E5%88%86%E9%85%8D)、[alloca](https://blog.csdn.net/lan120576664/article/details/38078855)
        > - malloc 在内存的动态存储区中分配一块长度为size字节的连续区域，size为需要的内存空间的长度，返回该区域的地址。不会初始化分配的内存。
        > - calloc 在内存的动态存储区中分配一块长度为nmemb(参数个数)*size（单位元素长度）字节的连续区域。calloc会将所分配的空间中的每一位都初始化为零
        > - realloc 是给一个已经分配了地址的指针重新分配空间，参数ptr为原有的空间地址， size是重新申请的地址空间。返回的指针可能指向新地址。
        > - malloc原理： 将可用的内存连接为一个长长的链表（即所谓的空闲链表）。调用malloc函数时，它沿连接表寻找一个大到足以满足用户请求所需要的内存块，然后将该内存块一分为二（一块的大小与用户申请的大小一样，另一块就是剩下的字节），接下来，将分配给用户的那块内存传给用户，并将剩下的那块（如果有的话），返回到链表上，调用free函数时，它将用户释放的内存块连接到空链上，到最后，空闲链表会被切成很多的小内存片段，如果这时用户申请一个大的内存片段，那么空闲链上可能没有可能满足用户要求的片段了，于是malloc函数请求延时，并开始在空间中翻箱倒柜的检查内存片段，对它们进行整理，并将相邻的小空闲块合成较大的内存块

    * 7）调用malloc函数之后，OS会马上分配内存空间吗？（不会，只会返回一个虚拟地址，待用户要使用内存时，OS会发出一个缺页中断，此时，内存管理模块才会为程序分配真正内存）

    * 8）[delete](https://github.com/arkingc/note/blob/master/C++/C++%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B.md#1new)（步骤、delete与析构、可以delete空指针、可以delete动态const对象）

    * 9）为什么要内存对齐？([性能原因、平台原因](temp/C++.md/#1为什么要内存对齐))
        > - 编译器为了便于CPU快速访问而采用的一项技术。只能从特定倍数的地址开始取值。
        > - 内存对齐可以提高存取效率（例如，有些平台每次读都是从偶地址开始，如果一个int型存放在偶地址开始的地方，那么一个读周期就可以读出这32bit，而如果存放在奇地址开始的地方，就需要2个读周期，并且要对两次读出的结果的高低字节进行拼凑才能得到这32bit的数据）
        > - 各个硬件平台对存储空间的处理有很大的不同，一些平台对某些特定类型的数据只能从某些特定地址开始存取，例如，有些架构的CPU在访问一个没有对齐的变量时会发生错误，那么这时候编程必须保证字节对齐

    * 10）[struct内存对齐方式？](https://github.com/arkingc/llc/blob/master/cpp/alignment/struct.cpp#L1)
        > - 结构体的大小等于结构体内最大成员大小的整数倍
        > - 结构体内的成员的首地址相对于结构体首地址的偏移量是其类型大小的整数倍(比如说double型成员相对于结构体的首地址的地址偏移量应该是8的倍数)
        > - 为了满足规则1和2编译器会在结构体成员之后进行字节填充
        > - 64位系统遵循8字节对齐，32位遵循4字节对齐

    * 11）如何取消内存对齐？（添加预处理指令`#pragma pack(1)`）
    * 12）什么是内存泄露？如何检测与避免？（Mtrace，[valgrind](temp/C++.md/#2valgrind)）

    * 13）[智能指针相关](https://mubu.com/doc/BGwWx-huk)
        * 种类、区别、原理、能否管理动态数组
            > unique_ptr 可以直接管理动态数组。shared_ptr 不可以。
        * shared_ptr（使用、计数的变化，get()函数要注意什么）
            > get()时要注意一旦shared_ptr指向的对象被释放，则get()返回的指针为空悬指针。
        * unique_ptr(如何转移控制权)
            > release()
        * [weak_ptr(特点、用途：可以解决shared_ptr的循环引用问题)](https://www.cnblogs.com/DswCnblog/p/5628314.html)
            > 还可以通过尝试升级成 shared_ptr 来检测其指向的对象是否已经被释放。只能通过升级后的 shared_ptr 来对对象进行操作。
        * 手写实现智能指针

    * 14）[实现memcpy](../数据结构与算法/算法题总结.md#1实现memcpy)
        > - void *memcpy(void*dest, const void *src, size_t n);
        > - 由src指向地址为起始地址的连续n个字节的数据复制到以destin指向地址为起始地址的空间内。

    * 15）memcpy与memmove的区别（前者不处理重叠，后者处理重叠）
        > memmove() 更为灵活，当src 和 dest 所指的内存区域重叠时，memmove() 仍然可以正确的处理，不过执行效率上会比使用 memcpy() 略慢些。

    * 16）[能否使用memcpy比较两个结构体对象？](https://blog.csdn.net/peng314899581/article/details/60766892)
        > 不能比较。关键是存在内存对齐问题。剩余部分不知道是什么。

    * 17）实现[strlen](../数据结构与算法/算法题总结.md#1实现strlen)、[strcmp](../数据结构与算法/算法题总结.md#2实现strcmp)、[strcat](../数据结构与算法/算法题总结.md#3实现strcat)、[strcpy](../数据结构与算法/算法题总结.md#4实现strcpy)

* **五.STL**
    * 1）[顺序容器与关联容器的比较？](https://blog.csdn.net/JIEJINQUANIL/article/details/51175858)[有哪些顺序容器与关联容器？](https://github.com/arkingc/note/blob/master/pic/stl-4-1.jpeg)
        > 关联容器是通过键(key)存储和读取元素的，而顺序容器则通过元素在容器中的位置顺序存储和访问元素。

    * 2）[vector底层的实现](https://github.com/arkingc/note/blob/master/C++/STL%E6%BA%90%E7%A0%81%E5%89%96%E6%9E%90.md#1vector)（迭代器类型为随机迭代器）？insert具体做了哪些事？[resize()](https://github.com/arkingc/note/blob/master/C%2B%2B/tass-sgi-stl-2.91.57-source/stl_vector.h#L209)调用的是什么？
        > - 容量会自动扩充。增加新元素时，如果超过当时容量，则容量会至少增加到两倍，仍不足则扩的更大。（如果原位置内存不够，则需要重新配置、移动元素、释放原内存）。
        > - 内部使用三个指针表示，分别指向当前头部，元素尾部和实际空间的尾部。size = 元素尾部-元素头部， capacity = 实际空间的尾部-元素头部.
        > - insert 时，所有后边的元素都要往后移动一位，如果已满则分配更大内存。erase()也类似，所以不要求顺序性的话，可以将要删除的元素换到末尾删除。  
  
    * 3）vector的push_back要注意什么（大量调用会伴随大量的拷贝构造与析构，内存分配与释放）
        > - 最好提前分配好空间，或给出建议大小。  
    
    * 4）emplace_back()
        > - 与 push_back()对应。可以直接接受参数来直接调用构造函数初始化对象，而push_back()不行。

    * 5）vector的resize()与[reserve()](https://github.com/arkingc/note/blob/master/C%2B%2B/tass-sgi-stl-2.91.57-source/stl_vector.h#L129)（[测试程序](https://github.com/arkingc/llc/blob/master/cpp/container/vector/size.cpp#L5)）
        > - reserve(n) 用来给vector分配capacity值，推荐预分配内存大小，实际有可能分配的更多。当传入的 n < size时，reserve() 什么都不会做。
        > - 对于resize(n)，当n < size()时会删除多余元素，capacity不变；n > size() 时会增加元素并初始化；n > capacity()时还会重新分配内存。

    * 6） shirink_to_fit()
        > - erase()和resize()缩小size时不会改变capacity，可以使用 shirink_to_fit()建议编译器缩小capacity至 size，但是编译器可能会拒绝，不一定能保证退回内存空间。

    * 7）[如何释放vector的空间？](https://blog.csdn.net/u014774781/article/details/48197891)（swap）、[容器的元素类型为指针？](https://blog.csdn.net/u014774781/article/details/48197891)（会有内存泄露，[指针是trivial_destructor](https://github.com/arkingc/note/blob/master/C%2B%2B/tass-sgi-stl-2.91.57-source/stl_construct.h#L72)；也可以使用智能指针来管理）
        > - 如果   vector   中存放的是指针，那么当   vector   销毁时，那些指针指向的对象不会被销毁，那些内存不会被释放。

    * 8）[vector的clear](https://github.com/arkingc/note/blob/master/C%2B%2B/tass-sgi-stl-2.91.57-source/stl_vector.h#L210)与[deque的clear](https://github.com/arkingc/note/blob/master/C%2B%2B/tass-sgi-stl-2.91.57-source/stl_deque.h#L774)（vector的erase和clear只会析构不会释放内存，deque的erase和clear不但会析构，还可能会释放缓冲区）

    * 9）[vector的迭代器失效](https://www.cnblogs.com/wxquare/p/4699429.html)？
        > - 对于 vector，当插入时，当capacity不改变时，只失效之后的迭代器，否则全部失效。删除时被删除节点后所有迭代器失效。
        > - 对于list、set、map，插入时所有迭代器不失效；删除时只有被删除节点的迭代器失效。

    * 7）[list的底层实现](https://github.com/arkingc/note/blob/master/C++/STL%E6%BA%90%E7%A0%81%E5%89%96%E6%9E%90.md#23-list%E7%9A%84%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84)（迭代器类型为双向迭代器）
        > - 是一个环状双向链表，所以只需一个指针就可以完整实现整个链表。

    * 8）[deque的底层实现](https://github.com/arkingc/note/blob/master/C++/STL%E6%BA%90%E7%A0%81%E5%89%96%E6%9E%90.md#33-deque%E7%9A%84%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84)（迭代器类型为随机迭代器）
        > - deque采用一块所谓的map作为主控(中控器)。这里所谓的map是指一小块连续空间，其中每个元素都是一个指针，指向另一段（较大的）连续线性空间，称为缓冲区。缓冲区才是deque的存储空间主体。
        > - deque除了维护一个指向map的指针外，也维护start，finish两个迭代器。分别指向第一缓冲区的第一个元素和最后缓冲区的最后一个元素（的下一位置）。此外，也必须记住目前的map大小。因为一旦map所提供的节点不足，就必须重新配置更大的一块map

    * 9）vector与deque的区别？（deque能以常数时间在首尾插入元素；deque没有capacity的概念）
    * 10）[map](https://github.com/arkingc/note/blob/master/C++/STL%E6%BA%90%E7%A0%81%E5%89%96%E6%9E%90.md#3map)、[set](https://github.com/arkingc/note/blob/master/C++/STL%E6%BA%90%E7%A0%81%E5%89%96%E6%9E%90.md#2set)的实现原理（红黑树、对于set来说key和value合一，value就是key，map的元素是一个pair，包括key和value、set不支持[]，map(不包括multimap)支持[]）
    * 11）set(map)和multiset(multimap)的区别？
        > - set不允许key重复,其insert操作调用rb_tree的insert_unique函数，multiset允许key重复,其insert操作调用rb_tree的insert_equal函数
        > - 而且set的迭代器是 const_iterator，因此不允许更改。这其实是有道理的，因为 set 的值本身就是 key，

    * 12）set(multiset)和map(multimap)的迭代器（由于set(multiset)key和value合一，迭代器不允许修改key、map(multimap)除了key有data，迭代器允许修改data不允许修改key）
    * 13）map与[unordered_map](https://blog.csdn.net/hk2291976/article/details/51037095)的区别？（hash_map需要hash函数及等于函数，map只需小于函数）
        > 存储的对象都是pair，map会按key排序，unordered_map不会。map底层是红黑树，unordered_map是hash_table

    * 14）set(multiset)和map(multimap)的迭代器[++操作、--操作的时间复杂度](https://github.com/arkingc/note/blob/master/C++/STL%E6%BA%90%E7%A0%81%E5%89%96%E6%9E%90.md#12-rb-tree%E7%9A%84%E8%BF%AD%E4%BB%A3%E5%99%A8)？
        > RB-tree迭代器属于双向迭代器，但不具备随机定位能力。前进操作operator++()调用了基类迭代器的increment()，后退操作operator--()调用了基类迭代器的decrement()。前进或后退的举止行为完全依据二叉搜索树的节点排列法则.O(1)

    * 15）空间分配器allocator
        - [将new和delete的2阶段操作分离](https://github.com/arkingc/note/blob/master/C++/STL%E6%BA%90%E7%A0%81%E5%89%96%E6%9E%90.md#%E4%BA%8C%E7%A9%BA%E9%97%B4%E5%88%86%E9%85%8D%E5%99%A8)（construct和destroy负责内存分配？allocate和deallocate负责对象构造析构？）
        - [SGI符合部分标准的空间分配器——std::allocator](https://github.com/arkingc/note/blob/master/C++/STL%E6%BA%90%E7%A0%81%E5%89%96%E6%9E%90.md#%E4%BA%8C%E7%A9%BA%E9%97%B4%E5%88%86%E9%85%8D%E5%99%A8)
        - [SGI特殊的空间分配器——std::alloc](https://github.com/arkingc/note/blob/master/C++/STL%E6%BA%90%E7%A0%81%E5%89%96%E6%9E%90.md#3sgi%E7%89%B9%E6%AE%8A%E7%9A%84%E7%A9%BA%E9%97%B4%E5%88%86%E9%85%8D%E5%99%A8stdalloc)（[对象构造与析构](https://github.com/arkingc/note/blob/master/C++/STL%E6%BA%90%E7%A0%81%E5%89%96%E6%9E%90.md#31-%E5%AF%B9%E8%B1%A1%E6%9E%84%E9%80%A0%E4%B8%8E%E6%9E%90%E6%9E%84)、内存分配与释放——[两级分配器](https://github.com/arkingc/note/blob/master/C++/STL%E6%BA%90%E7%A0%81%E5%89%96%E6%9E%90.md#1%E4%B8%A4%E7%BA%A7%E5%88%86%E9%85%8D%E5%99%A8)）
            + [第一级分配器](https://github.com/arkingc/note/blob/master/C++/STL%E6%BA%90%E7%A0%81%E5%89%96%E6%9E%90.md#2%E7%AC%AC%E4%B8%80%E7%BA%A7%E5%88%86%E9%85%8D%E5%99%A8__malloc_alloc_template)（如何仿真new-handler机制？不能直接用C++ new-handler，因为没有使用::operator new）
            + [第二级分配器](https://github.com/arkingc/note/blob/master/C++/STL%E6%BA%90%E7%A0%81%E5%89%96%E6%9E%90.md#3%E7%AC%AC%E4%BA%8C%E7%BA%A7%E5%88%86%E9%85%8D%E5%99%A8__default_alloc_template)（为什么要二级分配器？内存池与16个free-list？空间分配和释放的步骤？）
    * 16）[traits与迭代器相应类型](https://github.com/arkingc/note/blob/master/C++/STL%E6%BA%90%E7%A0%81%E5%89%96%E6%9E%90.md#2traits%E7%BC%96%E7%A8%8B%E6%8A%80%E6%B3%95)
        > - 类型萃取：例如当对vector进行拷贝的时候，如果对象是基本类型则直接malloc即可，如果是类类型则需要执行new。类型萃取可以实现对不同的类型去执行不同的函数。
        > - 萃取是根据模板的特化实现的，例如提前定义好哪些类型属于“可以执行直接malloc的类型”，哪些类型属于“需要执行new的类型”，然后在执行时根据传入的类型进行判断。
        > - 为了符合规范，任何迭代器都应该提供5个内嵌相应类型，以便于traits萃取，否则便是自别于整个STL架构，可能无法与其它STL组件顺利搭配。可以直接继承自stl提供的iterator class.
* **六.对象内存模型**
    * **数据成员**
        - [成员变量在类对象中的布局规则](https://github.com/arkingc/note/blob/master/C++/C++%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B.md#32-data-member%E7%9A%84%E5%B8%83%E5%B1%80)
            > - C++标准要求，同一access section中，members的排列只需符合“较晚出现的members在class object中有较高的地址”即可，各个members并不一定得连续排列。
            > - vptr一般不是放在对象开头就是放在末尾。
            > - C++标准允许多个access sections之中的data memebers自由排列，不必在乎它们出现在class声明中的顺序
            > - access section指的是private、protected、public等区段。

        - [通过指针和通过'.'进行Data Member存取的区别](https://github.com/arkingc/note/blob/master/C++/C++%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B.md#33-data-member%E7%9A%84%E5%AD%98%E5%8F%96)
            > - 欲对一个nonstatic data member进行存取操作，编译器需要把class object的起始位置加上data member的偏移位置。每一个nonstatic data member的偏移位置在编译时期即可获知，甚至如果member属于一个“基类子对象”也是一样，因此，存取一个nonstatic data member的效率和存取一个C struct member或一个非派生类的member是一样的。
            > - 但是，虚继承将为“经由基类子对象存取class members”导入一层新的间接性，如果通过指针存取，这个存取操作必须延迟至执行期，经由一个额外的间接引导才能解决

        - 数据成员的布局——[无继承](https://github.com/arkingc/note/blob/master/C++/C++%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B.md#33-data-member%E7%9A%84%E5%AD%98%E5%8F%96)
        - 数据成员的布局——[不含多态的继承](https://github.com/arkingc/note/blob/master/C++/C++%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B.md#2%E4%B8%8D%E5%90%AB%E5%A4%9A%E6%80%81%E7%9A%84%E7%BB%A7%E6%89%BF)（C++标准并未强制指定派生类和基类成员的排列顺序；理论上编译器可以自由安排。在大部分编译器上，基类成员总是先出现，虚基类除外）
        - 数据成员的布局——[含多态的继承](https://github.com/arkingc/note/blob/master/C++/C++%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B.md#3%E5%90%AB%E5%A4%9A%E6%80%81%E7%9A%84%E7%BB%A7%E6%89%BF)（vptr的位置也没有强制规定，放在不同位置分别有什么好处？）
        - 数据成员的布局——[多重继承](https://github.com/arkingc/note/blob/master/C++/C++%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B.md#4%E5%A4%9A%E9%87%8D%E7%BB%A7%E6%89%BF)（基类子对象的排列顺序也没有硬性规定；指针的调整方式？）
        - 数据成员的布局——[虚继承](https://github.com/arkingc/note/blob/master/C++/C++%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B.md#5%E8%99%9A%E7%BB%A7%E6%89%BF)（虚基类子对象的偏移信息记录在虚函数表之前与使用一个额外指针来记录的对比？）
        - [指向数据成员的指针](https://github.com/arkingc/note/blob/master/C++/C++%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B.md#35-%E6%8C%87%E5%90%91data-members%E7%9A%84%E6%8C%87%E9%92%88)
    * **函数成员**
        - [nonstatic成员函数的转换](https://github.com/arkingc/note/blob/master/C++/C++%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B.md#41-member%E7%9A%84%E5%90%84%E7%A7%8D%E8%B0%83%E7%94%A8%E6%96%B9%E5%BC%8F)（目的是为了提供和一般非成员函数相同的效率）
            > 编译器内部会将”member函数实例“转换为对等的”nonmember函数实例“.改写函数原型，安插一个额外的this指针作为参数到member function中（有点像python?）,将每一个”对nonstatic data member的存取操作“改为经由this指针来存取.
        - [重载成员函数的名字处理](https://github.com/arkingc/note/blob/master/C++/C++%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B.md#%E6%88%90%E5%91%98%E5%87%BD%E6%95%B0%E9%87%8D%E8%BD%BD%E7%9A%84%E5%A4%84%E7%90%86)
            > 对于重载的成员函数，会加上类名。
        - [static成员函数的转换](https://github.com/arkingc/note/blob/master/C++/C++%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B.md#2static-member-functions%E9%9D%99%E6%80%81%E6%88%90%E5%91%98%E5%87%BD%E6%95%B0)
            > static成员函数会转成不接收this指针的一般函数。
        - [编译器如何处理经由指针和经由‘.’进行的调用](https://github.com/arkingc/note/blob/master/C++/C++%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B.md#3virtual-member-functions%E8%99%9A%E5%87%BD%E6%95%B0)
            > 通过.调用则直接调用该静态类型的成员函数。通过->的调用，如果是虚函数会找到在虚函数表中的索引值，调用对应的虚函数。
        - [指向函数成员的指针](https://github.com/arkingc/note/blob/master/C++/C++%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B.md#43-%E6%8C%87%E5%90%91member-function%E7%9A%84%E6%8C%87%E9%92%88)
            > - 取一个nonstatic memeber function的地址，如果函数非虚，得到的结果是它在内存中真正的地址
            > - static member functions(没有this指针)的类型是“函数指针”，而不是“指向member function的指针”
            > - 对于没有继承、虚函数等情况下，前边两者效率相同。

        - 虚函数的调用——[单继承](https://github.com/arkingc/note/blob/master/C++/C++%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B.md#1%E5%8D%95%E7%BB%A7%E6%89%BF%E4%B8%AD%E7%9A%84%E8%99%9A%E5%87%BD%E6%95%B0)
            > 对于单继承，编译器虽然不知道会调用哪张虚函数表中的函数，但是却可以在编译期就确定该函数在虚函数表中的偏移量。
        - 虚函数的调用——[多重继承](https://github.com/arkingc/note/blob/master/C++/C++%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B.md#2%E5%A4%9A%E7%BB%A7%E6%89%BF%E4%B8%AD%E7%9A%84%E8%99%9A%E5%87%BD%E6%95%B0)（子类对象关联有多少个虚函数表？不同虚函数表的名称？执行期什么情况下如何调整this指针？）
            > 必须在执行期调整this指针。这里不太懂。。 为啥要多继承？不用不行么
* **七.关键字**
    * 1）extern？（extern "C"?、与static？、有什么问题？、extern的时候定义变量？）
        > extern声明可以拷贝n次，但是定义只能定义一次。
        > 与 static 相比，参照前边的全局变量和static变量的对比。
    * 2）const？（修饰变量、修饰指针与引用、修饰成员函数 [《Effective C++:条款3》](https://github.com/arkingc/note/blob/master/C++/EffectiveC++.md#%E6%9D%A1%E6%AC%BE03%E5%B0%BD%E5%8F%AF%E8%83%BD%E4%BD%BF%E7%94%A8const)）
        > - 修饰变量：表示该变量不可更改
        > - 修饰指针：表示该指针的指向不可更改，但所指的对象可以更改（除非也是const）
        > - 引用本身就不可更改
        > - 修饰成员函数表示保证该成员函数不会修改成员变量。
        > - 修饰返回值：表示该返回值不可更改

    * 3）mutable？
        > - mutable 是为了突破 const 的限制而设置的。被 mutable 修饰的变量，将永远处于可变的状态，即使在一个 const 函数中，甚至结构体变量或者类对象为 const，其 mutable 成员也可以被修改。
        > - mutable 在类中只能够修饰非静态数据成员。
        > - 可以被 const 成员函数修改。

    * 4）[static](https://www.nowcoder.com/ta/nine-chapter/review?page=15)？（修饰变量、类中使用）
    * 5）[define与const](https://www.nowcoder.com/questionTerminal/a60c01a7c4ab473e81218ed0b333b4e6)、enum、inline？（[《Effective C++:条款2》](https://github.com/arkingc/note/blob/master/C++/EffectiveC++.md#%E6%9D%A1%E6%AC%BE02%E5%B0%BD%E9%87%8F%E4%BB%A5constenuminline%E6%9B%BF%E6%8D%A2define)、C中默认const是外部连接的，而C++中默认const是内部连接的）
        > - const：有数据类型，编译进行安全检查，可调试 
        > - define:宏，不考虑数据类型，没有安检，不能调试 ，而且不重视作用域。
        > - 因此尽量不要使用define。可以使用inline函数代替define的函数。使用const定义一般常量，使用enum代替类内常量(有些编译器不支持类内初始化const static)。

    * 6）explict?（抑制隐式转换、可通过显示转换或直接初始化解决、类外定义时不应重复出现）
    * 7）noexcept？（承诺不会抛出异常）
    * 8）default、delete?（显示要求编译器合成、不能被调用）
    * 9）using？（用于命名空间？、用于类中？）
    * 10）final？（修饰类？、修饰成员函数？只有虚函数能使用final）
    * 11）auto(初始值为引用时类型为所引对象的类型、必须初始化、不能用于函数及模板)、decltype？
        > decltype与auto关键字一样，用于进行编译时类型推导，不过它与auto还是有一些区别的。decltype的类型推导并不是像auto一样是从变量声明的初始化表达式获得变量的类型，而是总是以一个普通表达式作为参数，返回该表达式的类型,而且decltype并不会对表达式进行求值。

    * 12）volatile?（对象的值可能在程序的控制外被改变时，应将变量申明为volatile，告诉编译器不应对这样的对象进行优化，如果优化，从内存读取后CPU会优先访问数据在寄存器中的结果，但是内存中的数据可能在程序之外被改变、可以既是const又是volatile，const只是告诉程序不能试图去修改它.volatile是告诉编译器不要优化，因为变量可能在程序外部被改变）
* **八.其它**
    * 1）调试程序的方法?（[gdb](https://github.com/arkingc/note/blob/master/Linux/Linux%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4.md#3%E8%B0%83%E8%AF%95%E5%B7%A5%E5%85%B7gdb)）
    * 2）遇到coredump要怎么调试？
        > - Coredump叫做核心转储，它是进程运行时在突然崩溃的那一刻的一个内存快照。操作系统在程序发生异常而异常在进程内部又没有被捕获的情况下，会把进程此刻内存、寄存器状态、运行堆栈等信息转储保存在一个文件里。
        > - 可以使用gdb打开分析。查找错误出现的代码的位置。
    * 3）模板的用法与适用场景
    * 4）用过C++11？新特性？（auto,decltype、explicit、[lambda](https://mubu.com/doc/1ckW18B1Ak)、final）
    * 5）函数调用的压栈过程
        > 栈中变量分布是从高地址到低地址分布。函数各个参数从右向左逐步压入栈中，最后压入返回地址。然后变量按申明顺序依次存储。出栈顺序与压栈相反。栈帧就是一个函数执行的环境：函数参数、函数的局部变量、函数执行完后返回到哪里等等。
    * 6）[sizeof](https://github.com/arkingc/llc/blob/master/cpp/sizeof.cpp#L4)和strlen的区别？（运算符与函数、计算的对象、编译时运行时）
        > sizeof 本身其实不是函数，是一个操作符
    * 7）union？
        > 一种节省空间的类。一个union可以有多个数据成员，但任意时刻只有一个数据成员可以有值。当给union的某个成员赋值后，其他成员变为未定义状态。
    * 9）C++是不是类型安全的？（不是，两个不同类型指针可以强制转换，reinterpret_cast）
    * 10）gcc和g++的区别？（gcc代表GUN Compiler Collection，是一堆编译器的集合，包括g++）
    * 11）[运行时类型识别实现对象比较函数](https://github.com/arkingc/llc/blob/master/cpp/RTTI/RTTI.cpp#L9)
        > - RTTI, 运行时类型识别。C++通过 typeid 和 dynamic_cast 提供 RTTI.
        > - 对于带虚函数的类，在运行时执行RTTI操作符，返回动态类型信息；对于其他类型，在编译时执行RTTI，返回静态类型信息。
        > - typeid最常见的用途是比较两个表达式的类型，或者将表达式的类型与特定类型相比较。也可以使用 type_info 类提供的函数进行类型比较。

    * 12）[使用C++实现线程安全的单例模式](https://www.cnblogs.com/ccdev/archive/2012/12/19/2825355.html)
    * 13）[什么是异常安全？](../C++/EffectiveC++.md#1异常安全的2个条件)
        > - 当异常被抛出时，带有异常安全性的函数会： __不泄露任何资源__， __不允许数据破坏__
        > - 对于资源泄露，使用RAII即可完美解决。对于数据破坏，可以提供三种级别的保证：基本承诺（同上），强烈保证（失败会回到调用前的状态），不抛掷保证。
    * 14）全特化和偏特化
        > 全特化是对所有模板参数特化，都定死；偏特化是只特化其中一部分模板参数，而且还可以对参数做出一些要求，例如特化接收参数的指针或引用的情况。
    * 15）lambda表达式
        > - lambda表达式被编译器编译为一个未命名类的未命名对象，在其产生的类中有一个重载的函数调用运算符。
        > - 对于其捕获值列表：
        >   - =， 函数体内可以使用Lambda所在作用范围内所有可见的局部变量（包括Lambda所在类的this），并且是值传递方式（相当于编译器自动为我们按值传递了所有局部变量）。
        >   - &， 同上，但是是引用方式
        >   - this, 函数体内可以使用Lambda所在类中的成员变量。
        >   - =，&a, &b, 除a和b按引用进行传递外，其他参数都按值进行传递。
    * 16）匿名 namespace
        > 编译器会自动生成一个 unique_name，并自动using此命名空间。名称的作用域被限制在当前文件中，无法通过在另外的文件中使用extern声明来进行链接。
    * 17）std::bind()
        > 用于生成一个可调用对象，并且绑定一部分参数。当绑定成员函数时，传入的第一个参数必须是this指针。未绑定的参数用 std::placeholder 占位符代替。

    * 18）一个C++源文件从文本到可执行文件经历的过程
        > - 预处理，产生.ii文件
        > - 编译，产生汇编文件(.s文件)
        > - 汇编，产生目标文件(.o或.obj文件)
        > - 链接,产生可执行文件(.out或.exe文件)

    * 19）无锁数据结构
        > 无锁机制的实现是基于CPU提供的一种原子操作CAS（Compare and Swap），CAS是这样工作的，它会原子地将一块内存的值与一个给定的值进行比较，如果它们相等就用新值替换返回true，否则什么也不做直接返回false。