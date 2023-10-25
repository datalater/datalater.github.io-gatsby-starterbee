# datalater.github.io

Built with [gatsby-starter-bee](https://github.com/JaeYeopHan/gatsby-starter-bee).

## 로컬 서버 실행하기

```sh
npm start
```

## 포스트 작성하기

다음 두 곳에서 포스팅을 추가할 수 있습니다.

- 블로그 포스팅은 `content/blog` 디렉토리에 추가해주세요.
- 웹에 올려둘 이력서는 `content/__about` 디렉토리에 추가해주세요.

> 몇 가지의 메타데이터와 마크다운 문법으로 포스팅을 작성할 수 있습니다.

### 새로운 포스트를 작성할 때 커맨드라인을 통해 할 수 있습니다

![cli-tool-example](assets/cli-tool-example.gif)

```sh
npm run post
```

위 커맨드를 입력하면 새로운 포스트가 생성됩니다.

👉 **gatsby-post-gen** CLI 도구를 사용합니다. (https://github.com/JaeYeopHan/gatsby-post-gen)

## 메타데이터 수정

`/gatsby-meta-config.js` 파일에서 블로그를 설정하는 여러 요소를 수정할 수 있습니다.

## 배포

[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/JaeYeopHab/gatsby-starter-bee)

:bulb: github pages를 통해 배포하고 싶다면 아래 npm script를 `package.json`에 추가해주세요.

```json
"scripts": {
  "deploy": "gatsby build && gh-pages -d public -b master -r 'git@github.com:datalater/datalater.github.io.git'"
}
```

> `gh-pages` 모듈이 필요할 경우 설치가 필요합니다.

## 🧐 입맛에 맞게 바꾸기

### ⚙ 설정

```sh
/root
├── gatsby-browser.js // font, polyfill, onClientRender ...
├── gatsby-config.js // Gatsby config
├── gatsby-meta-config.js // Template meta config
└── gatsby-node.js // Gatsby Node config
```

### ⛑ 구조

```sh
src
├── components // Just component with styling
├── layout // home, post layout
├── pages // routing except post: /(home), /about
├── styles
│   ├── code.scss
│   ├── dark-theme.scss
│   ├── light-theme.scss
│   └── variables.scss
└── templates
    ├── blog-post.js
    └── home.js
```

### 🎨 스타일

`src/styles` 디렉토리에서 CSS 속성들을 수정할 수 있습니다.

```sh
src/styles
├── code.scss
├── dark-theme.scss
├── light-theme.scss
└── variables.scss
```

### 🍭 꿀팁

- 프로필 사진! (replace file in `/content/assets/profile.png`)
- 파비콘 이미지! (replace file in `/content/assets/felog.png`)
- 헤더의 그라데이션! (\$theme-gradient `/styles/variables.scss`)
- `robots.txt` 에 배포되는 도메인으로 업데이트를 위한 설정을 해주세요! (replace file in `gatsby-config.js` 의 `https://your-blog.netlify.app` 부분)
- Utterances를 위한 repository를 설정을 해주세요! (`/gatsby-meta-config.js`의 repository 주소를 교체해주세요.)
  - ⚠️ 이 가이드(https://utteranc.es/)를 꼭 확인해주세요.
