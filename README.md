# vue-flying-emoji

画面全体に弾けるスタンプボタンのコンポーネント Vue.js (Vue 3)

[デモサイト](https://yammer.jp/vue-flying-emoji/)

- 下方の、次のような絵文字をクリックすると、画面のランダムな位置へ弾けます。
- flyボタンを押すと、画面右上から絵文字が出現します。


## 特徴

クリックするボタンの描画位置を取得しており、ボタンの描画位置が変わっても、ボタンから弾けるようなエフェクトが崩れないこと

## Vue 2 への対応

コンポーネントの保持するデータの更新を検知してもらうために、以下の代入を this.$set インスタンスメソッドに置き換えると動作します

https://github.com/yammerjp/vue-flying-emoji/blob/5971c2dfbae0452f24cbc0d759f448fc85c65813/src/components/Background.vue#L34

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

