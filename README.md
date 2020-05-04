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
+ typescript@3.8.3  # nodenv-default-packages で自動追加
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

### npmモジュールインストール

```bash
$ npm init
$ npm install --save-dev webpack webpack-cli babel-loader @babel/core @babel/preset-env
$ cat package.json
...
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack"
  },
...
  "devDependencies": {
    "@babel/core": "^7.9.6",
    "@babel/preset-env": "^7.9.6",
    "babel-loader": "^8.1.0",
    "webpack": "^4.43.0",
    "webpack-cli": "^3.3.11"
  }
}
```

### webpack設定ファイル

```bash
$ vi webpack.config.js
$ cat webpack.config.js
module.exports = {
  mode: "development",
  entry: "./src/index.js",
  module: {
    rules: [
      {
        test: /\.js$/,
        use: [
          {
            loader: 'babel-loader',
            options: {
              presets: [
                '@babel/preset-env',
              ]
            }
          }
        ]
      }
    ]
  }
};
```

### ビルド

```bash
$ npm run build
...
Hash: b2ac1705fd0e89fdf70c
Version: webpack 4.43.0
Time: 577ms
Built at: 05/04/2020 3:53:15 PM
  Asset      Size  Chunks             Chunk Names
main.js  4.67 KiB    main  [emitted]  main
Entrypoint main = main.js
[./src/index.js] 75 bytes {main} [built]
[./src/sub.js] 176 bytes {main} [built]
```
