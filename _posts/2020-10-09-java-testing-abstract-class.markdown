---
layout: post
title:  "자바 추상클래스 테스트하기"
date:   2020-10-09
tags: [java]
---
자바에서 클래스를 테스트하는 방법은 무엇일까? 예를 들어 `MyClass`라는 클래스를 테스트하고 싶다면, 통상적으로 `MyClassTest`라는 테스트 전용 클래스를 만든 다음, 그 안에서 `MyClass`의 인스턴스를 생성해서 테스트 로직을 구현한다. 하지만 만약 `MyClass`가 추상 클래스 (abstract class)라면? 이 경우엔 `MyClass`의 인스턴스를 생성할 수 없기 때문에 기존 방법을 사용할 수 없게 된다. 

한 가지 대책은 `MyClass`의 하위 클래스를 사용하는 것이다. 예를 들어 `MyClass`를 상속하는 `MySubClass`라는 하위 클래스가 있다고 해보자. 그러면 `MyClassTest`에서 `MySubClass`의 인스턴스를 생성해서 `MyClass` 타입으로 선언한 뒤 테스트 로직을 구현하면 된다.
```java
public class MyClassTest {
    @Test
    public void test1() {
        MyClass myClass = new MySubClass();
        // 나머지 테스트 로직
    }
}
```
대강 이런 식으로 말이다.

하지만 이 방법은 `MyClass`의 테스트가 `MySubClass`에 의존하게 된다는 치명적인 단점이 있다. 만약 코드가 수정되어서 `MySubClass` 클래스가 없어진다면 `MyClass` 클래스는 변경되지 않았음에도 불구하고 `MyClassTest`를 수정해야 한다. 이런 상황을 회피하기 위해 오직 `MyClass`의 테스트만을 위한 기능 없는 하위 클래스를 하나 만들어놓는 방법을 생각할 수 있지만, `main` 아래에 오직 테스트만을 위한 클래스가 존재한다는 건 나같이 디지털 결벽증이 있는 사람에게는 절대 용납할 수 없는 일이다.

그렇다면 하위 클래스에 의존하지 않고 추상 클래스만으로 테스트를 만들 수 있는 방법이 있을까? 바로 Mockito 라이브러리를 사용하면 된다.

# Mockito를 사용해 추상 클래스의 인스턴스 만들기
기본적으로 Mockito는 목(mock)을 제공해주는 라이브러리다. 목 객체는 클래스를 흉내내는 가짜 객체에 불과하기 때문에 테스트하려는 클래스의 인스턴스를 목 객체로 만드는 것은 보통 좋지 않다. 하지만 추상 클래스에 대해선 예외가 될 수 있다. Mockito가 추상 클래스의 인스턴스를 목 객체로 만들어주는 기능을 제공하기 때문이다. 

예를 들어 `MyClass`가 다음과 같이 구현되어 있다고 가정하자.
```java
public abstract class MyClass {
    int a;

    public MyClass() {
        a = 1;
    }

    public int getA() {
        return a;
    }

    public void add(int b) {
        a += b;
    }
}
```

그러면 다음과 같이 목 객체를 만들어 테스트할 수 있다.
```java
public class MyClassTest {
    @Test
    public void testAdd() {
        MyClass myClass = mock(MyClass.class, withSettings().useConstructor().defaultAnswer(CALLS_REAL_METHODS));
        myClass.add(2);
        assertEquals(3, myClass.getA());
    }
}
```
여기서 `withSettings()`에 체이닝된 메서드들의 의미는 다음과 같다.
- `useConstructor()`: 생성자를 사용한다는 의미이다. 원래는 `useConstructor(Object... args)` 형태로 사용되며 `args`가 생성자의 파라미터로 들어가지만, 여기서는 파라미터 없는 생성자를 사용하고 있다 (Mockito 2.7.14 버전 이후만 해당, 그 이전 버전은 파라미터 없는 생성자만 사용할 수 있다).
- `defaultAnswer(CALLS_REAL_METHODS)`: 이 설정으로 만들어진 목 객체는 메서드를 따로 스터빙(stubbing)하지 않으면 실제 메서드를 호출한다. 이러한 목 객체를 스파이(spy)라고도 부르며 Mocikto는 스파이 객체를 만드는 기능도 따로 제공한다. 그래서 위 코드는 다음과 같이 쓸 수도 있다.
```java
public class MyClassTest {
    @Test
    public void testAdd() {
        MyClass myClass = spy(MyClass.class);
        myClass.add(2);
        assertEquals(3, myClass.getA());
    }
}
```

만약 다음과 같이 `MyClass`에 파라미터를 받는 생성자가 있고, 테스트에서 이 생성자를 사용해서 목 객체를 만들고 싶다면?
```java
    public MyClass(int a) {
        this.a = a;
    }
```
그러면 `useConstructor()`에 파라미터를 넣어주면 된다.
```java
    MyClass myClass = mock(MyClass.class, withSettings().useConstructor(1).defaultAnswer(CALLS_REAL_METHODS));
```
# 제네릭 추상 클래스 테스트하기
만약 `MyClass`가 다음과 같이 제네릭 추상 클래스로 구현되어 있다면 목 객체를 만들 수 있을까?
```java
public abstract class MyClass<T> {
    Map<T, Integer> a;

    public MyClass() {
        a = new HashMap<>();
    }

    public void put(T key, int value) {
        a.put(key, value);
    }

    public int get(T key) {
        return a.get(key);
    }
} 
```
이 문제는 의의로 쉽다. 다음과 같이 타입만 지정해주면 된다.
```java
public class MyClassTest {
    @Test
    public void testPut() {
        MyClass<String> myClass = spy(MyClass.class);
        myClass.put("a", 1);
        assertEquals(1, myClass.get("a"));
    }
}
```

쉬웠으니까 좀 더 복잡하게 만들어 보자. 만약 다음과 같이 제네릭 타입이 재귀적으로 정의되어 있으면 어떻게 해야 할까?
```java
public abstract class MyClass<T, U extends MyClass<T, U>> {
     Map<T, Integer> a;

    public MyClass() {
        a = new HashMap<>();
    }

    public void put(T key, int value) {
        a.put(key, value);
    }

    public int get(T key) {
        return a.get(key);
    } 

    public U filter(int threshold) {
        Map<T, Integer> newA = new HashMap<>();
        for (Map.Entry<T, Integer> entry : a.entrySet()) {
            if (entry.getValue() > threshold) {
                newA.put(entry.getKey(), entry.getValue());
            }
        }
        a = newA;
        return (U) this;
    }

    public U scale(int factor) {
        for (Map.Entry<T, Integer> entry : a.entrySet()) {
            a.put(entry.getKey(), entry.getValue() * factor);
        }
        return (U) this;
    }
}
```
(이런 식으로 제네릭 타입을 정의하면 자기 자신의 타입을 리턴하는 메서드를 하위 클래스에서 재정의하지 않아도 된다. 메서드 체이닝을 위한 메서드들을 구현할 때 유용하다.)

다음과 같이 나이브하게 타입을 지정해주면 컴파일 에러가 뜬다.
```java
    MyClass<String, MyClass> myClass = spy(MyClass.class);
    // Type parameter 'MyClass' is not within its bound; should extend 'MyClass<java.lang.String,MyClass>'
```
이럴 때는 다음과 같이 와일드카드 타입으로 선언하면 된다.
```java
    MyClass<String, ? extends MyClass> myClass = spy(MyClass.class);
```

### 참고한 페이지
[Mockito Documentation](https://javadoc.io/doc/org.mockito/mockito-core/latest/org/mockito/Mockito.html){:target="_blank"}