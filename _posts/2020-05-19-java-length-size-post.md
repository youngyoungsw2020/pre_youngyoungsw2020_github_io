---
title: "java에서는 길이를 구할 때 왜 length와 size를 혼합하여 사용할까?"
date: 2020-05-19 16:48:28 -0400
categories: jekyll update
---

1. length
 - arrays(int[], double[], String[])

 - length는 배열의 길이를 알고자 할때 사용된다.

2. length()
 - String related Object(String, StringBuilder etc)

 - length()는 문자열의 길이를 알고자 할때 사용된다.

3. size()
 - Collection Object(ArrayList, Set etc)
 - size()는 컬렉션프레임워크 타입의 길이를 알고자 할때 사용된다.
 - java.util.ArrayList는 Collection 타입을 상속받아 사용하기 때문에 길이값을 구할 때 size() 함수를 사용한다. 


참고사이트 
자바_ length / length() / size() 사용법 및 차이
https://mine-it-record.tistory.com/126 [JAVA] 


[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/