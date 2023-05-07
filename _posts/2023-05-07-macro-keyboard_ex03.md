---
layout: post
title: development
description: >
  아두이노를 이용하여 매크로 키보드 제작 (활용편)
sitemap: false
hide_last_modified: true
---

# 매크로 키보드 제작 (활용)

### 버튼으로 복사/붙여넣기 하기

컴퓨터를 사용하다보면 복붙(복사하기/붙여넣기)를 매우 자주 사용하게 되는데, 반복 작업 시 손가락이 불편해지기 마련이다. Ctrl + C, Ctrl + V 조작을 택트 스위치로 대체하여 사용할 수 있는 매크로 키보드를 제작한다. 실제 사용할 수 있는 매우 유용한 작업이다.

### 회로도

![](/assets/img/2023-05-07-macro-keyboard_ex03/macrokeyboard_ex03_circuit.png){: width="600"}

회로도와 같이 복사하기를 할 택트 스위치에 2번과 GND를 연결하고, 붙여넣기용 택트 스위치에 4번과 GND를 연결한다.

![](/assets/img/2023-05-07-macro-keyboard_ex03/macrokeyboard_ex03.JPG){: width="400"}

아래와 같이 코딩 후 컴파일 및 업로드한다.

***※ 업로드 시 자동 업로드가 되지 않으면 업로드 시도를 할 때 리셋 버튼을 동시에 눌러주면 정상적으로 업로드가 된다.***

복사할 문자를 선택한 후 복사하기 택트 스위치를 눌러 복사하고, 다시 붙여넣기 택트 스위치로 붙여넣기를 하여 잘 동작되는지 확인한다.

### Source code

```c
/*
  Macro keyboard ex03 (for Windows platform)

  복사하기, 붙여넣기 버튼 만들기
*/

#include "Keyboard.h" // 키보드 라이브러리

const int copyButtonPin = 2;    // copy pin for pushbutton
const int pasteButtonPin = 4;   // paste pin for pushbutton

int previousCopyButtonState = HIGH;
int previousPasteButtonState = HIGH;

void setup() {
  Serial.begin(9600);
  pinMode(copyButtonPin, INPUT_PULLUP);
  pinMode(pasteButtonPin, INPUT_PULLUP);
  Keyboard.begin();
}

void loop() {
  // Copy
  int copyButtonState = digitalRead(copyButtonPin);
  if ((copyButtonState != previousCopyButtonState) && copyButtonState == LOW)
  {
    CopyButton();
  }

  // Paste
  int pasteButtonState = digitalRead(pasteButtonPin);
  if ((pasteButtonState != previousPasteButtonState) && pasteButtonState == LOW)
  {
    PasteButton();
  }

  previousCopyButtonState = copyButtonState;
  previousPasteButtonState = pasteButtonState;
  delay(100);
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

### 동작 확인

![](/assets/img/2023-05-07-macro-keyboard_ex03/macrokeyboard_ex03_serialmonitor.png){: width="500"}
