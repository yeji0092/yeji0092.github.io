---
layout : post
title : Lambda Expression
author : YEJI KIM
date : 2019-09-10
categories : JAVA

---
# Lambda Expression
- 객체 지향 언너보다 함수 지향 언어에 가까움
- 함수를 간략하면서도 명확한 식으로 표현가능
- 메소드를 람다식으로 표현 시, 메소드 이름 및 반환값이 없어지므로 익명함수 라고도 함
- 람다식의 형태는 매개 변수를 가진 코드블록이지만, 런타임 시에는 익명 구현 객체를 생성  


---
## 1. Lambda의 표현 방식

````
(parameters) -> expression body
(parameters) -> {expression body}
() -> {expression body}
() -> expression body
````

---
## 2. Lambda를 사용한 Map foreach

```java
List<Map<String,Object>> myList1 = new ArrayList<>();
myList1.add(myMap1);
myList1.add(myMap2);

Map<String, Object> myMap3 = new HashMap<>();
Map<String, Object> myMap4 = new HashMap<>();
 
myMap3.put("name", "이종호");
myMap3.put("age", "27");
myMap3.put("country", "CHINA");
 
myMap4.put("name", "강준성");
myMap4.put("age", "28");
myMap4.put("country", "UK");
 
// finalMap 안에 List와 Map을 담음
finalMap.put(0, myList1);
finalMap.put(1, myMap3);
finalMap.put(2, myMap4);

/*
finalMap :
{
  0=[{country=KOREA, name=이상현, age=29}, {country=USA, name=김철수, age=25}]
  , 1={country=CHINA, name=김수르, age=26}
  , 2={country=UK, name=김영희, age=23}
}
*/

// 1. for문
for(int i=0; i< finalMap.size(); i++) {
  System.out.println(finalMap.get(0));
}
 
// 2. foreach문 - keySet사용
for ( Integer key : finalMap.keySet() ) {
  System.out.println( key );
  System.out.println(finalMap.get(key));
}
 
// 3. foreach문 - entrySet사용
for ( Map.Entry<Integer, Object> entry : finalMap.entrySet()) {
  System.out.println(entry.getKey());
  System.out.println(entry.getValue());
}
 
// 4. lambda 사용한 foreach문
finalMap.forEach((k,v) ->{
  System.out.println(k);
  System.out.println(v);
});
 
// 5. lambda 사용한 foreach문
  finalMap.forEach((k,v) -> System.out.println(k +""+ v));

```

---
## 3. Lambda로 interface 추상화메소드 호출

```java
// Lambda식을 위한 인터페이스에서 추상 메소드는 단 하나여야 한다.
// @FunctionalInterface 어노테이션을 사용함으로써 추상메소드를 1개만 선언할수 있게 제한
@FunctionalInterface
public interface myInterface1{
  public int compareMethod(int value1, int value2);
}

public static void func1(myInterface1 myinterface1){
  int value1 = 100;
  int value2 = 200;
 
  int finalValue = myinterface1.compareMethod(value1, value2);
  System.out.println(finalValue);
}

public static void main(String[] args) {
 
  // Lambda 사용한 인터페이스 메소드 호출 1
  func1((i, j)->{
    return  i * j;
  });
  // output : 20000
}
```

```java
@FunctionalInterface
public interface myInterface2 {
  public int calc(int a, int b);
}

public static void main(String[] args) {
  // Lambda 사용한 인터페이스 메소드 호출 2
  myInterface2 addExp1 = (int a, int b) -> a + b;
  myInterface2 addExp2 = (int a, int b) -> { return a + b; };
  myInterface2 sub = (int a, int b) -> a - b;

  int result = addExp1.calc(1, 2) + addExp2.calc(1, 2) + sub.calc(-5, 5); // 6 - 10 = -4
  System.out.println(result);
  // output : -4
}
```
  

---
## 4. Lambda를 사용하여 함수 정의 및 호출

```java
new Thread(new Runnable(){
  @Override
  public void run(){
    System.out.println("Thread Runnable Define");
  }
}).start();

new Thread(()-> {
  System.out.println("Thread Lambda Express");
}).start();

```

---

## 5. Lambda를 사용하여 List Stream Method

```java
List<Integer> myList1 = new ArrayList<>();
for(int i=0; i<=4; i++) {
  myList1.add(i);
}
 
// 스트림// 스트림
myList1.stream();                
        
// stream 요소 반복
myList1.stream().forEach(System.out::println);                             
// 0 1 2 3 4
        
// stream 요소를 연산가능하게 함
myList1.stream().map(i -> i*i).forEach(System.out::println);      
// 0 1 4 9 16
        
// stream 요소의 인덱스까지 제한함
myList1.stream().limit(1).forEach(System.out::println);                
// 0

// stream 요소의 인덱스를 생략
myList1.stream().skip(1).forEach(System.out::println);                
// 1 2 3 4
        
// stream 요소를 조건문과 비교하여 필터
myList1.stream().filter(i-> i<=1).forEach(System.out::println);     
// 0 1
        
// stream 단일요소 반환 0+1+2+3+4
myList1.stream().reduce((a,b)-> a+b).get();                                
// 10
```

