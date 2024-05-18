---
title: "[FE Portfolio] boinda 프로젝트를 하면서 겪은 문제점들 정리"

toc: true
toc_sticky: true
date: 2024-05-17
last_modified_at: 2024-05-17
---

### pyscript의 자바스크립트 객체

react에서 csv파일을 입력받아 pyscript에서 csv파싱을 위해 File타입의 데이터를 넘겨주었는데 , pyscript에서는 JsProxy객체로 자동으로 변환되었다.

그걸 모르고 계속 파이썬의 dict처럼 사용하려다가 에러가 발생했는데, JsProxy는 자바스크립트 객체를 파이썬에서 사용할 수 있게 해주는데 파이썬의 dict대괄호 접근이 아닌 자바스크립트의 접근방식 .으로 가져와야했다.

### pyscript에서의 Class인스턴스 만들기

react에서 csv파일을 입력받아 pyscript에서 csv파싱을 하려고 했는데 pyscript에서 FileReader인스턴스를 만들기위해 new FileReader()를 사용했으나 error가 발생했다.

pyscript에선 자바스크립트 클래스의 인스턴스를 만들기 위해선 Class.new()로 만들어야 했다.
