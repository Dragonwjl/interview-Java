1 一个表中有很多数据，id是主键且是自增的，怎么从数据表中快速查找到最后一条数据
    使用max函数进行查询
2 MySQL中分页是怎么做到的，在数据量很大时，有什么操作可以使数据出来的更快点
    1 数据量不大时，可以使用limit来进行分页
    2 数据量较大时，可以有以下几种方法
        1 建立主键或唯一索引, 利用索引(假设每页10条)
        2 基于索引再排序
        3 利用MySQL支持ORDER操作可以利用索引快速定位部分元组,避免全表扫描
        4

3 MySQL中常用函数有哪些
    1 数学函数：ABS() PI() SQRT() MOD() CEIL() CEILING FLOOR ROUND ...
    2 字符串函数:CHAR_LENGTH() CONCAT INSERT() LEFT() RIGHT() TRIM() REPLACE() SUBSTRING() REVERSE()
    3 日期和时间函数:CURDATE() MONTH() DAY()
    4 条件判断函数:IF() IFNULL() CASE THEN THEN
    5 系统信息函数:VERSION CONNECTION USER() CHARSET
    6 加密函数:PASSWORD() MD5()
    7 格式化函数:FORMAT



