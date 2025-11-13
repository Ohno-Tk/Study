# Reactの基礎

## 目次
* JavaScript基礎
  * [DOMとは？](#contents1)
  * [仮想DOMとは？](#contents2)
  * [パッケージマネージャー](#contents3)
  * [npm/yarnの基本](#contents4)
  * [ECMAScriptとは](#contents5)
  * [モジュールバンドラーとは](#contents6)
  * [トランスパイラとは](#contents7)
  * [SPAとは](#contents8)
* React基礎
  * [jsx記法とは](#contents9)
  * [コンポーネントとは？](#contents10)
  * [StrictModeとは？](#contents11)
  * [jsとjsx](#contents12)
  * [props](#contents13)
  * [state](#contents14)
  * [再レンダリング(userEffect)](#contents15)

## JavaScript基礎
<a id="contents1"></a>

### DOMとは？
Document Object Modelの略。ドムと読む  
HTMLなどを解釈し木構造で表現したもの  
開発者ツールで読むことが出来る。  
  
従来のDOMは、素のJavaScriptやJQueryなど  
直接操作をしていた。

> $('ul > li:fisrt-child').remove();
> $('ul').append('<li>追加する要素</li>');

問題点としては、レンダリングコスト高、コードの複雑化  
上記を解決するために作成されたのが、仮想DOM

<a id="contents2"></a>

### 仮想DOMとは？
JavaScriptのオブジェクトで仮想的に作られたDOM  
いきなりDOMを操作せず、JS上で仮想DOMを操作し差分を出してからDOMに反映

<a id="contents3"></a>

### パッケージマネージャー
かつてのJavaScriptは、1つのJSファイルに全ての処理を記述していた  
→処理が複雑になるにつれてコードがカオス化。  
→コードの再利用が出来ないなどの問題があった。

少し改善されたJavaScriptは、他のJSファイルを読み込んで使っていた。  
→コードの再利用、共通化は出来るようになった  
→読み込み順を意識しないとエラーになる(依存関係)  
→何がどこから読み込まれたものか分からない  

試行錯誤があって、モダンなJavaScriptでは、  
npm/yarn等のパッケージマネージャーを使用  
→内部ではNode.jsが動いている。  
　→依存関係を勝手に解決してくれる。  
　→import先が明示的に分かる  
　→世界中で公開されているパッケージをコマンド1つで利用可能  
　→チーム内での共有も簡単に  

<a id="contents4"></a>

### npm/yarnの基本
![React_1.png](./img/React_1.png)

<a id="contents5"></a>

### ECMAScriptとは
* 読み方は、えくますくりぷと
* JavaScriptの標準規格(こういうルールで書くぜ！)
* 欧州電子計算機工業会(ECMA:European Computer Manufacturers Association)の略
* 毎年1回発表される
* ES5 = ES2024、ES6 = ES2025と少しややこしい
* ES20xxの呼び方が一般化している
* ES2015で機能追加が多くあり、近代JSの転換期と言える。  
  
ES2015で追加された規格
* let、constを用いた変数宣言
* アローファンクション
* Class構文
* 分割代入
* テンプレート文字列
* スプレッド構文
* Promise  
など  

<a id="contents6"></a>

### モジュールバンドラーとは
複数のjs(css/image)ファイルを1つにまとめたもの  
依存関係についてもいい感じにまとめてくれる。

<a id="contents7"></a>

### トランスパイラとは
新しいJavaScriptの記法を古い記法に変換してくれる。  
例)BABEL、SWCなど

<a id="contents8"></a>

### SPAとは
Single Page Applicationの略。  
→モダンJavaScriptはSPAが基本  
→HTMLは1つのみでJavaScriptで画面を書き換える。  

* SPAのメリット
  * ページ遷移毎のチラつきがなくなる
  * 表示速度のアップによるユーザ体験向上
  * コンポーネント分割が用意になることで開発効率アップ



## React基礎

<a id="contents9"></a>

### jsx記法とは
JSXとは"JavaScript XML"の略で，Reactを実装するためのJavaScriptの拡張構文  
JSXはJavaScriptの中にHTMLとほとんど同じように記述することができる。  
そのため，UIを簡単に記述し，視覚的に理解しやすくしたもの。

<a id="contents10"></a>

### コンポーネントとは？
ReactではJavaScriptの中でHTMLを書くことができ、  
ボタンやヘッダー、フッターなど、画面の部品単位でパーツを作れます。  
これをコンポーネントと言います。

JavaScriptの中でHTMLで書く方法を「jsx」と言います。  
Reactではこの方法を使いコンポーネントファイルを作成。

> const App = () => {  
>  return < h1>こんにちは！< /h1>  
>}  
> root.render(  
>  < StrictMode>  
>    < App />  
>  < /StrictMode>  
>);

App関数の中で複数のタグを返却したい場合は、()で囲むが以下のようなエラーとなる。
> const App = () => {  
>  return (
>  < h1>こんにちは！< /h1>  
>  < p>お元気ですか？< /p>
>);  
>};  
> root.render(  
>  < StrictMode>  
>    < App />  
>  < /StrictMode>  
>);

> Adjacent JSX elements must be wrapped in an enclosing tag,

returnでは、何かしらのタグで囲まれていないといけないので以下の様に修正。

> const App = () => {  
>  return (
>  < React.Fragment>  
>    < h1>こんにちは！< /h1>  
>    < p>お元気ですか？< /p>  
>  < /React.Fragment>  
>);  
>};  
> root.render(  
>  < StrictMode>  
>    < App />  
>  < /StrictMode>  
>);


関数の前にexportの記述することで
外部のjsから呼び出す事が出来る。
> export const App = () => {  
>  return (
>  < React.Fragment>  
>    < h1>こんにちは！< /h1>  
>    < p>お元気ですか？< /p>  
>  < /React.Fragment>  
>);  
>};  

<a id="contents11"></a>

### StrictModeとは？
React StrictModeは、コンポーネント内の実装問題を警告したり、
予期せぬ動作の要因になりうる使用法を提示するためのモード。

* 純粋でない (impure) レンダーによって引き起こされるバグを見つけるために、レンダーを追加で1回行う
* コンポーネントは、エフェクトのクリーンアップし忘れによるバグを見つけるために、エフェクトの実行を追加で1回行う
* コンポーネントは、ref のクリーンアップし忘れによるバグを見つけるために、ref コールバックの実行を追加で1回行う
* コンポーネントが非推奨のAPIを使用していないかチェックします

<a id="contents12"></a>

### jsとjsx
開発者がわかりやすいように、明示的にJSXが書かれているファイルなのか、  
そうでないかを判別するためのもの。  
.js: jsxを使わないファイル  
.jsx: jsxを使うファイル

<a id="contents13"></a>

### props
コンポーネントへ渡す引数のようなもの

> export const App = () => {  
>  return (  
>  < React.Fragment>  
>    < h1>こんにちは！< /h1>  
>    < ColorfulMessage color="blue" message="お元気ですか？" />  
>  < /React.Fragment>  
>);  
>};  
>
> export const ColorfulMessage = (props) => {  
>  const contentStyleA = {  
>  color: props.color,  
>  fontSize: "18px"  
>}  
>  return < p style={contentStyleA}>{props.message}< /p>  
>};  

props.childrenにすると、messageが要らなくなる。
> export const App = () => {  
>  return (  
>  < React.Fragment>  
>    < h1>こんにちは！< /h1>  
>    < ColorfulMessage color="blue">お元気ですか？< /ColorfulMessage>  
>  < /React.Fragment>  
>);  
>};  
>
> export const ColorfulMessage = (props) => {  
>  const contentStyleA = {  
>  color: props.color,  
>  fontSize: "18px"  
>}  
>  return < p style={contentStyleA}>{props.children}< /p>  
>};  

分割代入することでprops.の記述を省略できる。
> export const ColorfulMessage = (props) => {  
>  const { color, children } = props;
>  const contentStyleA = {  
>  color: color,  
>  fontSize: "18px"  
>}  
>  return < p style={contentStyleA}>{children}< /p>  
>};  

<a id="contents14"></a>

### state
それぞれのコンポーネントが持っている状態のこと。

> export const App = () => {  
>  const [num, setNum] - useState(0);  
>  const onClickCountUp = () => {  
>    setNum(num + 1):  
>};  
>  return (  
>  < React.Fragment>  
>    < h1>こんにちは！< /h1>  
>    < ColorfulMessage color="blue">お元気ですか？< /ColorfulMessage>  
>    < button onClick={onClickCountUp}>カウントアップ< /button>  
>    < p>{num}< /p>  
>  < /React.Fragment>  
>);  
>};  

stateを使う上での注意点
* stateの更新は、関数を読んだ瞬間に実行されるわけではない。

<a id="contents15"></a>

### 再レンダリング(userEffect)
再レンダリングは、stateの状態を検知してReactが勝手にレンダリングしてくれる。
仮想DOMが動いてくれる。

> export const App = () => {  
>  const [num, setNum] - useState(0);  
>  const [isShowFace, setIsShowFace] - useState(true);  
>  const onClickCountUp = () => {  
>    setNum(num + 1):  
>};  
>  const onClickToggle = () => {  
>    setIsShowFace(!isShowFace):  
>};  
>  return (  
>  < React.Fragment>  
>    < h1>こんにちは！< /h1>  
>    < ColorfulMessage color="blue">お元気ですか？< /ColorfulMessage>  
>    < button onClick={onClickCountUp}>カウントアップ< /button>  
>    < p>{num}< /p>  
>    < button onClick={onClickToggle}>on/off< /button>  
>    {isShowFace && < p>('ω')ノ< /p>}  
>  < /React.Fragment>  
>);  
>};  

以下は、3の倍数の時に顔文字を表示させる機能を実装する。  
useEffectは、最初のレンダリング時と[]の変数に変更があった時に実行される。
処理の関心の切り分けが出来る。
> export const App = () => {  
>  const [num, setNum] - useState(0);  
>  const [isShowFace, setIsShowFace] - useState(false);  
>  const onClickCountUp = () => {  
>    setNum(num + 1):  
>};  
>  const onClickToggle = () => {  
>    setIsShowFace(!isShowFace):  
>};  
>  
>  useEffect(() => {  
>  console.log("--useEffect--");  
>    if(num > 0) {
>      if(num % 3 === 0) {  
>        isShowFace || setIsShowFace(true):  
>      } else {  
>        isShowFace && setIsShowFace(false):  
>      }  
>    }
>  }, [num]);  
>  
>  return (  
>  < React.Fragment>  
>    < h1>こんにちは！< /h1>  
>    < ColorfulMessage color="blue">お元気ですか？< /ColorfulMessage>  
>    < button onClick={onClickCountUp}>カウントアップ< /button>  
>    < p>{num}< /p>  
>    < button onClick={onClickToggle}>on/off< /button>  
>    {isShowFace && < p>('ω')ノ< /p>}  
>  < /React.Fragment>  
>);  
>};  