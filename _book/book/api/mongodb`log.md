# MonggoDB



***


  使用数据库和集合前不用建立，执行插入数据时会自动建立


***

这里的mongodb连接视频里还没有讲
(http://www.runoob.com/mongodb/mongodb-connections.html)


***


`alt+t 是新建一个窗口，在打开mongo之后，新建窗口后输入monge才能进入命令
使用alt+d也行`


***


### 文档
文档是一组键值对


需要注意的是：
  * 文档中的键/值对是有序的。
  * 文档中的值不仅可以是在双引号里面的字符串，还可以是其他几种数据类型（甚至可以是整个嵌入的文档)。
  * MongoDB区分类型和大小写。
  * MongoDB的文档不能有重复的键。
  * 文档的键是字符串。除了少数例外情况，键可以使用任意UTF-8字符。

文档键命名规范：
  * 键不能含有\0 (空字符)。这个字符用来表示键的结尾。
  * .和$有特别的意义，只有在特定环境下才能使用。
  * 以下划线"_"开头的键是保留的(不是严格要求的)。


***

### 集合
* 集合就是 MongoDB 文档组
* 集合没有固定的结构，这意味着你在对集合可以插入不同格式和类型的数据，但通常情况下我们插入集合的数据都会有一定的关联性。


***

常用命令：
  * use db_name（切换到指定数据库）
  >如:use test就是切换到test数据库
  * db.库名.insert(...) （向集合foo插入文档）

  *或db.库名.insert(...)*
  >此处的db指的就是目前所在的数据库
  >如:db.blogg.insert({'id':1,'tetle':'MyBloge'})就是将这两个对象插入test库下的blogg表
  * db.库名.find() （查询集合foo文档）
  >如:db.blogg.find()就是查询显示blogg表中的内容
  >如:db.blogg,find({'id':1})就是查询id为1的文档
  * db.库名.findOne() （查询集合foo文档，显示方式不同）
  >显示方式为按排序
  * db.库名.update() （更新集合foo文档）
    1. '$set' 增加或修改指定键值对
    ```
格式如：
            db.集合名.update(
            <查询对象键值对>,
           <update(如：($set)($inc))>,
           {
             upsert: <boolean>,(若不存在，是否插入)
             multi: <boolean>,(是否只更新找到的第一条信息)
             writeConcern: <document>(抛出异常的级别)
           }
          )```
      > 如db.blogg.update({'id':2},{'$set':'YourBlog'}})

      > 就是将blogg表中di为2的键，其值改为'$set'指定的值
    2. '$unset' 删除指定的键，及其值
    3. '$inc' 增减指定键的值，符合条件的第一个
    4.
  *

***
