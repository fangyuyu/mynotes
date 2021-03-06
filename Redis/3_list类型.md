#### 业务场景

+ 微信朋友圈点赞，要求按照点赞顺序显示点赞好友信息, 如果取消点赞，移除对应好友信息。

  ![image-20200810204653576](img\image-20200810204653576.png)

+ 新浪微博、腾讯微博中个人用户的关注列表需要按照用户的关注顺序进行展示，粉丝列表需要将最近关注的粉丝列在前面

  ![image-20200810204825968](img\image-20200810204825968.png)

+ 日志存储，比如下单流程（减库存、生成订单、生成佣金）
  1. 调用商品服务减库存（将异常信息存储 rpush 001:create:order goods_error）
  2. 调用订单服务服务生成订单（将异常信息存储 rpush 001:create:order order_error）
  3. 调用用户服务生成佣金（将异常信息存储 rpush 001:create:order user_error）

#### List类型数据操作的注意事项

1. list中保存的数据都是string类型的，数据总容量是有限的，最多2 32 - 1 个元素 (4294967295)。 
2. list具有索引的概念，但是操作数据时通常以队列的形式进行入队出队操作，或以栈的形式进行入栈出栈操作
3. 获取全部数据操作结束索引设置为-1 
4. list可以对数据进行分页操作，通常第一页的信息来自于list，第2页及更多的信息通过数据库的形式加载