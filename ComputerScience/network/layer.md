# 계층
## 종류
### TCP/IP 4계층 
- 애플리케이션
- 전송
- 인터넷
- 링크 
? 역할

### OSI 7 계층
- 애플리케이션
- 프레젠테이션
- 세션
- 전송
- 네트워크
- 데이터 링크
- 물리
? 역할

## 전송 계층
### TCP
- 가상회선 방식의 통신
    - 장: 순서 보장
    - 단: 신뢰 관계 구축 필요
- 연결 시작 시
    - 3 way handshake
        1. ISN + SYN
        1. ISN + ACK + SYN
        1. ISN + ACK
- 연결 종료 시
    - 4 way handshake
        1. FIN: 클라 FIN Wait 1 
        1. ACK: 클라 Fin Wait 2 서버 close wait 
        1. FIN:                 서버 Last ack
        1. ACK: 클라 Time wait  서버 close
    - 얼만큼 기다리나
        1. 서버의 Last ACK FIN
        1. 클라의 Time wait
            - 운영체제 별로 다르다고 한다.

### UDP
- 데이터 그램 방식의 통신
    - 장: 빠름
    - 단: 순서 보장 안함, 무결성 보장 안함

## 링크 계층
### 전이중화 통신
- 동시에 양방향
- 이전에는 CSMA/CD라는 반이중화 유선 통신함

### 반이중화 통신
- WIFI
- Congestion controll 필요
- CSMA/CA (Carrier Sense Multiple Access with collision avoidance)

- 영역 기준
    - BSS
        기본 서비스 집합
    - ESS
        BSS 집합
