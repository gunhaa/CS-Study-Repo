# 스택과 힙
- 가장 뚜렷한 차이는 다음과 같다
    - 스택은 빠르다
    - 힙은 느리다
        - -> 미심 쩍을 때는 스택을 택하라(일반적인 프로그래밍 언어)
        - Rust의 경우 Sized를 구현한 타입을 사용하라(컴파일 시점에 컴파일러가 타입의 크기를 파악한 타입)
## 스택
- 스택은 접시 더미에 비유하지만, 사실 정확하지 않다
    - 스택은 두가지 수준의 객체를 담는다
        - 스택 프레임
            - 스택 프레임은 호출 시 함수 상태를 보관한다
            - 함수가 함수내에서 호출되면 이전 함수의 값은 고정된다
            - 스택 프레임은 크기가 각각 다르다
            - 함수 인자, 원래 호출 지점(call site)을 가르키는 포인터, 지역 변수(힙에 할당된 데이터 제외)를 담고 있다
        - 데이터
    - 스택은 최상위 아이템에만 접근하는 수준이 아니라 그 안에 저장된 다수의 요소에 접근할 수 있도록 한다
    - 임의의 크기 요소를 담을 수 있는데, 접시 비유에서는 모든 요소가 동일한 크기라는 점에서 차이가 있다
    - 스택이 빠른 이유는 함수의 변수는 메모리에 연달아 놓이기 때문이며, 이 방식은 접근 속도를 높인다
## 힙
- 컴파일 타임에 크기를 모르는 타입을 위한 프로그램 메모리 영역
- Rust의 경우 슬라이스 타입([T])이 자주 언급되는 예시이다
    - 이런 타입을 동적 크기 타입이라고 한다
- rust의 트레이트 객체가 대표적인 힙영역이며, 컨테이너에 끼워넣어 동적 언어의 일부 기능을 흉내낼 수 있다
- Box::new(T)
    - T를 힙에 할당한다
    - 박스된 대상은 힙에, 포인터는 스택에 놓인다