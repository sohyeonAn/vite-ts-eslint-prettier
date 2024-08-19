## Airbnb Javascript 스타일 가이드

**1. 설치**

[`eslint-config-airbnb`](https://www.npmjs.com/package/eslint-config-airbnb)를 설치합니다.

```bash
$ yarn add --dev eslint-config-airbnb eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react
```

`peerDependencies`를 확인하고 모든 의존성을 설치합니다.

```bash
# peerDependencies 확인하는 방법
$ npm info "eslint-config-airbnb@latest" peerDependencies
```

**2. ESLint 설정**

- `.eslintrc.js`

  ```js
  module.exports = {
    ...
    extends: [
      'airbnb',
      'airbnb/hooks',
      ...
    ],
    ...
  }
  ```

### 참고

- [Javascript 스타일 한국어 가이드](https://github.com/ParkSB/javascript-style-guide)
- [React 스타일 가이드](https://github.com/airbnb/javascript/tree/master/react/)
