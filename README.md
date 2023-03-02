# yarn-berry-Vite-Twin.macro-Mui-Redux

### why yarn berry
1. 빌드 시간을 일부 단축시켜준다.
2. 개발과정에서의 안정성을 높여준다.
3. 기존 패키지 매니저에서 일어나는 비효율성, 유령 의존성을 해결한다.

### 고려할점
1. .yarnrc.yml의 링커 설정을 pnp가 아닌 node-modules 로 하게 된다면 기존처럼 node_modules를 설치하여 의존성을 관리하게 됩니다. 
하지만 이렇게 사용할 경우 앞서 설명드린 PnP의 장점들을 활용하지 못하게 됩니다.
2. yarn 2.x 버전 부터는 pre-hook(ex. preinstall , prepare 등) 을 지원하지 않습니다. 문서에 따르면 이는 사이드 이펙트를 줄이기 위한 
의도적인 변경이라고 하며, 호환성을 위해서 preinstall 과 install 은 postinstall의 일부로서 실행됩니다.
기존에 husky 등을 사용하기 위해 걸어둔 pre-hook이 있었다면 yarn berry 업그레이드 후 작동하지 않을 것이므로 이에 대한 처리가 필요합니다.

#### package.json

```
  "babelMacros": {
    "twin": {
      "preset": "emotion"
    }
  },
``` 
preset이 기본적으로 emotion으로 되어있으므로, 다른 옵션을 사용할때는 반드시 명시해줘야한다.
```
```
패키지들이 zip 아카이브로 관리되기 때문에 기존의 방식으로는 정상적으로 타입이 불러와지지 않는다.
Editor SDK 설정을 하기 전에 먼저 VSCode에서 zipfs 을 설치해줍니다. 
이 extension는 zip 아카이브에서 직접 파일을 읽을 수 있도록 VSCode에 지원을 추가한다


#### tsconfig.json : vite 기본 설정 + twin.macro에서 요구하는 설정 추가


#### .yarnrc.yml : 
v2부터 유효한 Yaml로 작성되어야 하고 올바른 확장자를 가져야 합니다 (단순히 .yarnrc 파일을 호출 하면 실행되지 않음).
````
plugins:
  - path: .yarn/plugins/@yarnpkg/plugin-typescript.cjs
    spec: "@yarnpkg/plugin-typescript"

yarnPath: .yarn/releases/yarn-3.4.1.cjs

````
plugin부분은 @yarnpkg/sdks vscode


#### .pnp.cjs

````

````

#### .pnp.loader.mjs
````
````

참고 : https://github.com/ben-rogerson/twin.examples/tree/master/vite-emotion-typescript


