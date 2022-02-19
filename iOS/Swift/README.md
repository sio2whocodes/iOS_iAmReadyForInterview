# Swift

<details>
<summary> mutating 키워드가 무엇인가요? </summary>
<div markdown="1">

- 스위프트에서 클래스는 레퍼런스 타입이고 구조체와 열거형은 값 타입이다. 값 타입은 기본적으로 인스턴스 메소드에서 내부 데이터를 수정할 수가 없다.

- 값 타입의 속성을 수정하려면 인스턴스 메서드에서 mutating 키워드를 사용해야 한다.

</div>
</details>


<details>
<summary> class, static, instance 메서드에 대해 설명해주세요 </summary>
<div markdown="1">

- 인스턴스 메소드 : 클래스, 구조체, 열거형의 인스턴스에 속한 메소드를 의미합니다. 클래스를 인스턴스화 후 해당 메소드를 호출해야한다.

- 타입 메소드 : class, static 키워드가 붙는다. 클래스를 인스턴스와 하지 않아도 바로 타입 자체에서 호출할 수 있다. class는 오버라이드 가능, static은 불가, final + class == static

</div>
</details>

<details>
<summary> 컬렉션타입, 구조체, 열거형, 클래스, 클로저를 값타입과 참조타입인지 나눠주세요 </summary>
<div markdown="1">

- 스위프트에서 모든 데이터타입(Int, Double, Set, Array, Dictionary 등등)은 모두 구조체 기반으로 구현되어있다. 구조체 기반이기 때문에 값타입이다. 열거형은 값타입이다.

- 클래스와 클로저(함수)는 참조타입이다.

</div>
</details>

<details>
  <summary> 컬렉션 타입의 종류와 특징에 대해 설명해주세요 </summary>
  <p>
      
  - 이름처럼 ‘데이터들의 집합'으로, swift에서는 ‘지정된 타입의 데이터들의 묶음’을 말한다.
    지정된(데이터) 타입이라고 하는 이유는 swift의 컬렉션 타입이 모두 Generic Collection으로 구현되어 있기 때문이다.

  - swift에서는 Array, Set, Dictionary 세 가지 컬렉션 타입이 있다.
    세 가지 타입은 변수로 생성하면 데이터 구성을 변경할 수 있고, 상수로 선언하면 변경할 수 없다.

  공식문서 노트에 따르면..

  > 컬렉션은 생성한 이후 수정할 필요가 없다면, 상수에 할당하는 것이 바람직하다. “앞으로 이 컬렉션은 수정하면 안 된다.”라는 의도를 코드에 명시하므로 다른 개발자가 코드를 이해하기 쉽다.
  또한 컴파일러의 성능 최적화(performance optimization)를 가능하게 한다.
  > 

  ### Array

  - 같은 데이터 타입의 값들을 순서대로 저장하는 리스트이다.
  - 중복 값을 저장할 수 있고, 순서가 있다. (순서가 있기에 중복값 구분 가능)

  ```swift
  var fruits: [String] = [] // 빈 배열로 초기화 및 선언
  fruits = ["apple", "banana", "kiwi", "apple"] // 값이 중복되어도 순서가 있으므로 상관없다.
  ```

  ### Set
  - 같은 데이터 타입의 값들을 순서없이 저장하는 리스트이다.
  - 순서가 없다는 점을 빼고는 Array와 비슷하다.
  - 순서가 없기 때문에 서로 같은 값을 구분할 수 없으므로 중복값이 허용되지 않는다.

  → 공식문서에서 ‘세트는 순서가 중요하지 않거나, 유일한 값일 때 사용하라.’고 적혀있다.

  - 집합 연산을 할 수 있다.
  - swift는 타입 추론을 하기 때문에, 만약 그냥 선언하면 배열로 인식해버린다.
  - 따라서 선언할 때 반드시 타입을 적어주어야 한다.
  - Set에 들어가는 값의 타입은 꼭 Hashable 프로토콜을 채택하고 있어야 한다.

  ```swift
  var lottos = Set<Int>()
  lottos = [1, 3, 1, 5, 8] // 배열과 같이 대괄호로 표현한다.

  // 중복값이 있는 상태로 대입해줄 수는 있지만, 프린트 해보면 중복값이 제거 되어있다.
  print(lottos) // 1,3,5,8
  ```

  ### Dictionary

  - 순서 없이 key 와 value가 한 쌍으로 데이터를 저장하는 컬렉션 타입이다.
  - key와 value에 대한 타입을 지정해놓으면 해당 타입만 입력할 수 있다. 
  (모든 key의 타입 동일, 모든 value의 타입 동일)
  - 마찬가지로 순서가 없다.
  - key의 타입은 꼭 Hashable 프로토콜을 채택하고 있어야 한다.
  - 정렬하고 싶다면, key 또는 value 프로퍼티에 대해서 sorted()를 사용할 수 있다.

  ```swift
  var phoneBook: [String: String] = [:] // String타입의 key, String타입의 value인 딕셔너리 초기화 및 선언
  phoneBook["홍길동"] = "010-1111-1111" // 딕셔너리에 값 넣기
  phoneBook["김철수"] = "010-2222-2222"

  print(phoneBook["홍길동"]) // 010-1111-1111
  ```
  </p>
</details>


<details>
<summary>class, struct는 공통점이 무엇인가요?(언제 사용하나요?)</summary>
<div markdown="1">

  1.  서로 다른 타입들을 하나로 묶을 수 있다.
  2.  묶은 자료형들을 새로운 타입처럼 사용 가능하다.
  3.  클래스, 구조체 안에 함수나 프로퍼티를 정의할 수 있다.
  4.  extension이 가능하다.

</div>
</details>