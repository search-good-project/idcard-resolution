# 身份证解析小工具
## 使用说明
可以根据输入的身份证号输出，此身份证号的省份，城市，区县，性别，出生日期。

### Demo

```java

    String idcard = "341125199001011995";
	IdcardInfoExtractor extractor = new IdcardInfoExtractor(idcard);
	extractor.getGender();
	extractor.getCity();
	extractor.getProvince();
	extractor.getBirthday();
	System.out.println(extractor.toString());

```
输出为


```

省份：安徽省，城市：滁州市，地区：定远县,性别：男,出生日期：Mon Jan 01 00:00:00 CST 1990

```


## 原理说明
**判断18位身份证的合法性**根据〖中华人民共和国国家标准GB11643-1999〗中有关公民身份号码的规定，公民身份号码是特征组合码，由十七位数字本体码和一位数字校验码组成。排列顺序从左至右依次为：六位数字地址码，八位数字出生日期码，三位数字顺序码和一位数字校验码。
*   顺序码：表示在同一地址码所标识的区域范围内，对同年、同月、同 日出生的人编定的顺序号，顺序码的奇数分配给男性，偶数分配 给女性。
*   前1、2位数字表示：所在省份的代码； 
*   第3、4位数字表示：所在城市的代码； 
*   第5、6位数字表示：所在区县的代码；
*   第7~14位数字表示：出生年、月、日；
*   第15、16位数字表示：所在地的派出所的代码；
*   第17位数字表示性别：奇数表示男性，偶数表示女性；
*   第18位数字是校检码：也有的说是个人信息码，一般是随计算机的随机产生，用来检验身份证的正确性。校检码可以是0~9的数字，有时也用x表示。
*   第十八位数字(校验码)的计算方法为： 
    * 将前面的身份证号码17位数分别乘以不同的系数。从第一位到第十七位的系数分别为：7 9 10 5 8 4 2 1 6 3 7 9 10 5 8 4 2
    * 将这17位数字和系数相乘的结果相加。
    * 用加出来和除以11，取余数
    * 余数只可能有0 1 2 3 4 5 6 7 8 9 10这11个数字。其分别对应的最后一位身份证的号码为1 0 X 9 8 7 6 5 4 3
    * 通过上面得知如果余数是2，就会在身份证的第18位数字上出现罗马数字的Ⅹ。如果余数是10，身份证的最后一位号码就是2。
	