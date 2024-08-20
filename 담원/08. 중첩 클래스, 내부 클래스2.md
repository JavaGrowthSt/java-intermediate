### 지역 클래스(Local class)

 내부 클래스의 특별한 종류의 하나이고 그 특징을 그대로 가진다. 

 예를 들어, 지역 클래스도 내부 클래스이므로 바깥 클래스의 인스턴스 멤버에 접근할 수 있다.
 그리고 코드 블럭 안에서 정의된다.

 ```java
  class Outer {
	
		   public void process() {

      //지역 변수
		   int localVar = 0;

       //지역 클래스
		   class Local {...}
		   Local local = new Local();

	   }
  }
```

지역 클래스의 특징

- 지역 클래스는 지역 변수처럼 코드 블럭 안에 클래스를 선언한다.
- 지역 클래스는 지역 변수에 접근할 수 있다.

`지역 클래스가 접근하는 지역 변수의 값은 변경하면 안된다.`


### 변수의 생명 주기

![image](https://github.com/user-attachments/assets/6b47d99d-3938-4207-aab4-be8b03078814)
- 클래스 변수: 프로그램 종료 까지, 가장 길다(메서드 영역) <br>
  클래스 변수(static 변수)는 메서드 영역에 존재하고, 자바가 클래스 정보를 읽어 들이는 순간부터 프로그램 종료까지 존재한다.
- 인스턴스 변수: 인스턴스의 생존 기간(힙 영역) <br>
  인스턴스 변수는 본인이 소속된 인스턴스가 GC 되기 전까지 존재한다. 생존 주기가 긴 편이다.
- 지역 변수: 메서드 호출이 끝나면 사라짐(스택 영역) <br>
  지역 변수는 스택 영역의 스택 프레임 안에 존재한다. 따라서 메서드가 호출 되면 생성되고, 메서드 호출이 종료되면 스택 프레임이 제거되면서 그 안에 있는 지역 변수도 모두 제거된다.
  생존 주기가 아주 짧다. 참고로 매개변수도 지역 변수의 한 종류이다.

### 지역 변수 캡쳐

지역 변수의 생명주기는 짧고, 지역 클래스를 통해 생성한 인스턴스의 생명 주기는 길다.
지역 클래스를 통해 생성한 인스턴스가 지역 변수에 접근해야 하는데, 둘의 생명 주기가 다르기 때문에 인스턴스는 살아있지만, 지역 변수는 이미 제거된 상태일 수 있다.

```
지역 변수 캡처
자바는 이런 문제를 해결하기 위해 지역 클래스의 인스턴스를 생성하는 시점에
필요한 지역 변수를 복사해서 생성한 인스턴스에 함께 넣어둔다.
이런 과정을 변수 캡처(Capture)라 한다
```

지역 클래스가 접근하는 지역 변수는 절대로 중간에 값이 변하면 안된다.<br>
따라서 final 로 선언하거나 또는 사실상 final 이어야 한다.<br>

(자바 언어를 설계할 때 지역 변수의 값이 변경되면 인스턴스에 캡처한 변수의 값도 함께 변경하도록 설계하면, <br>
수 많은 문제들이 파생될 수 있기에 final로 변경 불가능하게 한다.)

### 익명 클래스

익명 클래스(anonymous class)는 지역 클래스의 특별한 종류의 하나이다.<br>
익명 클래스는 지역 클래스인데, 클래스의 이름이 없다는 특징이 있다.<br>

익명 클래스를 사용하면 클래스의 이름을 생략하고, 클래스의 선언과 생성을 한번에 처리할 수 있다.

```java
  Printer printer = new Printer(){
   //body
  }
```

```java
package nested.anonymous;

import nested.local.Printer;

public class AnonymousOuter {
	 private int outInstanceVar = 3;
	 
	 public void process(int paramVar) {
			 int localVar = 1;
			 Printer printer = new Printer() {
			 int value = 0;
			 @Override
			 public void print() {
			 System.out.println("value=" + value);
			 System.out.println("localVar=" + localVar);
			 System.out.println("paramVar=" + paramVar);
			 System.out.println("outInstanceVar=" + outInstanceVar);
			}
	 };
	 printer.print();
	 
	 System.out.println("printer.class=" + printer.getClass());
	 }
 
	 public static void main(String[] args) {
		 AnonymousOuter main = new AnonymousOuter();
		 main.process(2);
	 }
}
```

#### 익명 클래스의 특징

- 이름 없는 지역 클래스를 선언하면서 동시에 생성한다.
- 부모 클래스를 상속 받거나, 또는 인터페이스를 구현해야 한다.
- 익명 클래스를 사용할 때는 상위 클래스나 인터페이스가 필요하다.
- 익명 클래스는 말 그대로 이름이 없다. 이름을 가지지 않으므로, 생성자를 가질 수 없다. (기본 생성자만 사용됨)
- 익명 클래스는 AnonymousOuter$1 과 같이 자바 내부에서 바깥 클래스 이름 + $ + 숫자로 정의된다. 익명 클
래스가 여러개면 $1 , $2 , $3 으로 숫자가 증가하면서 구분된다.

#### 익명 클래스의 장점

- 클래스를 별도로 정의하지 않고도 인터페이스나 추상 클래스를 즉석에서 구현할 수 있어 코드가 더 간결해진다. 하지만, 복잡하거나 재사용이 필요한 경우에는 별도의 클래스를 정의하는 것이 좋다.
