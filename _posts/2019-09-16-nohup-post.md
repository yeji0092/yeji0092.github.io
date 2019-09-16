---
layout : post
title : NOHUP
author : YEJI KIM
date: 2019-09-16
categories: LINUX

---

## nohup

명령어 뒤에 &만 붙이면 백그라운드로 작업 수행 가능  
하지만, 터미널 세션이 끊길 시 백그라운드로 작업중이던 것도 함께 종료

=> nohup 명령어를 사용하면 세션 종료 시에도 실행  

```
$nohup ./indexer -license ../license.xml ... -log stdout &
```

표준 입출력 파일(stdin, stdout, stderr)에 대해 입출력을 수신하면 터미널에 행(hang)이 걸리게 될 수도 있다.  
nohup은 프로세스 우선 순위를 낮추기 위해 `nice` 명령어와 결합해서 사용할 수 있다. 
```
$nohup nice ./indexer &
```

---

## nohup에 의해 수행중인 작업 종료하는 법
```
$ps -ef | grep indexer
```
1) 해당 프로세스가 정상적으로 떠 있는 것을 확인한다.
2) pid 확인 후 kill 명령어로 죽여야만 작업 종료가 된다.  

---

## nohup 표준 출력
별다른 설정 없을 경우, 기본 표준 출력은 nohup.out 파일에 찍히게 된다.  

nohup.out 파일 확인법  

- **명령어 입력때 까지 찍힌 출력내용만 확인**
```
$cat nohup.out 
$tail nohup.out
```
- **진행중인 출력내용 실시간으로 계속해서 확인**
```
$tail -f nohup.out
```


