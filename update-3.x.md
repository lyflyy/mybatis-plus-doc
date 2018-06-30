# 从2.x到3.x升级指南

## 2.x到3.x有以下改进

* 分页查询可以直接返回`Ipage<T>`的子类(下面会有详细使用说明)
* `Wrapper<T>`实现类的改动
    > 1.`EntityWrapper<T>`更名为`QueryWrapper<T>`    
    2.新增一个实现类`UpdateWrapper<T>`用于`update`方法
* `BaseMapper<T>`的改动
    > 1.去除了`insertAllColumn(T entity)`方法  
     2.去除了`updateAllColumn(T entity)`方法     
     3.新增`update(T entity, Wrapper<T> updateWrapper)`方法
    
## `Wrapper<T>`使用
 
### `QueryWrapper<T>`与`UpdateWrapper<T>`共有方法

方法名 | 说明
--------|--------
allEq       |   基于 map 内容等于=
eq          |   等于 =
ne          |   不等于 <>
gt          |   大于 >
ge          |   大于等于 >=
lt          |   小于 <
le          |   小于等于 <=
between     |   BETWEEN 条件语句
notBetween  |   NOT BETWEEN 条件语句
like        |   LIKE '%值%''
notLike     |   NOT LIKE '%值%'
likeLeft    |   LIKE '%值'
likeRight   |   LIKE '值%'
--------|--------
isNull      |   NULL 值查询
isNotNull   |   NOT NULL 值查询
in          |   IN 查询
notIn       |   NOT IN 查询
inSql       |   IN 查询(sql注入式)
notInSql    |   NOT IN 查询(sql注入式)
groupBy     |   分组 GROUP BY  
orderByAsc  |   ASC 排序 ORDER BY
orderByDesc |   DESC 排序 ORDER BY
orderBy     |   排序 ORDER BY
having      |   HAVING 关键词(sql注入式)
--------|--------
or          |   or 拼接
apply       |   拼接自定义内容(sql注入式)
last        |   拼接在最后(sql注入式)
exists      |   EXISTS 条件语句(sql注入式)
notExists   |   NOT EXISTS 条件语句(sql注入式)
--------|--------
and(Function)   |   AND (嵌套内容)
or(Function)    |   OR  (嵌套内容)
nested(Function)|   (嵌套内容)



#### `QueryWrapper<T>`特有方法

方法名 | 说明
---|---
select  |   SQL 查询字段内容,例如:id,name,age(重复设置以最后一次为准)


#### `UpdateWrapper<T>`特有方法

方法名 | 说明
---|---
set     |   SQL SET 字段(一个字段使用一次)


### 分页查询

```java
IPage<T> selectPage(IPage<T> page, @Param("ew") Wrapper<T> queryWrapper);
```

> 以上面的方法为例,入参一个`IPage<T>`接口的子类(可以使用mp自带的一个叫`Page<T>`的子类),
返回一个`IPage<T>`,其实这个`返回的分页类==入参的分页类`,
如果你需要自定义一个分页方法只需要注意一点:入参第一位放置你使用的`IPage<T>`子类!

### `update(T entity, Wrapper<T> updateWrapper)`使用

> 只需要注意,入参第一位是需要update的实体类,`updateWrapper`里的实体类是用于生成where条件的