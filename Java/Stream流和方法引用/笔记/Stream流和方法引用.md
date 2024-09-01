# Stream流和方法引用

## Stream流



### Stream流的终结方法

| 名称                          | 遍历                           |
| ----------------------------- | ------------------------------ |
| void forEach(Consumer action) | 遍历                           |
| long count()                  | 统计                           |
| toArray()                     | 收集流中的数据，放到数组中。   |
| collect(Collector collector)  | 收集流中的数据，放到集合当中。 |

前三个方法：

```Java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Arrays;


public class StreamMethod{
	public static void main(String[] args){
		ArrayList<String> list = new ArrayList<>();
		// 使用Collections工具类的addAll方法addAll(Collectino<? super T>, T... elements)
		Collections.addAll(list, "张无忌", "周芷若", "赵敏", "张强", "张三丰", "张翠山", "张良", "王二麻子", "谢广坤");
		
		// Stream中的终结方法
		// 1.forEach 返回值是void无法继续使用stream中的方法所以是终结方法
		// Consumer是FunctionInterface, 因此可以用作lambda表达式或方法引用的赋值目标
		list.stream().forEach(s -> System.out.println(s));
		
		// 2. count 返回值是long无法继续使用stream中的方法，为终结方法
		System.out.println(list.stream().count());	// 9
		
		// 3. toArray 重载了
		// 3.1 返回值 Object[] toArray()
		// 3.2 返回值 <A> A[] toArray(IntFunction<A[]> generator)
		// IntFunction也是函数式接口，其功能方法是apply(int)
		Object[] objects = list.stream().toArray();
		System.out.println(Arrays.toString(objects));
		
		String[] strings = list.stream().toArray(value -> new String[value]);
		
		System.out.println(Arrays.toString(strings));

	}
}
```

collect方法

```Java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Arrays;

public class StreamDemo1{
	public static void main(String[] args){
		ArrayList<String> list = new ArrayList<>();
		// 使用Collections工具类的addAll方法addAll(Collectino<? super T>, T... elements)
		Collections.addAll(list, "张无忌", "周芷若", "赵敏", "张强", "张三丰", "张翠山", "张良", "王二麻子", "谢广坤");
		
		// Stream中的终结方法
		// 1.forEach 返回值是void无法继续使用stream中的方法所以是终结方法
		// Consumer是FunctionInterface, 因此可以用作lambda表达式或方法引用的赋值目标
		list.stream().forEach(s -> System.out.println(s));
		
		// 2. count 返回值是long无法继续使用stream中的方法，为终结方法
		System.out.println(list.stream().count());	// 9
		
		// 3. toArray 重载了
		// 3.1 返回值 Object[] toArray()
		// 3.2 返回值 <A> A[] toArray(IntFunction<A[]> generator)
		// IntFunction也是函数式接口，其功能方法是apply(int)
		Object[] objects = list.stream().toArray();
		System.out.println(Arrays.toString(objects));
		
		String[] strings = list.stream().toArray(value -> new String[value]);
		
		System.out.println(Arrays.toString(strings));

	}
}
```

### Stream总结

1. Stream流的作用：

   结合Lambda表达式，简化集合、数组的操作。

2. Stream的使用步骤

   - 获取Stream对象
   - 使用中间方法处理数据
   - 使用终结方法处理数据

3. 如何获取Stream流对象

   - 单列集合：Collection中的默认方法stream
   - 双列集合：不能直接获取
   - 数组：Arrays工具类型中的静态方法stream
   - 一堆零散的数据：Stream接口的静态方法of

4. 常见方法

   - 中间方法：filter、limit、skip、distinct、concat、map
   - 终结方法：forEach、count、collect

   ## 方法引用

   1. 什么是方法引用

   就是把已经有的方法拿过来用，当作函数式接口抽象方法的方法体。

   2. ::是什么符号？

   方法引用符号

   3. 方法引用时需要注意什么？
      - 需要函数式接口
      - 被引用的方法必须已经存在
      - 被引用的方法的形参和返回值需要跟抽象方法保持一致
      - 被引用方法的功能要满足当前的需求

   ### 方法引用的分类

   ### 引用静态方法

   格式：类名::静态方法

   范例：Integer::parseInt

   ### 引用成员方法

   格式：对象::成员方法

   ① 其他类：其他类对象::方法名

   ② 本类：this::方法名

   ③ 父类：super::方法名

   ==注：2.、3在引用出不能是静态方法，因为静态方法中没有this==
   
   ### 引用构造方法
   
   格式：类名::new
   
   范例：Student::new
   
   ### 引用数组的构造方法
   
   格式：数据类型[]::new
   
   范例：int[]::new
   
   
   
   
