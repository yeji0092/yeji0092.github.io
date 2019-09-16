---
layout : post
title : Scanner와 BufferedReader 차이
author : YEJI KIM
date : 2019-09-10
categories : JAVA

---
  
  
Scanner VS BufferedReader (+InputStreamReader)
---
  
`Scanner`의 버퍼 크기는 1024 chars  
`BufferedReader`의 버퍼 크기는 8192 chars  

`Scanner`의 장점  
* `BufferedReader`의 경우 import BufferedReader, InputStreamReader 2개,   
`Scanner`의 경우 하나만 불러오면 된다.  

* 콘솔 입력을 보다 쉽게 처리 가능하다.  

* `Scanner`는 Space와 Enter를 모두 경계로 인식하여 데이터 가공이 편리하다.  
`BufferedReader`의 경우 Enter만을 경계로 인식 + 입력받은 데이터 String으로 고정

* `BufferedReader`의 경우 예외처리를 꼭 해주어야한다.  
readLine 할때마다 try&catch 활용(보통 throws IOException 활용)  


`BufferedReader`의 장점  
* 속도가 빠르다.  

* 버퍼사이즈가 크다.  
많은양의 데이터 처리에는 `Scanner`보다 속도가 빠르고 유리하다.  

* 동기화가 가능하다. 멀티쓰레드에 안전하다.  
멀티쓰레드의 경우, 여러 쓰레드가 같은 프로세스 내에서 자원을 공유하므로 서로의 작업에 영향을 줄 수 있다.  
`BufferedReader`는 동기화가 되므로 멀티쓰레드에 안전하다.  

---

Scanner
---
```java
Scanner sc = new Scanner("YEJI KIM/Female/26");
sc.useDelimiter("/");

while(sc.hasNext())
    System.out.println(sc.next());

sc.close();

/*
-----------------------print---------------------------
YEJI KIM
Female
26
*/
```
---
BufferedReader
---

`InputStreamReader`는 입력을 character 로 읽어들인다.   
한글자가 아닌 줄단위의 문자열을 입력으로 받기 편하기 위해 생긴 게 `BufferedReader`이다.  

`BufferedReader` 는 `InputStreamReader`에 버퍼링 기능 추가한 것으로   
사용자가 요청할때마다 읽어오는 것이 아닌, 일정량사이즈로 한번에 읽어온 후 버퍼에 보관한다.  
그리고 사용자가 요구할 때! 버퍼에서 읽어오게 한다. 

```java
//InputStreamReader 필요
BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
String str = bf.readLine();

//읽어온 데이터 String 으로 고정이므로 다른 타입으로 입력 받기 위해서는 형변환이 필수! 
int i1 = Integer.parseInt(bf.readLine());

/*
읽어온 데이터 가공
1. StringTokenizer 사용 
nextToken()을 이용해 입력받은 값을 공백단위로 구분하여 순서대로 호출
*/
StringTokenizer st = new StringTokenizer(str);
String s1 = st.nextToken();
String s2 = st.nextToken();
int i2 = Integer.parseInt(st.nextToken());

/*
2. String.split() 사용
배열에 공백단위로 끊어서 데이터 넣고 사용
*/
String arr[] = s.split(" ");
```

---
+BufferedWriter
---
일반적인 출력때는 `System.out.println("");` 사용하나,  
마찬가지로 많은 양의 데이터 출력에서는 BufferedWriter 활용한다. 
  
```java
BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
String str = "YEJI KIM/Female/26";

//bw.write()에는 자동개행기능이 없기 때문에 개행처리 따로 해주어야함
bw.write(str + "\n");

/*
남아있는 데이터를 모두 출력시킴
BufferedWriter의 경우 버퍼를 잡아 놓았기 때문에 반드시 flush() & close()를 호출해 
후처리를 해주어야 함
*/
bw.flush();
bw.close();
```








