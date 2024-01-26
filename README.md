# TypeScript-Beginner
> Programming with Mosh
<https://www.youtube.com/watch?v=d56mG7DezGs>\
> 布魯斯前端
<https://www.youtube.com/watch?v=GinkGJZBHIY>
## What is TypeScript?
> JavaScript w/ type checking
> A porgamming language(created by Microsoft) to address shortcomings of JavaScript
### A programming language built on top of JavaScript
- Every JavaScript file is a valid TypeScript file(TypeScript is a superset of JavaScript)
- TypeScript offers Static typing, Code completion, Refactoring, Shorthand notations
- Drwbacks: Compilation(browsers don't understand TypeScript), Discipline in coding
> Recommand to use TypeScript in a medium to large project
## Enviornment setting
1. Install node.js
2. Open a terminal window and enter `npm i -g typescript`. `-g` means install it globally so we can access it in every directory
3. Enter `tsc -v` to check the TypeScript version you install
## Transpilation
Enter `tsc index.js`(or `npx tsc index.js`) to get the transpilated JavaScript file.
```typescript
let age: number = 20;
age = 'a' // type 'string' is not assignable to type 'number'.
```
Transpilate following program
```typescript
let age: number = 20;
```
to the following JavaScript file
```javascript
var age = 20;
```
## Configuring the TypeScript Compiler
### Create a configuration file of the TypeScript compilor
Enter `tsc --init` in terminal
### Something in the configuration file
- `target`: version of JavaScript the compilor generate(es2016 is a safe option)
- `module`: `commonjs`
- `rootDir`: present the current folder(`./src`)
  - In convention, we put our source code into a separate folder(src folder)
- `outDir`: output JavaScript file(`./dist`)
- `removeComments`: generate JavaScript code without comment
- `noEmitOnError`: `true` won't generate JavaScript when TypeScript code has error
Enter `tsc` to compile all the TypeScript file
Additional: Some important settings
```jsonld
{
  "compilerOptions": {
    "target": "ES5", // 編譯後的JavaScript程式碼版本

    /* Modules */
    "module": "CommonJS", // 編譯後產生的模組形式 (註：設定為commonjs通常是為了能讓程式在Node上執行)
    "rootDir": "./src", // 設定編譯根目錄

    /* JavaScript Support */
    "allowJs": true, // 允許js檔案是否被TypeScript Compilet檢查 (官方建議可設"checkJs"為true來取得錯誤報告)
    "checkJs": true, // 會對js檔案進行型別檢查且輸出錯誤報告

    /* Emit */
    "sourceMap": true, // 可建立來源檔案與輸出的js檔案關係map
    "outDir": "./public", // 編譯器編譯後的js檔案放置處 (註：public通常是要部署專案到伺服器用的資料夾)
    "removeComments": true, // 不會輸出註解
    "noEmit": true, // 可避免輸出不符型別檢查的js檔案, 例如Day 1的string型態變數再賦值number值的範例

    /* Interop Constraints */
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true, // 對import進來的模組檔名強制作大小寫轉換, 可避免如 import LearnTS.ts 寫成 import learnTS.ts 的大小寫錯誤

    /* Type Checking */
    "strict": true
    "noImplicitAny": true    // 不允許未指定型別的變數
    "alwaysStrict":true  // 採用JavaScript嚴格模式檢查型別, 並且會在輸出的每一份JS檔案首行加上 "use strict"
  },
  "files": ["type.ts", "type.spec.ts"], // 編譯檔案白名單, 意即指定要編譯的檔案 (不可用glob指定檔案或資料夾)
  "include": ["src"], // 編譯白名單, 意即指定要編譯的檔案和資料夾
  "exclude": ["node_modules", "**/*.spec.ts"] // 編譯黑名單, 意即指定不要編譯的檔案和資料夾
}
```
source: <https://ithelp.ithome.com.tw/articles/10294197>
## Debugging TypeScript
Enable `sourceMap` in configuration file
- `sourceMap`: Specify how each line of TypeScript code maps to the generated JavaScript code
Enter `tsc` to compile TypeScript code again, you can find a .js.map file in the dist folder(the context is for the machine)
### Debug line-by-line
To debug the following TypeScript code:
```typescript=
let age: number = 20;
if (age < 50)
    age += 10;
```
1. Set a breakpoint at line 1(execute stop at line 1)
2. Go to Run and Debug(`Ctrl+Shift+D`) in VS Code and click on "create a launch.json file" to get the following JSON file:
```jsonld
"configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "Launch Program",
            "skipFiles": [
                "<node_internals>/**"
            ],
            "program": "${workspaceFolder}\\src\\index.ts",
            "outFiles": [
                "${workspaceFolder}/**/*.js"
            ]
        }
    ]
```
3. Add `"preLaunchTask": "tsc: build - tsconfig.json"` between `"program"` and `"outFiles"`
```jsonld
"configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "Launch Program",
            "skipFiles": [
                "<node_internals>/**"
            ],
            "program": "${workspaceFolder}\\src\\index.ts",
            "preLaunchTask": "tsc: build - tsconfig.json",
            "outFiles": [
                "${workspaceFolder}/**/*.js"
            ]
        }
    ]
```
4. Go to Run and Debug and click on "Launch"(`F5`)
## Build-in Types
| JavaScript | TypeScript |
| :--------- | :--------- |
| number     | any        |
| string     | unknown    |
| boolean    | never      |
| null       | enum       |
| undefined  | tuple      |
| object     |            |


