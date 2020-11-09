# sam-typescript

<!-- https://levelup.gitconnected.com/how-to-use-typescript-for-aws-lambda-in-3-steps-1996243547eb -->

- sam에서 타입스크립트 쓰기

1. package.json에 추가

```json
"scripts": {
  "compile": "tsc"
},
"devDependencies": {
  "aws-sdk": "^2.655.0",
  "@types/aws-lambda": "^8.10.51",
  "@types/node": "^13.13.5",
  "typescript": "^3.8.3"
}
```

2. package.json과 같은 경로에 tsconfig.json 추가

```json
{
  "compilerOptions": {
    "module": "CommonJS",
    "target": "ES2017",
    "noImplicitAny": true,
    "preserveConstEnums": true,
    "outDir": "./built",
    "sourceMap": true
  },
  "include": ["src-ts/**/*"],
  "exclude": ["node_modules", "**/*.spec.ts"]
}
```

3. `npm i` 로 패키지 설치

4. src-ts 밑에 app.ts 작성

5. template.yaml 수정

```yaml
Resources:
  HelloWorldFunction:
    Type: AWS::Serverless::Function
    Properties:
      CodeUri: hello-world/built
      Handler: app.lambdaHandler
```

현재까지 디렉터리 구조

```
├── README.md
├── hello-world
│   ├── package-lock.json
│   ├── package.json
│   ├── src-ts
│   │   └── app.ts
│   └── tsconfig.json
├── samconfig.toml
└── template.yaml
```

6. tsc and deploy

```
npm run compile
sam deploy --guided
```
