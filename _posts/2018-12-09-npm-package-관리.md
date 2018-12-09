---
layout: post
title: "npm package 관리"
tags: [npm]
comments: true
---

- npm의 목적은 *설치된 패키지 관리*이다. '패키지'는 완전한 애플리케이션, 코드 샘플, 프로젝트에서 사용할 모듈 또는 라이브러리 등 다양한 형태이다.
- npm은 노드를 설치할 때 함께 설치된다.
- NodeJS 홈페이지(https://nodejs.org/) 방문하여 설치할 수 있으며, 안정 버전, 최신 버전 중 안정 버전 설치를 권장 한다.

> $ brew install node

> $ node -v

> $ npm -v


- npm 패키지는 전역(Globally) 또는 로컬(Locally)로 설치 가능하다.
- 전역 패키지는 보통 개발 과정에서 사용하는, 터미널에서 실행하는 도구들이다.
- 로컬 패키지는 각 프로젝트에 종속되는 패키지이다.

> npm install [package name]
> npm install [package name@version]

- 로컬 모듈은 프로젝트 루트에 node_modules라는 디렉터리로 생성된다.
- 설치하는 모듈이 늘어나면 모듈을 추적하고 관리할 방법이 필요해지는데 프로젝트에 설치하고 사용하는 모듈을 의존성(dependency)이라고 부른다.
- npm은 package.json 파일을 통해 의존성을 관리한다.
> npm init
- 의존성은 일반 의존성과 개발 의존성으로 나뉜다.
- 개발 의존성은 앱을 실행할 때는 필요 없지만, 프로젝트를 개발할 때 필요하거나 도움이되는 패키이다.
- 로컬 패키지를 설치할 때 --save 또는 --save-dev 플래그를 사용한다.
- 위 플래그를 사용하지 않으면 package.json에 등록되지 않는다.
> npm install
- package.json 파일을 읽고 필요 패키지를 다시 내려받아 설치한다.

