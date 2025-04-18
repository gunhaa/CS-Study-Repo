# 확장

> 쉘에서 의미를 가지는 특수한 기호들

## 경로명 확장

- `echo text` 는 text를 출력한다.
- 파일을 빠르게 생성할 수 있는 방법이다.

### wildcard character

- `*` 는 와일드카드로 모든 것을 가져온다.
- ex) `ls *.html` 을 사용하면 .html 확장자를 전부 가져온다
- `echo *` 는 해당 디렉토리의 모든 파일을 가져온다.
- `ls *` 재귀적으로 모든 폴더내의 파일까지 싹 가져온다.
- `?` 는 한개의 character만 올 수 있다.
    - `ls pic?.png`
    - 이 경우 pic1.png, pic2.png 등이 나타나고 pic35.png의 경우는 두자리이기 때문에 나타나지 않게된다.
    - pic35.png 같은 이름을 찾고싶다면, `ls pic??.png` 로 작성해야한다.
- `[]` 는 Range wildcard로 범위의 모든 것들을 가져온다.
    - `ls pic[123]` 띄여쓰기 없이 사용하면 pic1 pic2 pic3 을 찾는다.
    - `ls file[0-9]` -를 사용한다면 file0 , file1 ... file9 를 찾는다.
    - `ls [A-F]` 로 찾으면 한글자로 된 A-F를 찾는다.
    - A-F로 시작하는 것을 찾기위해서는 `ls [A-F]*` 로 찾아야 한다.
- `^` 은 일치하지 않는 것을 찾는다
    - `ls [^a]` 는 a로 시작하지 않는 것을 찾는다.
    - `ls [^0-9]` 는 숫자로 시작하지 않는 것을 찾는다.

### `~`

- 내 계정의 홈 경로를 의미한다
- `echo ~` 로 확인해 볼 수 있다.

### Brace Expansion(중괄호 확장)

- `touch page{1,2,3}.txt` 
- 중괄호 안에 있는 것은 `,` 를 통해 seperate되며, 각각의 명령어를 수행한다.
- 파일이나 폴더를 만들 때 유용하다.
- 디렉토리 생성 예시
    - `mkdir -p {mon,tue,wed,thu,fri}/{breakfase,lunch,dinner}` 로 한번에 만들 수 있다.

### Ranges

- `..` 으로 할 수 있다.
- `echo jan{1..31}` jan1~31까지 출력된다. 
- `echo jan{1..31..2}` 를 통해 단위를 조절 가능하다.
- `echo group-{a..e}` 처럼 문자로 사용할 수 있다.

### Nested Brace Expansion
- `echo {x,y{1..5},z}` 로 사용할 수 있다.

### Arithmetic Expansion(산술 확장)

- `$((expanssion))` 으로 사용할 수 있다.
- `$((계산식))` 으로 사용할 수 있다.
- `echo $((30+10))`
- `echo $((3*10))`
- `echo $((10/3))` 등으로 사용 가능하다.
- `echo 10+3` 을 하면 `10+3` 이 출력되서 필요하다.
- 잘 사용하지 않는다.

### Quoating

- `echo hello             there` 을 입력하면, 공백문자는 완전히 무시되고 하나만 남는다
- 이는 쉘이 단어분리(word splitting)을 수행하기 때문이다.
- 띄어쓰기나 `$` 같은 특수한 기호를 입력하기 위해 특수한 기호가 필요하다
    - `"` 를 사용하면 공백문자를 보존하고, 특수한 기호들을 사용할 수 있다($변수 사용 등)
    - ex) `echo "hello      there`
    - `'` 를 사용하면 모든 기호를 그대로 출력한다. 특수한 기호를 사용하지 않는 점이 `"` 와 구별된다.

### Command Substitution (명령어 치환)

- `$` 는 쉘에서 특별한 의미를 가지고 있다.
    - `` 백틱으로도 사용 가능하다.
    - echo today \`date\`
- `$var` 변수 var를 찾는다.
- `echo $PATH` 로 확인 가능하다.