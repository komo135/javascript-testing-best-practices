# JavaScriptテストのベストプラクティス — 日本語版

[英語原文](readme-en.md) · [翻訳元のリポジトリ](https://github.com/goldbergyoni/javascript-testing-best-practices)

Yoni Goldbergらによるガイドの日本語訳です。翻訳元は[コミット `63a2bb0` のREADME](https://github.com/goldbergyoni/javascript-testing-best-practices/blob/63a2bb07bb718d0a34a9c1249ef0df9b1266dad8/readme.md)です。

---

<img src="/assets/jtbp-header-blue.png" width="1920px" alt="JavaScript テストのベストプラクティス"/>


<br/>

# 👇 このガイドでテストのスキルを一段引き上げる

<br/>

## 📗 50以上のベストプラクティスを徹底的に網羅

JavaScript と Node.js の信頼性を高めるための、基礎から応用までを扱うガイドです。数多くの優れたブログ記事、書籍、ツールを厳選し、その要点をまとめています。

## 🚢 基礎のはるか先まで踏み込む高度な内容

基礎を大きく越えて、本番環境でのテスト、ミューテーションテスト、プロパティベーステストなど、高度なトピックや実務で役立つ戦略・ツールを学びましょう。このガイドを隅々まで読めば、テストのスキルを大きく伸ばせるはずです。

## 🌐 フロントエンド、バックエンド、CIまでフルスタックに対応

まずは、アプリケーションのどの層でも基盤となる、共通のテストプラクティスを理解しましょう。その後はフロントエンド・UI、バックエンド、CIのうち、関心のある分野を深掘りしてください。もちろん、すべてを学んでもかまいません。

<br/>

### 著者：Yoni Goldberg — JavaScript・Node.js コンサルタント

<a id="course-announcement"></a>

### 👨‍🏫 著者からのお知らせ：2年間の収録と編集を経て、テストを徹底的に学べる講座を公開しました。[🎁 公開記念の特別価格は残り48時間未満です](https://testjavascript.com/)

<br/>

### 各言語の翻訳

- 🇨🇳[中国語（簡体字）](readme-zh-CN.md) — 翻訳：[Yves yao](https://github.com/yvesyao)
- 🇰🇷[韓国語](readme.kr.md) — 翻訳：[Rain Byun](https://github.com/ragubyun)
- 🇵🇱[ポーランド語](readme-pl.md) — 翻訳：[Michal Biesiada](https://github.com/mbiesiad)
- 🇪🇸[スペイン語](readme-es.md) — 翻訳：[Miguel G. Sanguino](https://github.com/sanguino)
- 🇧🇷[ポルトガル語（ブラジル）](readme-pt-br.md) — 翻訳：[Iago Angelim Costa Cavalcante](https://github.com/iagocavalcante)、[Douglas Mariano Valero](https://github.com/DouglasMV)、[koooge](https://github.com/koooge)
- 🇫🇷[フランス語](readme-fr.md) — 翻訳：[Mathilde El Mouktafi](https://github.com/mel-mouk)
- 🇯🇵[日本語（ドラフト）](https://github.com/yuichkun/javascript-testing-best-practices/blob/master/readme-jp.md) — 翻訳：[Yuichi Yogo](https://github.com/yuichkun)、[ryo](https://github.com/kawamataryo)
- 🇹🇼[中国語（繁体字）](readme-zh-TW.md) — 翻訳：[Yubin Hsu](https://github.com/yubinTW)
- 🇺🇦[ウクライナ語](readme-ua.md) — 翻訳：[Serhii Shramko](https://github.com/Shramkoweb)
- 🇮🇷[ペルシャ語](readme-pr-fr.md) — 翻訳：[Ali Azmoodeh](https://github.com/TREER00T)
- 🇷🇺[ロシア語](readme-ru.md) — 翻訳：[Alex Popov](https://github.com/Saimon398)

- ご自身の言語への翻訳を希望する方は、上流リポジトリでIssueを作成してください 💜

<br/><br/>

## 目次

#### [第0章：黄金律](#section-0)

ほかのすべての指針の基礎となる、たった1つの助言（1項目）

#### [第1章：テストの構造](#section-1)

読みやすいテストを組み立てるための基礎（12項目）

#### [第2章：バックエンド](#section-2)

バックエンドとマイクロサービスのテストを効率よく書く（13項目）

#### [第3章：フロントエンド](#section-3)

コンポーネントテストからE2Eテストまで、Web UIのテストを書く（11項目）

#### [第4章：テストの有効性を測る](#section-4)

見張り役を見張る — テストそのものの品質を測る（4項目）

#### [第5章：継続的インテグレーション](#section-5)

JavaScriptにおけるCIの指針（9項目）

<br/><br/>

<a id="section-0"></a>

# 第0章：黄金律

<br/>

## ⚪️ 0 黄金律：無駄がなくシンプルなテストを設計する

:white_check_mark: **推奨：**
テストコードは本番コードとは違います。短く、きわめてシンプルで、構造が平坦で、扱いやすいものにしましょう。テストを見た瞬間に、その意図を理解できることが大切です。

私たちの頭は、本来の仕事である本番コードのことで、すでにいっぱいです。これ以上の複雑さを受け入れる余裕はありません。そこに別のサブシステムを詰め込もうとすると、チームの速度が落ち、テストをする本来の目的に逆行します。実際、ここでテストを諦めてしまうチームは少なくありません。

テストには、別の役割を担える可能性があります。小さな投資で大きな価値をもたらす、親切なアシスタントや副操縦士という役割です。科学では、人間には2つの思考システムがあるとされています。「システム1」は空いた道路で車を運転するような、あまり意識的な努力を必要としない活動に使われます。「システム2」は数学の方程式を解くような、複雑で意識的な作業に使われます。テストはシステム1で扱えるように設計しましょう。テストコードを見るとき、2×(17×24)を計算するような難しさではなく、HTML文書を修正するくらい簡単だと_感じられる_ことが理想です。

そのためには、費用対効果と投資収益率（ROI）の高い手法、ツール、テスト対象を選び抜きます。必要な分だけテストし、軽快さを保つよう努めましょう。場合によっては、一部のテストを減らし、信頼性と引き換えに機動性やシンプルさを得ることにも価値があります。

![複雑さをこれ以上抱え込む余裕はない](/assets/headspace.png "複雑さをこれ以上抱え込む余裕はない")

以下の助言の大半は、この原則から導かれています。

### それでは始めましょう

<br/><br/>

<a id="section-1"></a>

# 第1章：テストの構造

<br/>

## ⚪️ 1.1 テスト名に3つの要素を含める

:white_check_mark: **推奨：** テストレポートは、コードに詳しくない人にも、現在のアプリケーションの変更が要件を満たしているかどうかを伝える必要があります。読むのはテスターやデプロイを担当するDevOpsエンジニア、そして2年後の自分かもしれません。そのためには、テストを要件の言葉で記述し、次の3つの要素を含めるのが効果的です。

(1) 何をテストするのか。例：ProductsService.addNewProductメソッド。

(2) どのような条件・シナリオなのか。例：メソッドに価格が渡されていない場合。

(3) 期待する結果は何か。例：新しい商品は承認されない。

<br/>

❌ **守らないと：** デプロイが失敗し、「商品を追加する」というテストが落ちました。これだけで、何が正しく動いていないのか具体的にわかるでしょうか。

<br/>

**👇 補足：** 各項目にはコード例があり、図解が付いているものもあります。クリックすると展開できます。
<br/>

<details><summary>✏ <b>コード例</b></summary>
  
<br/>
  
### :clap: 良い例：3つの要素を含むテスト名

![Mochaを使った例](https://img.shields.io/badge/🔨%20Example%20using%20Mocha-blue.svg "Mochaを使った例")

```javascript
//1. unit under test
describe('Products Service', function() {
  describe('Add new product', function() {
    //2. scenario and 3. expectation
    it('When no price is specified, then the product status is pending approval', ()=> {
      const newProduct = new ProductService().add(...);
      expect(newProduct.status).to.equal('pendingApproval');
    });
  });
});

```

<br/>

### :clap: 良い例：3つの要素を含むテスト名

![3つの要素を含むテスト名](/assets/bp-1-3-parts.jpeg "3つの要素を含むテスト名")

</details>

<br/>
<details><summary>© <b>出典・参考資料</b></summary>
  1. <a href='https://osherove.com/blog/2005/4/3/naming-standards-for-unit-tests.html'>Roy Osherove — ユニットテストの命名規則</a>
</details>

<br/><br/>

## ⚪️ 1.2 AAAパターンでテストを構成する

:white_check_mark: **推奨：** Arrange（準備）、Act（実行）、Assert（検証）の3つの部分を明確に分けてテストを構成しましょう。頭文字を取ってAAAと呼びます。この構造に従えば、読み手はテストの段取りを理解するために頭を悩ませずに済みます。

1つ目のA — Arrange：テストしたいシナリオを再現するための準備をすべて行います。テスト対象のインスタンス生成、DBレコードの追加、オブジェクトのモックやスタブの設定などが含まれます。

2つ目のA — Act：テスト対象を実行します。通常は1行です。

3つ目のA — Assert：得られた値が期待を満たすことを確認します。通常は1行です。

<br/>

❌ **守らないと：** 本番コードの理解に何時間も使ったうえに、その日の仕事で最も簡単なはずのテストでも、頭を酷使することになります。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：AAAパターンで構成したテスト

![Jestを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Jestを使った例") ![Mochaを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Mochaを使った例")

```javascript
describe("Customer classifier", () => {
  test("When customer spent more than 500$, should be classified as premium", () => {
    //Arrange
    const customerToClassify = { spent: 505, joined: new Date(), id: 1 };
    const DBStub = sinon.stub(dataAccess, "getCustomer").reply({ id: 1, classification: "regular" });

    //Act
    const receivedClassification = customerClassifier.classifyCustomer(customerToClassify);

    //Assert
    expect(receivedClassification).toMatch("premium");
  });
});
```

<br/>

### :thumbsdown: アンチパターン：区切りのない一塊のコードは意図を読み取りにくい

```javascript
test("Should be classified as premium", () => {
  const customerToClassify = { spent: 505, joined: new Date(), id: 1 };
  const DBStub = sinon.stub(dataAccess, "getCustomer").reply({ id: 1, classification: "regular" });
  const receivedClassification = customerClassifier.classifyCustomer(customerToClassify);
  expect(receivedClassification).toMatch("premium");
});
```

</details>

<br/><br/>

## ⚪️ 1.3 プロダクトの言葉で期待を記述する：BDDスタイルのアサーションを使う

:white_check_mark: **推奨：** 宣言的なスタイルでテストを書けば、読み手はほとんど頭を使わずに意図をつかめます。条件分岐だらけの命令的なコードでは、そのぶん理解に負担がかかります。独自の判定コードを書くのではなく、`expect`や`should`を使い、人間の言葉に近い宣言的なBDDスタイルで期待を表現しましょう。ChaiやJestに目的のアサーションがなく、それを繰り返し使うのであれば、[Jestのマッチャーの拡張](https://jestjs.io/docs/en/expect#expectextendmatchers)や[独自のChaiプラグイン](https://www.chaijs.com/guide/plugins/)を検討してください。
<br/>

❌ **守らないと：** チームが書くテストは減り、面倒なテストには`.skip()`が付けられるようになります。

<br/>

<details><summary>✏ <b>コード例</b></summary><br/>

![Mocha & Chaiを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Mocha & Chaiを使った例") ![Jestを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Jestを使った例")

### :thumbsdown: アンチパターン：テストの意図を知るだけで、長めの命令的なコードを読み解く必要がある

```javascript
test("When asking for an admin, ensure only ordered admins in results", () => {
  //assuming we've added here two admins "admin1", "admin2" and "user1"
  const allAdmins = getUsers({ adminOnly: true });

  let admin1Found,
    adming2Found = false;

  allAdmins.forEach(aSingleUser => {
    if (aSingleUser === "user1") {
      assert.notEqual(aSingleUser, "user1", "A user was found and not admin");
    }
    if (aSingleUser === "admin1") {
      admin1Found = true;
    }
    if (aSingleUser === "admin2") {
      admin2Found = true;
    }
  });

  if (!admin1Found || !admin2Found) {
    throw new Error("Not all admins were returned");
  }
});
```

<br/>

### :clap: 良い例：宣言的なテストなら、ひと目で意図をつかめる

```javascript
it("When asking for an admin, ensure only ordered admins in results", () => {
  //assuming we've added here two admins
  const allAdmins = getUsers({ adminOnly: true });

  expect(allAdmins)
    .to.include.ordered.members(["admin1", "admin2"])
    .but.not.include.ordered.members(["user1"]);
});
```

</details>

<br/><br/>

<a id="practice-1-4"></a>

## ⚪️ 1.4 ブラックボックステストに徹する：公開メソッドだけをテストする

:white_check_mark: **推奨：** 内部実装のテストは、大きな負担のわりに得るものがほとんどありません。コードやAPIが正しい結果を返しているのに、内部で「どう」動いたかのテストにさらに3時間を費やし、壊れやすいテストを保守する必要があるでしょうか。公開された振る舞いを確認すれば、非公開の実装も間接的にテストされます。テストが失敗するのは、出力が間違っているなど、実際に問題がある場合だけです。この方法は`振る舞いのテスト（behavioral testing）`とも呼ばれます。一方、内部実装を調べるホワイトボックス方式では、コンポーネントが生む結果から細かな実装へと関心が移ります。結果が正しくても小さなリファクタリングでテストが壊れ、保守の負担が大幅に増えてしまいます。
<br/>

❌ **守らないと：** テストは[オオカミ少年](https://en.wikipedia.org/wiki/The_Boy_Who_Cried_Wolf)のように、誤った警報を出すようになります。たとえば非公開変数の名前を変えただけでテストが失敗します。やがてCIの通知が無視されるようになり、いつか本物のバグまで見過ごされてしまいます。

<br/>
<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：正当な理由もなく内部実装をテストする

![Mocha & Chaiを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Mocha & Chaiを使った例")

```javascript
class ProductService {
  //this method is only used internally
  //Change this name will make the tests fail
  calculateVATAdd(priceWithoutVAT) {
    return { finalPrice: priceWithoutVAT * 1.2 };
    //Change the result format or key name above will make the tests fail
  }
  //public method
  getPrice(productId) {
    const desiredProduct = DB.getProduct(productId);
    const finalPrice = this.calculateVATAdd(desiredProduct.price).finalPrice;
    return finalPrice;
  }
}

it("White-box test: When the internal methods get 0 vat, it return 0 response", async () => {
  //There's no requirement to allow users to calculate the VAT, only show the final price. Nevertheless we falsely insist here to test the class internals
  expect(new ProductService().calculateVATAdd(0).finalPrice).to.equal(0);
});
```

</details>

<br/><br/>

## ⚪️ 1.5 適切なテストダブルを選ぶ：モックよりスタブとスパイを優先する

:white_check_mark: **推奨：** テストダブルはアプリケーションの内部実装と結び付くため、必要悪といえます。それでも大きな価値をもたらすものもあります（[モック・スタブ・スパイの違いについての解説](https://martinfowler.com/articles/mocksArentStubs.html)）。

テストダブルを使う前に、簡単な問いを自分に投げかけましょう。「これは要件書に書かれている、または書かれうる機能をテストするためのものか」。そうでなければ、ホワイトボックステストに陥っている兆候です。

たとえば、決済サービスが停止しているときにアプリケーションが適切に振る舞うことを確認したいなら、決済サービスをスタブに置き換えて「応答なし」の状態を作り、テスト対象が正しい値を返すことを確かめます。これは特定の状況におけるアプリケーションの振る舞い・応答・結果の確認です。サービス停止時にメールが送信されることをスパイで検証してもよいでしょう。これも「決済を保存できなければメールを送る」という、要件書に登場しそうな振る舞いの確認です。逆に、決済サービスをモックに置き換え、正しいJavaScriptの型で呼ばれたかを確認すると、テストはアプリケーションの機能と関係がなく、頻繁に変わりうる内部の事情に焦点を当てることになります。
<br/>

❌ **守らないと：** リファクタリングのたびに、コード中のモックをすべて探して修正しなければなりません。テストは頼れる味方ではなく、負担になってしまいます。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：内部実装に焦点を当てたモック

![Sinonを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Sinon-blue.svg "Sinonを使った例")

```javascript
it("When a valid product is about to be deleted, ensure data access DAL was called once, with the right product and right config", async () => {
  //Assume we already added a product
  const dataAccessMock = sinon.mock(DAL);
  //hmmm BAD: testing the internals is actually our main goal here, not just a side-effect
  dataAccessMock
    .expects("deleteProduct")
    .once()
    .withArgs(DBConfig, theProductWeJustAdded, true, false);
  new ProductService().deletePrice(theProductWeJustAdded);
  dataAccessMock.verify();
});
```

<br/>

### :clap: 良い例：スパイで要件を検証する。内部実装に触れるのは、そのために避けられない副作用にすぎない

```javascript
it("When a valid product is about to be deleted, ensure an email is sent", async () => {
  //Assume we already added here a product
  const spy = sinon.spy(Emailer.prototype, "sendEmail");
  new ProductService().deletePrice(theProductWeJustAdded);
  //hmmm OK: we deal with internals? Yes, but as a side effect of testing the requirements (sending an email)
  expect(spy.calledOnce).to.be.true;
});
```

</details>

<br/><br/>

## 📗 これらのプラクティスを動画で学びたい方へ

### 著者のオンライン講座 [Testing Node.js & JavaScript From A To Z](https://www.testjavascript.com) をご覧ください

<br/><br/>

<a id="practice-1-6"></a>

## ⚪️ 1.6 「foo」ではなく、実際にありそうな入力データを使う

:white_check_mark: **推奨：** 本番のバグは、特定の予想外の入力によって見つかることがよくあります。テストの入力が現実に近いほど、早期にバグを発見できる可能性が高まります。[Chance](https://github.com/chancejs/chancejs)や[Faker](https://www.npmjs.com/package/faker)などの専用ライブラリを使い、本番データの多様性や形式に似た疑似データを生成しましょう。実在しそうな電話番号、ユーザー名、クレジットカード情報、会社名、さらには「lorem ipsum」の文章まで生成できます。ユニットテストを置き換えるのではなく追加する形で、生成データをランダム化して対象を広く試したり、本番環境の実データを取り込んだりするテストも考えられます。さらに進めたい場合は、次の項目のプロパティベーステストを参照してください。
<br/>

❌ **守らないと：** 「Foo」のような単調な入力では開発中のテストがすべて成功し、誤った安心感を得てしまいます。本番で攻撃者が「@3e2ddsf . ##’ 1 fdsfds . fds432 AAAA」のような厄介な文字列を渡した途端に、失敗するかもしれません。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：非現実的なデータのおかげで成功してしまうテストスイート

![Jestを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Jestを使った例")

```javascript
const addProduct = (name, price) => {
  const productNameRegexNoSpace = /^\S*$/; //no white-space allowed

  if (!productNameRegexNoSpace.test(name)) return false; //this path never reached due to dull input

  //some logic here
  return true;
};

test("Wrong: When adding new product with valid properties, get successful confirmation", async () => {
  //The string "Foo" which is used in all tests never triggers a false result
  const addProductResult = addProduct("Foo", 5);
  expect(addProductResult).toBe(true);
  //Positive-false: the operation succeeded because we never tried with long
  //product name including spaces
});
```

<br/>

### :clap: 良い例：実際にありそうな入力をランダムに生成する

```javascript
it("Better: When adding new valid product, get successful confirmation", async () => {
  const addProductResult = addProduct(faker.commerce.productName(), faker.random.number());
  //Generated random input: {'Sleek Cotton Computer',  85481}
  expect(addProductResult).to.be.true;
  //Test failed, the random input triggered some path we never planned for.
  //We discovered a bug early!
});
```

</details>

<br/><br/>

## ⚪️ 1.7 プロパティベーステストで多くの入力の組み合わせを試す

:white_check_mark: **推奨：** 通常、各テストでは少数の入力例を選びます。[「foo」を使わない](#practice-1-6)という助言に従って現実的な形式にしても、試すのは`method('', true, 1)`や`method("string", false, 0)`など、ごく一部の組み合わせにすぎません。しかし本番では、引数を5つ取るAPIに何千もの組み合わせが渡され、そのうち1つがプロセスを停止させるかもしれません（[ファジング](https://en.wikipedia.org/wiki/Fuzzing)も参照）。1つのテストから異なる入力の組み合わせを1,000通り自動的に送り、どの入力で正しい応答が得られないかを特定できたらどうでしょう。まさにそれを行うのがプロパティベーステストです。テスト対象に可能な入力の組み合わせを幅広く与え、思いがけないバグに出会う機会を増やします。たとえば`addNewProduct(id, name, isDiscount)`というメソッドがあれば、ライブラリは`(1, "iPhone", false)`、`(2, "Galaxy", true)`など、数値・文字列・真偽値のさまざまな組み合わせで呼び出します。[js-verify](https://github.com/jsverify/jsverify)や、より充実したドキュメントを備える[testcheck](https://github.com/leebyron/testcheck-js)を使えば、MochaやJestなど、普段使っているテストランナーで実行できます。追記：Nicolas Dubienから、追加機能があり活発に保守されているように見える[fast-check](https://github.com/dubzzz/fast-check#readme)も勧められました。
<br/>

❌ **守らないと：** 無意識のうちに、正常に動くコードパスだけを通る入力を選びがちです。その結果、バグを見つける手段としてのテストの効果が下がります。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：fast-checkで多くの入力の組み合わせを試す

![Jestを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Jestを使った例")

```javascript
import fc from "fast-check";

describe("Product service", () => {
  describe("Adding new", () => {
    //this will run 100 times with different random properties
    it("Add new product with random yet valid properties, always successful", () =>
      fc.assert(
        fc.property(fc.integer(), fc.string(), (id, name) => {
          expect(addNewProduct(id, name).status).toEqual("approved");
        })
      ));
  });
});
```

</details>

<br/><br/>

## ⚪️ 1.8 スナップショットが必要なら、短くインラインで記述する

:white_check_mark: **推奨：** [スナップショットテスト](https://jestjs.io/docs/en/snapshot-testing)が必要な場合は、3〜7行程度の短く焦点を絞ったスナップショットだけを使いましょう。外部ファイルではなく、テストの中に[インラインスナップショット](https://jestjs.io/docs/en/snapshot-testing#inline-snapshots)として記述します。そうすれば、テストはそれ自体で意図が伝わり、壊れにくくなります。

一方、従来型のスナップショットの解説やツールは、コンポーネントの描画結果のマークアップやAPIのJSON応答などを大きな外部ファイルとして保存し、テストのたびに現在の結果と比較する方法を勧めています。これでは、テストの作者が読んでも検討してもいない1,000行・3,000個の値に、テストが暗黙のうちに結び付いてしまいます。何が問題なのでしょうか。テストが失敗する理由が1,000個もできてしまうことです。1行変わるだけでスナップショットが一致しなくなり、それは空白やコメント、小さなCSS・HTMLの変更のたびに起こりえます。しかもテスト名からは原因を推測できません。単に1,000行が変わっていないかを確認しているだけだからです。さらに、検査も検証もできていない長い文書を「正解」として受け入れることを促してしまいます。どれも、焦点が定まらず、一度に多くを確かめようとする、意図の不明瞭なテストの兆候です。

ただし、長い外部スナップショットが許容できるケースもあります。値を取り除いてフィールドに着目し、データではなくスキーマを検証する場合や、対象の文書がめったに変わらない場合です。
<br/>

❌ **守らないと：** UIテストが失敗しました。コードは正しく見え、画面もきれいに表示されています。何が起きたのでしょう。スナップショットが差分として検出したのは、Markdownに追加された空白1文字だけだった、ということになりかねません。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：目を通していない2,000行のコードにテストを結び付ける

![Jestを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Jestを使った例")

```javascript
it("TestJavaScript.com is renderd correctly", () => {
  //Arrange

  //Act
  const receivedPage = renderer
    .create(<DisplayPage page="http://www.testjavascript.com"> Test JavaScript </DisplayPage>)
    .toJSON();

  //Assert
  expect(receivedPage).toMatchSnapshot();
  //We now implicitly maintain a 2000 lines long document
  //every additional line break or comment - will break this test
});
```

<br/>

### :clap: 良い例：期待する内容が見えていて、焦点が絞られている

```javascript
it("When visiting TestJavaScript.com home page, a menu is displayed", () => {
  //Arrange

  //Act
  const receivedPage = renderer
    .create(<DisplayPage page="http://www.testjavascript.com"> Test JavaScript </DisplayPage>)
    .toJSON();

  //Assert

  const menu = receivedPage.content.menu;
  expect(menu).toMatchInlineSnapshot(`
<ul>
<li>Home</li>
<li> About </li>
<li> Contact </li>
</ul>
`);
});
```

</details>

<br/><br/>

## ⚪️ 1.9 コードを複製するなら、必要な部分だけにする

:white_check_mark: **推奨：** テストの結果に影響する情報はすべて含め、それ以外は含めないようにしましょう。たとえば、入力用に100行のJSONを組み立てるテストを考えます。毎回そのまま貼り付けるのは大変です。一方、すべてを外部の`transferFactory.getJSON()`に移すと、テストの意味が曖昧になります。データが見えなければ、「なぜステータス400を返すはずなのか」といった、結果と原因の関係がわかりにくいからです。名著『xUnit Test Patterns』では、これを「ミステリーゲスト」と呼びます。見えない何かが結果に影響しているのに、その正体がわからない状態です。繰り返し登場する長い部分は外に出しつつ、テストに重要な情報は明示すれば改善できます。先ほどの例なら、`transferFactory.getJSON({sender: undefined})`と引数を渡して重要な点を強調します。これなら読み手は、senderフィールドが空であるために、バリデーションエラーなどの適切な結果を期待しているのだとすぐに理解できます。
<br/>

❌ **守らないと：** 500行のJSONを毎回コピーすれば、読みにくく保守できないテストになります。すべてを外に出せば、何をしているのかつかみにくいテストになります。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：原因が外部の巨大なJSONに隠れていて、失敗の理由がわからない

![Mochaを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Mochaを使った例")

```javascript
test("When no credit, then the transfer is declined", async() => {
      // Arrange
      const transferRequest = testHelpers.factorMoneyTransfer() //get back 200 lines of JSON;
      const transferServiceUnderTest = new TransferService();

      // Act
      const transferResponse = await transferServiceUnderTest.transfer(transferRequest);

      // Assert
      expect(transferResponse.status).toBe(409);// But why do we expect failure: All seems perfectly valid in the test 🤔
    });
```

<br/>

### :clap: 良い例：その結果になる理由をテスト自身が明示している

```javascript

test("When no credit, then the transfer is declined ", async() => {
      // Arrange
      const transferRequest = testHelpers.factorMoneyTransfer({userCredit:100, transferAmount:200}) //obviously there is lack of credit
      const transferServiceUnderTest = new TransferService({disallowOvercharge:true});

      // Act
      const transferResponse = await transferServiceUnderTest.transfer(transferRequest);

      // Assert
      expect(transferResponse.status).toBe(409); // Obviously if the user has no credit it should fail
    });
  ```

</details>

<br/><br/>

## ⚪️ 1.10 エラーをcatchするのではなく、発生することを期待する

:white_check_mark: **推奨：** ある入力でエラーが起きることを検証するとき、try-catch-finallyを使い、catch節に入ったかを確かめたくなるかもしれません。しかし、その方法では次の例のように不自然で冗長なテストになり、本来は単純な意図と期待する結果が見えにくくなります。

より簡潔なのは、Chaiの専用アサーション`expect(method).to.throw`、またはJestの`expect(method).toThrow()`を1行で使う方法です。例外にエラーの種類を示すプロパティが含まれることも、必ず確認してください。一般的なエラーしかなければ、アプリケーションはユーザーに残念なメッセージを表示する以上の対応ができません。
<br/>

❌ **守らないと：** CIなどのテストレポートから、何が問題だったのかを読み取るのが難しくなります。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：try-catchでエラーの発生を確かめる、長いテストケース

![Mochaを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Mochaを使った例")

```javascript
it("When no product name, it throws error 400", async () => {
  let errorWeExceptFor = null;
  try {
    const result = await addNewProduct({});
  } catch (error) {
    expect(error.code).to.equal("InvalidInput");
    errorWeExceptFor = error;
  }
  expect(errorWeExceptFor).not.to.be.null;
  //if this assertion fails, the tests results/reports will only show
  //that some value is null, there won't be a word about a missing Exception
});
```

<br/>

### :clap: 良い例：QA担当者や技術に詳しいPMにも理解できそうな、読みやすい期待の記述

```javascript
it("When no product name, it throws error 400", async () => {
  await expect(addNewProduct({}))
    .to.eventually.throw(AppError)
    .with.property("code", "InvalidInput");
});
```

</details>

<br/><br/>

## ⚪️ 1.11 テストにタグを付ける

:white_check_mark: **推奨：** テストの種類によって、実行すべきタイミングは異なります。I/Oを伴わない短いスモークテストは保存やコミットのたびに、完全なE2Eテストは通常、新しいプルリクエストの作成時に実行します。`#cold`、`#api`、`#sanity`などのキーワードでタグ付けすると、テスト実行ツールで検索し、必要なものだけを動かせます。たとえばMochaでsanityグループだけを実行するなら、`mocha --grep 'sanity'`を使います。
<br/>

❌ **守らないと：** 開発者が少し変更するたびに、何十回もDBを問い合わせるものを含む全テストが動くと、非常に時間がかかり、テストを実行しなくなってしまいます。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：「#cold-test」タグで高速なテストだけを実行する。ColdとはI/Oを伴わず、入力中でも頻繁に実行できる短いテストのこと

![Jestを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Jestを使った例")

```javascript
//this test is fast (no DB) and we're tagging it correspondigly
//now the user/CI can run it frequently
describe("Order service", function() {
  describe("Add new order #cold-test #sanity", function() {
    test("Scenario - no currency was supplied. Expectation - Use the default currency #sanity", function() {
      //code logic here
    });
  });
});
```

</details>

<br/><br/>

## ⚪️ 1.12 テストを少なくとも2階層に分類する

:white_check_mark: **推奨：** テストスイートに構造を持たせ、ときどき読む人でも要件と各シナリオを理解できるようにしましょう。テストは最良のドキュメントです。よく使われる方法は、各テストを少なくとも2つの`describe`ブロックで囲むことです。1つ目にはテスト対象の名前を、2つ目にはシナリオや独自のカテゴリなどを指定します。以下のコード例と画面を参照してください。テストレポートも読みやすくなり、カテゴリを把握して必要な箇所を詳しく見たり、失敗したテストの共通点を見つけたりしやすくなります。テスト数が多いスイートのコードもたどりやすくなります。ほかにも[given-when-then](https://github.com/searls/jasmine-given)や[RITE](https://github.com/ericelliott/riteway)などの構造を検討できます。

<br/>

❌ **守らないと：** テストが平坦な長い一覧になっていると、主なシナリオや失敗したテストの共通点を知るために、長文を読み流す必要があります。100件中7件が失敗した場合を考えてください。平坦な一覧では、失敗した各テストの文章を読んで関係を調べなければなりません。階層的なレポートなら、同じフローやカテゴリの配下でまとめて失敗しているとわかり、根本原因や少なくともその所在を素早く推測できます。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：テスト対象名とシナリオでスイートを構成すると、次のような読みやすいレポートになる

![Jestを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Jestを使った例")

```javascript
// Unit under test
describe("Transfer service", () => {
  //Scenario
  describe("When no credit", () => {
    //Expectation
    test("Then the response status should decline", () => {});

    //Expectation
    test("Then it should send email to admin", () => {});
  });
});
```

![テスト対象とシナリオごとに階層化されたレポート](assets/hierarchical-report.png)

<br/>

### :thumbsdown: アンチパターン：平坦なテスト一覧では、ユーザーストーリーや失敗したテストの関係をつかみにくい

![Mochaを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Mochaを使った例")

```javascript
test("Then the response status should decline", () => {});

test("Then it should send email", () => {});

test("Then there should not be a new transfer record", () => {});
```

![階層のない平坦なテストレポート](assets/flat-report.png)

<br/>

</details>

<br/><br/>

## ⚪️ 1.13 テスト全般で押さえておきたい、そのほかの基本

:white_check_mark: **推奨：** このガイドはNode.jsに関係する助言、または少なくともNode.jsで例示できる助言を中心にしています。この項目では、Node.jsに限らない、よく知られた基本をまとめます。

[TDDの原則](https://www.sm-cloud.com/book-review-test-driven-development-by-example-a-tldr/)を学び、実践してみましょう。多くの人にとって非常に有益ですが、自分のスタイルに合わなくても気後れする必要はありません。そう感じるのはあなただけではありません。[レッド・グリーン・リファクタリング](https://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html)の流れで、実装より先にテストを書くことを検討してください。各テストでは1つのことだけを確認します。バグを見つけたら、修正前に、将来同じバグを検出できるテストを書きます。各テストは、成功させる前に少なくとも一度は失敗させてください。モジュールは、まずテストを満たす簡単なコードから始め、段階的にリファクタリングして本番に耐える品質へ引き上げます。パスやOSなど、環境への依存も避けましょう。
<br/>

❌ **守らないと：** 何十年もかけて蓄積された知恵を取り逃してしまいます。

<br/><br/>

<a id="section-2"></a>

# 第2章：バックエンドのテスト

## ⚪️ 2.1 テストの選択肢を広げる：ユニットテストとテストピラミッドの先を見る

:white_check_mark: **推奨：** [テストピラミッド](https://martinfowler.com/bliki/TestPyramid.html)は、提唱から10年以上が経っても有用なモデルです。3種類のテストを提示し、多くの開発者のテスト戦略に影響を与えています。その一方で、新しく有望なテスト手法が数多く登場しているのに、ピラミッドの陰に隠れてしまっています。マイクロサービス、クラウド、サーバーレスなど、この10年の劇的な変化を踏まえると、かなり前の1つのモデルが*あらゆる*アプリケーションに適合するでしょうか。テストの世界でも、新しい手法をもっと受け入れるべきではないでしょうか。

誤解しないでください。2019年の時点でも、テストピラミッド、TDD、ユニットテストは強力で、多くのアプリケーションに最適な選択肢でしょう。ただ、どのモデルもそうであるように、有用であっても[常に正しいとは限りません](https://en.wikipedia.org/wiki/All_models_are_wrong)。たとえば、多数のイベントをKafkaやRabbitMQのメッセージバスに取り込み、データウェアハウスへ流し、最後に分析用UIから問い合わせるIoTアプリケーションを考えます。連携が中心でロジックがほとんどないアプリケーションに、テスト予算の50%をユニットテストとして投入するべきでしょうか。ボット、暗号資産、Alexaスキルなど、アプリケーションの種類が多様化するほど、テストピラミッドが最適ではない状況も増えます。

テストの選択肢を広げ、さらに多くの種類を知りましょう。次の項目から、そのためのアイデアをいくつか紹介します。テストピラミッドなどのモデルを意識しつつ、実際に直面している問題に合うテストを選んでください。「APIの互換性が壊れた。それなら利用者主導のコントラクトテストを書こう」といった具合です。リスク分析に基づいてポートフォリオを組む投資家のように、テストも分散させます。どこに問題が生じそうかを評価し、そのリスクを抑える対策を対応付けましょう。

なお、ソフトウェア業界のTDD論争は、誤った二者択一に陥りがちです。どこでも使うべきだという人もいれば、悪魔のように扱う人もいます。絶対論で語る人は、誰であれ間違っています :]

<br/>

❌ **守らないと：** 驚くほど費用対効果の高いツールを見逃します。ファジング、リント、ミューテーションテストなどには、10分で価値を得られるものもあります。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：Cindy Sridharanが優れた記事「Testing Microservices — the sane way」で提案する、多様なテストの組み合わせ

![Cindy Sridharanによる多様なテストの組み合わせ](assets/bp-12-rich-testing.jpeg "記事『Testing Microservices — the sane way』で提案されているテストの組み合わせ")

**☺️ 例：** [YouTube：ユニットテストの先へ — 注目のNode.jsテスト5種類（2018年、Yoni Goldberg）](https://www.youtube.com/watch?v=-2zP494wdUY&feature=youtu.be)

<br/>

![Yoni Goldbergによるテスト手法の紹介](assets/bp-12-Yoni-Goldberg-Testing.jpeg "ユニットテストの先にあるテスト手法")

</details>

<br/><br/>

## ⚪️ 2.2 コンポーネントテストが最良の選択肢かもしれない

:white_check_mark: **推奨：** ユニットテストが確認するのはアプリケーションのごく一部であり、全体を網羅するには費用がかかります。一方、E2Eテストは広範囲を簡単に確認できますが、不安定で遅くなりがちです。それなら、ユニットテストより大きく、E2Eテストより小さい、バランスの取れたテストを書いてはどうでしょう。コンポーネントテストは、テストの世界で十分に評価されていない手法です。適度な実行速度とTDDの適用しやすさに、現実に近い広い網羅性を兼ね備えています。

コンポーネントテストは、マイクロサービスを1つの「単位」として扱います。APIを通じて操作し、そのマイクロサービス自身に属するものはモックにしません。DBも実物、少なくとも同じDBのインメモリ版を使います。一方、ほかのマイクロサービスへの呼び出しなど、外部のものはスタブに置き換えます。これにより、実際にデプロイするものを、外側から内側へとテストでき、妥当な時間で大きな安心感を得られます。

[コンポーネントテストの適切な書き方に特化した、詳しいガイドもあります](https://github.com/testjavascript/nodejs-integration-tests-best-practices)。

<br/>

❌ **守らないと：** 何日もかけてユニットテストを書いたのに、システム全体の20%しかカバーできていなかった、ということになりかねません。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：Supertestで同一プロセス内からExpress APIを呼び出す。高速で、複数の層を確認できる

![Mochaを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Mochaを使った例")

![Supertestを使ったコンポーネントテスト](assets/bp-13-component-test-yoni-goldberg.png "Supertestなら同一プロセス内でExpress APIを呼び出し、複数の層を高速にテストできる")

</details>

<br/><br/>

## ⚪️ 2.3 コントラクトテストで、新しいリリースがAPIの互換性を壊さないことを確認する

:white_check_mark: **推奨：** マイクロサービスには複数のクライアントがあり、互換性を保つために複数のバージョンを運用しているとします。あるフィールドを変えた途端、そのフィールドに依存する重要なクライアントが動かなくなりました。これはシステム連携の世界のジレンマです。サーバー側がすべてのクライアントの期待を把握するのは困難ですが、リリース日を決めるのはサーバー側なので、クライアント側も自由にテストできません。この契約上の問題を緩和する手法には、単純なものから、高機能で習得に時間がかかるものまであります。簡単で推奨できる方法は、API提供側がJSDocやTypeScriptなどでAPIの型を記述したnpmパッケージを公開することです。利用側はそのライブラリを取り込み、実装中の補完や検証を利用できます。さらに高度な方法が[PACT](https://docs.pact.io/)です。PACTは、この手続きを仕組み化するために、サーバーではなくクライアントが「サーバーのテスト」を定義するという画期的な考え方を採用しています。クライアントの期待を記録し、「ブローカー」という共有の場所に置くと、サーバーはそれを取得し、ビルドごとにPACTライブラリで実行できます。これにより、満たされていないクライアントの期待、つまり契約違反を検出します。サーバーとクライアントのAPIの不一致をビルドやCIで早期に見つけられれば、多くの苦労を避けられます。
<br/>

❌ **守らないと：** 消耗する手動テストを続けるか、デプロイを恐れながら過ごすことになります。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：コントラクトテストの流れ

![PACTを使った例](https://img.shields.io/badge/🔧%20Example%20using%20PACT-blue.svg "PACTを使った例")

![PACTによるコントラクトテストの流れ](assets/bp-14-testing-best-practices-contract-flow.png)

</details>

<br/><br/>

## ⚪️ 2.4 ミドルウェアを単独でテストする

:white_check_mark: **推奨：** ミドルウェアはシステムの小さな一部分で、稼働中のExpressサーバーも必要だとして、テストを避ける人がいます。しかし、どちらも適切な理由ではありません。ミドルウェアは小さくても、すべて、または大半のリクエストに影響します。また、`req`と`res`というJavaScriptオブジェクトを受け取る純粋な関数のように、簡単にテストできます。関数を直接呼び出し、`req`・`res`とのやり取りを[Sinonなど](https://www.npmjs.com/package/sinon)のスパイで監視して、適切な操作が行われたか確かめればよいのです。[node-mocks-http](https://www.npmjs.com/package/node-mocks-http)なら、`req`・`res`オブジェクトの生成と、その振る舞いの監視まで行えます。たとえば次の例では、`res`に設定されたHTTPステータスが期待どおりかを検証します。
<br/>

❌ **守らないと：** Expressのミドルウェアのバグは、すべて、または大半のリクエストのバグに直結します。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：ネットワーク通信やExpress全体の起動なしで、ミドルウェアを単独でテストする

![Jestを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Jestを使った例")

```javascript
//the middleware we want to test
const unitUnderTest = require("./middleware");
const httpMocks = require("node-mocks-http");
//Jest syntax, equivelant to describe() & it() in Mocha
test("A request without authentication header, should return http status 403", () => {
  const request = httpMocks.createRequest({
    method: "GET",
    url: "/user/42",
    headers: {
      authentication: ""
    }
  });
  const response = httpMocks.createResponse();
  unitUnderTest(request, response);
  expect(response.statusCode).toBe(403);
});
```

</details>

<br/><br/>

## ⚪️ 2.5 静的解析ツールで測定し、リファクタリングする

:white_check_mark: **推奨：** 静的解析ツールは、コード品質を改善し、保守しやすい状態を保つための客観的な手掛かりを与えてくれます。CIビルドに組み込み、問題のあるコードを検出したら中断することもできます。通常のリントに対する主な強みは、重複の検出など複数ファイルにまたがる品質の検査、コードの複雑度などの高度な分析、問題の履歴や改善状況の追跡です。例として、[SonarQube](https://www.sonarqube.org/)（[スター](https://github.com/SonarSource/sonarqube)4,900以上）と[Code Climate](https://codeclimate.com/)（[スター](https://github.com/codeclimate/codeclimate)2,000以上）があります。

協力：[Keith Holliday](https://github.com/TheHollidayInn)

<br/>

❌ **守らないと：** コード品質が低ければ、バグや性能の問題はつきまといます。新しいライブラリや最先端の機能でも、それを解決することはできません。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：複雑なメソッドを検出できる商用ツール、Code Climate

![CodeClimateを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Code%20Climate-blue.svg "CodeClimateを使った例")

![Code Climateによる複雑なメソッドの検出](assets/bp-16-yoni-goldberg-quality.png "Code Climateは複雑なメソッドを検出できる商用ツール")

</details>

<br/><br/>

<a id="practice-2-6"></a>

## ⚪️ 2.6 Node.js特有の障害への備えを確認する

:white_check_mark: **推奨：** 不思議なことに、ソフトウェアのテストの大半はロジックとデータだけを扱います。しかし、特に深刻で対処しにくい問題の中には、インフラに起因するものがあります。プロセスのメモリが逼迫したときや、サーバー・プロセスが停止したときに何が起こるか、テストしたことはあるでしょうか。APIが50%遅くなったとき、監視システムは気付けるでしょうか。こうした問題を試し、影響を軽減するために、Netflixで[カオスエンジニアリング](https://principlesofchaos.org/)が生まれました。混乱を伴う障害に対するアプリケーションの回復力を検証するための考え方、フレームワーク、ツールを提供します。有名な[Chaos Monkey](https://github.com/Netflix/chaosmonkey)はサーバーをランダムに停止させ、単一のサーバーに依存せずにサービスを提供し続けられるかを確認します。Podを停止させるKubernetes版の[kube-monkey](https://github.com/asobti/kube-monkey)もあります。これらはホスティングやプラットフォームの層で動作しますが、Node.jsそのものの障害を起こしたい場合はどうでしょう。未捕捉のエラー、処理されていないPromiseの拒否、V8のメモリが上限の1.7GBに達した場合への対処や、イベントループが頻繁にブロックされても十分なUXを保てるか、といった確認です。そのために、著者はNode.jsに関するさまざまな障害を起こせる[node-chaos](https://github.com/i0natan/node-chaos-monkey)（アルファ版）を作りました。
<br/>

❌ **守らないと：** 逃れることはできません。マーフィーの法則が、本番環境を容赦なく襲います。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：node-chaosでNode.jsのさまざまな障害を起こし、アプリケーションの回復力を試す

![node-chaosでNode.js特有の障害を再現する](assets/bp-17-yoni-goldberg-chaos-monkey-nodejs.png "node-chaosで障害を起こし、アプリケーションの回復力を確かめる")

</details>

<br/>

## ⚪️ 2.7 グローバルなフィクスチャやシードを避け、テストごとにデータを追加する

:white_check_mark: **推奨：** 第0章の黄金律に従い、各テストは専用のDBレコードを追加し、それだけを操作しましょう。テスト間の結び付きを防ぎ、流れを理解しやすくなります。実際には、性能を上げるため、テスト実行前にDBへ共通データを投入する「テストフィクスチャ」によって、この原則がよく破られています。性能は確かに重要ですが、改善する手段があります。「コンポーネントテスト」の項目も参照してください。一方、テストの複雑さはより深刻な負担なので、多くの場合はほかの事情より優先すべきです。各テストケースが必要なDBレコードを明示的に作成し、そのレコードだけを操作するようにします。性能がどうしても問題になるなら、問い合わせなど、データを変更しないテストスイートだけでシードデータを共有するのが、バランスの取れた妥協案かもしれません。
<br/>

❌ **守らないと：** いくつかのテストが失敗し、デプロイが中断されました。バグだろうかとチームが貴重な時間を使って調べた結果、2つのテストが同じシードデータを書き換えていただけだとわかります。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：テストが独立しておらず、グローバルなフックが投入する共通DBデータに依存している

![Mochaを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Mochaを使った例")

```javascript
before(async () => {
  //adding sites and admins data to our DB. Where is the data? outside. At some external json or migration framework
  await DB.AddSeedDataFromJson('seed.json');
});
it("When updating site name, get successful confirmation", async () => {
  //I know that site name "portal" exists - I saw it in the seed files
  const siteToUpdate = await SiteService.getSiteByName("Portal");
  const updateNameResult = await SiteService.changeName(siteToUpdate, "newName");
  expect(updateNameResult).to.be(true);
});
it("When querying by site name, get the right site", async () => {
  //I know that site name "portal" exists - I saw it in the seed files
  const siteToCheck = await SiteService.getSiteByName("Portal");
  expect(siteToCheck.name).to.be.equal("Portal"); //Failure! The previous test change the name :[
});

```

<br/>

### :clap: 良い例：必要なデータをテスト内で把握でき、各テストが専用のデータだけを操作する

```javascript
it("When updating site name, get successful confirmation", async () => {
  //test is adding a fresh new records and acting on the records only
  const siteUnderTest = await SiteService.addSite({
    name: "siteForUpdateTest"
  });
  const updateNameResult = await SiteService.changeName(siteUnderTest, "newName");
  expect(updateNameResult).to.be(true);
});
```

</details>

<br/>

## ⚪️ 2.8 データ削除の方針を明確にする：全テスト後（推奨）か、各テスト後か

:white_check_mark: **推奨：** DBをいつ空にするかによって、テストの書き方が決まります。主な選択肢は、すべてのテストの終了後か、個々のテストの終了後です。各テストの終了後に削除すると、毎回テーブルが空になり、開発者にとって便利です。テスト開始時にほかのレコードが存在しないので、どのデータを問い合わせているかが確実にわかり、アサーションで行数を数えたくなるかもしれません。しかし重大な欠点があります。マルチプロセスで実行すると、テスト同士が干渉しやすいのです。プロセス1がテーブルを空にした瞬間、プロセス2がデータを問い合わせて失敗するかもしれません。また、失敗したテストを調べるときにも、DBにはすでにレコードがなく、原因を追いにくくなります。

もう1つの選択肢は、すべてのテストファイルの実行後、あるいは1日1回だけ削除することです。この方法では、既存レコードが入った同じDBを、すべてのテストとプロセスが使います。互いに干渉しないよう、各テストは自分が追加した特定のレコードだけを操作しなければなりません。レコードの追加を確認したければ、ほかにも何千件ものレコードがあると考え、自分が追加したものを明示的に検索します。削除を確認したければ、テーブル全体が空だと仮定せず、そのレコードが存在しないことを調べます。この方法には大きな利点があります。そのままマルチプロセスで実行でき、何が起きたかを調べるときもデータが残っています。DBが人工的に空にされず、多くのレコードが存在するため、バグを発見する可能性も高まります。[詳しい比較表はこちらです](https://github.com/testjavascript/nodejs-integration-tests-best-practices/blob/master/graphics/db-clean-options.png)。
<br/>

❌ **守らないと：** レコードを分離する、または削除する方針がなければ、テスト同士が干渉します。トランザクションを使う方法はリレーショナルDBに限られ、内部にもトランザクションがあると複雑になりがちです。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：すべてのテストの終了後に削除する。毎回削除する必要はない。テスト中のデータが多いほど、本番の条件に近付く

```javascript
  // After-all clean up (recommended)
// global-teardown.js
module.exports = async () => {
  // ...
  if (Math.ceil(Math.random() * 10) === 10) {
    await new OrderRepository().cleanup();
  }
};
```

</details>

<br/>

## ⚪️ 2.9 HTTPインターセプターでコンポーネントを外部から隔離する

:white_check_mark: **推奨：** 外向きのHTTPリクエストを捕捉し、必要な応答を返すことで、連携先のHTTP APIを実際に呼び出さずにテスト対象を隔離します。Nockは、外部サービスの振る舞いを簡潔な構文で定義できる優れたツールです。隔離は、余計な不安定要因や遅延を避けるだけでなく、さまざまな状況と応答を再現するために不可欠です。優れたフライトシミュレーターは、青空を描くだけでなく、嵐や混乱を安全に体験させてくれます。これは、ほかのサービス群を巻き込まず、1つのコンポーネントに集中すべきマイクロサービス構成で、特に重要です。テストダブル、つまりモックでも外部の振る舞いを模擬できますが、デプロイされるコードには触れず、ネットワークの層で操作するほうが、純粋なブラックボックステストを保てます。ただし隔離すると、連携先の変更やサービス間の認識違いを見落とします。少数のコントラクトテストやE2Eテストで必ず補いましょう。
<br/>

❌ **守らないと：** 呼び出し側がローカルに配置できる、通常はDockerを使った代替版を提供するサービスもあります。準備と実行速度は改善しますが、さまざまな応答の再現には役立ちません。本物のサービスを呼び出しても課金や副作用が発生しない「サンドボックス」を提供するサービスもありますが、準備の手間が減る一方で、任意のシナリオは再現できません。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：外部コンポーネントへの通信を止めることで、シナリオを再現し、余計な不安定要因を減らす

```javascript
// Intercept requests for 3rd party APIs and return a predefined response 
beforeEach(() => {
  nock('http://localhost/user/').get(`/1`).reply(200, {
    id: 1,
    name: 'John',
  });
});
```

</details>
<br/>

## ⚪️ 2.10 応答のスキーマをテストする：自動生成フィールドがある場合は特に重要

:white_check_mark: **推奨：** 具体的な値を検証できない場合は、必須フィールドの存在と型を確認しましょう。応答には日付や連番など、テストを書く時点では予測できない、動的で重要な値が含まれることがあります。APIの契約が、そのフィールドはnullではなく、正しい型であると約束しているなら、必ずテストすべきです。多くのアサーションライブラリは型の検証に対応しています。応答が小さければ、次のコード例のように、値と型を同じアサーションで確認します。OpenAPI文書（Swagger）に照らして応答全体を検証する方法もあります。多くのテストランナーには、API応答をそのドキュメントと照合するコミュニティ製の拡張機能があります。


<br/>

❌ **守らないと：** 呼び出し側がIDや日付などの動的なフィールドに依存しているのに、それが応答に含まれず、契約を破ってしまうかもしれません。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：動的な値を持つフィールドが存在し、正しい型であることを検証する

```javascript
  test('When adding a new valid order, Then should get back approval with 200 response', async () => {
  // ...
  //Assert
  expect(receivedAPIResponse).toMatchObject({
    status: 200,
    data: {
      id: expect.any(Number), // Any number satisfies this test
      mode: 'approved',
    },
  });
});
```

</details>

<br/>

## ⚪️ 2.11 外部連携の境界的なケースや障害を確認する

:white_check_mark: **推奨：** 連携を確認するときは、通常の成功パターンと失敗パターンの先まで試しましょう。HTTP 500のようなエラー応答だけでなく、応答の遅延やタイムアウトなど、ネットワーク層の異常も確認します。これにより、タイムアウト後に適切な処理へ進むこと、壊れやすい競合状態がないこと、再試行に対するサーキットブレーカーを備えていることなど、さまざまな通信状況への耐性を確認できます。実績のあるインターセプターなら、ときどき失敗する不安定なサービスなど、多様な通信の振る舞いを簡単に再現できます。HTTPクライアントの既定のタイムアウト値が、シミュレートする応答時間より長いことを検知し、実際に待たずにその場でタイムアウト例外を投げることさえできます。


<br/>

❌ **守らないと：** テストがすべて通っているのに、外部サービスが例外的な応答を返したとき、本番だけがクラッシュしたり、エラーを正しく報告しなかったりします。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：通信障害時に、サーキットブレーカーが役立つことを確認する

```javascript
  test('When users service replies with 503 once and retry mechanism is applied, then an order is added successfully', async () => {
  //Arrange
  nock.removeInterceptor(userServiceNock.interceptors[0])
  nock('http://localhost/user/')
    .get('/1')
    .reply(503, undefined, { 'Retry-After': 100 });
  nock('http://localhost/user/')
    .get('/1')
    .reply(200);
  const orderToAdd = {
    userId: 1,
    productId: 2,
    mode: 'approved',
  };

  //Act
  const response = await axiosAPIClient.post('/order', orderToAdd);

  //Assert
  expect(response.status).toBe(200);
});
```

</details>

<br/>


## ⚪️ 2.12 起こりうる5種類の結果をテストする

:white_check_mark: **推奨：** テストを計画するときは、典型的な処理の結果を5種類に分けて検討しましょう。API呼び出しなどの操作を起こすと、何らかの意味のある反応が生じ、それがテストの対象になります。関心があるのは内部で「どう」動くかではありません。外から観測でき、ユーザーに影響しうる結果です。その結果や反応は、次の5つに分類できます。

• 応答 — APIなどを通じて操作を行い、応答を受け取ります。応答データの正しさ、スキーマ、HTTPステータスを確認します。

• 新しい状態 — 操作の後に、**公開インターフェースから取得できる**データが変わることがあります。

• 外部呼び出し — 操作の後に、HTTPなどを通じて外部コンポーネントが呼ばれることがあります。SMSやメールの送信、クレジットカードへの課金などです。

• メッセージキュー — 処理の結果が、キューに追加されたメッセージになる場合もあります。

• 可観測性（オブザーバビリティ） — エラーや重要な業務イベントなど、監視すべきものがあります。トランザクションが失敗した場合、正しい応答だけでなく、適切なエラー処理、ログ、メトリクスも必要です。この情報は、本番環境のSREや管理者という、非常に重要な利用者へ直接届きます。


<br/><br/>

<a id="section-3"></a>

# 第3章：フロントエンドのテスト

## ⚪️ 3.1 UIの見た目と機能を分離する

:white_check_mark: **推奨：** コンポーネントのロジックをテストするとき、UIの細かな見た目は余計な情報になります。テストがデータそのものに集中できるよう切り離しましょう。具体的には、表示の実装に強く依存しない抽象的な方法でマークアップから必要なデータを取り出し、HTMLやCSSの見た目ではなく、そのデータだけを検証します。実行を遅くするアニメーションも無効にします。描画を省略し、サービス、アクション、ストアなどUIの背後にある部分だけをテストしたくなるかもしれません。しかし、それでは現実と異なるテストになり、正しいデータがそもそもUIに届いていない問題を見つけられません。

<br/>

❌ **守らないと：** 計算結果のデータは10ミリ秒で用意できるのに、テストと関係のない凝ったアニメーションのせいで全体が500ミリ秒かかり、100件なら約1分になってしまいます。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：UIの細部をテストから切り離す

![Reactを使った例](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Reactを使った例") ![react-testing-libraryを使った例](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "react-testing-libraryを使った例")

```javascript
test("When users-list is flagged to show only VIP, should display only VIP members", () => {
  // Arrange
  const allUsers = [{ id: 1, name: "Yoni Goldberg", vip: false }, { id: 2, name: "John Doe", vip: true }];

  // Act
  const { getAllByTestId } = render(<UsersList users={allUsers} showOnlyVIP={true} />);

  // Assert - Extract the data from the UI first
  const allRenderedUsers = getAllByTestId("user").map(uiElement => uiElement.textContent);
  const allRealVIPUsers = allUsers.filter(user => user.vip).map(user => user.name);
  expect(allRenderedUsers).toEqual(allRealVIPUsers); //compare data with data, no UI here
});
```

<br/>

### :thumbsdown: アンチパターン：アサーションにUIの細部とデータを混在させる

```javascript
test("When flagging to show only VIP, should display only VIP members", () => {
  // Arrange
  const allUsers = [{ id: 1, name: "Yoni Goldberg", vip: false }, { id: 2, name: "John Doe", vip: true }];

  // Act
  const { getAllByTestId } = render(<UsersList users={allUsers} showOnlyVIP={true} />);

  // Assert - Mix UI & data in assertion
  expect(getAllByTestId("user")).toEqual('[<li data-test-id="user">John Doe</li>]');
});
```

</details>

<br/><br/>

## ⚪️ 3.2 変わりにくい属性を使ってHTML要素を取得する

:white_check_mark: **推奨：** CSSセレクターとは違い、見た目が変わっても維持されやすい属性、たとえばフォームのラベルを使ってHTML要素を取得しましょう。そのような属性がなければ、`test-id-submit-button`のようなテスト専用の属性を作ります。こうすれば見た目の変更で機能やロジックのテストが壊れなくなり、その要素と属性はテストで使うため削除してはいけない、ということもチーム全体に伝わります。

<br/>

❌ **守らないと：** 多くのコンポーネント、ロジック、サービスにまたがるログイン機能をテストするとします。スタブやスパイを用意し、Ajax通信も隔離し、準備は完璧です。それなのに、デザイナーがdivのCSSクラスを`thick-border`から`thin-border`へ変えただけで、テストが失敗してしまいます。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：テスト専用の属性で要素を取得する

![Reactを使った例](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Reactを使った例")

```jsx
// the markup code (part of React component)
<h3>
  <Badge pill className="fixed_badge" variant="dark">
    <span data-test-id="errorsLabel">{value}</span>
    <!-- note the attribute data-test-id -->
  </Badge>
</h3>
```

```javascript
// this example is using react-testing-library
test("Whenever no data is passed to metric, show 0 as default", () => {
  // Arrange
  const metricValue = undefined;

  // Act
  const { getByTestId } = render(<dashboardMetric value={undefined} />);

  expect(getByTestId("errorsLabel").text()).toBe("0");
});
```

<br/>

### :thumbsdown: アンチパターン：CSSの属性に依存する

```jsx
<!-- the markup code (part of React component) -->
<span id="metric" className="d-flex-column">{value}</span>
<!-- what if the designer changes the classs? -->
```

```javascript
// this exammple is using enzyme
test("Whenever no data is passed, error metric shows zero", () => {
  // ...

  expect(wrapper.find("[className='d-flex-column']").text()).toBe("0");
});
```

</details>

<br/>

## ⚪️ 3.3 可能な限り、完全に描画したコンポーネントを使って現実に近いテストをする

:white_check_mark: **推奨：** 規模が適切な範囲であれば、ユーザーと同じようにコンポーネントを外側からテストしましょう。UIを完全に描画し、操作し、その振る舞いが期待どおりかを確認します。モック、部分的な描画、シャローレンダリングは避けます。そうした方法では実際の構成が欠けてバグを見逃すおそれがあり、内部実装に干渉するため保守も難しくなります。[ブラックボックステストの項目](#practice-1-4)も参照してください。子コンポーネントの1つが、アニメーションなどによって大幅な遅延や複雑な準備を招く場合は、そのコンポーネントを明示的に代替物へ置き換えることを検討します。

ただし注意も必要です。この方法は、子コンポーネントの数が適度な、小規模から中規模のコンポーネントに適しています。子が多すぎるコンポーネントを完全に描画すると、失敗の根本原因を理解しにくくなり、実行も遅くなりがちです。その場合、大きな親コンポーネントには少数のテストだけを書き、子コンポーネント側のテストを増やしましょう。

<br/>

❌ **守らないと：** 非公開メソッドを呼び、内部状態を確認するようなテストでは、コンポーネントの実装をリファクタリングするたびに、テストもすべて直す必要があります。それほどの保守負担を本当に引き受けられるでしょうか。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：完全に描画したコンポーネントを、実際の利用に近い形で操作する

![Reactを使った例](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Reactを使った例") ![Enzymeを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Enzyme-blue.svg "Enzymeを使った例")

```javascript
class Calendar extends React.Component {
  static defaultProps = { showFilters: false };

  render() {
    return (
      <div>
        A filters panel with a button to hide/show filters
        <FiltersPanel showFilter={showFilters} title="Choose Filters" />
      </div>
    );
  }
}

//Examples use React & Enzyme
test("Realistic approach: When clicked to show filters, filters are displayed", () => {
  // Arrange
  const wrapper = mount(<Calendar showFilters={false} />);

  // Act
  wrapper.find("button").simulate("click");

  // Assert
  expect(wrapper.text().includes("Choose Filter"));
  // This is how the user will approach this element: by text
});
```

### :thumbsdown: アンチパターン：シャローレンダリングで実際の構成を省略する

```javascript
test("Shallow/mocked approach: When clicked to show filters, filters are displayed", () => {
  // Arrange
  const wrapper = shallow(<Calendar showFilters={false} title="Choose Filter" />);

  // Act
  wrapper
    .find("filtersPanel")
    .instance()
    .showFilters();
  // Tap into the internals, bypass the UI and invoke a method. White-box approach

  // Assert
  expect(wrapper.find("Filter").props()).toEqual({ title: "Choose Filter" });
  // what if we change the prop name or don't pass anything relevant?
});
```

</details>

<br/>

## ⚪️ 3.4 sleepを使わず、フレームワークの非同期イベント対応を使う。高速化も工夫する

:white_check_mark: **推奨：** テスト対象の処理がいつ終わるかは、わからないことがよくあります。たとえばアニメーションのために要素の出現が遅れる場合です。そんなときは`setTimeout`などで固定時間待つのではなく、多くのプラットフォームが備える、より確実な方法を選びます。[Cypressの`cy.request('url')`](https://docs.cypress.io/guides/references/best-practices.html#Unnecessary-Waiting)のように操作の完了を待てるライブラリも、[@testing-library/domの`wait(expect(element))`](https://testing-library.com/docs/guide-disappearance)のような待機APIを提供するものもあります。APIなどの遅いリソースをスタブに置き換え、応答時点を確定できるようにしてから、コンポーネントを明示的に再描画するほうが簡潔な場合もあります。待機を伴う外部コンポーネントに依存するなら、[時計を進める](https://jestjs.io/docs/en/timer-mocks)ことも有効です。固定時間の待機は、長ければ遅く、短ければ失敗する危険があるため、避けるべきパターンです。待機やポーリングが不可避で、フレームワークにも支援機能がなければ、[wait-for-expect](https://www.npmjs.com/package/wait-for-expect)などのnpmライブラリが、ある程度予測可能な解決策になります。
<br/>

❌ **守らないと：** 長く待てばテストが桁違いに遅くなり、短く待てば処理が間に合わず失敗します。結局、不安定さと遅さのどちらかを選ぶことになります。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：非同期処理が完了してから解決するE2E用API（Cypress）

![Cypressを使った例](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Cypressを使った例")
![react-testing-libraryを使った例](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "react-testing-libraryを使った例")

```javascript
// using Cypress
cy.get("#show-products").click(); // navigate
cy.wait("@products"); // wait for route to appear
// this line will get executed only when the route is ready
```

### :clap: 良い例：DOM要素を待つテストライブラリ

```javascript
// @testing-library/dom
test("movie title appears", async () => {
  // element is initially not present...

  // wait for appearance
  await wait(() => {
    expect(getByText("the lion king")).toBeInTheDocument();
  });

  // wait for appearance and return the element
  const movie = await waitForElement(() => getByText("the lion king"));
});
```

### :thumbsdown: アンチパターン：独自に書いたsleep処理

```javascript
test("movie title appears", async () => {
  // element is initially not present...

  // custom wait logic (caution: simplistic, no timeout)
  const interval = setInterval(() => {
    const found = getByText("the lion king");
    if (found) {
      clearInterval(interval);
      expect(getByText("the lion king")).toBeInTheDocument();
    }
  }, 100);

  // wait for appearance and return the element
  const movie = await waitForElement(() => getByText("the lion king"));
});
```

</details>

<br/>

## ⚪️ 3.5 ネットワーク越しのコンテンツ配信を監視する

![Lighthouseを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Google%20LightHouse-blue.svg "Lighthouseを使った例")

✅ **推奨：** 実際のネットワーク条件でページの読み込みが最適化されているか、能動的に監視しましょう。遅いページ表示や圧縮・縮小されていないバンドルなど、UXに関わる問題を含めて調べます。検査ツールには豊富な選択肢があります。[Pingdom](https://www.pingdom.com/)、AWS CloudWatch、[GCP Stackdriver](https://cloud.google.com/monitoring/uptime-checks/)などの基本的なツールなら、サーバーが稼働し、妥当なSLAの範囲内で応答するかを簡単に監視できます。ただし、それだけでは問題の一部しか見えません。[Lighthouse](https://developers.google.com/web/tools/lighthouse/)や[PageSpeed](https://developers.google.com/speed/pagespeed/insights/)など、フロントエンドに特化した詳しい分析ツールを選ぶほうがよいでしょう。着目すべきなのは、ページ読み込み時間、[意味のある内容が描画されるまでの時間](https://scotch.io/courses/10-web-performance-audit-tips-for-your-next-billion-users-in-2018/fmp-first-meaningful-paint)、[操作可能になるまでの時間（TTI）](https://calibreapp.com/blog/time-to-interactive/)など、UXに直接影響する現象や指標です。加えて、コンテンツの圧縮、最初のバイトが届くまでの時間、画像の最適化、適切なDOMサイズ、SSLなど、技術的な原因も確認できます。こうした詳しい監視は、開発中、CIの一部、そして最も重要な本番サーバーやCDNに対する24時間365日の監視として行うことを勧めます。

<br/>

❌ **守らないと：** UIを丁寧に作り、機能テストが100%成功し、バンドルも工夫したのに、CDNの設定ミスで遅く使いにくい画面になっていたら、がっかりするはずです。

<br/>

<details><summary>✏ <b>コード例</b></summary>

### :clap: 良い例：Lighthouseによるページ読み込みの検査レポート

![Lighthouseによるページ読み込みの検査レポート](/assets/lighthouse2.png "Lighthouseによるページ読み込みの検査レポート")

</details>

<br/>

<a id="practice-3-6"></a>

## ⚪️ 3.6 バックエンドAPIなど、不安定で遅いリソースはスタブに置き換える

:white_check_mark: **推奨：** 通常のテスト、つまりE2E以外のテストでは、バックエンドAPIなど、自分の責任や制御が及ばないリソースを巻き込まず、スタブなどのテストダブルに置き換えましょう。実際にAPIへ通信する代わりに、[Sinon](https://sinonjs.org/)や[testdouble](https://www.npmjs.com/package/testdouble)などで応答をスタブ化します。最大の利点は、不安定さを防げることです。テスト環境やステージングのAPIは必ずしも安定しておらず、自分のコンポーネントが正しくても、ときどきテストを失敗させます。本番環境はテスト用途ではなく、通常はリクエスト数も制限されます。スタブなら、データが見つからない場合やAPIがエラーを返す場合など、コンポーネントの振る舞いに影響するさまざまな状況も再現できます。さらに、ネットワーク通信による大幅な遅延も防げます。

<br/>

❌ **守らないと：** 通常は数ミリ秒で済むテストでも、100ミリ秒以上かかる一般的なAPI呼び出しによって、約20倍遅くなってしまいます。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：API呼び出しをスタブ化、またはインターセプトする

![Reactを使った例](https://img.shields.io/badge/🔧%20Example%20using%20React-blue.svg "Reactを使った例") ![react-testing-libraryを使った例](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "react-testing-libraryを使った例")

```javascript
// unit under test
export default function ProductsList() {
  const [products, setProducts] = useState(false);

  const fetchProducts = async () => {
    const products = await axios.get("api/products");
    setProducts(products);
  };

  useEffect(() => {
    fetchProducts();
  }, []);

  return products ? <div>{products}</div> : <div data-test-id="no-products-message">No products</div>;
}

// test
test("When no products exist, show the appropriate message", () => {
  // Arrange
  nock("api")
    .get(`/products`)
    .reply(404);

  // Act
  const { getByTestId } = render(<ProductsList />);

  // Assert
  expect(getByTestId("no-products-message")).toBeTruthy();
});
```

</details>

<br/>

## ⚪️ 3.7 システム全体を通すE2Eテストは、ごく少数に絞る

:white_check_mark: **推奨：** E2E（エンドツーエンド）という言葉は、実ブラウザーを使ったUIだけのテストを指すこともあれば（[3.6参照](#practice-3-6)）、実際のバックエンドまで含めたシステム全体のテストを指すこともあります。後者は非常に有益です。データのスキーマに対する認識の違いによって起こる、フロントエンドとバックエンド間の連携バグを確認できます。マイクロサービスAがBに誤ったメッセージを送るようなバックエンド同士の連携問題や、デプロイの失敗を検出するにも有効です。バックエンドには、[Cypress](https://www.cypress.io/)や[Puppeteer](https://github.com/GoogleChrome/puppeteer)ほど使いやすく成熟したE2E向けのUIフレームワークに相当するものがありません。一方、多数のコンポーネントを備える環境の構築は高くつき、何よりテストが壊れやすくなります。50個のマイクロサービスのうち1つが失敗しただけで、E2E全体も失敗します。そのため、この手法は控えめに使い、1〜10件ほどにとどめるのがよいでしょう。少数でも、狙いとするデプロイや連携の不具合は検出できます。本番に近いステージング環境での実行を勧めます。

<br/>

❌ **守らないと：** UIの機能テストに力を注いでも、実際にバックエンドが返すペイロード、つまりUIが扱うデータのスキーマが想定と大きく違うことに、最後まで気付けないかもしれません。

<br/>

## ⚪️ 3.8 ログイン情報を再利用してE2Eテストを高速化する

:white_check_mark: **推奨：** 実際のバックエンドを使い、API呼び出しに有効なユーザートークンが必要なE2Eテストでは、リクエストごとにユーザーを作り、ログインするほど厳密に分離しても、費用に見合いません。代わりに、全テスト開始前のフック（before-all）で一度だけログインし、トークンをローカルの保存先に保持して、各リクエストで再利用します。これは「テストはリソースを共有せず、独立させる」という基本原則に反するように見えます。その懸念はもっともですが、E2Eでは性能が重要で、各テスト前に1〜3回のAPIリクエストを追加すると、実行時間が非常に長くなりえます。認証情報を再利用しても、同じユーザーデータを操作する必要はありません。支払い履歴などのデータに依存する場合は、各テストでそのデータを作り、他のテストと共有しないようにします。バックエンド自体を代替できることも忘れないでください。フロントエンドだけを確認するなら、隔離してAPIをスタブ化するほうが適切かもしれません（[3.6参照](#practice-3-6)）。

<br/>

❌ **守らないと：** 200件のテストで、ログインに100ミリ秒ずつかかるとすれば、同じログインの繰り返しだけで20秒を費やします。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：各テスト前（before-each）ではなく、全テスト前（before-all）にログインする

![Cypressを使った例](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Cypressを使った例")

```javascript
let authenticationToken;

// happens before ALL tests run
before(() => {
  cy.request('POST', 'http://localhost:3000/login', {
    username: Cypress.env('username'),
    password: Cypress.env('password'),
  })
  .its('body')
  .then((responseFromLogin) => {
    authenticationToken = responseFromLogin.token;
  })
})

// happens before EACH test
beforeEach(setUser => {
  cy.visit('/home', () => {
    onBeforeLoad (win => {
      win.localStorage.setItem('token', JSON.stringify(authenticationToken))
    })
  })
})
```

</details>

<br/>

## ⚪️ 3.9 サイト全体を巡回するE2Eスモークテストを1つ用意する

:white_check_mark: **推奨：** 本番監視と開発中の簡単な動作確認のために、サイトのすべて、または大半のページを訪問し、壊れていないことを確かめるE2Eテストを1つ用意しましょう。書くのも保守するのも簡単な一方、機能、ネットワーク、デプロイなど幅広い失敗を見つけられるため、費用対効果に優れます。ほかのスモークテストや簡易確認は、これほど確実で網羅的ではありません。たとえば運用チームが本番のトップページだけに疎通確認をしたり、開発者が統合テストを多数実行しても、パッケージングやブラウザーの問題を発見できなかったりします。もちろん、スモークテストは機能テストの代わりではなく、異常を素早く知らせる火災報知器の役目です。

<br/>

❌ **守らないと：** 全テストが成功し、本番のヘルスチェックも正常なのに、決済コンポーネントのパッケージングに問題があって、`/Payment`だけ表示できないかもしれません。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：すべてのページを巡回するスモークテスト

![Cypressを使った例](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Cypressを使った例")

```javascript
it("When doing smoke testing over all page, should load them all successfully", () => {
  // exemplified using Cypress but can be implemented easily
  // using any E2E suite
  cy.visit("https://mysite.com/home");
  cy.contains("Home");
  cy.visit("https://mysite.com/Login");
  cy.contains("Login");
  cy.visit("https://mysite.com/About");
  cy.contains("About");
});
```

</details>

<br/>

## ⚪️ 3.10 テストを、共同で使える生きたドキュメントとして公開する

:white_check_mark: **推奨：** テストには、信頼性を高めるだけでなく、アプリケーションの生きたドキュメントになるという魅力もあります。テストは技術の細部よりもプロダクトやUXの言葉で表されるため、適切なツールを使えば、開発者と顧客の認識をそろえるコミュニケーション手段になります。たとえば、処理の流れと期待する結果、つまりテスト計画を、人間が読みやすい言葉で記述できるフレームワークがあります。プロダクトマネージャーを含む関係者が読み、承認し、共同で更新できるようになれば、テストは生きた要件書になります。顧客が平易な言葉で受け入れ条件を定められるため、この手法は「受け入れテスト」とも呼ばれます。[BDD（振る舞い駆動開発）](https://en.wikipedia.org/wiki/Behavior-driven_development)を純粋な形で実践する方法です。代表的なフレームワークに、[JavaScript版もあるCucumber](https://github.com/cucumber/cucumber-js)があります。下の例を参照してください。似ていますが別の方法として、[Storybook](https://storybook.js.org/)ならUIコンポーネントを視覚的なカタログとして公開できます。フィルターのない表、複数行のある表、空の表など、各コンポーネントの状態を巡り、見た目とその状態の作り方を確認できます。プロダクト担当者にも役立ちますが、主にはコンポーネントを利用する開発者向けの、生きたドキュメントになります。

❌ **守らないと：** テストに多くの資源を投入したのに、その投資からさらに大きな価値を引き出せないのは、もったいないことです。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：cucumber-jsで、人間の言葉に近いテストを記述する

![Cucumberを使った例](https://img.shields.io/badge/🔨%20Example%20using%20Cucumber-blue.svg "Cucumberを使った例")

```text
This is how one can describe tests using cucumber: plain language that allows anyone to understand and collaborate

Feature: Twitter new tweet

  I want to tweet something in Twitter

  @focus
  Scenario: Tweeting from the home page
    Given I open Twitter home
    Given I click on "New tweet" button
    Given I type "Hello followers!" in the textbox
    Given I click on "Submit" button
    Then I see message "Tweet saved"
```

### :clap: 良い例：Storybookでコンポーネントの状態や入力を可視化する

![StoryBookを使った例](https://img.shields.io/badge/🔨%20Example%20using%20StoryBook-blue.svg "StoryBookを使った例")

![Storybookによるコンポーネントのカタログ](assets/story-book.jpg "Storybook")

</details>

<br/><br/>

## ⚪️ 3.11 自動化ツールで見た目の不具合を検出する

:white_check_mark: **推奨：** 変更時にUIのスクリーンショットを撮り、内容の重なりや表示崩れを検出する自動化ツールを設定しましょう。正しいデータが用意されているだけでなく、ユーザーに見やすく表示されていることも確認できます。この手法はまだ広く普及していません。テストというと機能を重視しがちですが、ユーザーが実際に体験するのは見た目です。端末の種類も多く、厄介なUIバグは簡単に見落とされます。無料ツールでも、スクリーンショットを生成・保存し、人が目視確認するための基本機能を備えたものがあります。小さなアプリケーションなら十分かもしれませんが、変更のたびに人手が必要という、手動テスト共通の弱点があります。一方、何を不具合とするかの明確な定義がないため、UIの問題を自動検出するのは困難です。そこで役立つのが「ビジュアルリグレッション」です。以前のUIと最新の変更を比較して差分を検出します。[Wraith](https://github.com/BBC-News/wraith)や[PhantomCSS](https://github.com/HuddleEng/PhantomCSS)など、OSSや無料のツールでも一部の機能を提供していますが、設定に相当の時間がかかる場合があります。[Applitools](https://applitools.com/)や[Percy.io](https://percy.io/)などの商用ツールは、導入を簡単にし、管理UI、通知、広告やアニメーションなどの「視覚的ノイズ」を除去した撮影、原因となったDOM・CSS変更の分析といった高度な機能も備えています。

<br/>

❌ **守らないと：** テストが100%成功し、すばやく読み込めて、内容も素晴らしいページでも、その半分が隠れて見えなければ、どれほど役立つでしょうか。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：内容は正しいのに表示が崩れている、典型的なビジュアルリグレッション

![表示が崩れたAmazonのページ](assets/amazon-visual-regression.jpeg "Amazonのページの表示崩れ")

<br/>

### :clap: 良い例：WraithでUIのスナップショットを撮影・比較する

![Wraithを使った例](https://img.shields.io/badge/🔨%20Example%20using%20Wraith-blue.svg "Wraithを使った例")

```
​# Add as many domains as necessary. Key will act as a label​

domains:
  english: "http://www.mysite.com"​

​# Type screen widths below, here are a couple of examples​

screen_widths:

  - 600​
  - 768​
  - 1024​
  - 1280​

​# Type page URL paths below, here are a couple of examples​
paths:
  about:
    path: /about
    selector: '.about'​
  subscribe:
      selector: '.subscribe'​
    path: /subscribe
```

### :clap: 良い例：Applitoolsでスナップショットの比較と高度な機能を利用する

![Applitoolsを使った例](https://img.shields.io/badge/🔨%20Example%20using%20AppliTools-blue.svg "Applitoolsを使った例") ![Cypressを使った例](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Cypressを使った例")

```javascript
import * as todoPage from "../page-objects/todo-page";

describe("visual validation", () => {
  before(() => todoPage.navigate());
  beforeEach(() => cy.eyesOpen({ appName: "TAU TodoMVC" }));
  afterEach(() => cy.eyesClose());

  it("should look good", () => {
    cy.eyesCheckWindow("empty todo list");
    todoPage.addTodo("Clean room");
    todoPage.addTodo("Learn javascript");
    cy.eyesCheckWindow("two todos");
    todoPage.toggleTodo(0);
    cy.eyesCheckWindow("mark as completed");
  });
});
```

</details>

<br/><br/>

<a id="section-4"></a>

# 第4章：テストの有効性を測る

<br/><br/>

## ⚪️ 4.1 安心して変更できるだけのカバレッジを確保する：80%程度が目安

:white_check_mark: **推奨：** テストの目的は、安心して素早く変更できるようにすることです。テストされているコードが多いほど、チームの安心感も増します。カバレッジは、テストがコードの何行、あるいは分岐や文のどれだけを通ったかを示します。では、どこまであれば十分でしょうか。10〜30%ではビルドの正しさを判断するには明らかに低すぎます。一方、100%を目指すと費用がかかり、重要な経路よりも、めったに使わない隅のコードに注意が向きかねません。正確には、アプリケーションの種類など多くの条件によります。次世代のAirbus A380を作るなら100%は必須ですが、漫画の画像を表示するサイトなら50%でも多すぎるかもしれません。適切な基準は状況次第だとするテストの専門家も、多くは80%を大まかな目安として挙げています。多くのアプリケーションに適した水準と考えられているためです（[Fowlerは「80%台後半から90%台」としています](https://martinfowler.com/bliki/TestCoverage.html)）。

実装のヒント：CIでカバレッジの下限を設定し、基準を満たさないビルドを止められます（[Jestの設定](https://jestjs.io/docs/en/configuration.html#collectcoverage-boolean)）。コンポーネントごとの下限も設定できます。下の例を参照してください。さらに、新しいコミットでカバレッジが下がったことを検出すると、開発者がテスト済みのコードを増やす、少なくとも減らさないようにする動機になります。ただし、カバレッジは量を測る指標の1つにすぎず、テストの確かさを判断するには不十分です。次の項目で示すように、見かけ上の数値を高くすることもできます。

<br/>

❌ **守らないと：** 安心感を得るには、裏付けとなる数値も必要です。システムの大半をテストしたと確認できなければ、不安が残り、変更の速度が落ちます。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 例：一般的なカバレッジレポート

![一般的なカバレッジレポート](assets/bp-18-yoni-goldberg-code-coverage.png "一般的なカバレッジレポート")

<br/>

### :clap: 良い例：Jestでコンポーネントごとにカバレッジを設定する

![Jestを使った例](https://img.shields.io/badge/🔨%20Example%20using%20Jest-blue.svg "Jestを使った例")

![Jestでコンポーネントごとにカバレッジを設定する](assets/bp-18-code-coverage2.jpeg "Jestのコンポーネント別カバレッジ設定")

</details>

<br/><br/>

## ⚪️ 4.2 カバレッジレポートで未テストの箇所や不自然な挙動を探す

:white_check_mark: **推奨：** 一般的なツールでは見つけにくく、気付かないうちに入り込む問題があります。明確なバグというより、深刻な影響を及ぼしかねない予想外の振る舞いです。たとえば、まったく、またはほとんど呼ばれていないコードがあるかもしれません。商品価格は常に`PricingCalculator`が設定していると思っていたのに、DBに1万件の商品があり、売上も多数あるにもかかわらず、一度も呼ばれていなかった、といったケースです。カバレッジレポートは、アプリケーションが想定どおりに動いているかを確かめる手掛かりになります。どんな種類のコードがテストされていないかもわかります。80%がテスト済みと聞くだけでは、重要な箇所が含まれるかはわかりません。レポートの生成は簡単です。本番またはテストでカバレッジを記録しながらアプリケーションを動かし、各箇所がどれくらい呼ばれたかを色分けしたレポートを見ます。時間を取って眺めると、思わぬ問題が見つかるかもしれません。
<br/>

❌ **守らないと：** どこが未テストかわからなければ、どこから問題が起こりそうかもわかりません。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：このカバレッジレポートのどこがおかしいか

QA環境でアプリケーションの利用状況を記録し、気になるログインの傾向を見つけた実例です。ヒントは、ログイン失敗の件数が不自然に多いことです。調査の結果、フロントエンドのバグが、バックエンドのログインAPIを繰り返し呼んでいたとわかりました。

![不自然に多いログイン失敗を示すカバレッジレポート](assets/bp-19-coverage-yoni-goldberg-nodejs-consultant.png "このカバレッジレポートのどこがおかしいか")

</details>

<br/><br/>

## ⚪️ 4.3 ミューテーションテストでロジックの検証範囲を測る

:white_check_mark: **推奨：** 従来のカバレッジ指標は、実態を表さないことがあります。カバレッジが100%でも、正しい応答を返す関数が1つもない、という状態がありえます。なぜでしょうか。測っているのはテストが通過したコード行であり、正しい応答をアサーションで確かめたかどうかではないからです。出張した人がパスポートのスタンプを見せても、仕事をした証明にはなりません。いくつかの空港とホテルを訪れたことがわかるだけです。

ミューテーションテストは、単に「通過した」コードではなく、実際に「検証した」コードの量を測ります。JavaScript用ライブラリの[Stryker](https://stryker-mutator.io/)は、次のように動きます。

(1) 意図的にコードを変え、「バグを埋め込み」ます。たとえば`newOrder.price===0`を`newOrder.price!=0`に変えます。この変更をミューテーションと呼びます。

(2) テストを実行します。すべて成功したら問題です。テストがバグを発見できておらず、このミューテーションは「生き残った」と呼ばれます。テストが失敗したら、狙いどおりです。ミューテーションを「検出した（killした）」ことになります。

すべて、または大半のミューテーションを検出できたとわかれば、通常のカバレッジよりも強い裏付けになります。導入にかかる時間は同程度です。
<br/>

❌ **守らないと：** カバレッジ85%なら、コードの85%にあるバグを検出できると思い込んでしまいます。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：カバレッジ100%、検証0%

![Strykerを使った例](https://img.shields.io/badge/🔨%20Example%20using%20Stryker-blue.svg "Strykerを使った例")

```javascript
function addNewOrder(newOrder) {
  logger.log(`Adding new order ${newOrder}`);
  DB.save(newOrder);
  Mailer.sendMail(newOrder.assignee, `A new order was places ${newOrder}`);

  return { approved: true };
}

it("Test addNewOrder, don't use such test names", () => {
  addNewOrder({ assignee: "John@mailer.com", price: 120 });
}); //Triggers 100% code coverage, but it doesn't check anything
```

<br/>

### :clap: 良い例：Strykerのレポートで、検出されなかったミューテーションを数え、実際には検証されていないコードを見つける

![Strykerによるミューテーションテストのレポート](assets/bp-20-yoni-goldberg-mutation-testing.jpeg "検出されなかったミューテーションから、未検証のコードを見つける")

</details>

<br/><br/>

## ⚪️ 4.4 テスト専用のリンターで、テストコードの問題を防ぐ

:white_check_mark: **推奨：** テストコードのパターンを検査し、問題を発見するためのESLintプラグインがあります。たとえば[eslint-plugin-mocha](https://www.npmjs.com/package/eslint-plugin-mocha)は、`describe()`の中ではなくグローバルにテストを書いた場合や、テストが[スキップされている](https://mochajs.org/#inclusive-tests)場合に警告します。スキップされたテストがあると、すべて成功したと誤解しかねません。同様に[eslint-plugin-jest](https://github.com/jest-community/eslint-plugin-jest)は、アサーションが1つもなく、何も確かめていないテストなどを警告できます。

<br/>

❌ **守らないと：** カバレッジ90%、テスト成功率100%を見て喜んだ後で、多くのテストにアサーションがなく、スイートもいくつもスキップされていたと気付くかもしれません。その誤った判断で、すでにデプロイしていなければよいのですが。

<br/>
<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：問題だらけのテストケース。幸い、リンターですべて検出できる

```javascript
describe("Too short description", () => {
  const userToken = userService.getDefaultToken() // *error:no-setup-in-describe, use hooks (sparingly) instead
  it("Some description", () => {});//* error: valid-test-description. Must include the word "Should" + at least 5 words
});

it.skip("Test name", () => {// *error:no-skipped-tests, error:error:no-global-tests. Put tests only under describe or suite
  expect("somevalue"); // error:no-assert
});

it("Test name", () => {// *error:no-identical-title. Assign unique titles to tests
});
```

</details>

<br/><br/>

<a id="section-5"></a>

# 第5章：CIと、そのほかの品質対策

<br/><br/>

## ⚪️ 5.1 リンターを充実させ、問題があればビルドを止める

:white_check_mark: **推奨：** リンターは少しの手間で多くの効果を得られます。5分ほど設定するだけで、入力中のコードを監視し、重大な問題を見つけてくれます。セミコロンの有無など、見た目だけを検査していた時代は終わりました。正しくないエラーの投げ方や、それによる情報の消失も検出できます。[ESLint standard](https://www.npmjs.com/package/eslint-plugin-standard)や[Airbnbスタイル](https://www.npmjs.com/package/eslint-config-airbnb)などの基本ルールに加え、専用のリンターも検討しましょう。[eslint-plugin-chai-expect](https://www.npmjs.com/package/eslint-plugin-chai-expect)はアサーションのないテストを、[eslint-plugin-promise](https://www.npmjs.com/package/eslint-plugin-promise?activeTab=readme)はresolveされず処理が進まないPromiseを検出できます。[eslint-plugin-security](https://www.npmjs.com/package/eslint-plugin-security?activeTab=readme)はDoS攻撃に悪用されうる正規表現を検出します。[eslint-plugin-you-dont-need-lodash-underscore](https://www.npmjs.com/package/eslint-plugin-you-dont-need-lodash-underscore)は、V8の標準機能で代替できるLodashのmapなどを使っていると警告してくれます。
<br/>

❌ **守らないと：** 本番でクラッシュが続くのに、ログにはスタックトレースがありません。原因は、誤ってErrorではないオブジェクトをthrowしていたことでした。頭を抱えたくなる状況ですが、5分のリンター設定で、この書き間違いを見つけられたかもしれません。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：誤ったオブジェクトをthrowすると、スタックトレースが残らない。ESLintなら本番に出る前に検出できる

![誤ったthrowを検出するESLint](assets/bp-21-yoni-goldberg-eslint.jpeg "Errorではないオブジェクトをthrowし、スタックトレースが失われる問題をESLintで検出する")

</details>

<br/><br/>

## ⚪️ 5.2 CIのチェックをローカルでも実行し、結果を早く受け取る

:white_check_mark: **推奨：** CIでテスト、リント、脆弱性検査などを行っているなら、その一連の処理を開発者がローカルでも実行できるようにしましょう。すぐに結果を得て、[フィードバックループ](https://www.gocd.org/2016/03/15/are-you-ready-for-continuous-delivery-part-2-feedback-loops/)を短くするためです。効果的なテストでは、(1)試す、(2)結果を知る、(3)修正する、という流れを何度も繰り返します。結果が早く返るほど、1つのモジュールに対して改善を重ねられます。逆に遅いと、1日にできる改善回数が減ります。チームが別の話題や作業、モジュールへ移ってしまい、元のモジュールを磨き込む気がなくなるかもしれません。

具体的には、[CircleCIのローカルCLI](https://circleci.com/docs/2.0/local-cli/)など、CIの処理をローカルで実行できるサービスがあります。[Wallaby](https://wallabyjs.com/)のように、試作中の開発者へ役立つテスト情報を返す商用ツールもあります。著者と同製品に利害関係はありません。単にpackage.jsonへ、テスト、リント、脆弱性検査などをまとめて実行するnpmスクリプトを追加してもよいでしょう。[concurrently](https://www.npmjs.com/package/concurrently)などを使えば、並列実行し、どれかが失敗したときに0以外の終了コードを返せます。開発者は`npm run quality`のような1コマンドで、すぐに結果を得られます。Gitフックを使い、品質チェックの失敗時にコミットを止めることも検討してください（[Husky](https://github.com/typicode/husky)が役立ちます）。
<br/>

❌ **守らないと：** コードを書いた翌日に結果が届くようでは、テストは開発の自然な一部ではなく、後から形式的に行う作業になります。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：npmスクリプトで品質チェックをまとめ、必要なときやpush時に並列実行する

```json
{
  "scripts": {
    "inspect:sanity-testing": "mocha **/**--test.js --grep \"sanity\"",
    "inspect:lint": "eslint .",
    "inspect:vulnerabilities": "npm audit",
    "inspect:license": "license-checker --failOn GPLv2",
    "inspect:complexity": "plato .",
    "inspect:all": "concurrently -c \"bgBlue.bold,bgMagenta.bold,yellow\" \"npm:inspect:quick-testing\" \"npm:inspect:lint\" \"npm:inspect:vulnerabilities\" \"npm:inspect:license\""
  },
  "husky": {
    "hooks": {
      "precommit": "npm run inspect:all",
      "prepush": "npm run inspect:all"
    }
  }
}
```

</details>

<br/><br/>

## ⚪️ 5.3 本番を忠実に再現した環境でE2Eテストを行う

:white_check_mark: **推奨：** E2Eテストは、どのCIパイプラインでも大きな課題です。関連するクラウドサービスを含め、本番と同じ一時環境をその場で作るのは、手間も費用もかかります。適切な妥協点を探しましょう。[Docker Compose](https://serverless.com/)なら、1つのテキストファイルで、同じコンテナーを使った隔離環境を作れます。ただし、ネットワークやデプロイ方式などの基盤は、実際の本番環境と異なります。[AWS Local](https://github.com/localstack/localstack)を組み合わせれば、AWSサービスのスタブも利用できます。[サーバーレス](https://serverless.com/)を採用しているなら、Serverless Frameworkや[AWS SAM](https://docs.aws.amazon.com/lambda/latest/dg/serverless_app.html)などで、FaaSのコードをローカルから呼び出せます。

Kubernetesのエコシステムは巨大で、新しいツールも頻繁に登場しますが、ローカル環境やCIで本番を再現するための、便利で標準的なツールはまだ定まっていません。1つの方法は、[Minikube](https://kubernetes.io/docs/setup/minikube/)や[MicroK8s](https://microk8s.io/)で小規模なKubernetesを動かすことです。本番に似た環境を、より少ない負担で用意できます。もう1つは、リモートの実際のKubernetes上でテストする方法です。[Codefresh](https://codefresh.io/)のようにKubernetesとの連携機能を備え、本物の環境でCIを実行しやすいサービスもあれば、独自スクリプトでリモートのKubernetesを操作できるサービスもあります。
<br/>

❌ **守らないと：** 本番とテストで異なる技術を使うと、2つのデプロイ方式を保守する必要があり、開発チームと運用チームの分断も続きます。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 例：Kubernetesクラスターをその場で作成するCIパイプライン（[出典：Dynamic Environments Kubernetes](https://container-solutions.com/dynamic-environments-kubernetes/)）

<pre name="38d9" id="38d9" class="graf graf--pre graf-after--p">deploy:<br>stage: deploy<br>image: registry.gitlab.com/gitlab-examples/kubernetes-deploy<br>script:<br>- ./configureCluster.sh $KUBE_CA_PEM_FILE $KUBE_URL $KUBE_TOKEN<br>- kubectl create ns $NAMESPACE<br>- kubectl create secret -n $NAMESPACE docker-registry gitlab-registry --docker-server="$CI_REGISTRY" --docker-username="$CI_REGISTRY_USER" --docker-password="$CI_REGISTRY_PASSWORD" --docker-email="$GITLAB_USER_EMAIL"<br>- mkdir .generated<br>- echo "$CI_BUILD_REF_NAME-$CI_BUILD_REF"<br>- sed -e "s/TAG/$CI_BUILD_REF_NAME-$CI_BUILD_REF/g" templates/deals.yaml | tee ".generated/deals.yaml"<br>- kubectl apply --namespace $NAMESPACE -f .generated/deals.yaml<br>- kubectl apply --namespace $NAMESPACE -f templates/my-sock-shop.yaml<br>environment:<br>name: test-for-ci</pre>

</details>

<br/><br/>

## ⚪️ 5.4 テストを並列実行する

:white_check_mark: **推奨：** 適切に作られたテストは、いつでも、ほぼ即座に結果を返してくれます。しかし、CPU負荷の高いユニットテストを500件、1つのスレッドで実行すると、時間がかかりすぎることがあります。幸い、[Jest](https://github.com/facebook/jest)、[AVA](https://github.com/avajs/ava)、[Mochaの拡張](https://github.com/yandex/mocha-parallel-tests)などのテストランナーやCI環境は、複数のプロセスにテストを分散し、待ち時間を大幅に減らせます。コンテナーをまたいで並列実行し、さらに短縮できるCIサービスもあります。ローカルの複数プロセスでも、クラウドのCLIから複数マシンを使う場合でも、各テストが別々のプロセスで動く可能性があるため、テストを独立させる必要があります。

❌ **守らないと：** pushから1時間後、すでに次の機能を書いているときにテスト結果が届くようでは、テストが軽視されやすくなります。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：Mochaの並列実行版とJestは、並列化によって従来のMochaを大きく上回る（[出典：JavaScript Test-Runners Benchmark](https://medium.com/dailyjs/javascript-test-runners-benchmark-3a78d4117b4)）

![Mochaの並列実行版とJestのベンチマーク](assets/bp-24-yonigoldberg-jest-parallel.png "並列化による高速化。出典：JavaScript Test-Runners Benchmark")

</details>

<br/><br/>

## ⚪️ 5.5 ライセンスと盗用を検査し、法的な問題を避ける

:white_check_mark: **推奨：** ライセンスや盗用は、今いちばん気になる問題ではないかもしれません。それでも10分で確認を追加できるなら、やっておきませんか。[license-checker](https://www.npmjs.com/package/license-checker)や、無料プランのある商用ツール[plagiarism-checker](https://www.npmjs.com/package/plagiarism-checker)などのnpmパッケージは、CIに簡単に組み込めます。制約の厳しいライセンスの依存パッケージや、Stack Overflowからコピーしたコードによる著作権侵害の疑いなどを調べられます。

❌ **守らないと：** 意図せず不適切なライセンスのパッケージを使ったり、商用コードをコピーしたりして、法的な問題に巻き込まれるかもしれません。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：依存パッケージのライセンスを検査する

```shell
# install license-checker in your CI environment or also locally
npm install -g license-checker

# ask it to scan all licenses and fail with exit code other than 0 if it found unauthorized license. The CI system should catch this failure and stop the build
license-checker --summary --failOn BSD
```

<br/>

![依存パッケージのライセンス検査結果](assets/bp-25-nodejs-licsense.png)

</details>

<br/><br/>

## ⚪️ 5.6 依存パッケージの脆弱性を継続的に検査する

:white_check_mark: **推奨：** Expressのように信頼されている依存パッケージにも、既知の脆弱性はあります。[npm audit](https://docs.npmjs.com/getting-started/running-a-security-audit)などのコミュニティのツールや、コミュニティ向け無料版もある商用ツール[Snyk](https://snyk.io/)を使えば、簡単に検査できます。どちらもCIからビルドごとに実行できます。

❌ **守らないと：** 専用ツールなしで脆弱性を避け続けるには、新しい脅威についての情報を常に追いかける必要があり、大変な手間になります。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 例：npm auditの結果

![npm auditの検査結果](assets/bp-26-npm-audit-snyk.png "npm auditの検査結果")

</details>

<br/><br/>

<a id="practice-5-7"></a>

## ⚪️ 5.7 依存パッケージの更新を自動化する

:white_check_mark: **推奨：** Yarnやnpmに新たにpackage-lock.jsonが導入され、重大な課題が生まれました。「地獄への道は善意で舗装されている」とは、このことです。今や既定ではパッケージが更新されません。`npm install`や`npm update`を使って何度も新しくデプロイしているチームでも、更新を取り込めないのです。その結果、よくても古い依存パッケージを使い続け、悪ければ脆弱なコードを使うことになります。package.jsonを手動で更新するか、[ncu](https://www.npmjs.com/package/npm-check-updates)などを手動実行するかは、開発者の注意と記憶に頼ってしまいます。より確実なのは、信頼できるバージョンの取得を自動化する方法です。万能な解決策はまだありませんが、自動化には次の2つの方向があります。

(1) 古い依存パッケージを含むビルドをCIで失敗させます。[`npm outdated`](https://docs.npmjs.com/cli/outdated)や`npm-check-updates（ncu）`を使えば、開発者に更新を促せます。

(2) コードを調べ、依存パッケージを更新するプルリクエストを自動で送る商用ツールを使います。残る問題は、どの頻度で更新するかです。パッチのたびに更新すると手間が増え、メジャー版の公開直後に更新すると、不安定な版を取り込むかもしれません。公開後の数日間で脆弱性が見つかるパッケージもあります（[eslint-scopeの事件](https://nodesource.com/blog/a-high-level-post-mortem-of-the-eslint-scope-security-incident/)を参照）。

有効な更新方針として、一定の待機期間を設ける方法があります。`@latest`より少し古い期間やバージョン差を許容し、その範囲を超えたら更新対象とします。たとえば、手元が1.3.1、公開版が1.3.8という状態です。
<br/>

❌ **守らないと：** 作者自身が危険と明示しているパッケージを、本番で動かし続けるかもしれません。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 例：[ncu](https://www.npmjs.com/package/npm-check-updates)を手動またはCIで実行し、最新版からどれだけ遅れているかを調べる

![ncuによる依存パッケージの更新確認](assets/bp-27-yoni-goldberg-npm.png "ncuを手動またはCIで実行し、最新版との差を調べる")

</details>

<br/><br/>

## ⚪️ 5.8 Node.jsに限らない、CIのそのほかの基本

:white_check_mark: **推奨：** このガイドはNode.jsに関係する助言、または少なくともNode.jsで例示できる助言を中心にしています。この項目では、Node.jsに限らない、よく知られたCIの基本をまとめます。

<ol><li>宣言的な構文を使います。多くのCIサービスではそれが唯一の選択肢ですが、古いJenkinsではコードやUIも使えます。</li><li>Dockerを標準でサポートするサービスを選びます。</li><li>失敗は早く検出しましょう。最も速いテストから実行します。リントやユニットテストなど、短い検査をまとめた「スモークテスト」のステップを用意し、コミットした人へすぐに結果を返します。</li><li>テスト、カバレッジ、ミューテーションテストの各レポートやログなど、ビルドの成果物を簡単に見渡せるようにします。</li><li>イベントごとにパイプラインやジョブを分け、ステップは共有します。たとえば機能ブランチへのコミット用とmasterへのプルリクエスト用で別々のジョブを作り、共通ステップを再利用します。多くのサービスには再利用の仕組みがあります。</li><li>ジョブの定義にシークレットを埋め込まないでください。シークレットストアやジョブの設定から取得します。</li><li>リリースビルドでバージョンを明示的に上げるか、少なくとも開発者が上げたことを確認します。</li><li>ビルドは一度だけ行い、Dockerイメージなどの同じ成果物に対して、すべての検査を実行します。</li><li>ビルド間で状態が持ち越されない一時環境でテストします。例外として考えられるのはnode_modulesのキャッシュ程度です。</li></ol>
<br/>

❌ **守らないと：** 長年蓄積された知恵を取り逃してしまいます。

<br/><br/>

<a id="practice-5-9"></a>

## ⚪️ 5.9 ビルドマトリックス：複数のNode.jsバージョンで同じCI手順を実行する

:white_check_mark: **推奨：** 品質チェックでは、試す範囲を広げるほど、思わぬ問題を早期に発見できる機会が増えます。再利用可能なパッケージを開発する場合や、顧客ごとに設定・Node.jsバージョンが異なる本番環境を運用する場合、CIはその組み合わせ全体でテストを実行する必要があります。たとえばMySQLを使う顧客とPostgresを使う顧客がいるとします。一部のCIサービスの「マトリックス」機能なら、MySQL・Postgresと、Node.js 8・9・10などのバージョンの全組み合わせでテストスイートを実行できます。テストなどの品質チェックがすでにあるなら、追加の実装は不要で、設定だけで対応できます。マトリックスを標準で備えないCIでも、拡張機能や設定の工夫で実現できる場合があります。
<br/>

❌ **守らないと：** テストを書くためにあれだけ苦労したのに、設定の違いだけでバグの侵入を許してしまってよいのでしょうか。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 例：Travis CIのビルド定義で、複数のNode.jsバージョンに同じテストを実行する

<pre name="f909" id="f909" class="graf graf--pre graf-after--p">language: node_js<br>node_js:<br>  - "7"<br>  - "6"<br>  - "5"<br>  - "4"<br>install:<br>  - npm install<br>script:<br>  - npm run test</pre>
</details>

<br/><br/>

# 制作チーム

## Yoni Goldberg

<br/>
<img width="480px" src="assets/yoni-goldberg.jpg" alt="著者 Yoni Goldberg"/>
<br/>

**役割：** 執筆

**紹介：** 独立したコンサルタントとして、Fortune 500企業から小さなスタートアップまで、JavaScript・Node.jsアプリケーションの改善を支援しています。何よりもテストに関心があり、その技術を極めたいと考えています。[Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices)の著者でもあります。

**📗 オンライン講座：** このガイドを気に入り、さらにテストの技術を磨きたい方は、著者の講座 [Testing Node.js & JavaScript From A To Z](https://www.testjavascript.com) をご覧ください。

<br/>

**リンク：**

- [🐦 Twitter](https://twitter.com/goldbergyoni/)
- [📞 お問い合わせ](https://testjavascript.com/contact-2/)
- [✉️ ニュースレター](https://testjavascript.com/newsletter//)

<br/>
<hr/>
<br/>

## [Bruno Scheufler](https://github.com/BrunoScheufler)

**役割：** 技術レビューと助言

全文の見直し、改善、リント、推敲を担当しました。

**紹介：** Node.jsとGraphQLを好む、フルスタックのWebエンジニアです。

<hr/>
<br/>

## [Ido Richter](https://github.com/idori)

**役割：** 構想、デザイン、助言

**紹介：** 経験豊富なフロントエンド開発者で、CSSの専門家。絵文字も大好きです。

## [Kyle Martin](https://github.com/js-kyle)

**役割：** プロジェクトの運営支援と、セキュリティ関連のプラクティスのレビュー

**紹介：** Node.jsのプロジェクトとWebアプリケーションのセキュリティに取り組むことを好んでいます。

## コントリビューター ✨

このリポジトリに貢献してくださった皆さんに感謝します。

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tbody>
    <tr>
      <td align="center"><a href="http://geospatialscott.blogspot.com/"><img src="https://avatars3.githubusercontent.com/u/1326248?v=4?s=100" width="100px;" alt="Scott Davis"/><br /><sub><b>Scott Davis</b></sub></a><br /><a href="#content-stdavis" title="執筆">🖋</a></td>
      <td align="center"><a href="https://github.com/AdrienRedon"><img src="https://avatars2.githubusercontent.com/u/5978436?v=4?s=100" width="100px;" alt="Adrien REDON"/><br /><sub><b>Adrien REDON</b></sub></a><br /><a href="#content-AdrienRedon" title="執筆">🖋</a></td>
      <td align="center"><a href="https://twitter.com/NoriSte"><img src="https://avatars0.githubusercontent.com/u/173663?v=4?s=100" width="100px;" alt="Stefano Magni"/><br /><sub><b>Stefano Magni</b></sub></a><br /><a href="#content-NoriSte" title="執筆">🖋</a></td>
      <td align="center"><a href="https://www.joer.im"><img src="https://avatars2.githubusercontent.com/u/47742486?v=4?s=100" width="100px;" alt="Yeoh Joer"/><br /><sub><b>Yeoh Joer</b></sub></a><br /><a href="#content-yjoer" title="執筆">🖋</a></td>
      <td align="center"><a href="http://jhonnymoreira.dev"><img src="https://avatars0.githubusercontent.com/u/2177742?v=4?s=100" width="100px;" alt="Jhonny Moreira"/><br /><sub><b>Jhonny Moreira</b></sub></a><br /><a href="#content-jhonnymoreira" title="執筆">🖋</a></td>
      <td align="center"><a href="https://github.com/Germanika"><img src="https://avatars2.githubusercontent.com/u/8846678?v=4?s=100" width="100px;" alt="Ian Germann"/><br /><sub><b>Ian Germann</b></sub></a><br /><a href="#content-Germanika" title="執筆">🖋</a></td>
      <td align="center"><a href="https://github.com/AbdelrahmanHafez"><img src="https://avatars3.githubusercontent.com/u/19984935?v=4?s=100" width="100px;" alt="Hafez"/><br /><sub><b>Hafez</b></sub></a><br /><a href="#content-AbdelrahmanHafez" title="執筆">🖋</a></td>
    </tr>
    <tr>
      <td align="center"><a href="http://www.ruxandrafediuc.com"><img src="https://avatars1.githubusercontent.com/u/11021586?v=4?s=100" width="100px;" alt="Ruxandra Fediuc"/><br /><sub><b>Ruxandra Fediuc</b></sub></a><br /><a href="#content-ruxandrafed" title="執筆">🖋</a></td>
      <td align="center"><a href="https://github.com/jacklee814"><img src="https://avatars0.githubusercontent.com/u/9951291?v=4?s=100" width="100px;" alt="Jack"/><br /><sub><b>Jack</b></sub></a><br /><a href="#content-jacklee814" title="執筆">🖋</a></td>
      <td align="center"><a href="https://www.petercarrero.com"><img src="https://avatars0.githubusercontent.com/u/231727?v=4?s=100" width="100px;" alt="Peter Carrero"/><br /><sub><b>Peter Carrero</b></sub></a><br /><a href="#content-aloyr" title="執筆">🖋</a></td>
      <td align="center"><a href="https://github.com/huhgawz"><img src="https://avatars3.githubusercontent.com/u/369338?v=4?s=100" width="100px;" alt="Huhgawz"/><br /><sub><b>Huhgawz</b></sub></a><br /><a href="#content-huhgawz" title="執筆">🖋</a></td>
      <td align="center"><a href="https://github.com/haakonmb"><img src="https://avatars1.githubusercontent.com/u/7099302?v=4?s=100" width="100px;" alt="Haakon Borch"/><br /><sub><b>Haakon Borch</b></sub></a><br /><a href="#content-haakonmb" title="執筆">🖋</a></td>
      <td align="center"><a href="https://jaimemendoza.com/"><img src="https://avatars3.githubusercontent.com/u/5395811?v=4?s=100" width="100px;" alt="Jaime Mendoza"/><br /><sub><b>Jaime Mendoza</b></sub></a><br /><a href="#content-jaimemendozadev" title="執筆">🖋</a></td>
      <td align="center"><a href="https://github.com/camerondunford"><img src="https://avatars0.githubusercontent.com/u/840612?v=4?s=100" width="100px;" alt="Cameron Dunford"/><br /><sub><b>Cameron Dunford</b></sub></a><br /><a href="#content-camerondunford" title="執筆">🖋</a></td>
    </tr>
    <tr>
      <td align="center"><a href="https://github.com/shadowspawn"><img src="https://avatars1.githubusercontent.com/u/15719847?v=4?s=100" width="100px;" alt="John Gee"/><br /><sub><b>John Gee</b></sub></a><br /><a href="#content-shadowspawn" title="執筆">🖋</a></td>
      <td align="center"><a href="https://github.com/aurelijusrozenas"><img src="https://avatars0.githubusercontent.com/u/3273544?v=4?s=100" width="100px;" alt="Aurelijus Rožėnas"/><br /><sub><b>Aurelijus Rožėnas</b></sub></a><br /><a href="#content-aurelijusrozenas" title="執筆">🖋</a></td>
      <td align="center"><a href="http://aaronshivers.com"><img src="https://avatars2.githubusercontent.com/u/42848750?v=4?s=100" width="100px;" alt="Aaron"/><br /><sub><b>Aaron</b></sub></a><br /><a href="#content-aaronshivers" title="執筆">🖋</a></td>
      <td align="center"><a href="https://tomdoes.tech/"><img src="https://avatars1.githubusercontent.com/u/8683577?v=4?s=100" width="100px;" alt="Tom Nagle"/><br /><sub><b>Tom Nagle</b></sub></a><br /><a href="#content-tomanagle" title="執筆">🖋</a></td>
      <td align="center"><a href="https://github.com/yvesyao"><img src="https://avatars0.githubusercontent.com/u/7723729?v=4?s=100" width="100px;" alt="Yves yao"/><br /><sub><b>Yves yao</b></sub></a><br /><a href="#content-yvesyao" title="執筆">🖋</a></td>
      <td align="center"><a href="https://github.com/Userbit"><img src="https://avatars1.githubusercontent.com/u/34487074?v=4?s=100" width="100px;" alt="Userbit"/><br /><sub><b>Userbit</b></sub></a><br /><a href="#content-Userbit" title="執筆">🖋</a></td>
      <td align="center"><a href="https://glaucialemos.netlify.com/"><img src="https://avatars0.githubusercontent.com/u/1631477?v=4?s=100" width="100px;" alt="Glaucia Lemos"/><br /><sub><b>Glaucia Lemos</b></sub></a><br /><a href="#maintenance-glaucia86" title="保守">🚧</a></td>
    </tr>
    <tr>
      <td align="center"><a href="https://twitter.com/koooge"><img src="https://avatars2.githubusercontent.com/u/7419215?v=4?s=100" width="100px;" alt="koooge"/><br /><sub><b>koooge</b></sub></a><br /><a href="#content-koooge" title="執筆">🖋</a></td>
      <td align="center"><a href="https://twitter.com/michalbiesiada"><img src="https://avatars0.githubusercontent.com/u/18367606?v=4?s=100" width="100px;" alt="Michal"/><br /><sub><b>Michal</b></sub></a><br /><a href="#content-mbiesiad" title="執筆">🖋</a></td>
      <td align="center"><a href="http://roywalker.me"><img src="https://avatars0.githubusercontent.com/u/611846?v=4?s=100" width="100px;" alt="roywalker"/><br /><sub><b>roywalker</b></sub></a><br /><a href="#content-roywalker" title="執筆">🖋</a></td>
      <td align="center"><a href="https://dangen-effy.github.io/"><img src="https://avatars3.githubusercontent.com/u/23185799?v=4?s=100" width="100px;" alt="dangen"/><br /><sub><b>dangen</b></sub></a><br /><a href="#content-dangen-effy" title="執筆">🖋</a></td>
      <td align="center"><a href="https://dev.to/mbiesiad"><img src="https://avatars1.githubusercontent.com/u/60202305?v=4?s=100" width="100px;" alt="biesiadamich"/><br /><sub><b>biesiadamich</b></sub></a><br /><a href="#content-biesiadamich" title="執筆">🖋</a></td>
      <td align="center"><a href="https://tarojsx.github.io"><img src="https://avatars3.githubusercontent.com/u/127009?v=4?s=100" width="100px;" alt="Yanlin Jiang"/><br /><sub><b>Yanlin Jiang</b></sub></a><br /><a href="#content-cncolder" title="執筆">🖋</a></td>
      <td align="center"><a href="https://github.com/sanguino"><img src="https://avatars2.githubusercontent.com/u/2077168?v=4?s=100" width="100px;" alt="sanguino"/><br /><sub><b>sanguino</b></sub></a><br /><a href="#content-sanguino" title="執筆">🖋</a></td>
    </tr>
    <tr>
      <td align="center"><a href="https://github.com/MorganGeek"><img src="https://avatars0.githubusercontent.com/u/3721240?v=4?s=100" width="100px;" alt="Morgan"/><br /><sub><b>Morgan</b></sub></a><br /><a href="#content-MorganGeek" title="執筆">🖋</a></td>
      <td align="center"><a href="https://luk4s.dev"><img src="https://avatars0.githubusercontent.com/u/8350985?v=4?s=100" width="100px;" alt="Lukas Bischof"/><br /><sub><b>Lukas Bischof</b></sub></a><br /><a href="https://github.com/goldbergyoni/javascript-testing-best-practices/commits?author=lukasbischof" title="テスト">⚠️</a> <a href="#content-lukasbischof" title="執筆">🖋</a></td>
      <td align="center"><a href="https://juanmaruiz.surge.sh"><img src="https://avatars2.githubusercontent.com/u/1837650?v=4?s=100" width="100px;" alt="JuanMa Ruiz"/><br /><sub><b>JuanMa Ruiz</b></sub></a><br /><a href="#content-JuanMaRuiz" title="執筆">🖋</a></td>
      <td align="center"><a href="https://luisangelorjr.com.br"><img src="https://avatars3.githubusercontent.com/u/22268900?v=4?s=100" width="100px;" alt="Luís Ângelo Rodrigues Jr."/><br /><sub><b>Luís Ângelo Rodrigues Jr.</b></sub></a><br /><a href="#content-luisangelorjr" title="執筆">🖋</a></td>
      <td align="center"><a href="https://jfernandezpe.wordpress.com/"><img src="https://avatars0.githubusercontent.com/u/12046620?v=4?s=100" width="100px;" alt="José Fernández"/><br /><sub><b>José Fernández</b></sub></a><br /><a href="#content-jfernandezpe" title="執筆">🖋</a></td>
      <td align="center"><a href="http://www.linkedin.com/in/AlejandroGutierrezB"><img src="https://avatars3.githubusercontent.com/u/56408597?v=4?s=100" width="100px;" alt="Alejandro Gutierrez Barcenilla"/><br /><sub><b>Alejandro Gutierrez Barcenilla</b></sub></a><br /><a href="#content-AlejandroGutierrezB" title="執筆">🖋</a></td>
      <td align="center"><a href="https://github.com/jasonandmonte"><img src="https://avatars1.githubusercontent.com/u/30088000?v=4?s=100" width="100px;" alt="Jason"/><br /><sub><b>Jason</b></sub></a><br /><a href="#content-jasonandmonte" title="執筆">🖋</a></td>
    </tr>
    <tr>
      <td align="center"><a href="https://github.com/otavionetoca"><img src="https://avatars.githubusercontent.com/u/11263232?v=4?s=100" width="100px;" alt="Otavio Araujo"/><br /><sub><b>Otavio Araujo</b></sub></a><br /><a href="https://github.com/goldbergyoni/javascript-testing-best-practices/commits?author=otavionetoca" title="テスト">⚠️</a> <a href="#content-otavionetoca" title="執筆">🖋</a></td>
      <td align="center"><a href="https://contributor.pw"><img src="https://avatars.githubusercontent.com/u/5027939?v=4?s=100" width="100px;" alt="Alex Ivanov"/><br /><sub><b>Alex Ivanov</b></sub></a><br /><a href="#content-contributorpw" title="執筆">🖋</a></td>
      <td align="center"><a href="https://github.com/YeeJone"><img src="https://avatars.githubusercontent.com/u/20400822?v=4?s=100" width="100px;" alt="Yiqiao Xu"/><br /><sub><b>Yiqiao Xu</b></sub></a><br /><a href="#content-YeeJone" title="執筆">🖋</a></td>
      <td align="center"><a href="https://github.com/yubinTW"><img src="https://avatars.githubusercontent.com/u/31545456?v=4?s=100" width="100px;" alt="YuBin, Hsu"/><br /><sub><b>YuBin, Hsu</b></sub></a><br /><a href="#translation-yubinTW" title="翻訳">🌍</a> <a href="https://github.com/goldbergyoni/javascript-testing-best-practices/commits?author=yubinTW" title="コード">💻</a></td>
      <td align="center"><a href="https://github.com/TREER00T"><img src="https://avatars.githubusercontent.com/u/76606342?v=4?s=100" width="100px;" alt="Ali Azmoodeh"/><br /><sub><b>Ali Azmoodeh</b></sub></a><br /><a href="#content-TREER00T" title="執筆">🖋</a></td>
      <td align="center"><a href="https://github.com/Saimon398"><img src="https://avatars.githubusercontent.com/u/71539667?v=4?s=100" width="100px;" alt="Alex Popov"/><br /><sub><b>Alex Popov</b></sub></a><br /><a href="#content-Saimon398" title="執筆">🖋</a></td>
      <td align="center"><a href="http://shramko.dev"><img src="https://avatars.githubusercontent.com/u/42001531?v=4?s=100" width="100px;" alt="Serhii Shramko"/><br /><sub><b>Serhii Shramko</b></sub></a><br /><a href="#content-Shramkoweb" title="執筆">🖋</a></td>
    </tr>
    <tr>
      <td align="center"><a href="https://github.com/yugoccp"><img src="https://avatars.githubusercontent.com/u/1724114?v=4?s=100" width="100px;" alt="Yugo Sakamoto"/><br /><sub><b>Yugo Sakamoto</b></sub></a><br /><a href="#content-yugoccp" title="執筆">🖋</a></td>
      <td align="center"><a href="https://yeovilhospital.co.uk/"><img src="https://avatars.githubusercontent.com/u/43814140?v=4?s=100" width="100px;" alt="Frazer Smith"/><br /><sub><b>Frazer Smith</b></sub></a><br /><a href="#content-Fdawgs" title="執筆">🖋</a></td>
      <td align="center"><a href="https://github.com/wralith"><img src="https://avatars.githubusercontent.com/u/75392169?v=4?s=100" width="100px;" alt="Wralith"/><br /><sub><b>Wralith</b></sub></a><br /><a href="#content-wralith" title="執筆">🖋</a></td>
      <td align="center"><a href="https://haranglog.tistory.com"><img src="https://avatars.githubusercontent.com/u/60910665?v=4?s=100" width="100px;" alt="Harang"/><br /><sub><b>Harang</b></sub></a><br /><a href="#content-saseungmin" title="執筆">🖋</a></td>
      <td align="center"><a href="https://github.com/rcanelav"><img src="https://avatars.githubusercontent.com/u/64812826?v=4?s=100" width="100px;" alt="rcanelav"/><br /><sub><b>rcanelav</b></sub></a><br /><a href="#content-rcanelav" title="執筆">🖋</a></td>
      <td align="center"><a href="https://github.com/drewrwilson"><img src="https://avatars.githubusercontent.com/u/4324656?v=4?s=100" width="100px;" alt="Drew Wilson"/><br /><sub><b>Drew Wilson</b></sub></a><br /><a href="#content-drewrwilson" title="執筆">🖋</a></td>
      <td align="center"><a href="https://github.com/XtLee"><img src="https://avatars.githubusercontent.com/u/30145777?v=4?s=100" width="100px;" alt="XtLee"/><br /><sub><b>XtLee</b></sub></a><br /><a href="#content-XtLee" title="執筆">🖋</a></td>
    </tr>
    <tr>
      <td align="center"><a href="https://www.smonn.se"><img src="https://avatars.githubusercontent.com/u/44818?v=4?s=100" width="100px;" alt="Simon Ingeson"/><br /><sub><b>Simon Ingeson</b></sub></a><br /><a href="#content-smonn" title="執筆">🖋</a></td>
      <td align="center"><a href="https://github.com/elfacu0"><img src="https://avatars.githubusercontent.com/u/30785449?v=4?s=100" width="100px;" alt="elfacu0"/><br /><sub><b>elfacu0</b></sub></a><br /><a href="#content-elfacu0" title="執筆">🖋</a></td>
      <td align="center"><a href="https://github.com/jorbelca"><img src="https://avatars.githubusercontent.com/u/76847923?v=4?s=100" width="100px;" alt="jorbelca"/><br /><sub><b>jorbelca</b></sub></a><br /><a href="#content-jorbelca" title="執筆">🖋</a></td>
    </tr>
  </tbody>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->
