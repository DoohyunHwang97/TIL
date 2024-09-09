# Elastic Search
`Elastic Search`는 검색 특화 인덱스 기반 NoSQL 저장소이다. `Index`를 기준으로 하여 하위 문서들을 관리한다.

## 특징
* 샤딩을 통한 확장성
* 역색인을 지원
* Document-Oriented
* Schemaless

## 단점
* 트랜잭션 롤백이 불가하다.
* 데이터의 수정이 불가하다.
* 완전 실시간은 아니다. 1초 정도의 지연이 존재한다.