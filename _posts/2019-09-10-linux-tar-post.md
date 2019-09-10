---
layout : post
title : LINUX tar을 이용한 파일 묶기, 풀기, 압축, 해제 
author : YEJI KIM
date : 2019-09-10
categories : LINUX

---

## LINUX tar 이용 
---

**현재 디렉토리에 있는 모든 파일 묶기**
* tar cvf 파일명 ./*


**현재 디렉토리에 파일 풀기**
* tar xvf 파일명

**현재 디렉토리에 있는 모든 파일을 파일명으로 압축**
* tar cvfz 파일명.gz ./*


**현재 디렉토리에 gz파일 푼다**
* tar xvfz 파일명.gz

---
ex) 
tar -zcvf sf1-v5.3-tower-ia64-glibc27-gcc41-x64.tar.gz ./bin  
  
추후 필요한 내용 추가



