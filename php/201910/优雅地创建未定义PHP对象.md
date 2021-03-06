# 优雅地创建未定义类PHP对象

在PHP中，如果没有事先准备好类，需要创建一个未定义类的对象，我们可以采用下面三种方式：

- new stdClass()
- new class{}
- (object)[]

首先是stdClass，这个类是一个空的类模板，是PHP的内部保留关键字及类名。可以把它相像成是Java中的Object基类，在Java中，所有类都天然继承自Object基类。而PHP中的这个stdClass则是完全的一个空的类模板。你自己新创建的类并不是它的子类。但是用这个类模板可以创建一个自己未定义类的对象。当然，这个对象内部没有任何东西。

```php

$a = new stdClass();
var_dump($a);

```

new class{}呢？做过一段时间开发，接触过前端js和其他动态语言的应该能猜到，这个是匿名类。一般在参数对象中很常见。它创建出来的对象是可以带属性方法的。

```php

$b = new class{
    public $p = 1;
};
var_dump($b);

```

最后我们来看到的是使用数组强转成对象的形式来生成一个对象。

```php

$c = (object)[
    'p' => 1
];
var_dump($c);

```

很明显，数组强转的形式生成的对象和第一种对象是一个类型的，而且它可以带属性也可以不带。但是，它不能带方法。

数组强转方式生成的对象非常的直观好理解。如果只是属性对象的封装，使用这种方式会更加地优雅舒服。复杂的对象生成可以使用匿名类的方式进行生成。而一些仅需要占位的对象，可以使用stdClass的方法，当然用空数组的方式也很方便。

需要注意的是，数组强转需要遵守类型转换的规则。比如数字下标的问题。

在日常开发中，我们对于一些接口或者数据库ORM框架的使用中会经常用这些功能。比如一些ORM框架的插入、修改需要传入的是只包含属性的对象。这时候就可以使用上述的方法灵活地生成对象而不用完整的定义类模板了。

测试代码：
[https://github.com/zhangyue0503/dev-blog/blob/master/php/201910/source/%E4%BC%98%E9%9B%85%E5%9C%B0%E5%88%9B%E5%BB%BA%E6%9C%AA%E5%AE%9A%E4%B9%89PHP%E5%AF%B9%E8%B1%A1.php](https://github.com/zhangyue0503/dev-blog/blob/master/php/201910/source/%E4%BC%98%E9%9B%85%E5%9C%B0%E5%88%9B%E5%BB%BA%E6%9C%AA%E5%AE%9A%E4%B9%89PHP%E5%AF%B9%E8%B1%A1.php)

参考资料：
[https://www.php.net/manual/zh/language.types.object.php#117149](https://www.php.net/manual/zh/language.types.object.php#117149)