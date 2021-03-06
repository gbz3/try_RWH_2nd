# try_RWH_2nd

## node.js 14.x.x インストール

```bash
$ nodenv install --list |grep ^14  # 14.x.x が無い
$ git -C "$(nodenv root)"/plugins/node-build pull
$ nodenv install --list |grep ^14
14.0.0
14.x-dev
14.x-next
14.1.0
$ nodenv install 14.1.0
Downloading node-v14.1.0-linux-x64.tar.gz...
-> https://nodejs.org/dist/v14.1.0/node-v14.1.0-linux-x64.tar.gz
Installing node-v14.1.0-linux-x64...
...
$ nodenv local 14.1.0
$ node -v
v14.1.0
$ npm -v
6.14.4
```

## 環境構築

- [最新版で学ぶwebpack 4入門
JavaScriptのモジュールバンドラ](https://ics.media/entry/12140/)
- [最新版で学ぶwebpack 4入門 - Babel 7でES2020環境の構築(React, Vue, Three.js, jQueryのサンプル付き)](https://ics.media/entry/16028/)
- [最新版TypeScript+webpack 4の環境構築まとめ(React, Vue.js, Three.jsのサンプル付き)](https://ics.media/entry/16329/)

### npmモジュールインストール

```bash
$ npm init
$ npm install --save-dev webpack webpack-cli typescript ts-loader
$ cat package.json
...
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack",
    "watch": "webpack -w"
  },
...
  "devDependencies": {
    "ts-loader": "^7.0.2",
    "typescript": "^3.8.3",
    "webpack": "^4.43.0",
    "webpack-cli": "^3.3.11"
  },
  "private": true
}
```

### tsconfig.json

```json
{
  "compilerOptions": {
    "sourceMap": true,
    "target": "es5",
    "module": "es2015"
  }
}
```

### webpack設定ファイル

```bash
$ vi webpack.config.js
$ cat webpack.config.js
module.exports = {
  mode: "development",
  entry: "./src/main.ts",
  module: {
    rules: [
      {
        test: /\.ts$/,
        use: 'ts-loader',
      }
    ]
  },
  resolve: {
    extensions: [
      '.ts', '.js',
    ]
  }
};
```

### ビルド

```bash
$ npm run build
...
Hash: ae298551ba1dce06f43c
Version: webpack 4.43.0
Time: 710ms
Built at: 05/04/2020 4:45:54 PM
  Asset     Size  Chunks             Chunk Names
main.js  4.7 KiB    main  [emitted]  main
Entrypoint main = main.js
[./src/main.ts] 76 bytes {main} [built]
[./src/sub.ts] 206 bytes {main} [built]
```
