# Vueの基礎

## 目次
* 視聴したコンテンツ
* [Vue.jsとは](#contents1)
* [クリックイベント(v-on)](#contents2)
* [条件分岐(v-if(if文))](#contents3)
* [属性の設定(v-bind)](#contents4)
* [ループ処理(v-for)](#contents5)
* [部品化(components)](#contents6)
* [データ渡し(props)](#contents7)
* [テンプレート構文](#contents8)
* [v-html](#contents9)


## 視聴したコンテンツ
* [超Vue.js 完全ガイド2025 (Vue Router, Pinia含む)](https://persolpt-eng.udemy.com/course/vue-js-complete-guide/)

<a id="contents1"></a>

## Vue.jsとは
Webのユーザインターフェースを簡単に作るためのJavaScriptフレームワーク

<a id="contents2"></a>

### クリックイベント(v-on)
```index.html
<html>
<head>
  <meta charset="utf-8" />
  <script src="https://unpkg.com/vue@3.0.0"></script>
</head>
<body>
  <div id="app1">
    <p>{{ count }}回クリックした</p>
    <button v-on:click="increment">+</button> <!--v-on:clickでクリックイベントを登録 -->
    <button v-on:click="decrement">-</button> <!--v-on:clickでクリックイベントを登録 -->
  </div>
  <script>
    const App1 = { //Vueコンポーネントを定義
      data() { //dataメソッドを定義 Vue.jsにこのデータを返すという宣言
        return {
          count: 0
        }
      },
      methods: { //methodsメソッドを定義
        increment() { //incrementメソッドを定義
          this.count+=1 //countをインクリメント
        },
        decrement(){
          this.count-=1 //countをデクリメント
        }
      }
    }
    app1 = Vue.createApp(App1) //Vueアプリケーションを作成
    app1.mount('#app1') //VueアプリケーションをHTML要素にマウント
  </script>
</body>
</html>
```
<a id="contents3"></a>

### 条件分岐(v-if(if文))
```index.html
<html>
<head>
  <meta charset="utf-8" />
  <script src="https://unpkg.com/vue@3.0.0"></script>
</head>
<body>
  <div id="app1">
    <span v-if="seen">ルフィ</span>
    <button v-on:click="off">非表示</button> <!--ボタンをクリックするとoffメソッドが実行される-->
  </div>
  <script>
    const App1 = { //Vueコンポーネントを定義
      data() { //dataメソッドを定義 Vue.jsにこのデータを返すという宣言
        return {
          seen: true　//seenがtrueなら表示、falseなら非表示
        }
      },
      methods: {
        off: function(){
          this.seen = false //seenをfalseにする offメソッドが実行されると、seenがfalseになり、ルフィが非表示になる
        }
      }
    }

    app1 = Vue.createApp(App1) //Vueアプリケーションを作成
    app1.mount('#app1') //VueアプリケーションをHTML要素にマウント
  </script>
</body>
</html>
```

<a id="contents4"></a>

### 属性の設定(v-bind)
* HTMLの属性や要素の値を動的に更新できる。  
HTMLの属性や要素の値をVue.jsのデータと結びつけたい時に、  
Vue.jsのデータの変更に応じて、HTMLの属性や要素の値が自動的に更新される。

```index.html
<html>
<head>
  <meta charset="utf-8" />
  <script src="https://unpkg.com/vue@3.0.0"></script>
</head>
<body>
<!--CSSのスタイルを記述-->
<style> 
  .lightblue {
    color:lightblue;
  }

  .orange {
    color: orange;
  }
</style>

  <div id="app1">
    <!--HTML属性は展開されないので、v-bindを使う-->
    <p v-bind:class="class1">水色</p>
    <!--省略した書き方-->
    <p :class="class2">オレンジ</p>
  </div>

  <script>
    const App1 = { //Vueコンポーネントを定義
      data() { //dataメソッドを定義 Vue.jsにこのデータを返すという宣言
        return {
          class1: 'lightblue',
          class2: 'orange'
        }
      },
    }

    app1 = Vue.createApp(App1) //Vueアプリケーションを作成
    app1.mount('#app1') //VueアプリケーションをHTML要素にマウント
  </script>
</body>
</html>
```

<a id="contents5"></a>

### ループ処理(v-for)
Vue.jsでのループ処理

``` index.html
<html>
<head>
  <meta charset="utf-8" />
  <script src="https://unpkg.com/vue@3.0.0"></script>
</head>
<body>
  <div id="app1">
    <ul>
      <li v-for="todo in todos">
        {{ todo.text }}
      </li>
    </ul>
  </div>

  <script>
    const App1 = { //Vueコンポーネントを定義
      data() { //dataメソッドを定義 Vue.jsにこのデータを返すという宣言
        return {
          todos: [
            { text: 'Laravel' },
            { text: 'Next.js' },
            { text: 'Ruby on Rails'},
          ]
        }
      },
    }

    app1 = Vue.createApp(App1) //Vueアプリケーションを作成
    app1.mount('#app1') //VueアプリケーションをHTML要素にマウント
  </script>
</body>
</html>
```

<a id="contents6"></a>

### 部品化(components)
HTML要素を部品化して、再利用できるようにしたもの。

```index.html
<html>
<head>
  <meta charset="utf-8" />
  <script src="https://unpkg.com/vue@3.0.0"></script>
</head>
<body>
  <div id="app1">
    <ul>
      <template1></template1>
    </ul>
  </div>

  <script>
    const App1 = {} //Vueコンポーネントを定義
    const app = Vue.createApp(App1) //Vueアプリケーションを作成

    app.component('template1',{ //Vueコンポーネントを定義
      template:`
      <button>ボタン</button>
      <br>
      `
    })

    app.mount('#app1') //VueアプリケーションをHTML要素にマウント
  </script>
</body>
</html>
```

<a id="contents7"></a>

### データ渡し(props)
親コンポーネントから子コンポーネントにデータを渡すためのもので、  
親コンポーネントで定義されたデータや属性を子コンポーネントに渡すことができる。

```index.html
<html>
<head>
  <meta charset="utf-8" />
  <script src="https://unpkg.com/vue@3.0.0"></script>
</head>
<body>
  <div id="app1">
    <ul>
      <template1 prop1 = "次へ"></template1>
      <template1 prop1 = "前へ"></template1>
    </ul>
  </div>

  <script>
    const App1 = {

    } //Vueコンポーネントを定義
    const app = Vue.createApp(App1) //Vueアプリケーションを作成

    app.component('template1',{ //Vueコンポーネントを定義
      props: ['prop1'],
      template:`
        <button>{{prop1}}</button>
        <br>
      `
    })

    app.mount('#app1') //VueアプリケーションをHTML要素にマウント
</script>
</body>
</html>
```

<a id="contents8"></a>

### テンプレート構文
* HTML に JavaScript のデータやロジックを埋め込むための仕組み

```
<script sutup>
    const name = ref('太郎');
</script>

<template>
  <div>
    <h1>こんにちは、{{ name }}!</h1>
  </div>
</template>
```

<a id="contents9"></a>

### v-html
* 文字列をhtmlタグとして認識させたい場合に使用できる。
* スタイルが効かないので注意。
* XSS攻撃(クロスサイトスクリプティング)の危険性があるので使用箇所に注意。

```
<script sutup>
    const name = ref('<h1>太郎</h1>');
</script>

<template>
  <div>
    <div v-html="name"></h1>
  </div>
</template>
```