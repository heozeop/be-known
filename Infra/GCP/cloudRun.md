## AWS - GCP custom domain 연결
[ref](https://thatapicompany.com/how-to-map-a-domain-from-aws-to-cloudrun/)

### 1. cloud run console
1. custom domain 클릭
2. add mapping
3. search console 가기
4. 도메인 인증 하기

### 2. aws route53
1. CNAME 타입으로 domain 연결

### 주의 사항
1. 생성한 region이 domain mapping을 지원하는지 확인이 필요함. [ref](https://cloud.google.com/run/docs/mapping-custom-domains?hl=ko&_gl=1*1r3olgz*_ga*MjAwMzI1ODgzMi4xNjUwNDI2OTI5*_ga_WH2QY8WWF5*MTcyMDQ4NzU3OS4zMDEuMS4xNzIwNDkxNDMyLjIxLjAuMA..&_ga=2.148653108.-2003258832.1650426929#run)
2. 변경하는데 시간이 꽤 걸리므로 라이브 서비스라면 위험함
