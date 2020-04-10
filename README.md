# JUnitGeneration 工具说明文档 
JUnitGeneration是一个自动生成JUnit测试代码的工具，其输入时Java字节码，输出是JUnit测试源代码。

### 所需环境
JDK1.8  （1.8+版本未测试） 
JUnit5

### 命令解释
| 命令       | 格式   |  说明 | 
|  -  | - | -  | 
| -t<br/>-targetByteCodeFolder| 文件夹路径；<br/>.jar文件全路径； | 必填参数；<br/>代表待测字节码的路径; |
| -jlib <br /> -javaLibJar| %YourJavaHome%/jre/lib/rt.jar | 必填参数；<br/>代表rt.jar的路径，jdk9及之后无该文件，暂时未处理该状况 |
|  -n  <br/> -number| 正整数  |  选填参数；<br/>每一个public方法生成的单元测试方法的数量；默认值为1  |

###  参数示例
| 命令       | 输入示例   |
|  -  | - |
|  -t  | 文件夹：C:\Users\C\eclipseworkspace\code\Sort\bin\ <br /> Jar包： C:\Users\C\eclipseworkspace\code\Sort.jar|
|  -jlib  | 有空格："C:\Program Files\Java\jdk1.8.0_231\jre\lib\rt.jar" <br /> 无空格: C:\Users\C\eclipseworkspace\rt.jar |
|  -n  | 2 |


### 命令行执行示例
```
java -cp JUnitGeneration_V0.2_20200305.jar cn.ios.junit.JUnitGenerationMain -t C:\Users\C\eclipseworkspace\code\Sort\bin\ -jlib "C:\Program Files\Java\jdk1.8.0_231\jre\lib\rt.jar" -n -2
```

### 执行后生成文件夹

| 输入  | 输出 |
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

### 工具未实现的支持
|| 未实现  | 说明 |
| -| - | - |
| 1| private\protected方法 | 可能影响覆盖率 |
| 2| 检测参数的合法性 | 生成的代码在执行时可能发生异常 |
| 3| 私有构造函数方法 | 代码生成时可能有编译错误（xxx is not visible） |
| 4| 泛型数组 | 程序执行时可能发生异常 | 
| 5| 断言语句 | 无法判断执行结果 |
| 6| 组合测试 | 未对该类的各个方法组合调用生成； |

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
![avatar](https://github.com/cuixiaoyiyi/Research/blob/master/Engineering/JUnitGeneration/JUnitGenerationSample1_src.png)  
### 2/5 运行命令  
```
java -cp JUnitGeneration_V0.2_20200305.jar cn.ios.junit.JUnitGenerationMain -t  /Users/cbq/Desktop/isca/workspace/JUnitGenerationSample1/bin -jlib ./jdk1_8_0_172/rt.jar -n 2
```
### 3/5 生成monkeytest目录  
![avatar](https://github.com/cuixiaoyiyi/Research/blob/master/Engineering/JUnitGeneration/monkeytest.png)  

### 4/5 在IDE中 Use as Source Folder   
![avatar](https://github.com/cuixiaoyiyi/Research/blob/master/Engineering/JUnitGeneration/monkeytest_tree.png)

### 5/5 import JUnit
