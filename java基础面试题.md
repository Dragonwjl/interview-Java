#Java 基础面试题
 1.JDK 和 JRE 有什么区别？
   JDK：Java Development Kit 的简称，java 开发工具包，提供了 java 的开发环境和运行环境。
   JRE：Java Runtime Environment 的简称，java 运行环境，为 java 的运行提供了所需环境。
   jvm：Java虚拟机，Java运行环境
   
 2.== 和 equals 的区别是什么？
    == 解读
        对于基本类型和引用类型 == 的作用效果是不同的
        基本类型：比较的是值是否相同；
        引用类型：比较的是引用是否相同，比较的是地址值；
    
   equals：默认比较地址，如果是要比较内容就需要对equals方法进行重写
        
 3.String 常用工具类
    分为以下几类：
        1 基本操作：length indexOf lastIndexOf chartAt
        2 转换操作:toCharArray valueOf toLowerCase toUpperCase
        3 替换与去除:replace trim
        4 截取与分割:split substring(注意命名的大小写) substring
        5 判断操作：equals startWith endWith contains isEmpty
 4. 统计一个字符串中相同字符出现的次数
    public class Demo {
        public static void main(String[] args) {
            String s = "welcome to rds";
            method1(s);
            method2(s);
        }
             //方法一
        public static void method1(String s) {
            Integer count;
            Map<Character, Integer> map = new HashMap<>();
            List<Map.Entry<Character, Integer>> list = new ArrayList<>();
            // 拆分字符串，统计字符个数
            for (int i = 0; i < s.length(); i++) {
                char ch = s.charAt(i);
                count = map.get(ch);
                if (count == null) {
                    map.put(ch, 1);
                } else {
                    map.put(ch, ++count);
                }
            }
            // 遍历map，存到list中
            for (Map.Entry<Character, Integer> entry : map.entrySet()) {
                list.add(entry);
            }
            // 根据字符个数进行比较
            Collections.sort(list, new Comparator<Map.Entry<Character, Integer>>() {
                @Override
                public int compare(Map.Entry<Character, Integer> o1, Map.Entry<Character, Integer> o2) {
                    //return o1.getValue() - o2.getValue(); // 升序
                    return o2.getValue() - o1.getValue(); // 降序
                }
            });
            // 遍历排序后输出
            for (Map.Entry<Character, Integer> entry : list) {
                System.out.println(entry.getKey() + "=" + entry.getValue());
            }
        }
            //方法二
        public static void method2(String s) {
            Map<Character,Integer> map = new HashMap<>();
            List<Map.Entry<Character,Integer>> list = new ArrayList<>();
            // 拆分字符串，统计字符个数
            for (int i = 0; i < s.length(); i++) {
                char ch = s.charAt(i);
                if (map.containsKey(ch)) {
                    map.put(ch, map.get(ch) + 1);
                } else {
                    map.put(ch, 1);
                }
            }
            // 遍历map，存到list中
            list.addAll(map.entrySet());
            // 根据字符个数进行比较
            Collections.sort(list, new Comparator<Map.Entry<Character,Integer>>() {
                @Override
                public int compare(Map.Entry<Character,Integer> o1, Map.Entry<Character,Integer> o2) {
                    //return o1.getValue() - o2.getValue(); // 升序
                    return o2.getValue() - o1.getValue(); // 降序
                }
            });
            // 遍历排序后输出
            for (Map.Entry<Character, Integer> entry : list) {
                System.out.println(entry.getKey() + "=" + entry.getValue());
            }
        }
     
    }
     
 
 5. jdk 1.8 中有什么新特性
    1 Lambda表达式 允许把函数作为一个方法的参数(函数作为参数传递进方法中)。可以使代码变的更加简洁紧凑。
    2 Java 8带来的另一个特性是在接口中可以定义静态方法，我们可以直接用接口调用这些静态方法
    3 Optional Java应用中最常见的bug就是空值异常。Optional 仅仅是一个容器，可以存放T类型的值或者 null 。它提供了一些有用的接口来避免显式的 null 检查
 
 6. 数组去重
 public static Object[]  ifRepeat2(Object[] arr){  
         //创建一个集合  
         List list = new ArrayList();  
         //遍历数组往集合里存元素  
         for(int i=0;i<arr.length;i++){  
             //如果集合里面没有相同的元素才往里存  
             if(!list.contains(arr[i])){  
                 list.add(arr[i]);  
             }  
         }  
         //toArray()方法会返回一个包含集合所有元素的Object类型数组  
         Object[] newArr = list.toArray();  
 		return newArr;  
   
   7.final关键字
   答：final 可以用来修饰的结构：类 、 方法 、 变量
   final修饰类，表示此类不能被继承，例如：String就是被final修饰的类
   修饰方法，表示方法不能再被重写
   final修饰基本数据类型的变量，表示为常量不可变，修饰引用数据类型的变量，是指引用数据类型的指向不可变，但其指向中的内容是可变的
   引申：static final 用来修饰属性 ：全局常量  
   
   8.String、StringBuffer、StringBuilder区别
   String与其他两者的区别是：String是final类型的，是不可变的对象，所以每次操作都会产生新的String对象。然后将引用指向新的String对象
   
   StringBuffer和StringBuilder，都是在原对象之上进行操作，所以是可变的，如果需要经常改变字符串内容，采用这两种方法
   （字符拼接问题，.append()）
   StringBuffer：是线程安全的，但是其性能不太高
   StringBuilder：是线程不安全的，但是其性能较高，开发中一般优先采用此方法（）

   9.什么时候需要考虑线程安全问题
    当多个线程访问同一个资源的时候
    
   10.接口和抽象类的区别
    语法：
        抽象类:方法有抽象的也有非抽象的，有构造器
        接口：方法都是抽象的，属性都是常量，默认有public static修饰 
        注意JDK1.8 之后，接口中可以有实现的方法，但注意要在声明上添加default或static  
    设计：
        抽象类：同一类事物的抽取，比如针对Dao层的封装
        接口：通常更像是一种标准，定制系统之间对接的标准
        
   11.多重继承、多实现、多继承
        多重继承：A->B->C(爷孙三代关系)
        多实现：Person implements IRunable,IEatable                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   
   12 求N的阶乘
    使用递归思想，递归就是方法内部调用方法本身
    递归注意事项：
        找出规律，编写递归公式
        找出边界（结束值），让递归有结束边界
        如果没有正确的结束递归，或者递归太多层，就会出现栈溢出的error
        
   13.int 和 Integer
    注意，自动装箱和自动拆箱
    注意，Integer自带缓存，如果不超过-128到127，就不需要重新创建，直接在缓存中取就行了
    判断是否相等，自动拆箱比较数值
        
   14.方法重写和重载之间的区别
   