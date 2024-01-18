---
title: "브라우저의 렌더링 과정"
excerpt: "웹 페이지가 어떤 과정을 통해 만들어지는지 알아보자"

categories: frontend

toc: true
toc_sticky: true
date: 2024-01-04
last_modified_at: 2024-01-04
---

### 간단하게 보는 렌더링 과정

# 사용자의 URL입력

사용자가 URL입력창에 정보를 입력하면 브라우저 프로세스가 가장 먼저 작업을 시작합니다.

브라우저 프로세스에는 스토리지 스레드와 네트워크 스레드, UI스레드 등등 여러 스레드들이 존재합니다.

이후 UI스레드가 URL입력창에 들어온 정보가 일반적인 텍스트인지 아니면 URL인지 확인한 후 텍스트라면 검색엔진에 해당 텍스트를 검색한 페이지로 이동시키고
URL이라면 해당 URL로 이동하기 위해 네트워크 스레드가 작업을 시작합니다.

# 응답 도착

네트워크 작업 후 서버에서 응답이 돌아왔다면 해당 응답이 어떤 타입인지 확인합니다.

응답이 파일일경우 다운로드 매니저에게 데이터주고 일반적인 HTML파일 이라면 렌더링 프로세스에게 데이터를 넘겨줍니다.

데이터와 렌더링 프로세스가 모두 준비가 되면 페이지를 이동하는데 이때 브라우저의 UI도 갱신되고 이후에 세션기록도 저장이 됩니다.

### 렌더링 프로세스

렌더링 프로세스는 HTML, CSS, 자바스크립트를 웹 페이지로 변환하는 작업을 수행합니다.

작업 순서는 (HTML을 파싱해서 DOM tree 생성, CSS를 파싱해서 CSSOM tree 생성) -> (Render tree생성) -> (Layout) -> (Paint) -> (합성)

### DOM, CSSOM tree

DOM은 HTML이나 XML같은 문서의 API인데요 문서를 각 요소들을 표현하는 노드, 노드의 속성을 나타내는 프로퍼티, 이런 노드와 프로퍼티를 조작할수있는 메서드를 모아서 구조화된 객체로 나타냅니다.

DOM은 문서를 노드로 나눠서 이 노드들이 특정 노드를 뿌리삼아 퍼지는 트리 형태로 나타내는데요 이것을 DOM tree라고 부릅니다 이때 트리의 최상위 노드를 root노드라고 합니다.

노드는 문서의 요소들을 나타내는 기본 데이터 타입으로 nodeType, nodeName, nodeValue와 자신의 형제, 자식 노드들에 대한 정보 등등 많이 정보들을 담고 있습니다.

다음으로는 CSSOM입니다 CSSOM은 CSS를 조작할수있게 해주는 API로서 DOM과 비슷하게 요소들을 노드로 표현한 트리구조를 가집니다.

간단하게 말해 DOM은 HTML을 CSSOM은 CSS를 조작할수 있게해줍니다.

개인적으로는 CSSOM을 어떻게 발음하는지 궁금하네요

### Render tree

Render tree는 DOM tree와 CSSOM tree를 합쳐서 만듭니다 Render tree에서 노드는 렌더 객체이며 트리의 노드들은 우리의 눈에 보이는 요소들만 포함합니다.

### Layout

Layout은 각 요소의 크기나 위치를 찾는 작업입니다 Render tree의 각 노드들은 자신의 자식 노드들의 레이아웃을 불러올수있는 Layout을 가지고 있습니다.

노드들의 위치는 좌표를 사용하여 표현합니다.

### Paint

Paint 단계에서는 Render tree를 기반으로 레이어를 생성합니다. 각 레이어는 화면에 그려질 때 별도로 처리되며, 이는 성능 최적화를 위해 사용됩니다.

각 레이어는 배경색, 배경 이미지, 텍스트 등의 스타일 정보를 가지고 있습니다. Paint 단계에서는 이러한 스타일 정보를 참고하여 각 레이어의 배경과 텍스트를 화면에 그립니다.

레이어들이 겹쳐있는 경우에는 z-index와 같은 스타일 속성에 따라 겹치는 순서가 결정됩니다. Paint 단계에서는 이러한 순서를 고려하여 레이어를 화면에 그립니다. z-index가 높은 레이어가 더 위에 나타납니다.

### Composite

이제 이전단계에서 얻은 모든정보를 가지고 뷰포트에 맞게 화면을 생성하는 단계입니다.