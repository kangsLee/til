# Codelyzer, TSLint를 사용하여 코드 품질 높이기

최근 [Angular Style Guide](https://angular.io/docs/ts/latest/guide/style-guide.html)를 따르며 코드를 작성하는데, lint task를 돌릴 때 발견하는 것보다 코드를 작성하는 과정에서 발견하는 것이 좋을 것 같아 Codelyzer를 적용해보았다.

### Codelyzer

Angular TypeScript 프로젝트의 정적 코드 분석을 위한 규칙을 정의해둔 분석기
웹 앱, NativeScript, Ionin 등, 에서도 실행 가능하다.

### TSLint

TypeScript 코드에서 가독성, 유지보수성 그리고 기능성 오류들을 검사해준다.



## 사용법

### 패키지 설치

```shell
npm i codelyzer@2.0.0-beta.4 tslint@4.0.0 typescript@2.0.9 @angular/core@2.4.0 @angular/compiler@2.4.0 rxjs@5.0.1 zone.js@0.7.2
```

### tslint 설정 파일 작성

tslint.json 파일을 만들어 아래와 같이 필요한 규칙을 설정한다.

```json
{
  "rulesDirectory": [
    "node_modules/codelyzer"
  ],
  "rules":{
    "directive-selector": [true, "attribute", "sg", "camelCase"],
    "component-selector": [true, "element", "sg", "kebab-case"],
    "use-input-property-decorator": true,
    "use-output-property-decorator": true,
    "use-host-property-decorator": true,
    "no-attribute-parameter-decorator": true,
    "no-input-rename": true,
    "no-output-rename": true,
    "no-forward-ref": true,
    "use-life-cycle-interface": true,
    "use-pipe-transform-interface": true,
    "pipe-naming": [true, "camelCase", "sg"],
    "component-class-suffix": true,
    "directive-class-suffix": true,
    "import-destructuring-spacing": true,
    "templates-use-public": true,
    "no-access-missing-member": true,
    "invoke-injectable": true
  }
}
```

### TSLint 실행

```shell
$ ./node_modules/.bin/tslint -c tslint.json component.ts
```

### 실시간 lint 체크

#### VSCODE

```json
{
  "tslint.rulesDirectory": "./node_modules/codelyzer",
  "typescript.tsdk": "node_modules/typescript/lib"
}
```

#### intellij based IDEs

- **Preferences** - **Node.js and NPM** - **+ 버튼** 클릭 - **Available Packages**에서 **tslint**를 찾아 설치
- **Preferences** - **Language&Frameworks** - **TypeScript** - **TSLint**에서 **Enable**클릭 후 **tslint.json**을 선택

**Reformat Code**를 사용한다면 아래 작업을 추가적으로 수행한다. ( import 괄호 양쪽 공백 추가 )

- **Preferences** - **Editor** - **TypeScript** - **Spaces** - **Within** - **ES6 import/export braces**



참고 사이트

> [Codelyzer](https://github.com/mgechev/codelyzer)
>
> [TSLint](https://palantir.github.io/tslint/)
>
> [Using TSLint Code Quality Tool](https://www.jetbrains.com/help/idea/2016.2/using-tslint-code-quality-tool.html?search=reformat)