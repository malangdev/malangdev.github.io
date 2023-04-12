---
layout: post
title: development
description: >
  전역 .gitignore 파일을 사용하지 않고 로컬에서만 ignore하는 방법
sitemap: false
hide_last_modified: true
---

## Git 사용 시 파일 변경을 무시하는 방법

Git을 사용할 때 추적을 할 필요가 없는 경우 대부분 .gitignore 파일에 추가하는 방식을 사용할 것입니다.
Git 초보인 저 또한 이 방법이 전부인 줄 알았습니다.

하지만, [Git을 사용하여 파일 변경 무시](https://learn.microsoft.com/ko-kr/azure/devops/repos/git/ignore-files?view=azure-devops&tabs=visual-studio-2022) 글을 통해서 .gitignore 파일 추가 외에도 3가지 방법이 더 있는 것을 알게 되었습니다. 아래는 그 내용 중 일부입니다.

* 파일을 사용하여 .gitignore 추적되지 않는 파일에 대한 변경 내용 무시
* 파일을 사용하여 추적되지 않은 파일에 대한 exclude 변경 내용 무시 - 이번에 설명할 내용
* git update-index를 사용하여 파일 추적 중지 및 변경 내용을 무시
* git rm을 사용하여 파일 추적 중지 및 변경 내용 무시

### exclude 제외 파일을 사용하여 로컬 변경 무시하기

.git/info/exclude 파일을 열어 untrack 하고 싶은 파일을 적으면 변경된 파일이 무시됩니다.
이 폴더 및 파일은 숨겨져 있기 때문에 탐색기에서 숨김 파일을 해제하지 않으면 보이지 않습니다.
