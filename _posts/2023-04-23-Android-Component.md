---
title:  "[Android] 안드로이드 컴포넌트 기반 개발"
description: "Android 컴포넌트 개념, 컴포넌트 종류 학습내용"

categories: [Android]
tags: [Android, Java, Architect, Component]
comments: true
 
date: 2023-04-23
last_modified_at: 2023-04-23
---
# Android 앱 아키텍처 특징
## Android 컴포넌트
### Android 컴포넌트란?
컴포넌트는 앱의 구성단위로 안드로이드 앱을 작성한다는 것은 컴포넌트를 작성한다는 것과 동일하다.<br/>
안드로이드에서 컴포넌트의 물리적인 모습은 Class(클래스)로 하나의 클래스가 컴포넌트이다.<br/>
단, 모든 클래스가 컴포넌트인 것은 아니다. 일반 클래스와 컴포넌트로 구분할 수 있는데 이 둘의 차이는 생명주기를 누가 관리하는지로 구분할 수 있다.
 - 일반 클래스 - 코드로 생명주기를 관리한다. 즉, 필요할 때 new 연산자로 생성, 필요 없어지면 null대입으로 소멸시킨다.
 - 컴포넌트 - 생명주기를 안드로이드 시스템이 생성해 관리 및 소멸함

### 컴포넌트 = 앱 내 독립적 실행단위
컴포넌트도 클래스이므로 시스템이 생명주기를 관리해 '독립적인 수행단위'로 동작한다.<br/>
따라서 직접 코드로 해당 컴포넌트를 실행시키는 것이 아닌 Intent를 매개로 결합하지 않고 독립적으로 실행시키며
독립적으로 실행할 수 있으므로 앱의 수행 시점이 다양할 수 있다.

### Android 컴포넌트 특징
 - 안드로이드는 컴포넌트 기반의 개발이다.
 - 각 컴포넌트는 개발자 코드 간 결합이 발생하지 않는다.
 - 컴포넌트의 생명주기는 시스템이 관리해 앱 수행시점이 다양할 수 있다.

### Android 컴포넌트 종류
 1. 액티비티(Activity): 사용자 화면을 제공하는 컴포넌트, 안드로이드 앱은 클라이언트 측 애플리케이션이므로 화면 구성이 중요해 가장 많이 작성하는 컴포넌트
   - 사용자 인터페이스(UI)를 제공하는 컴포넌트
   - 애플리케이션 화면을 구성하는 기본 단위
   - 하나의 애플리케이션은 여러개의 액티비티를 가질 수 있으며, 각 액티비티는 스택형태로 관리된다.
 2. 서비스(Service): 화면과 전혀 상관없이 눈에 보이지 않으며, 백그라운드에서 장시간 수행하는 컴포넌트
   - 백그라운드에서 실행되는 컴포넌트
   - UI없이 장시간 수행됨
   - 네트워크 연결, DB 엑세스 등 작업 처리
 3. 브로드캐스트리시버(BroadcastReceiver): 이벤트 모델 수행 컴포넌트로 인텐트 원리 이해 필요
   - 안드로이드 시스템으로부터 다양한 이벤트를 수신하는 컴포넌트, 이벤트를 수신해 특정 작업을 처리하는 등 동작을 수행함
 4. 콘텐츠프로바이더(ContentProvider): 앱 간 데이터 공유 목적으로 사용하는 컴포넌트
   - 애플리케이션 간 데이터를 공유하기 위한 컴포넌트, DB, FIle System 등 데이터에 접근할 수 있는 인터페이스를 제공

참고자료
- 깡샘의 안드로이드 프로그래밍
- ChatGPT 