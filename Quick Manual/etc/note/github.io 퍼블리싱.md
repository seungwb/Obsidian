- v4 브랜치로 이동
- content 폴더에 컨텐츠 붙여넣기
- `npm i` 로 라이브러리 설치
- `npx quartz build --serve` 로 빌드 후 확인까지
- `public` 폴더 생성 됨
- `v4` 브랜치에 `push`
- `public` 폴더 외부에 잘라내서 붙여넣기, `node_modules` 폴더 삭제 ( 이유: `gh-pages` 브랜치로 이동할때 해당 폴더들은 `gitignore` 되어있기 때문에 불편함을 감수해야한다.)
- `gh-pages` 브랜치로 이동
- `public`안에 내용물 싹다 복붙 (복붙 전에 삭제 할거 있는지 확인해볼 것)
- `gh-pages` 브랜치에 `push`
- 퍼블리싱 완료 됐는지 확인