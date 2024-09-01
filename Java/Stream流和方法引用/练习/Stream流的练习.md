# Stream流的练习

## 练习1

定义一个集合，并添加一些整数1, 2, 3, 4, 5, 6, 7, 8, 9, 10

并过滤奇数只留下偶数

并将结果保存下来

```Java
import java.util.ArrayList;
import java.util.Collections;
import java.util.stream.Collectors;
import java.util.List;
public class StreamExercise1{
	public static void main(String[] args){
		ArrayList<Integer> list1 = new ArrayList<>();
		Collections.addAll(list1, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
		
		List<Integer> list2 = list1.stream().filter(i -> i % 2 == 0).collect(Collectors.toList());
		System.out.println(list2);
	}
}
```

## 练习2
创建一个ArrayList:集合，并添加以下字符串，字符串中前面是姓名，后面是年龄
“zhangsan,23"
"lisi,24”
“wangwu,25"
保留年龄大于等于24岁的人，并将结果收集到Mp集合中，姓名为键，年龄为值

```Java
import java.util.ArrayList;
import java.util.Collections;
import java.util.stream.Collectors;
import java.util.Map;
public class StreamExercise2{
	public static void main(String[] args){
		ArrayList<String> list1 = new ArrayList<>();
		Collections.addAll(list1, "zhansan,23", "lisi,24", "wangwu,25");
		
		Map<String, Integer> map = list1.stream().filter(s -> Integer.parseInt(s.split(",")[1]) >= 24).collect(Collectors.toMap(
		s -> s.split(",")[0], 
		s -> Integer.parseInt(s.split(",")[1])));
		
		System.out.println(map);
	}
}
```

### 练习3

现在有两个ArrayList:集合，
第一个集合中：存储6名男演员的名字和年龄。第二个集合中：存储6名女演员的名字和年龄。
姓名和年龄中间用逗号隔开。比如：张三，23
要求完成如下的操作：
1，男演员只要名字为3个字的前两人
2,女演员只要姓杨的，并且不要第一个
3,把过滤后的男演员姓名和女演员姓名合并到一起
4,将上一步的演员信息封装成Actor对象。
5,将所有的演员对象都保存到List集合中。
备注：演员类Actor.,属性只有一个：name,age

```Java
package com.tango.collection.map;

import java.util.ArrayList;
import java.util.Collections;
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.Stream;

public class Exercise3 {
    public static void main(String[] args){
        ArrayList<String> maleList = new ArrayList<>();
        ArrayList<String> femaleList = new ArrayList<>();

        Collections.addAll(maleList, "蔡坤坤,24", "叶陶成,23", "刘不甜,22", "吴蓉,24", "谷辜,30", "肖粱粱,27");
        Collections.addAll(femaleList, "赵小颖,35", "杨颖,36", "高圆圆,43", "张天天,31", "刘诗,35","杨小幂,33");

        Stream<String> maleStream = maleList.stream().filter(s -> s.split(",")[0].length() == 3).limit(2);
        Stream<String> femalStream = femaleList.stream().filter(s -> s.split(",")[0].startsWith("杨")).skip(1);


        List<Actor> actors = Stream.concat(maleStream, femalStream).map(new Function<String, Actor>() {
            @Override
            public Actor apply(String s) {
                String[] arr = s.split(",");
                Actor actor = new Actor();
                actor.setName(arr[0]);
                actor.setAge(Integer.parseInt(arr[1]));
                return actor;
            }
        }).collect(Collectors.toList());
        actors.forEach(System.out::println);


    }
}

class Actor{
    private String name;
    private int age;

    public Actor(){
    }

    public Actor(String name, int age){
        this.name = name;
        this.age = age;
    }

    public String getName(){
        return name;
    }

    public void setName(String name){
        this.name = name;
    }

    public int getAge(){
        return age;
    }

    public void setAge(int age){
        this.age = age;
    }


    @Override
    public String toString(){
        return "Actor{"
                + "name = " + name
                + ", age = " + age
                + "}";
    }
}

```

