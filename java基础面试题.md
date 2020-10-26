#Java 基础面试题
 1.JDK 和 JRE 有什么区别？
   JDK：Java Development Kit 的简称，java 开发工具包，提供了 java 的开发环境和运行环境。
   JRE：Java Runtime Environment 的简称，java 运行环境，为 java 的运行提供了所需环境。
   
 2.== 和 equals 的区别是什么？
    == 解读
        对于基本类型和引用类型 == 的作用效果是不同的
        基本类型：比较的是值是否相同；
        引用类型：比较的是引用是否相同；
        
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
 
    