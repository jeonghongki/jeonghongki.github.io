---
title:  "[Android] 안드로이드 플랫폼 아키텍처"
description: "Android 앱 개발의 특징, 안드로이드 플랫폼 아키텍처 구성 학습내용"

categories: [Android]
tags: [Android, Java, Architect]
comments: true
 
date: 2023-03-11
last_modified_at: 2023-03-19
---
# Android 앱 개발 특징
## Android 플랫폼 아키텍처
### Android 아키텍처
기본적인 안드로이드 플랫폼 아키텍처는 아래와 같다.
![안드로이드 소프트웨어 스택(출처: https://developer.android.com/guide/platform)](/content_img/Android_software_stack.png)
안드로이드 소프트웨어 스택(출처: https://developer.android.com/guide/platform)

안드로이드 플랫폼은 리눅스 커널 기반이며 HAL(Hardware Abstaction Layer)은 자바 API프레임워크에 하드웨어 기능을 이용하는 표준 인터페이스를 제공한다.
 1. System Apps: Android Appplication 개발에 필요한 API를 제공, 일반적인 Application이 해당 계층에 속함 (ex, SMS, Email, Calendar Application 등...), Android Application Layer로 생각하면 될 것 같음.
   
 2. Java API Framework: Android Application개발에 필요한 기본 기능을 제공, Android Application에서 필요한 기능을 구현하기 위해서 사용되며, 이러한 API는 핵심 모듈식 시스템 구성 요소 및 서비스를 재활용을 단순화하여 Android App을 제작하는데 필요한 빌딩블록을 구성함, Application Framework Layer로 생각하면 될 것 같음.
    - Activity Manager - 앱의 수명 주기를 관리하고 공통 탐색 백 스택 제공
    - Window Manager - 앱의 Window Manager는 Display에 바인딩 됨, 앱 윈도우(Window)를 관리하고 디바이스 화면에 출력하는 역할을 수행함
    - Location Manager - 시스템 위치 서비스에 대한 액세스 제공
    - Telephony Manager - 디바이스의 전화 통신 서비스 및 정보에 대한 액세스 제공 
    - Resource Manager - 현지화된 문자열, 그래픽 및 레이아웃 파일과 같은 코드가 아닌 리소스에 대한 액세스 제공
    - View System - 목록, 그리드, 텍스트 상자, 버튼 및 삽입 가능한 웹브라우저를 포함하여 앱의 UI를 빌드하는 데 사용 가능
    - Notification Manager - 모든 앱이 상태 표시줄에 사용자 지정 알림을 표시할 수 있도록 지원
    -  Package Manager - 장치에 현재 설치되어 있는 응용 프로그램 패키지와 관련된 다양한 종류의 정보 액세스 제공
    -  Content Providers - 앱이 주소록 앱과 같은 다른 앱의 데이터에 액세스하거나 자신의 데이터를 공유할 수 있도록 지원
 3. Native C/C++ Libaries: Android Application 개발에 필요한 라이브러리 제공(ex, 그래픽 처리를 위한 OpenGL, DB관리를 위한 SQLite 등...), 추가로 C 또는 C++ 코드가 필요한 앱을 개발하는 경우에는 Android NDK를 사용하여 Native 코드에서 이러한 네이티브 플랫폼 라이브러리에 엑세스 가능, Libaries Layout로 생각하면 될 것 같음.
 4. Android Runtime: Android 5.0(API Level 21) 이상에서 실행하는 경우에는 각 앱이 자체 프로세스 내 자체 ART(Android 런타임) 인스턴스로 실행되며, API Level 21 이전 버전에서는 Dalvik이 Android 런타임이었음, 앱이 ART에서 제대로 실행되면 Dalvik에서도 제대로 실행되지만, 그 반대의 경우엔 제대로 실행된다는 보장이 없음, Android Runtime Layer로 생각하면 될 것 같음.
 5. HAL(하드웨어 추상화 계층): 상위수준 Java API 프레임워크에 기기 하드웨어 기능을 노출하는 표준 인터페이스를 제공, 여러 라이브러리 모듈로 구성되어 있음.
 6. Linux 커널: Android 플랫폼 기반은 Linux 커널임, Linux 커널을 사용하면 Android가 주요 보안 기능을 활성화하고 기기 제조업체가 널리 알려진 커널용 하드웨어 드라이버를 개발할 수 있음.

### 안드로이드 런타임(ART)
안드로이드 앱 개발은 Java언어를 사용한다. Java로 개발된 다른 애플리케이션은 런타임 때 JVM이 수행하지만, Android VM은 ART(ART는 API Level 21(Android 5.0)에서 새로 추가된 VM이며, 이전 버전 VM은 Dalvik을 이용)를 이용하며 그 위에 일반 애플리케이션 개발 시 이용할 수 있는 자바 API 프레임워크를 제공한다.

ART 기능 (Android 공식 문서내용, 공부가 더 필요한 부분...)
- AOT(Ahead-of-time) 컴파일
- 가비지컬렉션(GC) 개선
- 개발 및 디버깅 개선

ART 특징 (Chat GPT 답변 내용, 공부가 더 필요한 부분...)
- 빠른 실행속도: ART는 애플리케이션 실행 전 미리 컴파일(dex2oat 도구를 사용하여 컴파일, DEX파일을 입력으로 받음)하여 컴파일 된 앱을 생성하므로 Dalvik VM의 JIT(Just-in-Time) 컴파일 방식과 달리 미리 컴파일 > 최적화 된 코드를 생성해 실행속도가 빠름
- 작은 메모리 사용량: 이전 Dalvik VM에서는 필요한 메모리 공간을 할당했으나 ART는 메모리 사용량을 줄이기 위해서 필요한 메모리 공간만 할당함
- 앱의 시작속도 향상: ART는 미리 컴파일하여 최적화된 코드를 생성하므로 앱의 시작 속도가 향상됨
- 배터리 수명 향상: ART는 더 적은 CPU사용으로 더 적은 전력을 소모하므로 배터리 수명을 늘리는데 도움을 줌

참고자료
- 깡샘의 안드로이드 프로그래밍
- Android 플랫폼 아키텍처 (https://developer.android.com/guide/platform)
- Android 런타임(ART) 및 Dalvik (https://source.android.com/docs/core/runtime)
- ChatGPT 