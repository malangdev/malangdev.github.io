---
layout: post
title: development
description: >
  아두이노를 이용하여 매크로 키보드 제작 (인터럽트)
tags: arduino leonardo macro keyboard
sitemap: false
hide_last_modified: true
---

# 매크로 키보드 제작 (인터럽트 사용하기)

### 인터럽트(Interrupt) 사용하여 코드 개선하기

이전 예제에서는 폴링 방식으로 loop 문에서 버튼이 눌렸는지 반복적으로 체크하여 타이핑 로직을 호출하는 식으로 구현되었습니다. 이는 시간을 소비하기 때문에 비효율적인 방법입니다. 이에 반해 인터럽트(Interrupt)는 실행 중인 프로그램을 일시 중단하고 다른 프로그램을 끼워 넣어 실행시키는 것으로 MCU가 입력신호를 체크하는데 많은 시간을 들이지 않아 효율적이고 코드도 더 간결해질 수 있습니다. 따라서 기존 코드를 인터럽트를 사용하는 방식으로 변경해 봅니다.

### 회로도

[아두이노 공식 사이트](https://www.arduino.cc/reference/en/language/functions/external-interrupts/attachinterrupt/)에서 인터럽트를 위한 핀 정보를 확인할 수 있습니다. 레오나르도 보드는 0, 1, 2, 3, 7번 핀을 사용합니다.

Interrupt Numbers
![](/assets/img/2023-05-07-macro-keyboard-ex04/macrokeyboard_ex04_interrupt.png){: width="700"}

본 예제에서는 기존에 복사하기 2번 핀, 붙여넣기 4번 핀으로 구성하였으나 인터럽트 사용을 위해 붙여넣기 4번 핀을 3번 핀으로 변경하여 진행합니다.

![](/assets/img/2023-05-07-macro-keyboard-ex04/macrokeyboard_ex04_circuit.png){: width="600"}

회로도와 같이 복사하기를 할 택트 스위치에 2번과 GND를 연결하고, 붙여넣기용 택트 스위치에 3번과 GND를 연결합니다.

![](/assets/img/2023-05-07-macro-keyboard-ex04/macrokeyboard_ex04.jpg){: width="400"}

아래와 같이 코딩 후 컴파일 및 업로드합니다.

***※ 업로드 시 자동 업로드가 되지 않으면 업로드 시도를 할 때 리셋 버튼을 동시에 눌러주면 정상적으로 업로드가 됩니다.***

복사할 문자를 선택한 후 복사하기 택트 스위치를 눌러 복사하고, 다시 붙여넣기 택트 스위치로 붙여넣기를 하여 잘 동작되는지 확인합니다.

### Source code

```c
/*
  Macro keyboard ex03 (for Windows platform)

  Interrupt를 사용하여 복사하기(2번Pin), 붙여넣기(3번Pin) 버튼 만들기
  Leonardo의 Interrupt pin은 5개 제공(INT.0: 3, INT.1: 2, INT.2: 0, INT.3: 1, INT.4: 7)
*/

#include "Keyboard.h" // 키보드 라이브러리

const int copyButtonPin = 2;    // copy pin for pushbutton
const int pasteButtonPin = 3;   // paste pin for pushbutton

int previousCopyButtonState = HIGH;
int previousPasteButtonState = HIGH;

void setup() {
  Serial.begin(9600);
  pinMode(copyButtonPin, INPUT_PULLUP);
  pinMode(pasteButtonPin, INPUT_PULLUP);
  attachInterrupt(digitalPinToInterrupt(copyButtonPin), CopyButton, FALLING); // from high to low
  attachInterrupt(digitalPinToInterrupt(pasteButtonPin), PasteButton, FALLING); // from high to low
  
  Keyboard.begin();
}

void loop() {
}

void CopyButton()
{
  Serial.println("copy");
  Keyboard.press(KEY_LEFT_CTRL);
  Keyboard.write('c');
  delay(100);
  Keyboard.releaseAll();
}

void PasteButton()
{
  Serial.println("paste");
  Keyboard.press(KEY_LEFT_CTRL);
  Keyboard.write('v');
  delay(100);
  Keyboard.releaseAll();
}
```
