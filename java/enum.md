## Enum

1. 상수의 집합
2. 메모리
    1. Enum class 는 메소드 영역에서 각 객체 참조
    2. Enum 객체들은 힙 영역에
3. 허용 가능한 값들을 제한하여 유형 안전(type safe)을 제공
4. 주요함수
    1. name()
    2. valueOf(String name)
    3. values()
5. clone(), hashcode(), equals() final 처리
6. enum을 인스턴스화 할 수 없는 이유(싱글톤인 이유)
    1. enum 타입은 고정된 상수들의 집합으로써, 런타임(run-time)이 아닌 컴파일타임(compile-time)에 모든 값을 알고 있어야 하는 규칙이 있기 때문
7. ordinal() 사용 지양
    1. 인덱스를 반환
    2. ordinal()을 사용한 로직(순서 반환)은 용도에 맞지 않음
    3. 원래 용도는 EnumSet, EnumMap의 성능 최적화 // 대부분의 연산이 ordinal을 이용한 산술비트 연산
8. EnumSet
    1. Enum의 요소들을 Set으로 만든 것
    2. Set의 부분집합을 만들기 위한 정적 메소드 제공
    3. 산술 비트 연산을 사용하기 때문에, 계산이 매우 빠름(long 의 64비트 범위 내의 64개의 원소일 때 가장 효율적)

    ```java
    EnumSet<Status> statuses = EnumSet.allOf(Status.class);
    *// Enum 요소 모두 포함*
    EnumSet<Status> range = EnumSet.range(Status.RUNNING, Status.FINISH);
    *// range에 들어간 것만*
    EnumSet<Status> complementOf = EnumSet.complementOf(EnumSet.of(Status.RUNNING, Status.FINISH));
    *// 특정 요소 제외하고 나머지*
    ```

9. EnumMap
    1. Enum의 요소들을 키로하는 Map
    2. Enum의 ordinal()을 바탕으로 Array 형태로 저장

    ```java
     EnumMap<Status, String> activityMap = new EnumMap(Status.class);
     activityMap.put(Status.START, "start-test");
     activityMap.put(Status.RUNNING, "running-test");
     activityMap.put(Status.FINISH, "finish-test");
     
     activityMap.forEach((key,value) -> log.info("key={}, value={}", key, value));
    ```