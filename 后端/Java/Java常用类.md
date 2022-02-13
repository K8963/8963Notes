# Random 

作用：用于产生一个随机数

使用步骤：

1. 导包
2. 创建对象
3. 获取随机数

```java
import java.util.Random;

class RandomDom{
	public static void main(String[] args){
		Random r = new Random();
		int num = r.nextInt(10);
    // 获取数据的范围[0,10) 包括0，不包括10
		System.out.println(num);
	}
}
```

获取 1 - 100 的随机数

```java
// [0,99)+1 => [1,100)
r.nextInt(100)+1;
```

