# JUnitGeneration 工具说明文档 
JUnitGeneration是一个自动生成JUnit单元测试代码的工具，其输入是Java字节码，输出是JUnit测试源代码。

##  下载  
```
最新版本： JUnitGeneration_20200420.jar  release模块中下载
 [JUnitGeneration_20200420.jar](https://github.com/cuixiaoyiyi/JavaUnitTestGeneration/releases) 
rt.jar 可下载jdk1_8_0_172_rt.zip解压
```

### 所需环境
JDK1.8  （1.8+版本未测试） 
JUnit5

### 执行后生成文件夹

| 输入(-t)  | 输出 |
|  -  | - |
|  YouPath\bin\  | YouPath\monkeytest\ |
|   YouPath\  |  YouPath\monkeytest\ |
|   YouPath.jar  |  YouPath\jar\monkeytest\ |

其中monkeytest为生成JUnit代码的根目录，每个待测类会生成相应的测试代码类文件

### 生成结果使用
程序生成JUnit源代码。  
如果是使用Eclipse IDE，可以将monkeytest添加为源代码文件(monkeytest文件夹右键--> Build Path --> Use as Source Folder ) ，之后在IDE中使用JUnit执行。   
如果没有IDE，需要对Java文件进行编译，使用JUnit执行


### 工具已实现的支持
|| 已实现  | 说明 |
| -| - | - |
|1 | 基本类型| int, long, short, float, double, byte, char, boolean;  <br />支持String类型的随机常量生成
|2 |自定义类| 支持public 和 default 方法的测试；<br /> 支持static方法(类调用)和非static方法(对象调用) |
|3 | 泛型| 支持泛型嵌套；支持raw 类型；支持 <?> <? super AAA> <? extends AAA>|
|4 | 集合 | 支持两类集合(Collection和Map)及其子类；支持添加元素 |
|5 | 数组 | 支持对象数组；支持基本类型数组；<br /> 支持多维数组 |
|6 | 多级别生成 | 支持工程、包、类、方法、关键字各层次的单元测试生成 |

### 工具未实现的支持
|| 未实现  | 说明 |
| -| - | - |
| 1| private\protected方法 | 可能影响覆盖率 |
| 2| 检测参数的合法性 | 生成的代码在执行时可能发生异常 |
| 3| 私有构造函数方法 | 代码生成时可能有编译错误（xxx is not visible） |
| 4| 泛型数组 | 程序执行时可能发生异常 | 
| 5| 断言语句 | 无法判断执行结果 |
| 6| 组合测试 | 未对该类的各个方法组合调用生成； |


###  工程(project)级别单元测试代码生成
| 参数    | 说明      | 输入示例   |
|  -  | - |  - |
|  -l  | 必填;待测代码层级，取固定值 project | project |
|  -r  | 必填;rt.jar依赖库 | 有空格："C:\Program Files\Java\jdk1.8.0_231\jre\lib\rt.jar" <br /> 无空格: C:\Users\C\eclipseworkspace\rt.jar |   
|  -t  | 必填;待测代码；可以是.jar也可以是文件夹目录；多个以分号(;)相隔 | C:\Users\C\eclipseworkspace\JUnitGeneration\bin;<br />C:\Users\C\eclipseworkspace\JUnitGeneration\libs\xx.jar |
|  -d  | 如果有依赖，必填；无依赖不填;待测代码依赖的第三方库；可以是.jar也可以是文件夹目录；多个以分号(;)相隔 | C:\Users\C\eclipseworkspace\JUnitGeneration\libs\xx.jar |
|  -n  | 选填；正整数，代表每个方法生成的测试方法数，默认为1 | 2 |  

命令行示例
```
java -cp JUnitGeneration_20200420.jar cn.ios.junit.Main -l project -t C:\Users\C\Desktop\JUnitGenerationSample1\bin -r jdk1_8_0_172_rt.jar -n 2
```


###  包(package)级别单元测试代码生成
| 参数    | 说明      | 输入示例   |
|  -  | - |  - |
|  -l  | 必填;待测代码层级，取固定值 package | package |
|  -r  | 必填;rt.jar依赖库 | 有空格："C:\Program Files\Java\jdk1.8.0_231\jre\lib\rt.jar" <br /> 无空格: C:\Users\C\eclipseworkspace\rt.jar |   
|  -t  | 必填;待测代码；可以是.jar也可以是文件夹目录；多个以分号(;)相隔 | C:\Users\C\eclipseworkspace\JUnitGeneration\bin;<br />C:\Users\C\eclipseworkspace\JUnitGeneration\libs\xx.jar |
|  -p  | 必填；包名；严格匹配 | cn.ios.junit  |
|  -d  | 如果有依赖，必填；无依赖不填;待测代码依赖的第三方库；可以是.jar也可以是文件夹目录；多个以分号(;)相隔 | C:\Users\C\eclipseworkspace\JUnitGeneration\libs\xx.jar |  
|  -n  | 选填；正整数，代表每个方法生成的测试方法数，默认为1 | 2 |   

命令行示例
```
java -cp JUnitGeneration_20200420.jar cn.ios.junit.Main -l package -t C:\Users\C\Desktop\JUnitGenerationSample1\bin -r jdk1_8_0_172_rt.jar -p  cn.ios.ac.junit.sample -n 2
```

###  类(class)级别单元测试代码生成
| 参数    | 说明      | 输入示例   |
|  -  | - |  - |
|  -l  | 必填;待测代码层级，取固定值 class | class |
|  -r  | 必填;rt.jar依赖库 | 有空格："C:\Program Files\Java\jdk1.8.0_231\jre\lib\rt.jar" <br /> 无空格: C:\Users\C\eclipseworkspace\rt.jar |   
|  -t  | 必填;待测代码；可以是.jar也可以是文件夹目录；多个以分号(;)相隔 | C:\Users\C\eclipseworkspace\JUnitGeneration\bin;<br />C:\Users\C\eclipseworkspace\JUnitGeneration\libs\xx.jar |
|  -c  | 必填；类名（带包名）；严格匹配 | cn.ios.junit.Main  |
|  -d  | 如果有依赖，必填；无依赖不填;待测代码依赖的第三方库；可以是.jar也可以是文件夹目录；多个以分号(;)相隔 | C:\Users\C\eclipseworkspace\JUnitGeneration\libs\xx.jar |  
|  -n  | 选填；正整数，代表每个方法生成的测试方法数，默认为1 | 2 |  

命令行示例  
```
java -cp JUnitGeneration_20200420.jar cn.ios.junit.Main -l class  -t C:\Users\C\Desktop\JUnitGenerationSample1\bin -r jdk1_8_0_172_rt.jar -c  cn.ios.ac.junit.sample.Candy -n 2
```
###  方法(method)级别单元测试代码生成
| 参数    | 说明      | 输入示例   |
|  -  | - |  - |
|  -l  | 必填;待测代码层级，取固定值 method | method |
|  -r  | 必填;rt.jar依赖库 | 有空格："C:\Program Files\Java\jdk1.8.0_231\jre\lib\rt.jar" <br /> 无空格: C:\Users\C\eclipseworkspace\rt.jar |   
|  -t  | 必填;待测代码；可以是.jar也可以是文件夹目录；多个以分号(;)相隔 | C:\Users\C\eclipseworkspace\JUnitGeneration\bin;<br />C:\Users\C\eclipseworkspace\JUnitGeneration\libs\xx.jar |
|  -m  | 必填；方法签名；严格匹配；格式 <br /> <类名: 返回值类型 方法名(参数类型，多个以逗号分隔)>| <cn.ios.junit.Main: long get_max_running_time(long,java.lang.Integer)>  |
|  -d  | 如果有依赖，必填；无依赖不填;待测代码依赖的第三方库；可以是.jar也可以是文件夹目录；多个以分号(;)相隔 | C:\Users\C\eclipseworkspace\JUnitGeneration\libs\xx.jar |  
|  -n  | 选填；正整数，代表每个方法生成的测试方法数，默认为1 | 2 | 

命令行示例  
```
java -cp JUnitGeneration_20200420.jar cn.ios.junit.Main -l method  -t C:\Users\C\Desktop\JUnitGenerationSample1\bin -r jdk1_8_0_172_rt.jar -m "<cn.ios.ac.junit.sample.Candy: int candy(int[])>" -n 2
```
###  关键字(keyword)级别单元测试代码生成
| 参数    | 说明      | 输入示例   |
|  -  | - |  - |
|  -l  | 必填;待测代码层级，取固定值 key | key |
|  -r  | 必填;rt.jar依赖库 | 有空格："C:\Program Files\Java\jdk1.8.0_231\jre\lib\rt.jar" <br /> 无空格: C:\Users\C\eclipseworkspace\rt.jar |   
|  -t  | 必填;待测代码；可以是.jar也可以是文件夹目录；多个以分号(;)相隔 | C:\Users\C\eclipseworkspace\JUnitGeneration\bin;<br />C:\Users\C\eclipseworkspace\JUnitGeneration\libs\xx.jar |
|  -k  | 必填；关键字；类签名.contain匹配 | Basic  |
|  -d  | 如果有依赖，必填；无依赖不填;待测代码依赖的第三方库；可以是.jar也可以是文件夹目录；多个以分号(;)相隔 | C:\Users\C\eclipseworkspace\JUnitGeneration\libs\xx.jar |  
|  -n  | 选填；正整数，代表每个方法生成的测试方法数，默认为1 | 2 |   

命令行示例   
```
java -cp JUnitGeneration_20200420.jar cn.ios.junit.Main -l key  -t C:\Users\C\Desktop\JUnitGenerationSample1\bin -r jdk1_8_0_172_rt.jar -k Candy -n 2
```

### 工具效果展示

源代码示例   
```
package cn.ios.sort;

public class BubbleSort {

	public BubbleSort(int i, double d1, int j, char c, short s, byte b, boolean b2, double[] d, float[] f, byte[] bs,
			boolean[] bs1, short[] ss, String[] sss) {

	}

	public static void bubbleSort(int[] arr) {
		int tmp = 0;
		for (int i = 0; i < arr.length - 1; i++) {// 冒泡次数
			for (int j = 0; j < arr.length - 1 - i; j++) {// 比较的次数
				if (arr[j] > arr[j + 1]) {// 加入前面的元素小于后面的元素
					// 调换位置
					tmp = arr[j];
					arr[j] = arr[j + 1];
					arr[j + 1] = tmp;
				} else if (arr[j] == arr[j + 1]) {
					System.out.println("bubble here=");
				} else {
					System.out.println("bubblehere<");
				}
			}
		}
	}
	
	@Override
	public String toString() {
		return super.toString();
	}
}


```
生成对应的测试代码示例
```
package cn.ios.sort;

import org.junit.Test;

public class BubbleSort_Test {

  @Test
  public void test0(){

      int[] intArray0 = {927947039, -1227309943, 2027659101};
      cn.ios.sort.BubbleSort.bubbleSort(intArray0);

  }



  @Test
  public void test1(){

      int int1 = -1830979718;
      double double2 = 0.7876193907070153d;
      int int3 = -1090146517;
      char char4 = '\'';
      short short5 = -19355;
      byte byte6 = 74;
      boolean boolean7 = false;
      double[] doubleArray8 = {0.13428247594696296d, 0.7386975318837308d, 0.973030484476728d, 0.08691362570572014d};
      float[] floatArray9 = {0.0056562424f, 0.8168033f, 0.8146966f, 0.9335173f};
      byte[] byteArray10 = {73, 110, -100, 27};
      boolean[] booleanArray11 = {true, false, false, true};
      short[] shortArray12 = {9137, -26400};
      java.lang.String[] stringArray13 = {"e>U", ";PK'A).=S?,PJ<TR^"};
      cn.ios.sort.BubbleSort bubbleSort0 = new cn.ios.sort.BubbleSort(int1, double2, int3, char4, short5, byte6, boolean7, doubleArray8, floatArray9, byteArray10, booleanArray11, shortArray12, stringArray13);
      bubbleSort0.toString();

  }



}
```

# 使用示例
### 1/5 JUnitGenerationSample1 为例   
![avatar](https://github.com/cuixiaoyiyi/pic/blob/master/JUnitGenerationSample1_src.png)  
### 2/5 运行命令  
```
java -cp JUnitGeneration_V0.2_20200305.jar cn.ios.junit.JUnitGenerationMain -t  /Users/cbq/Desktop/isca/workspace/JUnitGenerationSample1/bin -jlib ./jdk1_8_0_172/rt.jar -n 2
```
### 3/5 生成monkeytest目录  
![avatar](https://github.com/cuixiaoyiyi/pic/blob/master/monkeytest.png)  

### 4/5 在IDE中 Use as Source Folder   
![avatar](https://github.com/cuixiaoyiyi/pic/blob/master/monkeytest_tree.png)

### 5/5 import JUnit
