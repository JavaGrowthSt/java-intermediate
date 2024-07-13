### java.lang 패키지

import 생략 가능 <br>
Object : 모든 자바 객체의 부모 클래스 <br>
String : 문자열 <br>

Integer, Long, Double : 래퍼 타입, 기본형 데이터 타입을 객체로 만든 것 <br>
Class : 클래스 메타 정보 <br>
System : 시스템과 관련된 기본 기능들을 제공 <br>

### import 생략 가능

java.lang 패키지는 모든 자바 애플리케이션에 자동으로 import된다. <br>
따라서 임포트 구문을 사용하지 않아도 된다. <br>

```java
package lang;

import java.lang.System;

public class LangMain{
		public static void main(String[] args){
				System.out.println("hello java");
		
		}

}
```
클래스에 상속 받을 부모 클래스가 없으면 묵시적으로 Object 클래스를 상속 받는다. <br>
쉽게 이야기 해서 자바가 extends Object 코드를 넣어준다. <br>
따라서 extends Object는 생략하는 것을 권장한다. <br>

```html
묵시적(Implicit) vs 명시적(Explicit)
묵시적 : 개발자가 코드에 직접 기술하지 않아도 시스템 또는 컴파일러에 의해 자동으로 수행된느 것을 의미
명시적 : 개발자가 코드에 직접 기술해서 작동하는 것을 의미
```

- 쉽게 이야기해서 자바가 extends Object 코드를 넣어준다
- extends Object는 생략하는 것을 권장


```java
public class ObjectMain{

		public static void main(String[] args){
		
				Child child = new Child();
				child.childMethod();
				child.parentMethod();
				
				String string = child.toString();
		
		}
}
```

child.toString

`toString()` 메서드는
인스턴스에 대한 정보를 문자열로 반환하기 때문에, 인스턴스의 정보를 출력하는데 사용된다.


Object.toString()

```java
public String toString(){
		retur getClass().getNAme() + "@" + Integer.toHexString(hashCode());
}
```
Object가 제공하는 toString()메서드는 기본적으로 패키지를 포함한 객체의 이름과 객체의 참조값(해시코드)를 16진수로 제공한다.

```java
public static String valueOf(Object obj){
		return (obj == null) ? "null" : obj.toString();
}
```
println()을 사용할 때, toString()을 직접 호출할 필요 없이 객체를 바로 전달하면 객체의 정보를 전달할 수 있다.

println()과 toString()

```java
//toString() 반환값  출력
String string = object.toString();
System.out.println(string);

//object 직접 출력
System.out.println(object);
```

```java
package lang.object.tostring;

public class ObjectPrinter{
		public static void print(Object obj){
				String string = "객체 정보 출력: " + obj.toString();
				System.out.println(string);
		}
}
```

toString()은 기본으로 객체의 참조값을 출력한다. 그런데 toString()이나 hashCode()를 재정의하면 객체의 참조값을 출력할 수 없다. 이때는 다음 코드를 사용하면 객체의 참조값을 출력할 수 있다.
