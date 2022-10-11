---
title: "Java 문법"
output:
  html_document:
    keep_md: true
disqusIdentifier: fdsF34ff34
categories: Java
clearReading: true
metaAlignment: center
date: '2022-09-18 13:13:19'
---


### day0918
<!-- excerpt -->

- 기본 자료형 8개
    - 논리형 - boolean
    - 문자형 - char
    - 정수형 - byte, short, int, long
    - 실수형 - float, double

- println() 에서 ln은 line의 줄임말이다. 자기혼자 한 줄 차지하는문법. (html의 <div>와 같다)
- printf()나 print()로 출력하면 옆으로 붙어서 나오는데 \n (원화표시+n) 을 붙이면 줄바꿈이 된다.
- println() = printf(”블라블라%d대충 욕\n”)

- 객체
    - 우리가 프로그래밍으로 구현할 대상.
    - 프로그램을 구성하는 로직을 변수화, 함수화로 구분 하여서 서로 연관된 행위나 속성들을 그룹화 하는 것
    - 이런 데이터들을 서로 연결해서 객체라는 껍데기에 응집시키는 것

- 접근제한자
    - private : 해당 클래스에서만 접근 가능(같은 패키지여도 접근불가)
    - public : 어떤 클래스에서도 접근 가능
    - default
    - protected

- class
    - String 과 같은 참조형 데이터타입이다.
    - class는 설계도와 같다.
    - 인스턴스화(생성) 해야 비로소 물리적인 구현으로 쓰여진다.

- 생성자
    - 접근제한자 class명(데이터타입 인풋명, 데이터타입 인풋명){ 본문 }
    - 객체를 인스턴스화(생성)하는 역할
    - 같은 클래스에는 적어도 하나 이상의 생성자가 있어야 하며, 자바에서는 생성자가 한개도 없으면 디폴트 생성자를 만든다.
    - 생성자가 하나라도 있으면 디폴트 생성자를 만들지 않는다.
    - 함수처럼 보이지만 리턴타입이 없고, 이름이 클래스명과 같다.