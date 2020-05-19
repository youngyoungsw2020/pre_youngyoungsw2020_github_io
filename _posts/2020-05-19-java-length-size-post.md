---
title: "java에서는 길이를 구할 때 왜 length와 size를 혼합하여 사용할까?"
date: 2020-05-19 17:02:28 -0400
categories: java Array List Size length
---

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
 - Collection Object(ArrayList, Set etc)
 - java.util.collection의 메소드이다
 - java.util.ArrayList, java.util.Set는 Collection 타입을 상속받아 사용하기 때문에 길이값을 구할 때 size() 함수를 사용한다.
 ```
   ex)
        ArrayList<String> testArr = new ArrayList<String>();
        testArr.add("one");
        testArr.add("Two");
        int num = testArr.size();
 ```

```
참고사이트 
[JAVA]자바_ length / length() / size() 사용법 및 차이
https://mine-it-record.tistory.com/126
{% post_url https://mine-it-record.tistory.com/126 %}

JAVA -size()와 length() 그리고 length의 차이
https://chibychi.blogspot.com/2019/01/java-size-length-length.html
```


