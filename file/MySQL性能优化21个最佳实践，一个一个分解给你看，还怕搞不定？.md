# MySQL性能优化21个最佳实践，一个一个分解给你看，还怕搞不定？

数据库的操作越来越成为整个应用的性能瓶颈了，这点对于 Web 应用尤其明显。关于数据库的性能，这并不只是 DBA  才需要担心的事，而这更是我们程序员需要去关注的事情。当我们去设计数据库表结构，对操作数据库时(尤其是查表时的 SQL  语句)，我们都需要注意数据操作的性能。这里，我们不会讲过多的 SQL 语句的优化，而只是针对 MySQL 这一 Web  应用最多的数据库。希望下面的这些21个优化技巧对你有用。



![img](https://upload-images.jianshu.io/upload_images/18375227-8dc710b8aae4e9d3.png?imageMogr2/auto-orient/strip|imageView2/2/w/633)

image.png

> 额...额...额...有点犯懒，就不打字儿了，直接就把每一个的详情内容截图展示出来啦~

# 最佳实践1：为查询缓存优化你的查询

![img](https://upload-images.jianshu.io/upload_images/18375227-fc1f7c7c68faa6f9.png?imageMogr2/auto-orient/strip|imageView2/2/w/613)

最佳实践1：为查询缓存优化你的查询.png

# 最佳实践2：EXPLAIN 你的 SELECT 查询

![img](https://upload-images.jianshu.io/upload_images/18375227-d4d66f9653bd7c5f.png?imageMogr2/auto-orient/strip|imageView2/2/w/416)

最佳实践2：EXPLAIN 你的 SELECT 查询.png

# 最佳实践3： 当只要一行数据时使用 LIMIT 1

![img](https://upload-images.jianshu.io/upload_images/18375227-f1431b68f9fa948a.png?imageMogr2/auto-orient/strip|imageView2/2/w/546)

最佳实践3： 当只要一行数据时使用 LIMIT 1.png

# 最佳实践4：为搜索字段建索引

![img](https://upload-images.jianshu.io/upload_images/18375227-4eb5d2357c2bd9d5.png?imageMogr2/auto-orient/strip|imageView2/2/w/605)

最佳实践4：为搜索字段建索引.png

# 最佳实践5：在 Join 表的时候使用相当类型的例，并将其索引

![img](https://upload-images.jianshu.io/upload_images/18375227-a18529d11d360a12.png?imageMogr2/auto-orient/strip|imageView2/2/w/614)

最佳实践5：在 Join 表的时候使用相当类型的例，并将其索引.png

# 最佳实践6：千万不要 ORDER BY RAND()

![img](https://upload-images.jianshu.io/upload_images/18375227-da36b7817cbb870b.png?imageMogr2/auto-orient/strip|imageView2/2/w/555)

最佳实践6：千万不要 ORDER BY RAND().png

# 最佳实践7：避免 SELECT *

![img](https://upload-images.jianshu.io/upload_images/18375227-08af50022c4fba7b.png?imageMogr2/auto-orient/strip|imageView2/2/w/598)

最佳实践7：避免 SELECT *.png

# 最佳实践8：**永远为每张表设置一个 ID**

![img](https://upload-images.jianshu.io/upload_images/18375227-c6a8dc6f0c5f2ef3.png?imageMogr2/auto-orient/strip|imageView2/2/w/570)

最佳实践8：永远为每张表设置一个 ID.png

# 最佳实践9：使用 ENUM 而不是 VARCHAR

![img](https://upload-images.jianshu.io/upload_images/18375227-a011475bcc8a3559.png?imageMogr2/auto-orient/strip|imageView2/2/w/574)

最佳实践9：使用 ENUM 而不是 VARCHAR.png

# 最佳实践10：从 PROCEDURE ANALYSE() 取得建议

![img](https://upload-images.jianshu.io/upload_images/18375227-2e35d8658321267f.png?imageMogr2/auto-orient/strip|imageView2/2/w/575)

最佳实践10：从 PROCEDURE ANALYSE() 取得建议.png

# 最佳实践11：尽可能的使用 NOT NULL

![img](https://upload-images.jianshu.io/upload_images/18375227-28f608c1629666ac.png?imageMogr2/auto-orient/strip|imageView2/2/w/590)

最佳实践11：尽可能的使用 NOT NULL.png

# 最佳实践12：Prepared Statements

![img](https://upload-images.jianshu.io/upload_images/18375227-4d109b90c44b27b2.png?imageMogr2/auto-orient/strip|imageView2/2/w/499)

最佳实践12：Prepared Statements.png

# 最佳实践13：无缓冲的查询

![img](https://upload-images.jianshu.io/upload_images/18375227-8f327063bf1cc473.png?imageMogr2/auto-orient/strip|imageView2/2/w/553)

最佳实践13：无缓冲的查询.png

# 最佳实践14：把 IP 地址存成 UNSIGNED INT

![img](https://upload-images.jianshu.io/upload_images/18375227-c2a3dd419dd5f6d6.png?imageMogr2/auto-orient/strip|imageView2/2/w/613)

最佳实践14：把 IP 地址存成 UNSIGNED INT.png

# 最佳实践15：固定长度的表会更快

![img](https://upload-images.jianshu.io/upload_images/18375227-66c75dbcf8433263.png?imageMogr2/auto-orient/strip|imageView2/2/w/550)

最佳实践15：固定长度的表会更快.png

# 最佳实践16：垂直分割

![img](https://upload-images.jianshu.io/upload_images/18375227-02665b9b105ba7d9.png?imageMogr2/auto-orient/strip|imageView2/2/w/575)

最佳实践16：垂直分割.png

# 最佳实践17：拆分大的 DELETE 或 INSERT 语句

![img](https://upload-images.jianshu.io/upload_images/18375227-8e89505c20df8cd2.png?imageMogr2/auto-orient/strip|imageView2/2/w/615)

最佳实践17：拆分大的 DELETE 或 INSERT 语句.png

# 最佳实践18：越小的列会越快

![img](https://upload-images.jianshu.io/upload_images/18375227-5082ff09059ecab4.png?imageMogr2/auto-orient/strip|imageView2/2/w/575)

最佳实践18：越小的列会越快.png

# 最佳实践19：选择正确的存储引擎

![img](https://upload-images.jianshu.io/upload_images/18375227-567bb50622a96084.png?imageMogr2/auto-orient/strip|imageView2/2/w/520)

最佳实践19：选择正确的存储引擎.png

# 最佳实践20：使用一个对象关系映射器(Object Relational Mapper)

![img](https://upload-images.jianshu.io/upload_images/18375227-ca5e1ab18b71b1ae.png?imageMogr2/auto-orient/strip|imageView2/2/w/577)

最佳实践20：使用一个对象关系映射器(Object Relational Mapper).png

# 最佳实践21：小心“永久链接”

![img](https://upload-images.jianshu.io/upload_images/18375227-a0be737566ec52c7.png?imageMogr2/auto-orient/strip|imageView2/2/w/545)

最佳实践21：小心“永久链接”.png

# 接下来看看阿里P8必备的MySQL：基础+索引+锁+日志+调优，你能答对的有多少？

- 基础篇问题

  ![img](https://upload-images.jianshu.io/upload_images/18375227-7a91c0a72821734b.png?imageMogr2/auto-orient/strip|imageView2/2/w/618)

  基础篇问题.png

- **索引篇问题**

![img](https://upload-images.jianshu.io/upload_images/18375227-adc20ed4f5379fe3.png?imageMogr2/auto-orient/strip|imageView2/2/w/561)

索引篇问题.png

- **锁篇问题**

![img](https://upload-images.jianshu.io/upload_images/18375227-0dd5bc521d532734.png?imageMogr2/auto-orient/strip|imageView2/2/w/467)

锁篇问题.png

- **日志问题**

![img](https://upload-images.jianshu.io/upload_images/18375227-3b13166216eb8c44.png?imageMogr2/auto-orient/strip|imageView2/2/w/615)

日志问题.png

- **性能优化问题**

![img](https://upload-images.jianshu.io/upload_images/18375227-827967d3b50c7c83.png?imageMogr2/auto-orient/strip|imageView2/2/w/433)