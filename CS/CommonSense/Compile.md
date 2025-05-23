# Compile

> 컴파일러의 구조는 프론트엔드와 백엔드로 나뉜다. 프론트엔드는 타겟과 독립적인 부분으로 이와 관계없이 소스 코드를 분석하고 중간 형태의 코드를 생성한다. 백엔드는 타겟에 의존적인 부분으로 프론트엔드에서 생성한 중간 코드를 특정 머신에 대한 목적 코드로 번역한다. 프론트엔드와 백엔드 사이에서는 중간 코드를 최적화하는 optimizer가 존재하며, 중간 코드는 중간 표현(Intermediate Representation; IR)이라고 부른다.


### 1. 프론트엔드 (Frontend)
- 타겟과 독립적인 부분으로, 소스 코드를 분석하고 중간 형태의 코드를 생성한다.
- 주요 작업:
  - 소스 코드 분석: 소스 코드를 문법적으로 분석하여 추상 구문 트리(AST)를 생성한다.
  - 중간 코드 생성: 추상 구문 트리를 바탕으로 중간 표현(IR)을 생성한다. 이 중간 코드는 타겟 머신에 종속되지 않는다.

### 2. 백엔드 (Backend)
- 타겟에 의존적인 부분으로, 프론트엔드에서 생성한 중간 코드를 특정 머신에 대한 목적 코드(machine code)로 번역한다.
- 주요 작업:
  - 중간 코드 변환: 중간 표현(IR)을 특정 타겟 머신에서 실행 가능한 목적 코드로 변환한다.
  - 최적화: 목적 코드를 효율적으로 실행할 수 있도록 다양한 최적화를 수행한다.

### 3. 최적화 (Optimizer)
- 프론트엔드와 백엔드 사이에 존재하며, 중간 표현(IR)을 최적화한다.
- 최적화는 중간 코드가 더 효율적으로 실행될 수 있도록 개선하는 과정이다.
  
### 4. 중간 표현 (Intermediate Representation; IR)
- 프론트엔드에서 생성하고 백엔드로 전달되는 중간 형태의 코드.
- 타겟 머신에 종속되지 않으며, 백엔드에서 최적화 후 목적 코드로 변환된다.

## 중간표현(IR)
- 자바와 같이 JVM이 필요하거나 플랫폼 독립성을 중요시하는 언어들은 중간 표현(IR/.class)을 사용한다.
    - Python에서도 PVM에 실행되기 위해 bytecode를 생성한다
        - 다만, Python은 인터프리터 언어라 주로 소스 코드를 바로 실행하기도 한다
    - Rust도 중간코드로 생성후 타겟 머신으로 컴파일한다.
- C, C++와 같은 언어는 IR 없이 기계어로 바로 컴파일되어 실행된다.
언어 설계와 실행 모델에 따라 IR의 사용 여부가 달라지므로, 모든 언어가 IR을 사용하는 것은 아니다. IR은 주로 가상 머신에서 실행되거나, 중간 단계에서 최적화를 위한 중요한 역할을 한다.