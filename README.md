## Husky + lint-staged

### Husky

[Husky](https://typicode.github.io/husky/)는 Git hooks를 설정하여 커밋 전후에 자동으로 스크립트를 실행할 수 있게 해줍니다. 이를 통해 lint, 테스트 등의 작업을 자동화합니다.

**1. Husky를 사용하는 이유**
Git hooks 는 `/.git/hooks` 디렉토리에 저장됩니다. 하지만 `./git` 디렉토리는 기본적으로 git ignore의 대상이기 때문에 hook를 공유하기 위해서 husky를 사용합니다.

**1. 설치**

```bash
$ yarn add --dev husky
```

**초기 설정**

```bash
$ yarn exec husky init
```

`init` 명령: `.husky`/에 `pre-commit` 스크립트를 생성하고, `package.json`의 `prepare` 스크립트를 업데이트합니다.

### lint-staged

[lint-staged](https://www.npmjs.com/package/lint-staged)는 Git hooks를 사용하여 스테이징된 파일에만 린트와 포맷 작업을 수행하는 도구입니다. 커밋하는 파일에만 검증을 집중할 수 있습니다.

**1. 설치**

```bash
$ yarn add --dev lint-staged
```

**2. 설정**

- `lint-staged` 설정:

  lint-staged 는 [다양한 방법으로 구성](https://github.com/lint-staged/lint-staged#configuration)할 수 있습니다. 이 프로젝트는 `package.json` 을 사용합니다.

  ```json
  // package.json
  {
    "scripts": { ... },
    "lint-staged": {
      "\*.{js,jsx,ts,tsx}": [
        "eslint --ext .ts,.tsx,.js,.jsx --fix"
      ]
    },
    ...
   }
  ```

  ```json
  // .lintstagedrc
  {
    "*.{js,jsx,ts,tsx}": ["eslint --ext .ts,.tsx,.js,.jsx --fix"]
  }
  ```

- `pre-commit` hook 설정

  Husky의 pre-commit 훅에 연결하여, 커밋하기 전에 자동으로 lint-staged를 실행합니다.

  ```js
  // .husky/pre-commit
  npx lint-staged
  ```

**3. 사용**

`git commit`을 실행할 때 `lint-staged`에 설정한 명령어가 자동으로 실행됩니다.
