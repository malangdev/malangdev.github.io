---
layout: post
title: development
description: >
  아두이노를 이용하여 매크로 키보드 제작 (기초편)
sitemap: false
hide_last_modified: true
---

# 매크로 키보드 제작 (기초)

### 아두이노를 이용하여 매크로 키보드 만들기

일반적으로 마우스나 키보드를 자동으로 제어하고 싶을 때 매크로를 주로 사용한다.
Auto Hot Key (https://www.autohotkey.com/) 라는 매우 유명한 S/W가 있고, 그 밖에 알리익스프레스에서 'macro keyboard'로 검색하면 펌웨어에서 매크로를 동작시키도록 제작된 다양한 키보드들이 있다.

또 다른 방법으로 아두이노를 사용하여 쉽게 매크로 키보드, 마우스를 만들 수 있다. 주로 사용하는 아두이노 우노(Arduino Uno)를 사용하여 만들수 도 있지만, 아두이노 레오나르도(Arduino Leonardo)를 사용하면 매우 쉽게 만들 수 있다.

### 아두이노 레오나르도

레오나르도는 [위키백과](https://ko.wikipedia.org/wiki/%EC%95%84%EB%91%90%EC%9D%B4%EB%85%B8_%EB%A0%88%EC%98%A4%EB%82%98%EB%A5%B4%EB%8F%84)의 설명을 보면 Atmega32U4 MCU를 사용하고 있어서 다른 아두이노와 다르게 컴퓨터에서 HID 장치인 USB 마우스, 키보드 장치로 인식한다. 그래서 마우스, 키보드 신호를 보내도록 프로그래밍을 하면 실제 마우스, 키보드가 동작하는 것과 같은 효과를 낼 수 있다. 자동으로 특정 키보드의 키를 누르거나 마우스를 클릭 또는 이동시켜야 하는 경우 아두이노 레오나르도를 사용하여 프로그래밍으로 가능하다.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/3/38/Arduino_Leonardo.jpg/400px-Arduino_Leonardo.jpg)


### 키 누르기 프로그램 작성하기

첫 번째 프로그램은 간단히 1초 간격으로 'a'를 타이핑하는 프로그램을 제작해 본다.

우선 레오나르도를 PC에 연결한 후 Arduino Sketch에서 보드를 레오나르도로 선택(툴 > 보드 > 아두이노 레오나르도 선택) 하고 포트로 선택한다. 그 후 예제 프로그램를 작성한 후 컴파일 및 업로드하여 잘 동작 되는지 확인한다.

***※ 업로드 시 자동 업로드가 되지 않으면 업로드 시도를 할 때 리셋 버튼을 동시에 눌러주면 정상적으로 업로드가 된다.***

### Source code

```c
/*
  Macro keyboard ex01

  10초 간격으로 a키 타이핑하기
*/

#include "Keyboard.h" // 키보드 라이브러리

void setup() {
  Keyboard.begin();   // 키보드 시작
}

void loop() {
  Keyboard.press('a');
  Keyboard.release('a');
  delay(1000);
}
```
