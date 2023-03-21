# HaskellBasic

https://wikidocs.net/1457 를 보고 학습한 하스켈 기초 내용 정리

## 변수

- 하스켈의 변수는 immutable (불변) 이다.
- 명령형 프로그래밍은 변수를 컴퓨터 메모리 안의 변경 가능 장소로 취급하지만,  
  함수형 프로그래밍은 변수들이 서로 어떻게 연결되는지를 정의하고,  
  단계별 명령으로의 번역은 컴파일러에게 맡긴다.

  ```haskell
  -- 아래 코드는 하스켈에서 불가능하다.
  a = 2
  a = 5

  -- 아래 코드는 r 을 1 증가시키는 것(메모리 값 갱신)이 아니고
  -- r에 대한 재귀적 정의다.
  r = r + 1

  -- 변수의 선언 순서는 중요하지 않다.
  y = x + 1
  x = 5
  ```

## 함수

- 인자 argument (혹은 매개변수 parameter) 값을 취해서 값을 돌려준다.

  ```haskell
  area r = pi * r ^ 2   -- [이름] [인자] = [함수 정의]
  area 5 * 3            -- (area 5) * 3
  area (5 * 3)          -- area 15
  ```

- 다중 인자의 경우 공백으로 구분한다.

  ```haskell
  areaTriangle b h = (b * h) / 2
  ```

- 합성 함수 : 정의한 함수를 이용해 함수를 정의할 수 있다.

  ```haskell
  areaRect l w = l * w
  areaSquare s = areaRect s s
  ```

- `where` : 지역 정의

  ```haskell
  heron a b c = sqrt (s * (s - a) * (s - b) * (s - c))
    where
    s = (a + b + c) / 2
  {-  s의 정의는 heron의 우변의 일부가 아니므로,
      heron의 우변의 일부로 만드려면 where이 필요하다. -}
  ```

## 중위 연산자

- 하스켈은 중위 연산자로 사용되는 함수를 괄호로 감싸면 표준 방식으로 사용할 수 있다.
  - `<, >, <=, >=`과 산술 연산자들(`+, *` 등)에도 적용된다.
  - 일반화하면 하스켈에서 실체가 있는 것들은 값 또는 함수라고 말할 수 있다.
  ```haskell
  4 + 9 == 13
  (==) (4 + 9) 13
  ```

## guard

- syntactic sugar (편의 문법, 동일한 로직을 다른 식으로 작성하는 것) 중 하나로  
  `|` 로 표현한다.
- 불리언 값에 기반해 단순하지만 강력한 함수를 작성할 수 있다.

  ```haskell
  absolute x
      | x < 0     = -x
      | otherwise = x   -- otherwise는 True 와 동일, 맨 마지막에 넣자

  -- where은 guard와 함께쓰기 좋다.
  numOfSolutions a b c
      | disc > 0  = 2
      | disc == 0 = 1
      | otherwise = 0
          where
          disc = b^2 - 4*a*c
  ```

## 타입

- 몇가지 예시
  - 불리언 : `Bool`
  - 문자 : `Char`
  - 문자열 : `String`, `[Char]` (하스켈에서 문자열은 Char 리스트)
- 함수의 타입 표현 : `인자 -> 반환 값`
- 다중 인자 함수의 타입 표현 : `인자 -> 인자 -> 반환 값`
  ```haskell
  xor :: Bool -> Bool -> Bool -- 시그니처
  xor p q = (p || q) && not (p && q)
  ```
- 타입 시그니처란 `:: 타입` 의 형태로, ...이 이 타입을 가진다는 뜻
  - 시그니처를 빼먹으면 컴파일러가 타입을 추론한다.
  - 문서화와 디버깅을 위해 시그니처는 꼭 적자
