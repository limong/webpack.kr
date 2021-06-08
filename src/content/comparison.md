---
title: Comparison
sort: 1
contributors:
  - pksjce
  - bebraw
  - chrisVillanueva
  - tashian
  - simon04
  - byzyk
related:
  - title: JSPM vs. webpack
    url: https://ilikekillnerds.com/2015/07/jspm-vs-webpack/
  - title: webpack vs. Browserify vs. SystemJS
    url: https://engineering.velocityapp.com/webpack-vs-browersify-vs-systemjs-for-spas-95b349a41fa0
---

webpack은 유일한 모듈 번들러가 아닙니다. webpack 또는 아래 번들러 중 하나를 사용하는 경우, webpack이 현재 경쟁 제품과 어떻게 비교되는지에 대한 기능별 비교가 아래에 있습니다.

| 기능 | webpack/webpack | jrburke/requirejs | substack/node-browserify | jspm/jspm-cli | rollup/rollup | brunch/brunch |
|---------|-----------------|-------------------|--------------------------|---------------|---------------|---------------|
| 요구에 따른 추가 청크 로드 | **예** | **예** | 아니오 | [System.import](https://github.com/systemjs/systemjs/blob/master/docs/system-api.md#systemimportmodulename--normalizedparentname---promisemodule) | 아니오 | 아니오 |
| AMD `define` | **예** | **예** | [deamdify](https://github.com/jaredhanson/deamdify) | 예 | [rollup-plugin-amd](https://github.com/piuccio/rollup-plugin-amd) | 예 |
| AMD `require` | **예** | **예** | 아니오 | 예 | 아니오 | 예 |
| AMD `require` loads on demand | **예** | 수동 설정으로 | 아니오 | 예 | 아니오 | 아니오 |
| CommonJS `exports` | **예** | `define`으로 감싼것만 | **예** | 예 | [commonjs-plugin](https://github.com/rollup/rollup-plugin-commonjs) | 예 |
| CommonJS `require` | **예** | `define`으로 감싼것만 | **예** | 예 | [commonjs-plugin](https://github.com/rollup/rollup-plugin-commonjs) | 예 |
| CommonJS `require.resolve` | **예** | 아니오 | 아니오 | 아니오 | 아니오 | |
| require에서의 연결 `require("./fi" + "le")` | **예** | 아니오♦ | 아니오 | 아니오 | 아니오 | |
| 디버깅 지원 | **소스Url(SourceUrl), 소스맵(SourceMaps)**  | 불필요 | 소스맵(SourceMaps) | **소스Url(SourceUrl), 소스맵(SourceMaps)** | **소스Url(SourceUrl), 소스맵(SourceMaps)**  | 소스맵(SourceMaps) |
| 의존성 | 19MB / 127 패키지 | 11MB / 118 패키지 | **1.2MB / 1 패키지** | 26MB / 131 패키지 | ?MB / 3 패키지 | |
| ES2015 `import`/`export` | **예** (webpack 2) | 아니오 | 아니오 | **예** | **예** | 예, [es6 모듈 트랜스파일러](https://github.com/gcollazo/es6-module-transpiler-brunch)를 통해
| require에서의 표현식 (가이드된) `require("./templates/" + template)` | **예 (모든 파일 매칭 포함)** | 아니오♦ | 아니오 | 아니오 | 아니오 | 아니오 |
| require에서의 표현식 (자율) `require(moduleName)` | 수동 설정으로 | 아니오♦ | 아니오 | 아니오 | 아니오 | |
| 단일 번들 생성 | **예** | 예♦ | 예 | 예 | 예 | 예 |
| 간접 require 구문 `var r = require; r("./file")` | **예** | 아니오♦ | 아니오 | 아니오 | 아니오 | |
| 각 파일을 별도로 로드 | 아니오 | 예 | 아니오 | 예 | 아니오 | 아니오 |
| 경로 이름 변경 | **예** | 아니오 | 부분적으로 | 예 | 불필요 (경로이름이 번들에 포함되지 않음) | 아니오 |
| 최소화 | [Terser](https://github.com/fabiosantoscode/terser) | uglify, 클로저 컴파일러 | [uglifyify](https://github.com/hughsk/uglifyify) | 예 | [uglify-plugin](https://github.com/TrySound/rollup-plugin-uglify) | [UglifyJS-brunch](https://github.com/brunch/uglify-js-brunch)
| 공통 번들로 구성된 다중 페이지 작성 | 수동 설정으로 | **예** | 수동 설정으로 | 번들 계산으로 | 아니오 | 아니오|
| 여러 개의 번들 | **예** | 수동 설정으로 | 수동 설정으로 | 예 | 아니오 | 예 |
| Node.js 내장 라이브러리 `require("path")` | **예** | 아니오 | **예** | **예** | [node-resolve-plugin](https://github.com/rollup/rollup-plugin-node-resolve) | |
| 그밖에 Node.js 관련 | process, __dir/filename, global | - | process, __dir/filename, global | process, __dir/filename, global for cjs | global ([commonjs-plugin](https://github.com/rollup/rollup-plugin-commonjs)) | |
| 플러그인 | **예** | 예 | **예** | 예 | 예 | 예 |
| 전처리 | **로더** | 로더 | 변환 | 플러그인 번역 | 플러그인 번환 | 컴파일러, 최적화 도구 |
| 브라우저 대체 | `web_modules`, `.web.js`, package.json 필드, 별칭 설정 옵션 | 별칭 옵션 | package.json 필드, 별칭 옵션 | package.json, 별칭 옵션 | 아니오 | |
| 필수 파일 | 파일 시스템 | **웹** | 파일 시스템 | 플러그인을 통해 | 파일 시스템이나 플러그인을 통해 | 파일 시스템 |
| 런타임 오버헤드 | **243B + 20B per module + 4B per dependency** | 14.7kB + 0B 모듈별로 + (3B + X) 의존성별로 | 415B + 25B 모듈별로 + (6B + 2X) 의존성별로 | 5.5kB 자체 실행 번들을 위해, 38kB 전체 로더와 폴리필을 위해, 0 일반 모듈, 293B CJS, 139B ES2015 System.register gzip실행전 | **ES2015 모듈이 없음** (다른 포멧이 있을 수 있음) | |
| Watch 모드 | 예 | 불필요 | [watchify](https://github.com/browserify/watchify) | 개발환경에서 필요없음 | [rollup-watch](https://github.com/rollup/rollup-watch) | 예 |

♦ 프로덕션 모드에서 (개발 모드와 반대)

X는 경로 문자열의 길이 입니다

## Bundling vs. Loading

_로딩_ 과 _번들링_ 모듈 간의 몇 가지 주요 차이점을 확인하는 것이 중요합니다. [JSPM의](https://github.com/jspm/jspm-cli) 내부에 있는 [SystemJS와] (https://github.com/systemjs/systemjs) 같은 도구를 사용하여 브라우저에서 런타임에 모듈을 로드하고 트랜스파일 합니다. 이는 모듈이 트랜스파일되고 ("로더"를 통해) 브라우저에 도달하기 전에 번들로 제공되는 webpack과는 상당히 다릅니다.

각 방법에는 장단점이 있습니다. 런타임에 모듈을 로드하고 트랜스파일하면 많은 모듈로 구성된 대규모 사이트와 애플리케이션에 많은 오버헤드를 추가할 수 있습니다. 이러한 이유로 SystemJS는 필요한 모듈이 적은 소규모 프로젝트에 더 적합합니다. 그러나 [HTTP/2가](https://http2.github.io/) 서버에서 클라이언트로 파일을 전송할 수 있는 속도를 향상시키기 때문에 다소 변경될 수 있습니다. HTTP/2는 _트랜스파일_ 모듈에 대한 어떤 것도 변경하지 않으며, 클라이언트에서 수행할 때 항상 시간이 더 오래 걸립니다.