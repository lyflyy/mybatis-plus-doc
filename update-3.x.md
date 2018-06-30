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

方法名           |     	说明
---------------- | ----------------
allEq            |      基于 map 内容等于=


#### `QueryWrapper<T>`特有方法

方法名           |     	说明
---------------- | ----------------


#### `UpdateWrapper<T>`特有方法

方法名           |     	说明
---------------- | ----------------
