1 SSM框架中常用注解有哪些，分别有什么作用
    @Controller---使用它标记在一个类上，dispatcher会扫描使用该注解类的方法，并检测该方法是否使用了@RequestMapping注解，加上RequestMapping注解的方法才是处理请求的处理器
           @Service-----会在注解里指定一个name，会将service实现装配到Bean里
           @RequestMapping----映射URL到控制器类或到控制器类方法
           @ResponseBody----将Java对象转换为Json格式的数据
           @Autowired----spring容器有一个专门扫描autowired注解的处理器，扫描到时，就在IOC容器查找相应的Bean，并装配给该对象的属性
    　　@Override-----提示是否正确重写了父类的方法，提示作用
    　　@RequestParam----直接获取参数，get和post请求的参数会自动转换赋值到注解所注解的变量上
    　　@JsonSerilized----对它所修饰的类返回值进行序列化，如ServerResponse返回值
    
       
    1、@Controller、@Service、@Component注解，都相当于是配置了一个bean标签，分别应用于控制层，服务层，第三个都可以使用(在不知道属于哪层的时候使用)
    2、@RequestMapping 该注解描述请求路径和当前方法的映射
    
            属性value -- 代表当前方法处理的请求路径地址，假设为@RequestMapping(“/login”)，会默认发布三个映射地址，分别是/login,/login.*,/login/。
    
            属性method -- 定义方法处理的请求方式，如果请求方式不支持，则页面报405错误，提示请求方式不支持，method是RequestMethod[]类型的属性，在注解中使用{}定义数组数据
    
            属性produces – 设置响应类型 只在服务方法返回类型为字符串，并提供ResponseBody注解时生效
    
    @RequestMapping(value=”/login”,method={RequestMethod.GET},produces=”application/json;charset=UTF-8”)
    
    3、@RequestParam 该注解处理不友好的请求参数
    
             属性value – 请求参数的名称，没有默认值(该名称为页面中的name)
    
             属性defaultValue– 如果没有传递请求参数，使用什么默认值
    
             属性required – 是否是一个必要的请求参数，默认值是true，如果必要参数没有传递，页面显示400错误，是请求错误
    
    @RequestParam(value=”TXT_PWD”,defaultValue=”123123”,required=”true”)Stringpassword
    
    4、@PathVariable 获取restful风格传参定义的变量数据
    
             属性value – 用于设置变量命名，如果变量名和方法参数名一致，可以省略
    
             Restful风格传参 @RequestMapping(“/testRestful/{username}/{password}”)
    
         @PathVariable(@PathVariable(“username”)Stringusername,@PathVariable String password)
    
    5、@ResponseBody 实现异步访问的json数据返回
    
    6、@Param 一般用在mapper层，简单类型（八种基本数据类型+包装类+String）传值的时候，会忽略占位符个数和命名，传给所有的占位符，使用@param注解，可以构建一个key-value键值对
    
          属性value --- 创建的键值对的key
    
          如：@Param(value="key")String value
    
    7、读取properties配置文件的时候，如果是写在其他配置文件中，如：applicaitonContext-mybatis.xml文件中配置datasource时读取properties文件，value中直接使用${key}格式，如：<property name=“url” value="${mysql.url}">(mysql.url为properties文件中的一个key值，使用之前需要先读取该properties文件，需要注意的是读取的properties文件只在当前容器中有效<context:property-placeholder location="classpath:com/cms/config/commons/db.properties">)
    
          如果是在java文件中需要使用到properties中配置的信息（如：serviceImpl文件中），前提是当前容器已经读取properties文件，使用标签来读取value值 格式为 @Value("${key}")  如: @Value("${FTP_HOST}")
    
    8、@JsonProperty 将对象转换成json字符串的时候，对应的key值，使用注解中的value属性值

2 bean和component的区别

3 SQL查询中#和$的区别
    1、#将传入的参数都当成一个字符串，会对自动传入的数据加一个双引号。如：order by #{age}，如果传入的值是18,那么解析成sql时的值为order by "18", 如果传入 age ,则会解析为 order by  "age"
    2、$将传入的参数直接显示生成在sql中,被当成一个对象。如：order by${age}，如果传入的值是18,那么解析成sql时的值为order by 18,  如果传入的值是age，则解析成的sql为order by age
    3、#方式底层采用预编译方式PreparedStatement，能够很大程度防止sql注入；$方式底层只是Statement，无法防止Sql注入。
    4、$方式一般用于传入数据库对象，例如传入表名.
    5、一般能用#的就别用$  注意点：MyBatis排序时使用order by 动态参数时需要注意，用$而不是#

4 mybatisSQL嵌套查询和嵌套结果
    1 
    2 嵌套语句的查询会导致数据库访问次数不定，进而有可能影响到性能。Mybatis还支持一种嵌套结果的查询：即对于一对多，多对多，多对一的情况的查询，
    Mybatis通过联合查询，将结果从数据库内一次性查出来，然后根据其一对多，多对一，多对多的关系和ResultMap中的配置，进行结果的转换，构建需要的对象。

5 