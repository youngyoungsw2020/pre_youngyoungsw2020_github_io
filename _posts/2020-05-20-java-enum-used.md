---
title: "Java Enum 클래스의 사용이유"
date: 2020-11-19 09:30:28 -0400
categories: [Java Enum,Enum,Java Enumeration]
tags: [Java Enum,Java Enum 사용이유,Enum,Java Enumeration]
layout: page
date: 2020-11-19 09:30:28
---
  
```
Why use Java Enum class?
```

Java에서 Enum 은 java 1.5 부터 지원된 클래스이다.

프로젝트를 소스 분석 중 Enum 클래스를 사용한 파일을 보게되었다.
소스를 확인해보니 기존에 상수를 선언하는 방식과는 약간 다르게 선언되어 있음을 알수있었다.

결국에는 상수로써 사용하는건데 왜 Enum 클래스를 사용하는걸까?

평소에 내가 프로젝트를 진행하며 보던 상수관리를 하는 클래스는 보통 이렇게 작성되어있다.


<pre><code>
public class CommonConstant {
	
	/**
	 * 날짜 공통상수
	 */
	public final static String COMMON_DATE_FORMAT = "dd.MM.yyyy";
	public final static String COMMON_TIME_FORMAT = "HH:mm:ss";
	public final static String COMMON_DATE_TIME_FORMAT = "dd.MM.yyyy HH:mm:ss";
	
	
	/**
	 * 자동차 공통상수
	 */
	public final static String COMMON_CAR_CODE = "333300";
	public final static String COMMON_BUS_CODE = "333301";
	public final static String COMMON_TEXI_CODE = "333301";
	
}
</code></pre>

아래는 Enum 클래스 예제이다.
Enum 클래스 사용시 조금 더 객체지향적으로 상수를 사용할 수 있으며 가시성이 뛰어나다!!

```
public class ApiCommonConstant {
	
	public enum DateFormat {
		dateFormat("dd.MM.yyyy")
		, timeFormat("HH:mm:ss")  
		, dateTimeFormat("dd.MM.yyyy HH:mm:ss")
		;
		
		private String str;
		DateFormat(String str){this.str = str;}
		
		public String getStr() {
			return str;
		}
	}
	
	public enum ResultStatusCode{
		car 	{String getCode(String val){return "333300";}}
		, bus 	{String getCode(String val){return (Integer.parseInt(val) + 1) + "";}}	// 보통 이렇게 사용하지 않는다. abstract Method 상속 예시를 위해 만듬  
		, texi	{String getCode(String val){return (Integer.parseInt(val) + 2) + "";}}	// 보통 이렇게 사용하지 않는다. abstract Method 상속 예시를 위해 만듬
		;
		
		ResultStatusCode(){}
		abstract String getCode(String val);
	}
	
}

```

```
public class test1 {

	public static void main(String args[]) {
	
		/* date Format 확인 */
		ApiCommonConstant.DateFormat DATE_FORMAT = ApiCommonConstant.DateFormat.dateFormat;
		ApiCommonConstant.DateFormat DATE_TIME_FORMAT = ApiCommonConstant.DateFormat.dateTimeFormat;
		ApiCommonConstant.DateFormat TIME_FORMAT = ApiCommonConstant.DateFormat.timeFormat;
		
		for(ApiCommonConstant.DateFormat dateFormat : ApiCommonConstant.DateFormat.values()) {
			System.out.println(dateFormat.ordinal() + "번째");
			System.out.println(dateFormat + " : " + dateFormat.getStr());
			
		}
		
		System.out.println();
		
		/* status Code 확인 */
		ApiCommonConstant.ResultStatusCode CAR = ApiCommonConstant.ResultStatusCode.car;
		ApiCommonConstant.ResultStatusCode BUS = ApiCommonConstant.ResultStatusCode.bus;
		ApiCommonConstant.ResultStatusCode TEXI = ApiCommonConstant.ResultStatusCode.texi;
		
		for(ApiCommonConstant.ResultStatusCode resultStatusCode : ApiCommonConstant.ResultStatusCode.values()) {
			String carCode = CAR.getCode("");
			System.out.println(resultStatusCode.ordinal() + "번째");
			System.out.println(resultStatusCode + " : " + resultStatusCode.getCode(carCode) );
		}
		
	}
	
}
```


<img src="https://youngyoungsw2020.github.io/myImages/enum-capture.png" width="350" height="200">

--- 

__참고사이트__
1. 우아한형제 기술블로그 - Java Enum 활용기
	<https://woowabros.github.io/tools/2017/07/10/java-enum-uses.html>
2. [Java] 열거 타입(Enum) 사용법 & 예제
	<https://coding-factory.tistory.com/522>	
