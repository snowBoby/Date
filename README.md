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
* Date.parse(..)：接收一个表示日期的**字符串参数**，然后尝试根据这个字符串返回相应日期的毫秒数。如果字符串不能表示日期，那么它会返回NaN。ECMA-262没有定义Date.parse()应该支持哪种日期格式，因此这个方法的行为因实现而异，而且通常是因地区而异。将地区设置为美国的浏览器通常都接受下列日期格式：
  * 月/日/年”，如6/13/2004；
  * “英文月名日,年”，如January 12,2004；
  * “英文星期几英文月名日年时:分:秒时区” ，如Tue May 25 2004 00:00:00 GMT-0700。
  * ISO  8601扩展格式YYYY-MM-DDTHH:mm:ss.sssZ（例如2004-05-25T00:00:00）。只有兼容ECMAScript 5的实现支持这种格式。
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
| 方  法 | 说  明 |
| --- | --- |
| getTime() | 返回表示日期的毫秒数；与valueOf()方法返回的值相同 |
| setTime(毫秒) | 以毫秒数设置日期，会改变整个日期 |
| getFullYear() | 取得4位数的年份（如2007而非仅07） |
| getUTCFullYear() | 返回UTC日期的4位数年份 |
| setFullYear(年) | 设置日期的年份。传入的年份值必须是4位数字（如2007而非仅07） |
| setUTCFullYear(年) | 设置UTC日期的年份。传入的年份值必须是4位数字（如2007而非仅07） |
| getMonth() | 返回日期中的月份，其中0表示一月，11表示十二月 |
| getUTCMonth() | 返回UTC日期中的月份，其中0表示一月，11表示十二月 |
| setMonth(月) | 设置日期的月份。传入的月份值必须大于0，超过11则增加年份 |
| setUTCMonth(月) | 设置UTC日期的月份。传入的月份值必须大于0，超过11则增加年份|
| getDate() | 返回日期月份中的天数（1到31）|
| getUTCDate() | 返回UTC日期月份中的天数（1到31）|
| setDate(日) | 设置日期月份中的天数。如果传入的值超过了该月中应有的天数，则增加月份 |
| setUTCDate(日) | 设置UTC日期月份中的天数。如果传入的值超过了该月中应有的天数，则增加月份|
| getDay() | 返回日期中星期的星期几（其中0表示星期日，6表示星期六）|
| getUTCDay() | 返回UTC日期中星期的星期几（其中0表示星期日，6表示星期六）|
| getHours() | 返回日期中的小时数（0到23）|
| getUTCHours() | 返回UTC日期中的小时数（0到23）|
| setHours(时) | 设置日期中的小时数。传入的值超过了23则增加月份中的天数 |
| setUTCHours(时) | 设置UTC日期中的小时数。传入的值超过了23则增加月份中的天数 |
| getMinutes() | 返回日期中的分钟数（0到59）| | getUTCMinutes() | 返回UTC日期中的分钟数（0到59）|
| setMinutes(分) | 设置日期中的分钟数。传入的值超过59则增加小时数 |
| setUTCMinutes(分) | 设置UTC日期中的分钟数。传入的值超过59则增加小时数 |
| getSeconds() | 返回日期中的秒数（0到59） | 
| getUTCSeconds() | 返回UTC日期中的秒数（0到59）| 
| setSeconds(秒) | 设置日期中的秒数。传入的值超过了59会增加分钟数 |
| setUTCSeconds(秒) | 设置UTC日期中的秒数。传入的值超过了59会增加分钟数 |
| getMilliseconds() | 返回日期中的毫秒数 |
| getUTCMilliseconds() | 返回UTC日期中的毫秒数 |
| setMilliseconds(毫秒) |设置日期中的毫秒数|
| setUTCMilliseconds(毫秒) | 设置UTC日期中的毫秒数|
| getTimezoneOffset() | 返回本地时间与UTC时间相差的分钟数。例如，美国东部标准时间返回300。在某地进入夏令时的情况下，这个值会有所变化 |

![补充图片](https://github.com/snowBoby/Date/blob/master/images/date_1.png)
![补充图片](https://github.com/snowBoby/Date/blob/master/images/date_2.png)
![补充图片](https://github.com/snowBoby/Date/blob/master/images/date2.png)

### 5、本地时间与UTC(GMT)时间转换
* UTC(GMT)：整个地球分为二十四时区，每个时区都有自己的本地时间。在国际无线电通信场合，为了统一起见，使用一个统一的时间，称为通用协调时(UTC, Universal Time Coordinated)。UTC与格林尼治平均时(GMT, Greenwich Mean Time)一样，都与英国伦敦的本地时相同。
* 本地时间：北京时区是东八区，领先UTC八个小时，在电子邮件信头的Date域记为+0800。

**注意**：
* 时区差格式为 符号+ 24小时制数字 + 分钟，如：北京与UTC时差记为+0800
* 时区差东为正，西为负。

**公式**：
* UTC = 本地时间 - 时区差
* UTC = 本地时间 + getTimezoneOffset(); 在Javascript中，Date对象提供了获取本地与UTC(GMT)时间差的函数getTimezoneOffset,该方法可返回格林威治时间和本地时间之间的时差，以分钟为单位。
