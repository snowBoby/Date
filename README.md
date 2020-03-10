# Date
Date引用类型；
创建日期对象必须使用new Date()。Date(..)传入的参数必须为日期的毫秒数（即从UTC时间1970年1月1日午夜起至该日期止经过的毫秒数），如果不是毫秒数会在后台调用Date.parse()/Date.UTC()（具体调用哪个主要看参数类型，还有一点明显不同：**构造函数隐式调用Date.UTC()日期和时间都基于本地时区而非GMT来创建**），以此来指定日期和时间，而不带参数的话则使用当前的日期和时间。
```
var someDate = new Date(Date.parse("May 25, 2004"));
//等价于
var someDate = new Date("May 25, 2004");

// GMT时间 2005年5月5日下午5:55:55 
var allFives = new Date(Date.UTC(2005, 4, 5, 17, 55, 55));
//等价于
// 本地时间 2005年5月5日下午5:55:55 
var allFives = new Date(2005, 4, 5, 17, 55, 55); 
```
### 1、Date构造函数的方法：
以下返回的都是毫秒数。
* Date.now()：获取当前时间毫秒数，在不支持它的浏览器中，可以使用+操作符。等价于`+new Date() / (new Date()).getTime()`
* Date.parse(..)：接收一个表示日期的**字符串参数**，然后尝试根据这个字符串返回相应日期的毫秒数。如果字符串不能表示日期，那么它会返回NaN。
* Date.UTC(..)：同样也返回表示日期的毫秒数，参数与Date.parse(..)不同，为年、月（0到11）、日（1到31）、时（0到23）、分、秒以及毫秒数。

### 2、Date实例继承的方法：
与其他引用类型一样，Date类型也重写了toLocaleString()、toString()和valueOf()方法；

* **toLocaleString**()：会按照与浏览器设置的地区相适应的格式返回日期和时间。
* **toString**()：通常返回带有时区信息的日期和时间。
* **valueOf**()：返回日期的毫秒数。

### 3、Date实例特有的日期格式化方法：

* **toDateString**()：以特定于实现的格式显示星期几、月、日和年；
* **toTimeString**()：以特定于实现的格式显示时、分、秒和时区；
* **toLocaleDateString**()：以特定于地区的格式显示星期几、月、日和年；
* **toLocaleTimeString**()：以特定于实现的格式显示时、分、秒；
* **toUTCString**()/**toGMTString**()：以特定于实现的格式完整的UTC日期。toGMTString()确保向后兼容。不过，推荐使用toUTCString()方法

### 4、Date实例日期/时间组件方法：
UTC日期指的是在没有时区偏差的情况下（将日期转换为GMT时间）的日期值。

![Alt text](https://github.com/snowBoby/Date/blob/master/images/date_1.png)
![Alt text](https://github.com/snowBoby/Date/blob/master/images/date_2.png)
![Alt text](https://github.com/snowBoby/Date/blob/master/images/date2.png)
