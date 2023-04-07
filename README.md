# malangdev.github.io

## 초기 설정

* Hydejack 테마 [https://hydejack.com/](https://hydejack.com/)
* _config.yml 설정
* 로고 설정
    - assets\img\logo.png
    - assets\img\sidebar-bg.jpg
    - assets\icons\favicon.ico
* utterances 댓글 기능 설정
* 포스팅 하기

### utterances 설정
* [https://hydejack.com/docs/config/#enabling-comments](https://hydejack.com/docs/config/#enabling-comments)
* Repository 만들기
    - Github에 댓글용 레파지토리 생성
* utterances 설치
    - https://github.com/apps/utterances 접속
    - Only select repositories
    - Repository 선택
        - repo: malangdev/comments
    - Mapping 선택
        - pathname 또는 url 선택
    - Issue Label 설정 (Optional)
        - "utterances" 입력
    - 테마 설정
        - GiHub Light 선택
    - Enable Utterances
        - script를 복사하여 원하는 페이지에 추가
        - Hydejack 설정 방법
            ```bash
            # # You can use the following to enable comments on all posts.
            - scope:
                type:            posts
                values:
                comments:        true
            ```
## 로컬 구동 방법

```bash
bundle install
bundle exec jekyll serve
```
