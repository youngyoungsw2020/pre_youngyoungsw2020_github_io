---
title: java에서는 길이를 구할 때 왜 length와 size를 혼합하여 사용할까?
date: '2020-05-19 17:02:28 -0400'
categories: java Array List Size length
published: true
---


size()는 java.util.Collection에 지정된 메소드이며 표준 라이브러리의 모든 데이터 구조에 의해 상속됩니다.  

length는 모든 배열의 필드입니다. (배열은 객체이며 클래스는 정상적으로 보지 못합니다)  

length()는 java.lang.String의 메소드이며 char[]의 얇은 래퍼입니다.  
설계 상으로는 문자열은 변경 불가능하며 모든 최상위 Collection 서브 클래스는 변경 가능합니다.  
따라서 "길이"가 표시되는 곳은 상수이고 "크기"가 표시되는 곳은 그렇지 않습니다.  


1. length
 - arrays(int[], double[], String[])
 - length는 배열의 길이를 알고자 할때 사용된다.
 - length는 array의 field값이다(그래서 뒤에 ()가 안붙는다)
 - arrays(int[] , double[] , String[]) 는 배열의 길이를 알고자할때 사용한다
 ```
   ex)
        String[] strarr = {"one", "two"};
        int num3 = strarr.length;
 ```
	
				
2. length()
 - String related Object(String, StringBuilder etc)
 - length()는 문자열의 길이를 알고자 할때 사용된다.
 - length(String)는 java.lang.String의 메소드이다.
 - length(String)는 문자열의 길이를 알고자 할때 사용한다
 ```
   ex)
        int num2 = "onetwo".length();
 ```
 
 
3. size()
 - Collection Object (ex> ArrayList, Set etc)
   > java.util.ArrayList, java.util.Set는 Collection 타입을 상속받아 사용하기 때문에 길이값을 구할 때 size() 함수를 사용한다.
 - java.util.Collection의 메소드이다
 - Collection을 상속받아 구현된 클래스 (ex java.util.ArrayList, java.util.Set 등)
 ```
   ex)
        ArrayList<String> testArr = new ArrayList<String>();
        testArr.add("one");
        testArr.add("Two");
        int num = testArr.size();
 ```

__참고사이트__
1. [JAVA]자바_ length / length() / size() 사용법 및 차이  
   <https://mine-it-record.tistory.com/126>
2. JAVA -size()와 length() 그리고 length의 차이  
   <https://chibychi.blogspot.com/2019/01/java-size-length-length.html>
3. java - 크기와 길이 방법의 차이?  
   <https://ko.coder.work/so/java/117210>
