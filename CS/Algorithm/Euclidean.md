# 유클리드 호제법(최대 공약수/최소 공배수)

## 최대공약수(gcd)

> 최대공약수(Greatest Common Divisor, GCD)는 두 수의 공약수 중 가장 큰 값을 의미한다.(같이 나눌수 있는 수)

>
$\text{GCD}(A, B) = \text{가장 큰 } d \text{ such that } d \mid A \text{ and } d \mid B
$
ex) 
```plaintext
4의 약수 - 1, 2, 4
16의 약수 - 1, 2, 4, 8, 16
→ 4와 16의 최대공약수는 4이다.
```

## 유클리드 호제법

> 두 수의 최대공약수를 구하는 알고리즘

> 유클리드(Euclid)에 의해 기원전 300년경에 발견된 가장 오래된 알고리즘이다.

### 사용방법

1. 큰 수를 작은 수로 나눈 나머지를 구한다. (72 % 30)

2. 나누었던 수(B)와 그 나머지(A % B의 결과인 12)로 다시 나머지 연산을 한다.

3. 이 과정을 나머지(A % B)가 0이 될 때까지 반복하며, 0이 된 시점에서의 첫 피연산자(B=6)가 최대 공약수가 된다.

| GCD(A, B)    | A  | B  | A % B |
|--------------|----|----|-------|
| GCD(72, 30)  | 72 | 30 | 12    |
| GCD(30, 12)  | 30 | 12 | 6     |
| GCD(12, 6)   | 12 | 6  | 0     |

### Javascript 구현 예제

```javascript
// 두 수 a, b를 넣는다.
function gcd(a,b){
  	// b(나머지)가 0이면 a(직전 나머지)를 반환하고 탈출
	if(b === 0){
    	return a;
    }
  	// b를 a로 보내고 a % b를 나눈 나머지를 매개변수 b로 넣어서 재귀함수로써 호출
  	return gcd(b, a % b);
};
```

## 최소공배수(lcm)

> (A,B의 최소공배수) = A * B / (A,B의 최대공약수) 로 구할 수 있다.

> 최소공배수(Least Common Multiple, LCM)는 두 수의 공통 배수 중에서 가장 작은 양의 정수를 의미한다.

$\text{LCM}(A, B) = \frac{A \times B}{\text{GCD}(A, B)}$

```javascript
let lcm = a * b / gcd(a,b);
```