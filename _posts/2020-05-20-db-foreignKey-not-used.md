---
title: "왜 DBMS에 있는 외래키(Foreign Key)를 사용하지 않는걸까?"
date: 2020-05-20 14:02:28 -0400
categories: [DBMS, Database, ForeignKey, 왜래키 사용안하는 이유]
tags: [DBMS, Database, ForeignKey, 왜래키 사용안하는 이유]
layout: page
date: 2020-05-20 14:20:00
---
  
```
Reasons not to use foreign keys.
Don't let the team leader use the foreign keys.
```

처음 회사에 입사 후 개발을 처음 시작할당시(코린이 시절) 테이블을 생성해야 하는 업무가 있었는데 개발팀 팀장님이 외래키를 만들지 말라고 하셨다.  
당시에는 개발에관한 지식이 전무하였기에 당연히 그대로 진행하였지만, 추후 여러 프로젝트를 진행하면서 실제로 외래키가 사용되는곳은 보지 못하였고 문득 외래키가 사용되지 않는 이유가 궁금해졌다.

<h1> 그렇다면 왜 외래키를 사용하지 않는걸까? </h1>

<h2><font color='blue'>Foreign Key를 사용하지 않을때의 문제</font></h2>
  - <font color='red'> a. 잠재적인 데이터 무결성 문제 </font>
    *  외래 키가 없으면 데이터베이스가 참조 무결성을 강화할 수 없으며, 상위 수준에서 올바르게 관리하지 않으면 데이터가 일치하지 않을 수 있습니다(해당 부모 행이없는 자식 행)
    
예시 1. 
<img src="https://dataedo.com/asset/img/blog/wrong_join_double.png" width="750" height="200"> 

그림2.
<img src="https://dataedo.com/asset/img/blog/wrong_join_missing.png" width="750" height="200"> 

```
select project_no, count(*)
from projects
group by project_no
having  count(*) > 1
```

  - b. <font color='red'> 테이블 관계의 이해도 부족 </font>
    * 데이터베이스에 외래 키 부족으로 인한 눈에 덜 띄는 또 다른 부정적인 영향은 스키마를 모르는 사람들이 올바른 테이블을 찾고 테이블 관계를 파악하는 데 어려움을 겪고 있다는 것입니다.
  데이터베이스에서 쿼리 및보고 에 심각한 문제 가 발생할 수 있습니다.





<h3><font color='blue'>Foreign Key를 사용하지 않을때 장점</font></h3>
  - a. <font color='red'>성능</font>
    * 테이블에 외래 키가 있으면 데이터 품질은 향상되지만 삽입(insert), 업데이트(update) 및 삭제(delete) 작업의 성능은 저하됩니다.   
    트랜잭션 방식(한번에 한행)으로 데이터를 처리하지 않고, 대량으로 데이터를 처리할 경우에 특히 그렇습니다.

  - b. <font color='red'>레거시 데이터</font>
    * 데이터 품질 및 무결성에 엄격하지 않은 오래된 데이터베이스 또는 프로그램 구성이 레거시 데이터를 저장하도록 설계된 많은 데이터베이스가 있습니다.  
  오래된 레거시 데이터 아키텍트를 포함하려면 아래와 같은 선택지가 있습니다.
	>  a) 레거시 데이터를 정리 및 변환합니다. (현실적으로 어려움)  
	>  b) 데이터베이스 수준에서 참조 무결성을 강화하는 것을 포기할 수 있습니다.

  - c. <font color='red'>DBMS의 변경 가능성 고려</font>
    * 어플리케이션 개발시 다양한 DBMS(Oracle, MySql, MS-SQL(SQL Server), PostgreSQL 등)를 선택할 수 있습니다.
  따라서 프로그램을 설계할 때 특정 DBMS에 종속되지 않게 구성하기 위해, 데이터베이스가 아닌 어플리케이션에서 참조무결성과 같은 역할을 할 수 있도록 구현 할 수 있습니다.


  - d. <font color='red'>수준높은 프레임워크의 편리한 사용으로 인해(Spring 등)</font>
    * 우리나라의 경우 MyBatis를 많이 사용하지만 Hibernate, JPA 등과 같은 ORM Framework도 많이 사용됩니다.  
    위와같은 프레임워크에서 데이터베이스 테이블 및 외래키를 생성 할 수 있지만, 개발자가 항상 외래키를 생성하지 않습니다.  
    가령 ORM Framework가 아닌 DBMS Tool(Toad, Orange, DBeaver, Microsoft SQL Server Management Studio 등)을 이용하여 테이블 및 외래키를 생성하여도 프로그램 개발 중 즉각적으로 체감하지 못할 수 있습니다.

  - e. <font color='red'>유연한 설계</font>
    * 우리가 데이터베이스에서 데이터를 저장하기 위해 제일 먼저 고려하는것은 테이블 및 컬럼생성입니다.  
    데이터의 연속성, 무결성, 고유값, 외래키 등은 제약조건이지 필수가 아니여서 종종 테이블 생성시 누락이됩니다.  
    (개발기간이 끝나고 단위테스트 및 통합테스트 진행시 필요에 의하여 추가되는경우가 종종 있습니다)  
    때로는 DBA나 아키텍쳐로 일하시는 분들이 놓치기도 합니다.

<h4>결론</h4>
외래키(Foreign Key)를 사용하지 않을때의 장단점을 고려하여 외래키를 사용하지 않는 이유를 생각해보면

외래키를 사용하지 않을 때 
- 단점 
  * 커버가 가능
- 장점
  * __<font color='red'>성능 같은 경우에는 대용량 트래픽을 처리하는데 있어서 고려해야 할 1순위 조건</font>__ 이기 때문에 실제로 많은 곳에서 외래키를 사용하지 않는것으로 보여집니다.
  * DB Migration과 같은 작업이 필요할 때, __<font color='red'>이전에 설계 및 적재 데이터 중 무결성조건에 맞지않은 데이터를 찾아내고 정리(클린징)하는것은 현실적으로 어렵기 때문에</font>__ 외래키를 사용하지 않는것으로 보여집니다.(참조 무결성 포기)

--- 

__참고사이트__
1. 9 reasons why there are no foreign keys constraints in your database (referential integrity checks)
	<https://dataedo.com/blog/why-there-are-no-foreign-keys-in-your-database-referential-integrity-checks>
