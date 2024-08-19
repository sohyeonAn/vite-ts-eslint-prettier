# Vite(react-ts) + ESLint + Prettier

이 프로젝트는 Vite를 사용하여 React와 TypeScript로 구성된 템플릿입니다. 코드 품질 유지를 위해 ESLint와 Prettier를 사용하였습니다.

## Vite(react-ts)

[Vite](https://vitejs.dev/guide/)는 빠르고 효율적인 웹 개발 도구로, ESM(ECMAScript Modules)을 활용하여 개발 서버의 빠른 시작과 실시간 핫 리로딩을 지원합니다. `Rollup`을 사용한 프로덕션 빌드로 최적화된 번들링을 제공하며, 다양한 프레임워크와 플러그인을 지원합니다.

**1. 템플릿을 통한 프로젝트 생성**

```bash
$ yarn create vite vite-ts-eslint-prettier --template react-ts
```

**2. 기본 구성 확인**

본 프로젝트는 **Vite@5.3.4** 버전을 통해 생성되었습니다. 기본 구성은 vite의 버전에 따라 다르게 생성될 수 있습니다.

- `package.json`

  ```json
  {
    "name": "vite-ts-eslint-prettier",
    "private": true,
    "version": "0.0.0",
    "type": "module",
    "scripts": {
      "dev": "vite",
      "build": "tsc -b && vite build",
      "lint": "eslint . --ext ts,tsx --report-unused-disable-directives --max-warnings 0",
      "preview": "vite preview"
    },
    "dependencies": {
      "react": "^18.3.1",
      "react-dom": "^18.3.1"
    },
    "devDependencies": {
      "@types/react": "^18.3.3",
      "@types/react-dom": "^18.3.0",
      "@typescript-eslint/eslint-plugin": "^7.15.0",
      "@typescript-eslint/parser": "^7.15.0",
      "@vitejs/plugin-react": "^4.3.1",
      "eslint": "^8.57.0",
      "eslint-plugin-react-hooks": "^4.6.2",
      "eslint-plugin-react-refresh": "^0.4.7",
      "typescript": "^5.2.2",
      "vite": "^5.3.4"
    }
  }
  ```

- `.eslintrc.cjs`
  ```js
  module.exports = {
    root: true,
    env: { browser: true, es2020: true },
    extends: [
      'eslint:recommended',
      'plugin:@typescript-eslint/recommended',
      'plugin:react-hooks/recommended',
    ],
    ignorePatterns: ['dist', '.eslintrc.cjs'],
    parser: '@typescript-eslint/parser',
    plugins: ['react-refresh'],
    rules: {
      'react-refresh/only-export-components': [
        'warn',
        { allowConstantExport: true },
      ],
    },
  }
  ```
- 이 외 구성은 프로젝트 세팅 [commit](https://github.com/sohyeonAn/vite-ts-eslint-prettier/commit/9bed2183d142eca3f9113fa40a52864f18faa84e) 을 통해 확인할 수 있습니다.

## ESLint

ESLint는 JavaScript와 TypeScript 코드의 일관성과 품질을 유지하는 데 도움을 주는 도구입니다. 코드의 문법 오류를 찾아내고, 스타일을 강제하여 일관된 코드 품질을 보장합니다.

\*vite로 react-ts 템플릿을 사용하여 프로젝트를 구성한 경우 eslint 가 세팅되어 있으므로 eslint의 설치 방법은 생략합니다.

## Prettier

Prettier는 코드의 포맷을 자동으로 맞추어 주는 도구입니다. 이를 통해 코드 스타일을 일관되게 유지할 수 있습니다.

**1. 설치**

```bash
$ yarn add --dev prettier
```

`.prettierrc` :

- Prettier의 코드 포맷팅 규칙을 설정하는 구성 파일입니다.
- Prettier를 사용하는 도구와 편집기(예: VSCode)에서 `.prettierrc` 파일을 읽어 자동으로 포맷팅을 적용합니다.
- 일반적으로 프로젝트의 루트 디렉토리에 위치해야 합니다.

**2. ESLint 설정**

- 기본 규칙: [`eslint-plugin-prettier`](https://www.npmjs.com/package/eslint-plugin-prettier) 를 기반으로 설정합니다.
- 설치:

  ```bash
  $ yarn add --dev eslint-plugin-prettier eslint-config-prettier
  ```

  `eslint-plugin-prettier`가 `eslint-config-prettier`를 사용하기 때문에 두 의존성을 모두 설치해야 합니다.

  > `eslint-plugin-prettier`: Prettier 규칙을 ESLint 규칙으로 변환하여, 코드가 Prettier의 스타일에 맞지 않을 때 ESLint가 오류를 발생시킵니다.<br/> > `eslint-config-prettier`: Prettier와 충돌하는 ESLint 규칙을 비활성화하여, Prettier가 적용된 스타일을 ESLint가 방해하지 않도록 합니다.

- `.eslintrc.js`에 플러그인 추가

  ```js
  module.exports = {
  ...
  extends: [
    ...
    "plugin:prettier/recommended",
  ],
  ...
  ```

  - ESLint가 코드 스타일 관련 규칙을 체크할 때 Prettier의 설정과 충돌하지 않도록 `extends` 의 가장 마지막 줄에 추가합니다.
  - 이렇게 설정하면 다음과 같은 일이 발생합니다: [참고](https://github.com/prettier/eslint-plugin-prettier#configuration-new-eslintconfigjs)<br/>
    > - `prettier/prettier` 규칙이 활성화됩니다.
    > - `arrow-body-style`과 `prefer-arrow-callback` 규칙이 비활성화됩니다. 이 규칙들은 이 플러그인과 함께 사용 시 문제가 발생할 수 있습니다.
    > - `eslint-config-prettier` 설정이 활성화되어, Prettier와 충돌하는 ESLint 규칙이 꺼집니다.
