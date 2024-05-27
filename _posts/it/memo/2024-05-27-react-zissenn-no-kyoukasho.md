---
layout:     post
title:      "React実践の教科書"
date:       2024-05-27 00:00:00 +0900
categories: it memo
---

![thumbnail](/assets/2024-05-27-react-zissenn-no-kyoukasho/thumbnail.png)

※本ブログの目的と内容[^1]、著作者の方へ[^2]

[^1]: 本ブログは「本を読み、理解した内容の備忘録（自分用）」を目的としている。重要なアイディアを昇華させ、自分の言葉でまとめるように努めている

[^2]: 内容に不快を感じ、ブログの取り下げを希望される著作者の方は、個別にご連絡いただけると幸いに思う

## 1 Reactを始める前に知っておきたいモダンJavaScriptの基礎

### 1-2 DOM・仮想DOM
DOMはHTMLを解釈し、木構造で表現したもの。Document Object Modelの略。
従来、JSで画面の要素を変更する場合は、DOMを直接指定して書き換えるような処理をしてきた。
このようなコードは手続き的で分かりやすい反面、レンダリングコスト（画面の表示速度）に問題が生じやすかったり、
プログラムコードが肥大化してくるとどこで何をしているか分からなくなるというつらさがあった。

#### 仮想DOMとは
JSのオブジェクトで作られた仮想的なDOMのこと。

### 1-3 パッケージマネージャー

#### パッケージマネージャーとは
パッケージの管理、インストール、アップグレード等をになってくれる管理ツール。

#### ECMAScript
JSの標準仕様。

#### 近代JSの転換期
ECMAScriptの大きな改定があったのがES2015(ES6)。

- let, constを用いた変数宣言
- アローファンクション
- Class構文
- 分割代入
- テンプレート文字列
- スプレッド構文
- Promise

#### モジュールバンドラー
「開発はファイルを分けて行い、本番用にビルドするときに１つのファイルにまとめよう」という思想を実現するために、
JSファイルやcssファイル等をまとめてくれるモジュールバンドラーが作られた。
モジュールバンドラーもまた、ファイルを１つにまとめる際に依存関係を解決してくれる優れもの。
現在主流のモジュールバンドラーはwebpack。

#### トランスパイル
JSの記法をブラウザで実行できる形に変換してくれる。
ブラウザによってはまだ新しい記法に対応していないため。
現在主流のトランスパイラはBabel。

#### 開発体験の優れたVite
開発環境においては、ソースコードをバンドルすることなく高速に実行できるようにしている。

### 1-6 SPAと従来のWebシステムの違い

#### 従来のWebシステム
ページ遷移の際に一瞬画面が白くなる（ちらつく）

#### SPAのWebシステム
HTMLファイルは１つのみで、JSによるDOMの書き換えで画面遷移を実現するのが基本

#### SPAのメリット

##### ユーザ体験の向上
ページの表示速度というのは思っている以上に重要で、特にECサイト等では売上に直結する問題で
「表示速度が0.1秒遅くなれば1%売上が減少し、1秒早くなれば10%売上が増加する」というのは有名な話。

##### フロントエンドエンジニアって？？
フロントエンドに特化しつつも、バックエンドやDBの知識もつけていかないといけない。

- タスクによってはバックエンドも合わせて対応できるほうがチームは助かる。自分の市場価値が高まる。
- アプリケーション全体を見て設計するためには一貫した知識がないと判断できない。


## 2 モダンJSの機能に触れる
まずはざっくり概念を把握してあとは手を動かしながら細かい知識を補完していく。

### 2-1 const, letでの変数宣言

#### const で定義した変数を変更できる例
オブジェクトの定義には基本的にconstを使用していく。
配列の場合も同様にconstで定義していく。

### 2-4 分割代入 {} []

#### 配列の分割代入

```javascript
// 1つ目のみ必要な場合
const [ name ] = myProfile;
```

### 2-6 スプレッド構文 ...

#### 要素の展開

```javascript
const arr1 = [1, 2];
const summaryFunc = (num1, num2) => console.log(num1 + num2);

// 普通に配列の値を渡す場合
summaryFunc(arr1[0], arr1[1]);

// スプレッド構文を用いた方法
summaryFunc(...arr1);
```

### 2-8 map, filter

#### indexの扱い

```javascript
const nameArr = ["田中", "山田", "佐藤"];
nameArr.map((name, index) => console.log(`${index + 1}番目は${name}です`));
```

map内の関数は第2引数を書くことができ、書いた場合はそこに0から順番にindexの情報が格納される。

### 2-9 三項演算子
「判定→変数設定」のような時に三項演算子は有用。

### 2-10 論理演算子の本当の意味 && ||
`||`は、その左側がfalse判定なら右側を返す。
`&&`は、その左側がtrue判定なら右側を返す。


## JSでのDOM操作

### 3-1 JSによるDOMアクセス
documentというのはDOMツリーのエントリーポイント。

```javascript
const containers = document.getElementsByClassName("container");
```

##### jQueryって何？？
jQueryはJSライブラリで、複雑なJSのメソッドをもっと簡単に扱えるようにしてるもの。
`document.getElementById("nushida")`は、`$("#nushida")`と書ける。


## Reactの基本

### 4-5 Props

#### Propsを扱うテクニック
Propsをどう扱うかはプロジェクト毎にルールを決めて統一する。
「Propsってdestructureします？」と言ったりする。

```javascript
// 分割代入しない
const Profile = (props) => {
  return (
    <div>
      <h1>{props.name}</h1>
      <p>{props.age}</p>
    </div>
  );
};

// 分割代入
const Profile = (props) => {
  const { name, age } = props;
  return (
    <div>
      <h1>{name}</h1>
      <p>{age}</p>
    </div>
  );
};

// 引数で分割代入
const Profile = ({ name, age }) => {
  return (
    <div>
      <h1>{name}</h1>
      <p>{age}</p>
    </div>
  );
};
```

### 4-6 State

##### useStateの更新関数内で関数？？
set関数を呼ぶ処理を2行続けて書いて動作させると違いがわかる。

```javascript
// 厳密に正しくない
setNum(num + 1);

// 関数内で関数を指定
setNum((prev) => prev + 1);
```

### 4-7 再レンダリングと副作用

#### 再レンダリング
Stateが更新された時に関数コンポーネントは再び頭から処理が実行される。
差分があるDOMを検知し、変更を反映して画面を表示している。
「変更を検知してコンポーネントを再処理」することを再レンダリングと呼ぶ。

初回レンダリング（コンポーネントのマウント）時と再レンダリング時は異なり、
useStateのカッコで設定する初期値はマウント時だけなので毎回初期化されることはない。

#### 副作用とuseEffect
useEffectの第2引数に[]を設定すると、「コンポーネントを表示した初回のみ実行するような処理」を記述できる。
画面を表示して初期データを取得する時などによく使用される。

Stateの数が多くなってくると再レンダリングの回数も増えてきて、
「再レンダリングの度にこの処理を実行するのはコスト（時間）が無駄にかかるからこの値が変わった時だけにしたいな」
という場面で役立つ。


## 5 ReactとCSS

### 5-2 CSS Modules
React開発の場合はコンポーネント毎にCSSファイルを用意することが多い。

#### CSS Modulesの使用
ファイル名は、「ファイル名.module.scss」という名称にする必要がある。

##### CssModules.modules.scss
```scss
.container {
  background-color: #f0f0f0;
}
.title {
  font-size: 20px;
}
```

##### CssModules.jsx
```javascript
import styles from "./CssModules.module.scss";

export const CssModules = () => {
  return (
    <div className={styles.container}>
      <p className={styles.title}>- CSS Modules -</p>
    </div>
  );
};
```

### 5-3 Styled JSX
CSS-in-JSと呼ばれる、コンポーネントファイルにCSSの記述をしていくライブラリ。
Styled JSXは積極的に採用しているチームはあまり見かけない。
SCSS記法は使用できない。使用する場合は、別途ライブラリのインストールと設定が必要になる。

#### Styled JSXの使用

##### StyledJsx.jsx
```javascript
export const StyledJsx = () => {
  return (
    <>
      <div className={styles.container}>
        <p className={styles.title}>- CSS Modules -</p>
      </div>

      <style jsx>{`
        .container {
          background-color: #f0f0f0;
        }
        .title {
          font-size: 20px;
        }
      `}</style>
    </>
  );
};
```

### 5-4 styled components
根強い人気を誇るライブラリ。

#### styled componentsの使用
```javascript
import styled from "styled-components";

export const StyledComponents = () => {
  return (
    <SContainer>
      <STitle>- Styled Components -</STitle>
    </SContainer>
  );
};

const SContainer = styled.div`
  background-color: #f0f0f0;
`;
const STitle = styled.p`
  font-size: 20px;
`;
```

先頭に大文字のSを付与しているのは、あとから見た時に「styled componentsで作成したコンポーネントなのか、
それ以外の外部ライブラリや他のコンポーネントなのか」が一目でわかるようにするため。

プロジェクトによって命名規則のルール等を設けてチームメンバー間で共通認識を持っておくと良い。
styled componentsの場合はSCSS記法がそのまま使えるので既存のCSSファイルを使用したシステムからCSS-in-JSへの移行も
比較的スムーズに行うことができるのがメリット。

### 5-5 Emotion
styled componentsと並び根強い人気を誇るCSS-in-JSライブラリ。
これまでに紹介してきた以下の全てに似たような書き方が用意されている。

- Inline Styles
- Styled JSX
- styled components

### 5-6 Tailwind CSS
近年非常に人気。ユーティリティファーストなフレームワーク。

#### Tailwind CSSの使用
慣れてしまえばスピードが出るのでCSSをガッツリ書くデザイナーさんがいないようなチームでは選択肢の１つになる。
Tailwind CSSのメリットは、「命名に悩まなくて良い」ということ。

##### コンポーネントは１から作らない？？？
実際の現場でもホントに０からスタイリングすることは少なくて、
大体コンポーネントライブラリを使ったりする。

- Tailwind製のHeadless UI
- Chakra UI
- Material-UI
- Semantic UI


## 6 再レンダリングの仕組みと最適化

### 6-1 再レンダリングが起きる条件
「今どのパターンの再レンダリングに対して最適化をしようとしているか」を意識しながら取り組むようにする。

#### 再レンダリングが起きる３つのパターン

1. Stateが更新された時
2. Propsが変更された時
3. 親コンポーネントが再レンダリングされた時

### 6-2 レンダリング最適化１

#### React.memo
コンポーネント、変数、関数などの再レンダリング時の制御をするにはメモ化を行う。
メモ化とは、前回の処理結果を保持しておくことで処理を高速化する技術。

```javascript
const Component = memo(() => {});
```

Propsに変更がない限り再レンダリングされない。

### 6-3 レンダリング最適化２

#### React.useCallback
関数をPropsに渡す時にコンポーネントをメモ化していても再レンダリングされてしまう原因は関数の再作成。
以下のような関数をPropsで渡していると、再レンダリングの際にコードが実行され、新しい関数が作成されている。

```javascript
const onClickReset = () => {
  setNum(0);
};
```

関数のメモ化。

```javascript
const onClickReset = useCallback(() => {
  setNum(0);
}, []);
```

依存配列は空なので関数は最初に作成されたものが使い回される。

### 6-4 変数のmemo化

#### React.useMemo

```javascript
const sum = useMemo(() => {
  return 1 + 3;
}, []);
```

変数設定のロジックが複雑だったり、膨大な数のループが実行される場合等に
使用することで変数設定による負荷を下げることが可能。


## 7 グローバルなState管理

### 7-1 グローバルなState管理が必要な理由

#### Propsのバケツリレー
バケツリレー式の弊害

1. コードが複雑化する
  - 「何をするためのコンポーネントなのか」が分かりづらくなる
1. 他の場所で再利用できないコンポーネントになってしまう
1. 本来再レンダリングが必要ないにもかかわらずState更新時に全て再レンダリングしてしまう

適切にStateやPropsの設計を行うことは非常に重要。

### 7-2 ContextでのState管理

#### ContextでのグローバルStateの基本的な使い方
1. Contextの器を作成する
1. グローバルStateを扱いたいコンポーネントを囲む
1. useContextを使う

##### AdminFlagProvider.jsx
```javascript
import { createContext } from "react";

export const AdminFlagContext = createContext();

export const AdminFlagProvider = (props) => {
  const { children } = props;
  const [isAdmin, setIsAdmin] = useState(false);

  return (
    <AdminFlagContext.Provider value={{ isAdmin, setIsAdmin }}>
      {children}
    </AdminFlagContext.Provider>
  );
};
```

##### どんな時にグローバル管理するの？？
ログインしているユーザの情報など。

#### 再レンダリングに注意
１つのContextオブジェクトの値が何か更新されたときは、
useContextでそのContextを参照しているコンポーネントは全て再レンダリングされる。
１つのContextに属性の異なるいろんなStateを詰め込むのは避ける必要がある。

### 7-3 その他のグローバルStateを扱う方法

#### Recoil
今後間違いなく主流になってくる。

##### Recoilの概念
導入と実装のハードルが低い。

#### Apollo Client
GraphQL APIをクライアント側で効率良く操作するためのライブラリ。

##### Reactive variables
APIの取得結果のキャッシュとは別で任意に作成できるデータストア。
比較的シンプルに実装することができる。

##### ApolloClientの現状
GraphQL APIのクライアントとしてApollo Clientを使用している場合に、
グローバルなStateを管理していきたい場合はApollo Clientが提供している機能を使うのが良い。


## 8 ReactとTS

### 8-1 TSの基本

#### 設定ファイル（tsconfig）

##### module
フロントエンドで使用する際はmoduleにesnextを指定する。
バックエンドで使用する場合はmoduleにcommonjsを指定する。

### 8-4 型定義の管理方法
型定義のimport時は忘れずにtype（`import type { ~ } from`）を使用する。

### 8-5 コンポーネントの型定義
JSXを返却していないとエラーにできたり、コンポーネント独自の設定ができたりするようになるので、
関数コンポーネントにはFCやVFCを指定する。

### 8-6 省略可能な型の定義

##### defaultProps
propsのデフォルト値を設定することができる。

```typescript
export const ListItem: FC<User> = (props) => {
  const { user, personalColor } = props;
  return (
      <p style={{ color: personalColor }}>{user.name}</p>
  );
};

ListItem.defaultProps = {
  personalColor: "blue",
};
```


## 9 カスタムフック

### 9-1 カスタムフックとは

#### カスタムフックの概要
カスタムフックファイルの中でも各種Hooksを使用することができる。
この点以外は、一般的な関数と同じ。

#### カスタムフックの必要性
本来コンポーネントの責務は与えられたデータに基づいて画面の見た目を構築すること。
複雑なロジックは分離してあげるほうがよい。

### 9-2 カスタムフックの実装
カスタムフックを適切に使用していくことで可読性・保守性の高いReact開発を行うことが可能になる。

##### useMemoList.ts
```typescript
import { useCallback, useState } from "react";

export const useMemoList = () => {
  const [memos, setMemos] = useState<string[]>([]);

  const addTodo = useCallback((text: string) => {
      const newMemos = [...memos];
      newMemos.push(text);
      setMemos(newMemos);
  }, [memos]);
  
    const deleteTodo = useCallback((index: number) => {
      const newMemos = [...memos];
      newMemos.splice(index, 1);
      setMemos(newMemos);
    }, [memos]);

  return { memos, addTodo, deleteTodo };
};
```

##### 開発・リファクタリング手順
1. まずは１つのコンポーネントに実装
1. コンポーネント化できそうな箇所を分解
1. ロジック分離できそうな箇所をカスタムフック化
