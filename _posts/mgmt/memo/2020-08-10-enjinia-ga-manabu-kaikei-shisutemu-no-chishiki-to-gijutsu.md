---
layout:     post
title:      "エンジニアが学ぶ会計システムの知識と技術"
date:       2020-08-10 00:00:00 +0900
categories: mgmt memo
---

![thumbnail](/assets/2020-08-10-enjinia-ga-manabu-kaikei-shisutemu-no-chishiki-to-gijutsu/thumbnail.png)

※本ブログの目的と内容[^1]、著作者の方へ[^2]

[^1]: 本ブログは「本を読み、理解した内容の備忘録（自分用）」を目的としている。重要なアイディアを昇華させ、自分の言葉でまとめるように努めている

[^2]: 内容に不快を感じ、ブログの取り下げを希望される著作者の方は、個別にご連絡いただけると幸いに思う

## サマリー&レビュー
#### 内容
本書を通して、大きく3つの内容を学べる。
- 会計と簿記の基本知識
  - エンジニアとして把握しておくべき網羅的業務知識
- 会計システムの利用
  - いつ、どのように、何の目的で使用されるのか
  - システムのインプットとアウトプットは何か
- 会計システムの開発
  - 要件定義から運用に至るまで、会計固有の観点で網羅的にカバー
  - 手を動かす開発者向けではなく、開発を管理する責任者向けの内容

#### 対象者
- 会計システムの担当となったシステムエンジニア・経理担当

#### 難易度
- 会計と開発に関する内容、それぞれ基本的な内容がしっかりと説明されている
- 無機質な説明が羅列されている感じであるため、受け身でぼんやりと読んでいると途中離脱しかねない

#### 評価
★★★★☆（4/5）
- 会計自体と会計システムの全貌は把握できる（ここの評価は高い）
- 最新の会計システム動向も期待していたが、当然で基本的な（特別最新ではない）内容な上に内容薄め
- 著者の間で内容の連携が取れていないためか、一部でほぼ同じ内容が繰り返されていたため星を一つ減点


## 会計と簿記の基本
### 企業会計原則
企業会計原則には、「企業が会計処理を行う上で従わなければならない会計の指針」が記されている。これ自体に強制力はないが、会社法や金融商品取引法などの法令を通じて法的強制力が付与される。
- 一般原則（企業会計全般に対する包括的な指針）
- 貸借対照表原則（貸借対照表の資産、負債および資本に関する会計処理や表示に関する指針）
- 損益計算書原則（損益計算書の本質、費用および収益の会計処理や表示に関する指針）

#### 発生主義と費用・収益対応の原則
売上計上のタイミングとお金が入ってくるタイミングは同一とは限らず、以下のルールに則り会計処理を行う。
##### 発生主義
費用について、支払いのタイミングとは関係なく、購入したものを使い切った時点や、サービスの提供を受けた時点で認識する。
##### 費用・収益対応の原則
関係性のある収益と費用は対応させ、同一の会計期間で計上する。

### 会計の種類
会計は4種類存在する。それぞれ目的と提示対照が異なり、提出するデータや算出方法が異なる。

|分類|項目|概要|
|:--|:--|:--|
|財務会計|金融商品取引法会計|投資家の保護が目的<br>株主総会等へ提出<br>すべての会社が対象|
|財務会計|会社法会計|株主と債権者の保護が目的<br>内閣総理大臣へ提出<br>主に上場企業が対象|
|財務会計|税法会計|会社の課税所得の計算が目的|
|管理会計|管理会計|経営者が意思決定・経営管理を適切に行うために構築する内部会計|

*税法会計では、財務会計で算出された会計上の税引前当期純利益に、必要な調整（財務調整）を行うことで課税所得を算出する

### 決算サイクル
四半期決算制度が導入されて以来、経理部門は**1年中決算**をしている状態といわれる。経理部門において**基本となる業務サイクルは月次決算**である。
![financial-cycle](/assets/2020-08-10-enjinia-ga-manabu-kaikei-shisutemu-no-chishiki-to-gijutsu/financial-cycle.png)
年度末決算などにおいて、帳票の出力タイミングで年初分から集計していると膨大な時間がかかってしまう。そこで、期中の月別の合計額を保持しておき、必要に応じてそれらを集計している。
##### ワン・イヤー・ルール
会計上で「長期」とは「1年超」を意味する。

### 財務諸表ができるまで
取引発生から財務諸表が作成されるまでのフローを以下に示す。
1. 取引の発生  
↓ 変換
1. 仕訳データ  
↓ 更新・蓄積
1. 総勘定元帳  
↓ 出力
1. 財務諸表

一昔前、仕訳帳から総勘定元帳への「転記」作業は「手作業」で行われていたが、近年ではシステム化されており手作業で行うことはほとんどない。

### キャッシュ・フロー計算書
損益計算書の数値が良くても資金が適切にまわっていなければ、会社は突然しするかもしれない。キャッシュ・フロー計算書により、**血液（資金）が問題なく循環しているか**を確認できる。利益が出ているのにキャッシュ・フローがマイナスになっている場合には注意が必要。

|項目別概要|具体例|
|:--|:--|
|**営業活動によるキャッシュ・フロー**<br>会社の営業力によって、お金を稼ぎ出す力<br>健全な会社であれば、この区分の数値はプラスに成る|モノやサービスの売上による収入<br>モノやサービスの仕入による支出<br>社員の給与などの支出|
|**投資活動によるキャッシュ・フロー**<br>工場の新設などの設備投資や固定資産税の売却など<br>投資なので収入より支出が多くマイナスになる|固定資産、有価証券の売却による収入<br>固定資産、有価証券の購入による支出|
|**財務活動によるキャッシュ・フロー**<br>会社の資金調達に関する諸活動<br>プラスにもマイナスにもなる|株式の発行による収入<br>配当による支出<br>借入金による収入/支出|

#### キャッシュ・フロー計算書の算出方法
直接法と間接法の2種類の算出方法がある。導かれるキャッシュ・フロー自体は同額となるが、開示内容は全く異なる。現在の会計は発生主義を採用しており、キャッシュ・フロー計算書の出力も間接法が主流となっている。
##### 直接法
「現金主義による損益計算書」

$$
\begin{align}
  商品販売収入 &= 期首売掛金残高 + 当期売上高 + 期末売掛金残高 \\\\
  商品仕入支出 &= 期首買掛金残高 + 当期仕入高 + 期末買掛残高
\end{align}
$$

##### 間接法
「発生主義による損益計算書を現金主義に直した書式」

$$
\begin{align}
  当期純利益 &= 当期売上高 - 当期仕入高 \\\\
  売掛金増減額 &= 期首売掛金残高 - 期末売掛金残高 \\\\
  買掛金増減額 &= 期首買掛金残高 - 期末買掛残高
\end{align}
$$

### 単式簿記と複式簿記
単式簿記と複式簿記の違いを以下の表に示す。

|項目|単式簿記|複式簿記|
|:--|:--|:--|
|概要|お金の出入りのみを管理する|**お金の出入りと資産の増減を同時に管理する**|
|記録数|1つの取引に対し、1つの記録|1つの取引に対し、2つの記録|
|分類数|収入・支出|収入（収益、負債、資本）・支出（資産、費用）|
|利用者|個人|会社|

### 仕訳
仕訳の例を以下に示す。日付、摘要、勘定科目、金額を基本情報とし、部門や事業セグメントなど、必要に応じて適宜情報を付与する。付与した情報は各種管理帳票を出力する際に使用される。すべての仕訳は貸借対照表と損益計算書につながる。

![journalizing](/assets/2020-08-10-enjinia-ga-manabu-kaikei-shisutemu-no-chishiki-to-gijutsu/journalizing.png)
*一般的に資産・負債には部門を付けない
原因（減ったモノ）が右側（貸方）に記載され、結果（増えたモノ）が左側（借方）に記載される。

### 勘定科目コード体系
勘定科目コード体系の例を以下に示す。仕訳の勘定科目には、これらの内のどれかを割り当てる。勘定科目は、貸借対照表に対応した勘定科目と、損益計算書に対応した勘定科目からなる。

![account-code](/assets/2020-08-10-enjinia-ga-manabu-kaikei-shisutemu-no-chishiki-to-gijutsu/account-code.png)


## 会計システムと帳簿・帳票
### 基幹システム
基幹システムとは「**売買、購買、生産、経理などの企業活動を支えるシステム郡**」のことを指す。基幹システムを構成する業務システムの範囲は、業種・業態や企業の規模により異なる。
#### 基幹システム一覧
以下に基幹システムの一覧を示す。これらのシステムは[会計システム鳥瞰図](#会計システム鳥瞰図)にも登場する。

|システム名|概要|
|:--|:--|
|購買管理システム|仕入先への発注を登録し、その発注に基づき、原材料や商品を研修して仕入計上を行うプロセスを管理する|
|生産管理システム|生産活動に関するプロセスを管理する|
|販売管理システム|顧客からの受注を登録し、その受注に基づき、商品や製品を出荷、納品し、売上計上を行うプロセスを管理する|
|在庫管理システム|製品の生産に使用する原材料、工場で生産された製品、外部から仕入れて販売する商品などに関する増減および残高にかかるプロセスを管理する|
|人事管理システム|従業員に関する業務プロセスを管理する|
|債務管理システム|仕入先からの請求書の受領、支払、残高状況などを管理する|
|債権管理システム|得意先に対する売上代金の請求書の発行、入金による消滅、残高や滞留の状況などを管理する|
|原価管理システム|製品の製造原価を計算する|
|総勘定元帳システム|企業の各種取引活動を記録し、決算書や各種会計帳簿を作成する|

#### 会計システム鳥瞰図
<embed src="/assets/2020-08-10-enjinia-ga-manabu-kaikei-shisutemu-no-chishiki-to-gijutsu/accounting-system_birds‐eye-view.pdf" type="application/pdf" height="400"/>
*財務諸表バージョンとは、会社法会計、金融商品取引法会計、税法会計など、財務諸表の目的に応じた勘定科目の集計ロジックがマスタとして登録されものであり、勘定項目マスタとは別物である
##### 仕訳例

|トランザクション|借方|貸方|
|:--|:--|:--|
|②仕入|原材料 10,000円<br>仮払消費税 1,000円|買掛金 11,000円|
|⑤作業報告|仕掛品 10,000円|労務費 10,000円|
|⑥完成報告|製品 10,000円|仕掛品 9,000円<br>原価差異 1,000円|
|⑧出荷|売上原価 10,000円|製品 10,000円|
|⑨売上計上|売掛金 16,500円|売上高 15,000円<br>仮受消費税 15,00円|
|⑪出庫|仕掛品 10,000円|原材料 10,000円|
|⑬支払|買掛金 10,000円|普通預金 10,000円|
|⑭支払|旅費交通費 10,000円<br>仮払消費税 1,000円|普通預金 11,000円|
|⑯入金消込|普通預金 10,000円|売掛金 10,000円|

[会計システム鳥瞰図](#会計システム鳥瞰図)に登場する仕訳の一部の例を以上に示す。

### 帳簿・帳票
#### 帳簿・帳票の種類
会社で扱う帳簿・帳票は4種類に大別される。

|種類|概要|
|:--|:--|
|財務諸表|自社の経営や財務の状況を説明・報告するための書類|
|会計帳簿|財務諸表作成の基礎となった情報の帳票。会計帳簿は一定期間、紙媒体や電子媒体で保管する義務がある|
|管理帳票|会計帳簿以外の各種帳票<br>財務諸表の作成時における入力内容の確認や経緯の確認などに使用する帳票<br>管理会計として社内の業務管理や経費管理のための帳票<br>|
|税務用帳票|法人税や消費税の税務申告に必要な情報を集計した帳票|

#### 各種帳簿・帳票
以下に各種帳簿・帳票を示す。これらの帳簿・帳票は、[会計システム鳥瞰図](#会計システム鳥瞰図)においても会計システムより出力されている。

|帳簿・帳票名|分類|概要|
|:--|:--|:--|
|貸借対照表|財務諸表|一定時点における財政状態|
|損益計算書|財務諸表|一定期間における企業の経営成績|
|キャッシュ・フロー計算書|財務諸表|一定期間におけるキャッシュの流れ|
|仕訳帳|会計帳簿|会計システムのインプットデータである「仕訳」の一覧表|
|総勘定元帳|会計帳簿|勘定科目別の残高およびその増減内容を表した帳票|
|残高試算表|管理帳票|勘定科目別の残高を一覧表示。月次、四半期、会計年度末など、期間を指定可能|
|月次推移表|管理帳票|勘定科目別の残高を月別に一覧表示。単月表示と累計表示が選択可能|
|部門別一覧表|管理帳票|経費や損益を部門別に一覧表|
|セグメント別一覧表|管理帳票|勘定科目別の残高を事業セグメント別に一覧表示|
|プロジェクト元帳|管理帳票|収益や費用をプロジェクト別に一覧表|
|取引先別一覧表|管理帳票|勘定科目別の残高を取引先別に一覧表示|
|消費税一覧|-|課税区分別の課税基準額と税額の一覧表。勘定科目と各課税区分ごとの課税基準額と税額が並ぶ|

#### 連結財務諸表
連結財務諸表とは、**企業グループ内の各社の貸借対照表、損益計算書、キャッシュ・フロー計算書などを合算した企業グループ全体の財務諸表**のこと。連結財務諸表の作成には、「相殺消去」（グループ間取引の消去）が必要。ただ単純に合算すると、売上げや仕入、売掛金や買掛金が両建てで膨れ上がってしまう。セグメント別一覧表と取引先別一覧表により相殺消去を行う。


## 会計システム開発
### 開発手法
クネビンフレームワークにより課題を分類し、その結果に応じて開発手法を決定すると良い。「単純系」と「困難系」はウォーターフォール型が適していて、「複雑系」と「カオス系」はアジャイル型が適している。
#### クネビンフレームワーク
課題の状況に応じて分類する。

|項目名|課題の概要|
|:--|:--|
|単純系|誰が見ても理解でき、既存のベストプラクティスを適用すればよいもの|
|困難系|専門知識が必要で、問題の分析によって計画的なプロジェクト化が可能|
|複雑系|問題分析だけでは理解不可能で、反復動作を繰り返す必要があるもの|
|カオス系|対照を理解することすら難しく、常に確認する必要があるもの|

### スクラッチ開発とパッケージ導入
#### 会計システムは「作る」べきか、「買う」べきか
> システムで実現する機能自体が商品やサービスの**差別化**につながり、**競争力の源泉**となり、作り込みに要する費用を上回る収益が十分見込まれる場合には、システムは「作る」戦略をとるのが正しい
> **競争領域でない**機能をシステムで実現する場合、外部からのノウハウや協調的な取組みによって開発コストを抑え、システムによる効率化を目指す場合には、「買う」戦略をとるのが正しい
> 会計システムについては、その機能によって会社の差別化につながるものでなく、システムによって**業務の効率化**を目指すものであるため、「買う」選択肢をとることが正しい

#### パッケージ導入時の注意点
「探す」という作業がパッケージ導入において重要である。よく「業務をパッケージに合わせる」ことがパッケージ導入のポイントといわれるが、合うものがなければ利用者は困ってしまう。そのため「合わせる」よりも、どちらかというと「探しに行く」（情報収集を行う）というイメージに近い。

### 開発計画
一般的にシステム構築の成功可否は「QCD（品質、コスト、納期）」によって評価される。3条件をすべて満たす成功プロジェクトは52.8%程度しかない。定常業務と異なり、「経験したことのないことを実行するため」に成功率が低下する。計画を作ること自体が大変なのである。プロジェクトで一番大きなリスクは「そういうことはない」と思いこむこと。
#### 課題管理のプロセス
課題の管理プロセスを以下に示す。
1. 課題を発見する
1. 課題を共有する（課題の「見える化」を行う）
1. 課題を合意し、優先順位づけを行う
1. 課題解決の担当者と期限を決める
1. 課題の状態を把握する（経過と結果を記録）

### 本番稼働のステップ
開発完了から本番稼働までのステップを以下に示す。
1. ユーザ受入れテスト
1. 並行稼動
1. 稼働可否判定
1. マスタ移行
1. 稼働開始
1. 残高データ移行

##### ユーザー受入れテスト
ユーザーの要求事項が新システムできちんと実現されているかをユーザー自身に確認してもうら。
##### 並行稼動
並行稼働は、旧システムと同じ運用をテスト環境（新システムと同じ設定をした稼働環境）で実施し、その結果と旧システムにおける結果との比較によって、新会計システムそのものの信頼性や新会計システムによる運用の信頼性を確認する。並行稼働は2-3ヶ月が妥当。


## 新技術と会計業務
会計業務への新技術適用領域を以下に示す。

|新技術|記録|仕訳|出力|
|:--|:--|:--|:--|
|RPA|o|-|-|
|AI|o|o|-|
|オープンAPI|o|-|o|

#### PRA (Robotic Process Automation)
人間の単純作業をコンピュータで再現し、代替させる。導入の容易性から近年導入が進んでいる。会計業務の中では入力作業に有用で、自動化させたい操作をRPAに記録させるだけで作成できる。実行方法には、「PC上での実行」と「サーバ上での実行」がある。

#### AI (Artificial Intelligence)
##### AI-OCR
取引入力の際の紙の伝票を読み込み、自動的に仕訳に必要なデータを抽出する。従来のOCRにAI機能を持たせたもので、AIによって非定型の帳票からでも必要なデータを抽出したり、手書きの徴用から文字を認識したいり、データを抽出することができる。
##### 自動仕訳
クレジットカードなどの明細データを連携する際、データを取り込むだけでなく、内容を判別して勘定科目を提案し、自動仕訳を行う。
##### チェックの効率化・正確性
決済時のチェックや監査をAIにより自動化する。決済時に過去との変動率が大きいといった際を発見し、修正の必要がありそうな仕訳を自動で探してアラートとして表示する。
##### 会計データの応用
- 経営データを分析して経営課題を抽出する経営特化型AI、企業データと会計データを組み合わせて融資の可否を自動判断するAI等が存在する。

#### オープンAPI
オープンAPIとは、「外部企業からアクセス可能な状態にされたAPI」のことである。セキュリティ面で「顧客情報などの社外流出」といった懸念がある。
##### 金融機関と会計システムの連携
金融機関口座の利用明細を会計システムに取り込むことで自動仕訳を行う。
##### その他外部システムと会計システムの連携
交通系ICカードやキャッシュレス事業者のアプリとAPIで連携することにより、経費精算および経費管理業務を効率化する。

#### XBRL (eXtensible Business Reporting Language)
企業が開示する財務諸表を中心とした各種財務データを各企業が共通の言語で作成することにより、集計や加工を容易にする。XML (eXtensible Markup Language) がベースである。以前は紙媒体の財務諸表から転記していたが、XBRLによりデータ抽出が用意となる。
##### タクソノミ
財務諸表の雛形。勘定科目の分類を定義したもの。
##### EDINET (Electronic Disclosure for Inverstors' NETwork)
有価証券報告書（XBRL形式）をインターネットを通じて閲覧できる。
