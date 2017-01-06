layout: post
title: Auto Layout
tags: ios, swift, whitehobbit, auto layout



> 이 문서는 Xcode의 storyboard를 이용하여 Auto Layout을 사용하는 방법을 다룬다.
>
> 작성자: *임하빈, 마지막 수정: 2017.01.06*

# Auto Layout

**index**

{:toc}

### 1. Auto Layout이란?

#### 1.1 개념

아이폰의 크기가 다양해지고, 아이패드가 등장하며 앱 화면의 디자인의 파편화가 심화되었다. 이를 극복하기 위해 등장한 것이 Auto Layout이다. 

Auto Layout은 다양한 화면 크기에 맞춰 자동으로 레이아웃을 조절해주는 역할을 한다. Constraint(제약)을 통해 위치와 크기에 대한 표시 규칙을 기반으로 레이아웃을 변경하고 조절한다.

**Constraint(제약)**

Constraint(제약)은 앱의 디자인이 각각의 다른 화면 크기로 표현될 때, 어떠한 것을 기준으로 element(요소)를 배치할 지를 지정하는 규칙을 의미한다.

배치에는 Align(정렬)과 Pin(고정)의 2가지 방식이 존재한다. Align은 가운데 정렬이나 다른 요소와 모아서 정렬을 하고자 할 경우 사용하며, 화면 상하 좌우 가장자리에 고정 표시할 경우와 크기 고정 시에는 Pin을 사용한다.

기본적인 Constraint(제약)에는 

​	Leading: elements 좌측

​	Trailing: elements 우측

​	Top: elements 상단

​	Bottom: elements 하단

​	Width: elements 너비

​	Height: elements 높이

​	centerX: elements 가로 중심

​	centerY: elements 세로 중심

​	Baseline: 문자 baseline

​	Horizontal: 수평

​	Vertical: 수직

​	Aspect Ratio: elements 가로세로 비율



**Constraint를 적용시키는 2가지 방법**

(1) Constraint를 적용하고자 하는 attribute를 선택하고 `Ctrl`키를 누른 상태에서 해당 attribute와 위치를 비교할 attribute와 이어주기

(2) Constraint를 적용하고자 하는 attribute를 선택하고 `Add New Constraints` 를 이용해 Constraint 추가하기



**Constraint의 요소**

First Item: Constraint를 적용시키고자 하는 attribute

Relation: Less Than or Equal, Equal, Greater Than or Equal, 최소 값, 최대 값, 특정 값 지정

Second Item: Constraint 비교 대상

Constant: value를 의미

priority: 우선순위를 의미 default값은 1000, 숫자가 작을 수록 우선순위가 높음

Mutiplier: First Item의 사이즈를 Second Item와 같게 했을 경우, Second Item에 대한 배율

Identifier: 해당 Constraint의 식별자

Installed: 이 속성을 체크해야지 해당 Constraint가 적용됨


### 2. Auto Layout 실전 활용

#### 2.1 Addrbook의 주소록 : 세부화면 만들기

**프로젝트 생성**

Xcode를 실행해 iOS 탭의 `Single View Application`을 선택하고 프로젝트를 하나 생성한다.

생성된 프로젝트의 `main.storyboard` 파일을 선택하면 아래와 같은 화면이 보인다.

![main.storyboard](https://github.com/whitehobbit/Addrbook-detail/blob/master/iOS%20Study/auto%20layout%2001.png?raw=true)

**타이틀 뷰 생성하기**

위 그림에서 보이는 뷰컨트롤러에 뷰의 타이틀이 들어갈 View를 하나 추가한다.

![뷰 추가](https://github.com/whitehobbit/Addrbook-detail/blob/master/iOS%20Study/auto%20layout%2002.png?raw=true)

이 뷰에 Constraint를 걸어 auto layout을 적용한다.

여기서 적용시킬 Constraint는 width, centerX, top, height이다.

`width`는 `부모 attribute의 width`와 동일하게, `centerX`는 `부모 attribute의 centerX`와 동일하게, 

`top`은 `top layout guide - 20`, `height`는 `60`으로 지정하고자 할 때,

Constraint를 적용시키는 방법은 크게 2가지가 존재한다. 

​	(1) 해당 attribute를 선택하고 `Ctrl`키를 누른 상태에서 해당 attribute와 위치를 비교할 attribute와 이어주기
​		(고정 width와 height 크기를 사용하고 싶은 경우에는 자기 자신으로 이어준다)

​	attribute를 선택하고 `Ctrl`키를 누른 상태에서 부모 attribute로 끌어오면 아래와 같이 나타난다.

![Constraint 01](https://github.com/whitehobbit/Addrbook-detail/blob/master/iOS%20Study/auto%20layout%2003.png?raw=true)

​	적용하고자 하는 Constraint를 선택하고, 수치를 입력한다. 

​	(여기서는 Equal Widths, Vertical Spacing to Top Layout Guide, Center Horizontally in Container를 선택)

​	`Height `를 60으로 지정하기 위해, 스스로에게 이어주면 아래와 같이 나타난다.

![Constraint 02](https://github.com/whitehobbit/Addrbook-detail/blob/master/iOS%20Study/auto%20layout%2004.png?raw=true)

​	`Height`를 선택하고 60을 지정해준다.

​	(2) 해당 attribute를 선택하고 `Add New Constraints` 를 이용해 Constraint 추가하기

​	`Add New Constraints` 버튼을 클릭하면 아래와 같이 나타난다.

![Constraint 03](https://github.com/whitehobbit/Addrbook-detail/blob/master/iOS%20Study/auto%20layout%2005.png?raw=true)

​	여기서 사용하고자 하는 Constraint를 선택 후 수치를 입력한 후, `Add Constraints`를 클릭.

**타이틀 Label 생성**

타이틀뷰에 `Label`을 하나 생성한 후, `Label`과 타이틀뷰를 이어 `Equal Width`, `Equal Height`, `Center Horizontally in Container`, `Bottom Space to Container`를 선택

`Equal Height`의 값을 `타이틀뷰의 Height-20`을 하기 위해 `Constant`에 `-20`을 써준다. 

타이틀 Label을 주소록 : 세부화면으로 변경하고 가운데 정렬을 하면 아래와 같이 나타난다.

![타이틀 label 생성](https://github.com/whitehobbit/Addrbook-detail/blob/master/iOS%20Study/auto%20layout%2006.png?raw=true)

**콘텐츠 뷰 생성**

뷰를 하나 생성하고 이름을 ContentsView로 정의한다.

콘텐츠 뷰를 전체뷰와 이어 `Equal Widths`, `Center Horizontally in Container`, `Vertical Spacing to Bottom Layout Guide`를 선택한다.

`Equal Widths`의 `Multiplier`를 `0.9`, `Vertical Spacing to Bottom Layout Guide`의 `Constant`를 `20`으로 지정한다.

콘텐츠 뷰를 타이틀 뷰와 이어 `Vertical Spacing`을 `20`으로 지정하면 아래와 같이 나타난다.

![콘텐츠 뷰 생성](https://github.com/whitehobbit/Addrbook-detail/blob/master/iOS%20Study/auto%20layout%2007.png?raw=true)

**콘텐츠 생성**

콘텐츠 뷰에 6개의 뷰를 생성하고 각각  `Name View`, `Email View`, `Tel View`, `Birth View`, `Comp View`, `Memo View`로 정의한다.

`Name View`의 `Constraints`는 콘텐츠 뷰와 이어 `Equal Widths`, `Equal Height`의` Multiplier = 1/7`, `Vertical Spacing to Top Layout Guide`의` Constant = 0`으로 지정한다.

`Name View`의 안에 `Label`을 2개 생성하여 `이름`, `홍길동`으로 정의한다. 

`이름 Label`의  `Constraints`는 `Name View`와 이어 `Equal Width`의 `Multipler = 0.35`, `Constant = -20`, `Leading Space to Container`의 `Constant = 20`으로 한다.

`홍 길동 Label`의 `Constraints`는 `Name View`와 이어 `Equal Width`의 `Multipler = 0.65`, `Constant = -15`, `Leading Space to Container`의 `Constant = 15`으로 한다.

`Email View`, `Birth View`, `Comp View`는 `Vertical Spacing to Top Layout Guide` 대신 위쪽 뷰와 이어 `Vertical Spacing`의 `Constant`를 `0`으로 설정하고 나머지는 `Constant` 동일하게 `Constraints`를 설정한다.

`Memo View`도 동일하게 생성하지만 `Equal Height`의` Multiplier`를 `2/7`로 설정한다.

`Memo View`를 제외한 각각의 뷰의 콘텐츠는 `Name View`와 동일하게 설정한다.

`Memo View`의 콘텐츠는 `Label` 1개와 `Text View` 1개로 구성하며, `Label`은 나머지 콘텐츠들과 동일하게 `Constraint`를 주고, `Text View`는 `Equal Height`의 `Multiplier = 0.8`을 추가한다.

`Constraints`를 전부 지정하면 아래와 같이 나온다.

![콘텐츠](https://github.com/whitehobbit/Addrbook-detail/blob/master/iOS%20Study/auto%20layout%2008.png?raw=true)

**[소스 코드][1]**

[1]:https://github.com/whitehobbit/Addrbook-detail
