---
layout : post
title : MAVEN(1)
author : yeji
date: 2019-09-09 
categories: java

---
## MAVEN

### Maven이란?  
:자바 프로젝트의 빌드를 자동화해주는 빌드 툴  
  
(자바소스를 compile 하고 package해서 deploy하는 일을 자동화 해주는 것)
  
    
**1) setting.xml**  
maven tool 자체에 관련된 설정을 담당  
  
MAVEN_HOME/conf/에 존재 (* MAVEN_HOME은 환경변수에 설정한 경로) 
  
  
**2) pom.xml**  
  
자바 프로젝트의 빌드 툴로 maven 설정했다면, 프로젝트 최상위 디렉토리에 "pom.xml"이라는 파일이 생성된다.
  
pom.xml은 POM(Project Object Model)을 설정하는 부분으로 프로젝트 내 빌드 옵션을 설정하는 부분이다.
  
다른 파일이름으로 저장 가능하나 다른 개발자들도 알아보기 쉽도록 pom.xml 주로 사용한다.


```java
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>kr.co.wisenut.search.util</groupId>
  <artifactId>querylog-parser</artifactId>
  <version>1.0-SNAPSHOT</version>

  <name>querylog-parser</name>
  <!-- FIXME change it to the project's website -->
  <url>http://www.example.com</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
    <jackson.version>2.9.6</jackson.version>
  </properties>

  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
    <!-- jackson -->
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>${jackson.version}</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>com.fasterxml.jackson.dataformat</groupId>
      <artifactId>jackson-dataformat-yaml</artifactId>
      <version>${jackson.version}</version>
      <scope>compile</scope>
    </dependency>
      <dependency>
          <groupId>org.apache.commons</groupId>
          <artifactId>commons-compress</artifactId>
          <version>1.14</version>
          <scope>test</scope>
      </dependency>
      <!-- //jackson -->
  </dependencies>

  <build>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <!-- clean lifecycle, see https://maven.apache.org/ref/current/maven-core/lifecycles.html#clean_Lifecycle -->
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.1.0</version>
        </plugin>
        <!-- default lifecycle, jar packaging: see https://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_jar_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.8.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.22.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-jar-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>2.5.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>2.8.2</version>
        </plugin>
        <!-- site lifecycle, see https://maven.apache.org/ref/current/maven-core/lifecycles.html#site_Lifecycle -->
        <plugin>
          <artifactId>maven-site-plugin</artifactId>
          <version>3.7.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-project-info-reports-plugin</artifactId>
          <version>3.0.0</version>
        </plugin>
      </plugins>
    </pluginManagement>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <configuration>
          <source>8</source>
          <target>8</target>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

\<modelVersion> : maven의 pom.xml의 모델 버전  
  
\<groupId> : 프로젝트를 생성한 조직 또는 그룹명 (보통 URL의 역순으로 지정)  
  
\<artifactId> : 프로젝트에서 생성되는 기본 아티팩트의 고유 이름  
  
\<version> : 애플리케이션 버전 (SANPSHOP이 붙으면 아직 개발단계라는 의미=> maven에서 라이브러리 관리하는 방식이 다름)  
  
\<packaging> : jar, war, ear, pom등 패키지 유형  
  
 \<name> : 프로젝트명  
   
 \<description> : 프로젝트 설명  
   
 \<url> : 프로젝트를 찾을 수 있는 URL
 
 위는 프로젝트 정보에 관련된 정보  
 
 **\<properties> : pom.xml에서 중복해서 사용되는 설정(상수) 값들을 지정해놓는 부분**   
 **다른 위치에서 ${...}로 표기해서 사용할 수 있다.**  
 **ex) java.version에 1.8 적용 후, 다른 위치에서 ${java.version}이라고 쓰면 "1.8"이라고 쓴 것과 동일한 효과**  
 
 **\<profiles> : dev, prod 이런식으로 개발할 때, 릴리즈할 때를 나눠야할 필요가 있는 설정값은 profiles로 설정할 수 있다.**  
 **maven goal 부분에 -P 옵션으로 프로파일을 선택할 수 있다.**    
   
 ```java
 <profiles>
  <profile>
   <id>dev</id>
   <properties>
    <java.version>1.8</java.version>
   </properties>
  </profile>
  <profile>
   <id>prod</id>
   <properties>
    <java.version>1.9</java.version>
   </properties>
  </profile>
</profiles>
```

 **ex) mvn compile -P prod 라고 하면 ${java.version}은 1.9가 된다.**  
 
 
 


