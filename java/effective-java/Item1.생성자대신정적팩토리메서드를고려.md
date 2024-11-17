> 이팩티브 자바를 보고 공부한 것을 정리한 것을 알립니다.

# 1. 정적 팩토리 메서드의 간략한 예시

```java
    public static Boolean valueOf(boolean b) {
      return b ? Boolean.TRUE : Boolean.FALSE;
    }
```

# 2. 정적 팩토리 메서드의 장점

1. 생성자와 달리 `객체 생성에 의미 있는 객체의 특성을 Naming`할 수 있다.
   * 이 점은 다른 개발자가 특정 목적에 따른 객체 생성이 어떠한 역할을 하는지 유추 가능해진다.
2. 호출할 때마다 인스턴스를 새로 생성하지 않아도 된다.
   * 그 덕에 불변 클래스로 사용하거나 언제 어느 인스턴스를 살아 있게 할지 개발자가 통제할 수 있다.
3. 반환 타입의 하위 타입 객체를 반환할 수 있는 능력이 있다.
   * 구현 클래스를 알지 못해도 사용할 수 있다. 예시를 들자면 자바의 collections가 있다. 개발자가 사용할 땐, add같은 함수가 어떻게 구현됬는지 알 수 없다.
4. 입력 매개변수에 따라 다른 클래스의 객체를 반환할 수 있다. 
   * EnumSet 클래스는 생성자 없이 정적 팩토리만 제공한다. 원소가 64개 이하라면 RegulerEnumSet 인스턴스, 65개 이상이라면 JumboEnumSet 인스턴스를 사용한다. 다음 릴리즈에서 원소가 적은 RegulerEnumSet을 삭제하더라도 전혀 문제가 발생하지 않는다.
5. 정적 팩토리 메서드는 작성하는 시점에 반환하는 클래스가 존재하지 않아도 된다.
   * 서비스 제공자 프레임워크의 근간 중 하나.
   * 서비스 인터페이스(service provider framework), 제공자 등록 API(provider registraion API), 서비스 접근 API(service access API)이 있다.
   * 여기서 서비스 접근 API가 '유연한 정적 팩터리'이다.

# 3. 팩토리 메서드의 단점

1. 상속하려면 public이나 protected 생성자가 필요하다, 하지만 정적 팩터리 메서드만 제공한다면 하위 클래스를 만들 수 없다.(아이템 17과 18) 컴포지션을 사용하면 해결 가능하다고 한다.
2. 정적 팩터리 메서드는 프로그래머가 찾기 어렵다. API와 메서드의 역할에 대한 문서화를 잘 정리해야 한다.

# 4. 정적 팩토리 메서드 명명

1. from: 매개 변수를 하나 받아서 해당 타입의 인스턴스를 반환하는 형변환 메서드

```java
import java.util.Date;

Date date = Date.from(instant);
```
2. of: 여러 매개변수를 받아 적합한 타입의 인스턴스를 반환하는 집계 메서드

```java
   import java.util.EnumSet;

Set<Rank> faceCards = EnumSet.of(JACK, QUEEN, KING);
```

3. valueOf: from과 of의 더 자세한 버전

```java
import java.math.BigInteger;

BigInteger prime = BigInteger.valueOf(Integer.MAX_VALUE);
```

4. instance 혹은 getInstance: (매개 변수를 받는다면) 매개변수로 명시한 인스턴스는 반환하지만, 같은 인스턴스임은 보장하지 않는다.

```java
StackWalker luke = StackWalker.getInstance(option);
```

5. create 혹은 newInstance: 매번 새로운 인스턴스를 생성하는 것을 보장

```java
import java.lang.reflect.Array;

Object newArray = Array.newInstance(classObject, arrayLen);
```

6. getType: getInstance와 같으나, 생성할 클래스가 아닌 다른 클래스에 팩터리 메서드를 정의할 때 사용한다.

```java
import java.nio.file.FileStore;
import java.nio.file.Files;
//Type은 반환할 객체의 이름을 뜻한다.
FileStore fs = Files.getFileStore(path);
```

7. newType: newInstance와 같으나, 생성할 클래스가 아닌 다른 클래스에 팩터리 메서드를 정의할때 쓴다.

```java
import java.io.BufferedReader;
import java.nio.file.Files;

BufferedReader br = Files.newBufferedReader(path);
```
8. type : getType,newType의 간단한 버전

```java
import java.util.Collections;
import java.util.List;
import javax.annotation.processing.Completion;

List<Completion> litany = Collections.list(legacyLitany);
```

