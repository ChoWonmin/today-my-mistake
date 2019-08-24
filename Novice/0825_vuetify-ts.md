# ts 환경에서 Vuetify plugin 에러

### 환경

``` bash
> node -v
# node : 10.16.3

> npm -v
# npm : 6.9.0

> vue --version
# vue-cli : 3.11.0
```

### 에러 메세지
``` console
Try `npm install @types/vuetify` if it exists or add a new declaration (.d.ts) file containing `declare module 'vuetify/lib';`
    1 | import Vue from 'vue';
  > 2 | import Vuetify from 'vuetify/lib';
      |                     ^
    3 | 
    4 | Vue.use(Vuetify);
    5 | 
```

``` bash
> npm install @types/vuetify
```
를 실행해도 에러

### 해결방법
https://github.com/vuetifyjs/vue-cli-plugin-vuetify/issues/43

tsconfig.json의 compilerOptions에 vuetify 옵션을 추가해줘야 ts-compiler가 정상 작동

``` json
"compilerOptions": {
    "types": ["vuetify", // other ],
```

