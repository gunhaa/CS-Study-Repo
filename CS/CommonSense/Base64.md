# Base64 인코딩이란?

Base64 인코딩은 바이너리 데이터를 텍스트 형식으로 변환하는 방식으로, 주로 데이터를 ASCII 문자로 안전하게 인코딩할 때 사용된다. 이는 네트워크 전송이나 텍스트 기반 데이터 저장에 적합하게 바이너리 데이터를 처리할 수 있도록 도와준다. 특히, 이메일, URL, JSON 등의 환경에서는 바이너리 데이터를 직접 처리할 수 없기 때문에 Base64 인코딩이 유용하게 쓰인다.

![Base64-1](images/Base64.png)

#### Base64인 이유

Base64 인코딩은 변환 단위가 6비트($2^6=64$)이기 때문에 64이고,
Base는 '진법'을 뜻한다.
<br> 즉, 64진법이라는 뜻이다.

## String으로 보내면 되는거 아님?

Base64를 사용하는 가장 큰 이유는 Binary 데이터를 텍스트 기반 규격으로 다룰 수 있기 때문이다. JSON과 같은 문자열 기반 데이터 안에 이미지 파일등을 Web에서 필요로 할때 Base64로 인코딩하면 UTF-8과 호환 가능한 문자열을 얻을 수 있다.  끝에 '='과 같은 패딩 기호가 있다면 이는 구분자로써 사용되므로 대부분 Base64로 생각할 수 있다.  
<br>
기존 ASCII 코드는 시스템간 데이터를 전달하기에 안전하지 않다. 모든 Binary 데이터가 ASCII 코드에 포함되지 않으므로 제대로 읽지 못한다. 반면 Base64는 ASCII 중 제어문자와 일부 특수문자를 제외한 53개의 안전한 출력 문자만 이용하므로 데이터 전달에 더 적합하다.

## BASE64 인코딩이 왜 필요한가에 대한 예제

### 예제: 바이너리 데이터 전송

가정: 단순한 바이너리 데이터가 포함된 1바이트 데이터로, 이 값은 0xFF(즉, 255)를 나타낸다고 하자. 이 데이터는 전송하려는 파일의 일부일 수 있다.

1. ASCII로 보내는 경우
- 바이너리 데이터: `0xFF` (255의 8비트 이진 표현: `11111111`)
- ASCII로 변환: ASCII는 0~127 범위의 문자만 지원하므로, `0xFF`는 ASCII로 변환할 수 없다. ASCII 문자 집합에는 `0xFF`에 해당하는 문자가 없다.
- 결과적으로, ASCII로 직접 전송하려고 하면 이 데이터는 누락되거나 잘못 해석된다. 예를 들어, ASCII로 255를 보내고 싶다면 문자열 '255'로 변환하지만, 이는 원래의 바이너리 데이터가 아니다.
2. Base64로 보내는 경우
- 바이너리 데이터: 여전히 `0xFF` (255)
- Base64 인코딩: 바이너리 데이터 `0xFF`를 8비트로 표현: `11111111`
- Base64는 6비트 단위로 인코딩하므로, 8비트 데이터를 6비트 조각으로 나눈다. 이 경우 8비트를 6비트로 변환할 수 없으므로 2비트를 추가로 패딩할 필요가 있다.
- 패딩을 추가한 후: `111111 11` → Base64로 인코딩
- `0xFF`는 Base64에서 /에 해당하므로 결과는 /가 된다.
- Base64 인코딩된 결과: 결과 문자열: /

#### 차이점 정리
- 전송 안전성: ASCII로 직접 전송하면 바이너리 데이터가 손실되거나 해석되지 않는다. 예를 들어, 0xFF는 전송되지 않거나 잘못된 값으로 전송된다. Base64로 인코딩하면 데이터가 안전하게 전송되어 수신자가 원래의 바이너리 데이터를 정확하게 복원할 수 있다.
- 호환성: ASCII는 7비트 기반으로 제한적이기 때문에 다양한 바이너리 데이터를 포함할 수 없다.
Base64는 ASCII 안전한 문자 집합을 사용하여 다양한 바이너리 데이터를 안전하게 텍스트 형식으로 전송할 수 있도록 한다.
- 데이터 크기: ASCII 문자열로 표현할 경우 데이터가 원래의 바이너리보다 불필요하게 커질 수 있으며, 인코딩 방식에 따라 33% 정도의 크기 증가가 발생할 수 있다. Base64는 이러한 증가를 감수하더라도 데이터의 안전성을 보장한다.

#### 결론
이 예제를 통해 Base64 인코딩이 바이너리 데이터를 안전하게 전송하는 데 얼마나 중요한지를 알 수 있다. ASCII로 전송하는 경우 데이터의 손실이 발생할 수 있지만, Base64는 모든 바이너리 데이터를 안전하게 인코딩하여 텍스트 기반 시스템에서 호환성을 유지할 수 있도록 돕는다.