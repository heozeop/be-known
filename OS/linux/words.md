### Symlink
- symbolic link
    - 리눅스 버전의 바로가기 링크
- 종류
    - soft link
         - 가리키기만 하는 것
         - 파일 시스템 상관없이 생성 가능
         ? 파일 시스템은 어떤 것들이 존재?

    - hard link
        - 같은 파일 시스템에서 생성 가능
- 사용
    - 생성: `ln <유형> <경로>`
    - 삭제: 
        1. `unlink <경로>`: 디렉터리는 삭제 풀가
        1. `rm <경로>`: 다 삭제 가능
- 깨진 링크
    - 파일 변경
    - `find <경로> -xtype l`
### xtype
- type의 동작과 같으나 심볼링 링크에서는 아래 동작함
    1. `-P -xtype l`: 깨진 링크에 true
    1. `-P -xtype X`: 타켓의 타입이 x면 true
    1. `-L -xtype l`: 항상 true
    1. `-L -xtype x`: 깨진 링크 아니면 False

### type
- `-type c`: type이 C면 TRUE
- options(-)
    1. b: block(buffered) special
    1. c: character(unbuffered) special
    1. d: directory
    1. p: named pipe (FIFO)
    1. f: regular file
    1. l: symbolic link, -L이면 symbolic link가 깨진 경우만 True임
    1. s: socket
    1. d: door



# REF
### symbolic
- [symbolic link](https://qjadud22.tistory.com/22)
- [freeCodeCamp](https://www.freecodecamp.org/korean/news/rinugseu-symlink-tyutorieol-simbolrig-ringkeu-symbolic-link-reul-saengseonghago-sagjehaneun-bangbeob/)
- [gnu](https://www.gnu.org/software/findutils/manual/html_node/find_html/Symbolic-Links.html)

### xtype
- [gnu](https://www.gnu.org/software/findutils/manual/html_node/find_html/Type.html)

