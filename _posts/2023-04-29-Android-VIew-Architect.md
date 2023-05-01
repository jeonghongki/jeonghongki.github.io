---
title:  "[Android] 뷰 아키텍처"
description: "Android View 계층구조 학습내용"

categories: [Android]
tags: [Android, Java, Architect, View, ViewGroup, DOM, Hierarchy]
comments: true
 
date: 2023-04-29
last_modified_at: 2023-05-01
---
# Android 뷰 아키텍처
## Android 뷰 계층구조
### Android 뷰의 계층구조 알아보기
뷰의 기본 구조는 뷰 객체간 계층으로 이루어져 있으며 SW모델로 이야기하면 DOM(Document Object Model)을 따르고 있으며<br/>
디자인 패턴으로는 Gof 디자인 패턴의 Composite 패턴이 적용된 구조이다.

### DOM(Document Object Model)
DOM(Document Object Model)은 문서 객체 모델을 의미한다.<br/>
HTML, XML과 같은 마크업 언어로 작성된 문서의 구조와 내용에 대한 표현을 기반으로 객체 모델을 구성하는 방식으로 트리 구조로 이루어져 있다.<br/>
이 트리 구조는 문서의 각 요소들을 객체로 표현하여 구성되며 각 객체들은 각 요소들이 가지는 속성/메소드를 포함한다.<br/>
DOM구조를 잘 사용하면 문서의 내용, 구조를 동적으로 변경하거나 특정 요소들에 접근하여 조작하는 작업들이 가능하다.<br/>
![디렉터리-파일 구조](/content_img/Directory-File_Structure.png)디렉터리-파일 구조(출처: 깡샘의 안드로이드 프로그래밍)

### 뷰의 계층구조
안드로이드 뷰 클래스 기본구조가 SW모델로 DOM(Document Object Model)을 따른다고 하였으므로<br/>
그에 맞춰 기본골격을 클래스 다이어그램(Class Diagram)으로 그리면 아래와 같다.<br/>
![뷰계층 구조](/content_img/View-Hierarchy_Structure.png)뷰 계층구조(출처: 깡샘의 안드로이드 프로그래밍)<br/>

디렉터리 계층구조와 뷰의 계층구조가 동일함을 확인할 수 있다.<br/>
전체적인 뷰 객체의 계층구조를 예시로 그려보면 아래와 같이 표현할 수 있다.<br/>
![뷰계층 구조](/content_img/ViewGroup-View-Hierarchy_Structure.png)뷰 계층구조(출처: 깡샘의 안드로이드 프로그래밍)<br/>
안드로이드 뷰 클래스도 디렉터리 클래스와 같이 객체를 원하는 만큼 생성한 다음 계층구조로 묶어서 사용한다.

참고자료
- 깡샘의 안드로이드 프로그래밍
- ChatGPT 