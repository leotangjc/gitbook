[安装见](http://www.jianshu.com/p/6b5eca8d908b)<br>
<br>
* string类型操作<br>
  * 使用``set 键 值``的方法进行写入操作<br>
  * 使用``get 键``的方式查看该键的值<br>
  * 使用``incr 键``的方式可以让数字值自加一<br>
  * 使用``decrby 键 数量``可让指定数字值减去指定数<br>
  list类型操作<br>
  * list列表的基本操作是push和pop，就如这两个动词，传入和读取元素时，就像对实体进行操作一样，一直使用lpush从左边推入的话，使用rpop从右边读取到的第一个数，就是最早推入的那个数<br>
* set类型操作<br>
  * 与上面的list类型的有序列表不同，set是无序列表<br>
  * 使用sadd添加元素<br>
  * 使用scard查看指定列表名下的元素数<br>
  * 使用sismember查看列表中有没有指定的值<br>
  * 使用srem删除指定值<br>
  * set类型中，相同值的元素会不会重复<br>
* hash类型操作<br>
  * 使用``HMSET 键名 字段1 值1 字段2 值2 ......``对哈希表中添加字段，会覆盖同名字* 段<br>
  * 使用``HGETALL 键名``获取指定键名下的所有值<br>
  * 使用``HDEL 键名 字段1 字段2....``删除指定字段<br>
  * 使用``HVALS 键名``获取哈希表中所有值<br>
  * 使用``HSETNX 键名 字段 值``在字段不存在时，添加值<br>
* sort set类型操作<br>
  * 值必须是唯一的<br>
  * 排名是按照分数从小到大进行排名<br>
  * 若分数一样，则按照值进行排名（转换为数字）<br>
  * 分数值可以是整数值或双精度浮点数<br>
  * 使用``ZADD 键名 分数1 值1 分数2 值2 ....``向指定键名下添加成员元素<br>


>失效？
<font size=1>使用``brew install redis``安装
使用``brew services start redis``启动
redis-server /usr/local/etc/redis.conf
