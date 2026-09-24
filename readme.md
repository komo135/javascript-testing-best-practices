# JavaScriptテストのベストプラクティス — 日本語版

[英語原文](readme-en.md) · [翻訳元のリポジトリ](https://github.com/goldbergyoni/javascript-testing-best-practices)

Yoni Goldbergらによるガイドの日本語訳です。翻訳元は[コミット `63a2bb0` のREADME](https://github.com/goldbergyoni/javascript-testing-best-practices/blob/63a2bb07bb718d0a34a9c1249ef0df9b1266dad8/readme.md)です。

---

<img src="/assets/jtbp-header-blue.png" width="1920px" alt="JavaScriptテストのベストプラクティス"/>


<br/>

# 👇 このガイドを読むとテストの腕が上がる理由

<br/>

## 📗 50以上のベストプラクティスを徹底的に、余すところなく

JavaScriptとNode.jsの信頼性を、AからZまで扱うガイドです。数あるブログ記事、書籍、ツールの中から優れたものを数十点選び、その内容をまとめました。

## 🚢 基礎から1万マイル先まで踏み込む、上級者向けの内容

基礎をはるかに越えた旅に出ましょう。本番環境でのテスト、ミューテーションテスト、プロパティベーステストをはじめ、戦略的に使える実践的なツールを数多く取り上げます。このガイドを隅々まで読めば、あなたのテストの腕も、平均を大きく上回るところまで上がるはずです。

## 🌐 フルスタック：フロントエンド、バックエンド、CI、何でも

まずは、アプリケーションのどの層でも土台になる、共通のテストプラクティスを理解しましょう。その後は、好きな分野を掘り下げてください。フロントエンド・UI、バックエンド、CI、それとも全部でしょうか？

<br/>

### 執筆：Yoni Goldberg — JavaScript・Node.jsコンサルタント

<a id="course-announcement"></a>

### 👨‍🏫 うれしいお知らせです！ 2年間の収録と編集を経て、テストを隅々まで学べる講座を公開しました。[🎁 公開記念の特別価格は、終了まで48時間を切っています](https://testjavascript.com/)

<br/>

### 翻訳 — 自分の言語で読む

- 🇨🇳[中国語](readme-zh-CN.md) — 翻訳：[Yves yao](https://github.com/yvesyao)
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

- 自分の言語に翻訳したいですか？ Issueを作成してください 💜

<br/><br/>

## `目次`

#### [第0章：黄金律](#section-0)

ほかのすべての助言のもとになる、たった1つの助言（特別な1項目）

#### [第1章：テストの構造](#section-1)

基礎 — すっきりしたテストの組み立て方（12項目）

#### [第2章：バックエンド](#section-2)

バックエンドとマイクロサービスのテストを効率よく書く（13項目）

#### [第3章：フロントエンド](#section-3)

コンポーネントテストやE2Eテストを含む、Web UIのテストを書く（11項目）

#### [第4章：テストの有効性を測る](#section-4)

見張り役を見張る — テストの品質を測る（4項目）

#### [第5章：継続的インテグレーション](#section-5)

JavaScriptの世界でのCIの指針（9項目）

<br/><br/>

<a id="section-0"></a>

# 第0章：黄金律

<br/>

## ⚪️ 0 黄金律：リーンなテストを設計する

:white_check_mark: **すべきこと：**
テストコードは本番コードではありません。短く、徹底してシンプルで、フラットで、扱っていて楽しいものになるよう設計しましょう。テストを見ただけで、その意図がすぐにわかるようにしてください。

考えてみてください。私たちの頭は、本業である本番コードのことですでにいっぱいです。これ以上複雑なものを受け入れる「頭の空き容量」なんてありません。そんな私たちの哀れな脳に、さらに別のサブシステムまで詰め込もうとすれば、チームの動きは遅くなります。テストをする本来の目的に逆行してしまうのです。実際、多くのチームがここでテストを諦めてしまいます。

テストは、少しの投資で大きな価値をもたらしてくれる、親切なアシスタントや副操縦士にもなれるのです。科学によれば、人の脳には2つのシステムがあります。システム1は、空いた道路を車で走るような、苦労せずにできる活動を担います。システム2は、方程式を解くような、意識して取り組む複雑な作業を担います。テストはシステム1向けに設計してください。テストコードを見るときには、HTML文書を修正するくらい簡単に**感じられる**べきで、2×(17×24)を解くような気分になってはいけません。

そのためには、費用対効果が高く、高い投資収益率（ROI）を得られる手法、ツール、テスト対象を選び抜きます。必要な分だけテストし、その軽快さを保つよう努めましょう。場合によっては、一部のテストをやめ、信頼性と引き換えに俊敏さやシンプルさを取る価値さえあります。

![これ以上複雑なものを抱え込む余裕はない](/assets/headspace.png "これ以上複雑なものを抱え込む余裕はない")

以下の助言のほとんどは、この原則から導かれています。

### 始める準備はできましたか？

<br/><br/>

<a id="section-1"></a>

# 第1章：テストの構造

<br/>

## ⚪️ 1.1 テスト名に3つの要素を含める

:white_check_mark: **すべきこと：** テストレポートは、アプリケーションの現在の版が要件を満たしているかを、コードに詳しくない人にも伝えるべきです。読むのはテスターかもしれませんし、デプロイを担当するDevOpsエンジニアや、2年後のあなたかもしれません。そのためには、テストを要件の言葉で記述し、次の3つの要素を含めるのが最も効果的です。

(1) 何をテストするのか？ たとえば、ProductsService.addNewProductメソッド。

(2) どのような条件・シナリオで？ たとえば、メソッドに価格が渡されていない場合。

(3) 期待する結果は？ たとえば、新しい商品は承認されない。

<br/>

❌ **そうしないと：** デプロイが失敗しました。「商品を追加する」という名前のテストが落ちています。これで、いったい何が正しく動いていないのかわかりますか？

<br/>

**👇 補足：** 各項目にはコード例があり、図解が付いているものもあります。クリックすると開きます。
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

:white_check_mark: **すべきこと：** テストをArrange（準備）、Act（実行）、Assert（検証）の3つにはっきり分けます。頭文字を取ってAAAです。この構造に従えば、読み手はテストの段取りを理解するために、脳のCPUを使わずに済みます。

1つ目のA — Arrange：テストしたい状況を作るための準備をすべて行います。テスト対象のコンストラクターを呼び出してインスタンスを作る、DBにレコードを追加する、オブジェクトにモックやスタブを設定するなど、必要な準備のコードがここに入ります。

2つ目のA — Act：テスト対象を実行します。通常は1行のコードです。

3つ目のA — Assert：受け取った値が期待を満たすことを確かめます。通常は1行のコードです。

<br/>

❌ **そうしないと：** 本番コードを理解するのに何時間もかかるだけでなく、その日の仕事でいちばん簡単なはずのテストにまで、頭を悩ませることになります。

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

### :thumbsdown: アンチパターン：区切りのない一塊のコードは読み解きにくい

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

:white_check_mark: **すべきこと：** 宣言的なスタイルでテストを書けば、読み手は脳のCPUを1サイクルも回さずに、その意図をつかめます。条件分岐を詰め込んだ命令的なコードでは、理解するためにもっとCPUを回さなければなりません。自前のコードで判定するのではなく、`expect`や`should`を使い、人間の言葉に近い宣言的なBDDスタイルで期待を記述してください。ChaiやJestに欲しいアサーションがなく、それを何度も使うなら、[Jestのマッチャーを拡張する](https://jestjs.io/docs/en/expect#expectextendmatchers)か、[Chaiのプラグインを自作する](https://www.chaijs.com/guide/plugins/)ことを検討しましょう。
<br/>

❌ **そうしないと：** チームが書くテストは減り、面倒なテストには`.skip()`という飾りが付くようになります。

<br/>

<details><summary>✏ <b>コード例</b></summary><br/>

![Mocha & Chaiを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Mocha & Chaiを使った例") ![Jestを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Jestを使った例")

### :thumbsdown: アンチパターン：何をするテストか知るだけで、短くもない命令的なコードに目を通さなければならない

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

### :clap: 良い例：この宣言的なテストなら、読むのも楽々

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

:white_check_mark: **すべきこと：** 内部実装のテストは、ほとんど得るものがないのに大きな負担がかかります。コードやAPIが正しい結果を返しているのに、内部で**どう**動いたかを確かめるためにさらに3時間を費やし、その壊れやすいテストを保守し続ける必要があるでしょうか。公開された振る舞いを確認すれば、非公開の実装も暗黙のうちにテストされます。テストが失敗するのは、出力が間違っているなど、何か問題があるときだけです。この方法は`振る舞いのテスト（behavioral testing）`とも呼ばれます。逆に内部実装をテストするホワイトボックス方式では、コンポーネントにどんな結果を求めるかではなく、細かな実装に目が向いてしまいます。結果は正しくても、ちょっとしたリファクタリングでテストが壊れるかもしれません。これでは保守の負担が大幅に増えます。
<br/>

❌ **そうしないと：** テストが[オオカミ少年](https://en.wikipedia.org/wiki/The_Boy_Who_Cried_Wolf)になり、誤った警報を叫び続けます。たとえば、非公開変数の名前を変えただけでテストが落ちます。やがてCIの通知が無視されるようになるのも当然です。そしていつか、本物のバグまで見過ごされてしまいます……。

<br/>
<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：正当な理由もなく内部実装をテストしている

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

## ⚪️ 1.5 適切なテストダブルを選ぶ：モックを避け、スタブとスパイを使う

:white_check_mark: **すべきこと：** テストダブルはアプリケーションの内部実装と結び付くため、必要悪です。それでも、大きな価値をもたらすものもあります（[テストダブルのおさらい：モック、スタブ、スパイの違い](https://martinfowler.com/articles/mocksArentStubs.html)）。

テストダブルを使う前に、単純なことを1つ自問してください。「これでテストしようとしている機能は、要件書に書かれている、あるいは書かれうるものだろうか？」そうでなければ、ホワイトボックステストのにおいがします。

たとえば、決済サービスが停止したときにアプリケーションが適切に振る舞うかをテストしたいなら、そのサービスをスタブに置き換えて「応答なし」の状態を起こし、テスト対象が正しい値を返すことを確かめます。これは、ある状況でのアプリケーションの振る舞い・応答・結果を確認しています。サービス停止時にメールが送られたかを、スパイで確かめてもよいでしょう。これも「決済を保存できなければメールを送る」という、要件書にありそうな振る舞いの確認です。反対に、決済サービスをモックに置き換え、正しいJavaScriptの型で呼び出されたかを確かめると、テストはアプリケーションの機能とは関係がなく、頻繁に変わりがちな内部の事情に集中してしまいます。
<br/>

❌ **そうしないと：** リファクタリングのたびに、コード中のモックをすべて探して直さなければなりません。テストは頼れる味方ではなく、重荷になります。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：モックが内部実装に焦点を当てている

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

### :clap: 良い例：スパイは要件をテストするために使う。その結果として、内部実装に触れることが避けられなくなるだけ

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

## 📗 これらのプラクティスを動画で学びたいですか？

### 私のオンライン講座 [Testing Node.js & JavaScript From A To Z](https://www.testjavascript.com) をご覧ください

<br/><br/>

<a id="practice-1-6"></a>

## ⚪️ 1.6 「foo」で済ませず、現実的な入力データを使う

:white_check_mark: **すべきこと：** 本番のバグは、ある特定の予想外の入力で見つかることがよくあります。テストの入力が現実的であるほど、早くバグを見つける確率も上がります。[Chance](https://github.com/chancejs/chancejs)や[Faker](https://www.npmjs.com/package/faker)のような専用ライブラリを使い、本番データの多様さや形をまねた疑似データを生成してください。こうしたライブラリなら、実際にありそうな電話番号、ユーザー名、クレジットカード情報、会社名、さらには「lorem ipsum」の文章まで作れます。生成したデータをランダム化してテスト対象をさらに試したり、本番環境の実データを取り込んだりするテストも書けます。ただし、ユニットテストの代わりではなく、追加する形で使います。もう一段先へ進みたいですか？ 次の項目、プロパティベーステストをご覧ください。
<br/>

❌ **そうしないと：** 「Foo」のような作り物の入力では、開発中のテストは全部緑になり、誤った安心感を与えます。ところが本番で、ハッカーが「@3e2ddsf . ##’ 1 fdsfds . fds432 AAAA」のような厄介な文字列を渡したら、赤になるかもしれません。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：非現実的なデータのおかげで通ってしまうテストスイート

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

### :clap: 良い例：現実的な入力をランダムに生成する

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

## ⚪️ 1.7 プロパティベーステストで、多くの入力の組み合わせを試す

:white_check_mark: **すべきこと：** 通常、各テストでは入力のサンプルをいくつか選びます。現実のデータに似た形式にしても（[「foo」で済ませない](#practice-1-6)を参照）、試すのは`method('', true, 1)`や`method("string", false, 0)`といった、わずかな組み合わせです。しかし本番では、引数を5つ取るAPIに何千通りもの組み合わせが渡され、そのうち1つでプロセスが落ちるかもしれません（[ファジング](https://en.wikipedia.org/wiki/Fuzzing)も参照）。たった1つのテストで、異なる入力を1,000通り自動的に送り、どの入力でコードが正しい応答を返せなくなるかを突き止められたらどうでしょう？ プロパティベーステストは、まさにそれをする手法です。考えられる入力の組み合わせをすべてテスト対象に送り、思わぬバグに出会う機会を増やします。たとえば`addNewProduct(id, name, isDiscount)`というメソッドがあれば、ライブラリが数値・文字列・真偽値の組み合わせをいくつも作り、`(1, "iPhone", false)`、`(2, "Galaxy", true)`などで呼び出します。[js-verify](https://github.com/jsverify/jsverify)や、ドキュメントがずっと充実している[testcheck](https://github.com/leebyron/testcheck-js)を使えば、MochaやJestなど、好みのテストランナーでプロパティベーステストを実行できます。追記：Nicolas Dubienがコメント欄で[fast-check](https://github.com/dubzzz/fast-check#readme)も勧めてくれました。追加機能があり、活発に保守されているようです。
<br/>

❌ **そうしないと：** 無意識のうちに、うまく動くコードパスだけを通る入力を選んでしまいます。残念ながら、それではバグを見つける手段としてのテストの効果が下がります。

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

## ⚪️ 1.8 スナップショットが必要なら、短いものをインラインで使う

:white_check_mark: **すべきこと：** [スナップショットテスト](https://jestjs.io/docs/en/snapshot-testing)が必要なときは、3〜7行程度の短く、焦点を絞ったスナップショットだけを使いましょう。外部ファイルではなく、[インラインスナップショット](https://jestjs.io/docs/en/snapshot-testing#inline-snapshots)としてテストの中に含めます。この方針を守れば、テストだけを読んで意味がわかり、壊れにくくもなります。

一方、従来のスナップショットの解説やツールは、コンポーネントの描画結果のマークアップやAPIのJSON応答といった大きなファイルを外部に保存し、テストのたびに取得した結果と比べるよう勧めています。たとえば、書き手が読んでも検討してもいない1,000行・3,000個の値に、テストを暗黙のうちに結び付けてしまうわけです。何がまずいのでしょうか？ テストが失敗する理由が1,000個もできてしまうのです。1行変わるだけでスナップショットは一致しなくなりますし、そんな変更はしょっちゅう起こります。どのくらい頻繁に？ 空白、コメント、ちょっとしたCSSやHTMLの変更のたびです。それだけではありません。テストは1,000行が変わっていないかを調べているだけなので、名前を見ても失敗の原因はわかりません。しかも、自分で調べて確かめられなかった長い文書を「正解」として受け入れるよう、書き手を仕向けてしまいます。どれも、焦点が定まらず、一度にあれもこれも確かめようとする、わかりにくいテストの症状です。

ただし、長い外部スナップショットが許容されるケースもいくつかあります。値を取り除いてフィールドに注目し、データではなくスキーマを検証するときや、取得する文書がほとんど変わらないときです。
<br/>

❌ **そうしないと：** UIテストが落ちました。コードは正しそうですし、画面も1ピクセルの狂いもなく描画されています。いったい何が？ スナップショットテストが、保存した文書と今の結果との差を見つけたのです。Markdownに空白が1文字増えていました……。

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

### :clap: 良い例：期待する内容が見えていて、焦点も絞られている

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

## ⚪️ 1.9 コードをコピーする。ただし必要なものだけ

:white_check_mark: **すべきこと：** テストの結果に関わる情報はすべて含め、それ以上は含めないようにします。たとえば、入力として100行のJSONを組み立てるテストを考えてください。毎回それを貼り付けるのは面倒です。かといって、外部の`transferFactory.getJSON()`に切り出すと、テストが曖昧になります。データが見えなければ、「なぜステータス400を返すはずなのか？」と、結果と原因を結び付けにくいからです。名著『xUnit Test Patterns』は、このパターンを「ミステリーゲスト」と名付けました。見えない何かがテストの結果を左右しているのに、それが何なのかわからない状態です。繰り返し現れる長い部分を外に出し、**同時に**、どの情報がこのテストで重要なのかを明示すれば、もっとよくできます。先ほどの例なら、`transferFactory.getJSON({sender: undefined})`のように引数で重要な点を示します。これなら、senderフィールドが空だからバリデーションエラーなどの適切な結果を期待しているのだと、読み手はすぐにわかるはずです。
<br/>

❌ **そうしないと：** 500行のJSONを貼り付ければ、読めない、保守できないテストになります。全部外へ出せば、何をしているのかわかりにくい、曖昧なテストになります。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：原因がすべて外部の巨大なJSONに隠れていて、テストが失敗する理由がわからない

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

### :clap: 良い例：なぜその結果になるのか、テスト自身が示している

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

## ⚪️ 1.10 エラーをcatchせず、発生を期待する

:white_check_mark: **すべきこと：** ある入力でエラーが起きることを確かめるとき、try-catch-finallyを使い、catch節に入ったかをアサーションで調べるのは、よい方法に見えるかもしれません。ところが結果は、下の例のように不格好で長いテストになります。単純なはずのテストの意図も、期待する結果も、その陰に隠れてしまいます。

もっとすっきり書くには、Chaiの専用アサーション`expect(method).to.throw`を1行使います。Jestなら`expect(method).toThrow()`です。例外に、エラーの種類を示すプロパティが含まれていることも、必ず確かめてください。単なる汎用的なエラーでは、アプリケーションはユーザーをがっかりさせるメッセージを出すくらいしかできません。
<br/>

❌ **そうしないと：** CIのレポートなど、テストの結果から何が問題だったのかを読み取るのが難しくなります。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：try-catchでエラーの発生を確かめようとする、長いテストケース

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

### :clap: 良い例：人が読んですぐわかる期待の記述。QA担当者や技術に詳しいPMにも伝わるかもしれない

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

:white_check_mark: **すべきこと：** テストの種類に応じて、実行する場面を変える必要があります。短時間で済む、I/Oを伴わないスモークテストは、開発者がファイルを保存・コミットするときに。完全なE2Eテストは、通常、新しいプルリクエストが出されたときに、といった具合です。`#cold`、`#api`、`#sanity`などのキーワードでタグを付ければ、テスト実行ツールでgrepして、必要なものだけを実行できます。たとえばMochaでsanityグループだけを実行するなら、`mocha --grep 'sanity'`です。
<br/>

❌ **そうしないと：** 開発者が少し変更するたびに、何十回もDBへ問い合わせるものまで含めて全テストを動かすと、ひどく時間がかかって、開発者がテストを実行しなくなってしまうことがあります。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：「#cold-test」とタグ付けして、高速なテストだけを実行できるようにする。Coldとは、I/Oを伴わず、開発者がコードを書いている最中でも頻繁に実行できる、短時間のテストのこと

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

:white_check_mark: **すべきこと：** たまに読む人でも要件やテストしているシナリオをすぐに理解できるよう、テストスイートに構造を持たせましょう。テストは最高のドキュメントです。よくある方法は、テストを少なくとも2つの`describe`ブロックで囲むことです。1つ目にはテスト対象の名前を、2つ目にはシナリオや独自のカテゴリといった、もう一段の分類を指定します。下のコード例と画面を参照してください。テストレポートも格段に読みやすくなります。カテゴリをつかみ、見たい箇所を詳しく調べ、失敗したテストの関係も読み取れます。テストが多いスイートでも、開発者がコードをたどりやすくなります。ほかにも、[given-when-then](https://github.com/searls/jasmine-given)や[RITE](https://github.com/ericelliott/riteway)などの構造を検討できます。

<br/>

❌ **そうしないと：** 階層のない長いテスト一覧を前に、読み手は主要なシナリオや失敗したテストの共通点を知るために、長文を読み流さなければなりません。100件中7件が失敗した場合を考えてみてください。平坦な一覧では、失敗した各テストの文章を読んで、どう関係しているのか調べる必要があります。階層的なレポートなら、その7件がすべて同じフローやカテゴリに属しているとわかるかもしれません。何が根本原因なのか、少なくともどこにあるのかを、すぐに見当が付きます。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：テスト対象の名前とシナリオでスイートを構成すると、下のような見やすいレポートになる

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

![階層化されたテストレポート](assets/hierarchical-report.png)

<br/>

### :thumbsdown: アンチパターン：平坦なテスト一覧では、ユーザーストーリーや失敗したテスト同士の関係がつかみにくい

![Mochaを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Jest-blue.svg "Mochaを使った例")

```javascript
test("Then the response status should decline", () => {});

test("Then it should send email", () => {});

test("Then there should not be a new transfer record", () => {});
```

![平坦なテストレポート](assets/flat-report.png)

<br/>

</details>

<br/><br/>

## ⚪️ 1.13 テスト全般で守りたい、そのほかの基本

:white_check_mark: **すべきこと：** この記事は、Node.jsに関係する、あるいは少なくともNode.jsで例を示せるテストの助言を中心にしています。ただ、この項目ではNode.jsに限らない、よく知られた助言をいくつかまとめます。

[TDDの原則](https://www.sm-cloud.com/book-review-test-driven-development-by-example-a-tldr/)を学び、実践してください。多くの人にとって非常に有益ですが、自分のやり方に合わなくても、気後れしないでください。そう感じるのはあなただけではありません。[レッド・グリーン・リファクタリング](https://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html)の流れで、コードより先にテストを書くことを検討しましょう。1つのテストでは、必ず1つのことだけを確かめます。バグを見つけたら、直す前に、そのバグを今後検出できるテストを書きます。各テストは、緑にする前に最低1回は失敗させてください。モジュールは、まずテストを満たす簡単なコードをさっと書くところから始め、少しずつリファクタリングして本番で使える水準まで仕上げます。パスやOSなど、環境への依存も避けてください。
<br/>

❌ **そうしないと：** 何十年もかけて集められた、珠玉の知恵を逃してしまいます。

<br/><br/>

<a id="section-2"></a>

# 第2章：バックエンドのテスト

## ⚪️ 2.1 テストのポートフォリオを充実させる：ユニットテストとピラミッドの先を見る

:white_check_mark: **すべきこと：** [テストピラミッド](https://martinfowler.com/bliki/TestPyramid.html)は、10年以上前のものですが、今も役立つ優れたモデルです。3種類のテストを示し、大半の開発者のテスト戦略に影響を与えています。その一方で、魅力的な新しいテスト手法がいくつも登場しているのに、テストピラミッドの陰に隠れてしまっています。マイクロサービス、クラウド、サーバーレスと、この10年に起きた劇的な変化を考えてみてください。かなり古い1つのモデルで、*あらゆる*種類のアプリケーションに対応できるものなのでしょうか？ テストの世界も、新しい手法を受け入れることを考えるべきではないでしょうか？

誤解しないでください。2019年でも、テストピラミッド、TDD、ユニットテストは強力で、多くのアプリケーションにはおそらく最適です。ただ、ほかのモデルと同じように、いくら有用でも[間違っている場合はある](https://en.wikipedia.org/wiki/All_models_are_wrong)はずです。たとえば、多数のイベントをKafkaやRabbitMQのようなメッセージバスへ取り込み、データウェアハウスに流し、最後に分析用UIから問い合わせるIoTアプリケーションを考えてください。連携が中心で、ロジックがほとんどないアプリケーションに、テスト予算の50%を使ってユニットテストを書くべきでしょうか？ ボット、暗号資産、Alexaスキルと、アプリケーションの種類が増えるほど、テストピラミッドが最適ではない場面も増えていきます。

テストのポートフォリオを充実させ、もっと多くの種類のテストを知るときです。次の項目から、そのための案をいくつか紹介します。テストピラミッドなどのモデルを意識しつつ、目の前の現実の問題に合ったテストを選びましょう。「おや、APIが壊れている。それなら利用者主導のコントラクトテストを書こう！」という具合です。リスク分析をもとにポートフォリオを組む投資家のように、テストも分散させてください。どこで問題が起こりそうかを見極め、そのリスクを抑える予防策を選びます。

ひと言注意を。ソフトウェアの世界のTDD論争は、典型的な誤った二者択一に陥りがちです。どこにでも使えと説く人もいれば、悪魔だと思っている人もいます。何でも絶対だと言う人は、誰であれ間違っています :]

<br/>

❌ **そうしないと：** 驚くほど投資収益率の高いツールを取り逃します。ファジング、リント、ミューテーションテストなどには、10分で効果が得られるものもあります。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：Cindy Sridharanが素晴らしい記事「Testing Microservices — the same way」で提案する、多様なテストのポートフォリオ

![多様なテストのポートフォリオ](assets/bp-12-rich-testing.jpeg "Cindy Sridharanが記事『Testing Microservices — the sane way』で提案する、多様なテストのポートフォリオ")

**☺️ 例：** [YouTube：「ユニットテストの先へ：注目のNode.jsテスト5種類」（2018年、Yoni Goldberg）](https://www.youtube.com/watch?v=-2zP494wdUY&feature=youtu.be)

<br/>

![3つの要素を含むテスト名](assets/bp-12-Yoni-Goldberg-Testing.jpeg "3つの要素を含むテスト名")

</details>

<br/><br/>

## ⚪️ 2.2 コンポーネントテストが、いちばんの相棒になるかもしれない

:white_check_mark: **すべきこと：** 1つのユニットテストで確認できるのは、アプリケーションのごく一部です。全体をカバーするには費用がかかります。反対に、E2Eテストは簡単に広範囲をカバーできますが、結果が不安定で、実行も遅くなります。それなら、ユニットテストより大きく、E2Eテストより小さい、バランスの取れたテストを書いてはどうでしょうか？ コンポーネントテストは、テスト界の隠れた実力者です。実行速度は適度で、TDDパターンも使え、現実に即した広いカバレッジを得られます。両方のよいところを取れるのです。

コンポーネントテストでは、マイクロサービスを1つの「単位」として扱います。APIを相手にテストし、そのマイクロサービス自身に属するものは何もモックにしません。たとえばDBは実物か、少なくともそのDBのインメモリ版を使います。一方、ほかのマイクロサービスへの呼び出しなど、外部のものはすべてスタブにします。こうすれば、実際にデプロイするものを、アプリケーションの外側から内側へとテストし、妥当な時間で大きな確信を得られます。

[コンポーネントテストの正しい書き方だけを扱った、詳しいガイドも用意しています](https://github.com/testjavascript/nodejs-integration-tests-best-practices)。

<br/>

❌ **そうしないと：** 何日もかけてユニットテストを書いた後で、システムの20%しかカバーできていないと気付くかもしれません。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：Supertestなら、同じプロセス内でExpress APIを呼び出せる。速く、複数の層をカバーできる

![Mochaを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Mocha-blue.svg "Mochaを使った例")

![Supertestによるコンポーネントテスト](assets/bp-13-component-test-yoni-goldberg.png "Supertestなら、同じプロセス内でExpress APIを呼び出せる。速く、複数の層をカバーできる")

</details>

<br/><br/>

## ⚪️ 2.3 コントラクトテストで、新しいリリースがAPIを壊さないことを確かめる

:white_check_mark: **すべきこと：** あなたのマイクロサービスには複数のクライアントがいて、互換性を保つために複数のバージョンを動かしているとします。これでみんな満足です。ところが、あるフィールドを変えた途端に、大問題！ そのフィールドに頼っていた重要なクライアントが怒り出します。これが連携の世界の「キャッチ22」、つまり逃れがたいジレンマです。サーバー側が、さまざまなクライアントの期待をすべて考慮するのはとても大変です。一方、リリース日を握っているのはサーバー側なので、クライアント側もテストができません。この契約の問題を和らげる手法には、単純なものから、多機能なぶん習得にも時間がかかるものまであります。簡単でお勧めできる方法は、API提供側が、JSDocやTypeScriptなどでAPIの型を記述したnpmパッケージを公開することです。利用側はこのライブラリを取り込めば、コーディング中に入力補完や検証を利用できます。もっと凝った方法が[PACT](https://docs.pact.io/)です。PACTは、この手続きを仕組みにするために、思い切った発想を持ち込みました。テスト計画を定義するのはサーバーではなく、クライアントです。しかも、定義するのは……サーバーのテストなのです！ PACTはクライアントの期待を記録し、「ブローカー」という共有の場所に置けます。サーバーはその期待を取得し、ビルドのたびにPACTライブラリで実行して、破られた契約、つまり満たされていないクライアントの期待を検出します。こうすれば、サーバーとクライアントのAPIの食い違いをビルドやCIの段階ですべて見つけられ、悩みの種をずいぶん減らせるかもしれません。
<br/>

❌ **そうしないと：** 待っているのは、くたくたになる手動テストか、デプロイへの恐怖です。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：

![PACTを使った例](https://img.shields.io/badge/🔧%20Example%20using%20PACT-blue.svg "PACTを使った例")

![コントラクトテストの流れ](assets/bp-14-testing-best-practices-contract-flow.png)

</details>

<br/><br/>

## ⚪️ 2.4 ミドルウェアを切り離してテストする

:white_check_mark: **すべきこと：** ミドルウェアはシステムの小さな部分にすぎず、テストには動作中のExpressサーバーが必要だとして、テストを避ける人が多くいます。どちらも間違いです。ミドルウェアは小さくても、すべて、または大半のリクエストに影響しますし、`req`と`res`というJavaScriptオブジェクトを受け取る純粋な関数として簡単にテストできます。ミドルウェアの関数を呼び、`req`・`res`とのやり取りを、たとえば[Sinon](https://www.npmjs.com/package/sinon)のスパイで監視して、正しい操作をしたか確かめるだけです。[node-mock-http](https://www.npmjs.com/package/node-mocks-http)なら、さらに一歩進んで、`req`・`res`オブジェクトの生成とその振る舞いの監視までできます。たとえば、`res`に設定されたHTTPステータスが期待どおりかを検証できます。下の例をご覧ください。
<br/>

❌ **そうしないと：** Expressのミドルウェアにバグがあるということは、すべて、または大半のリクエストにバグがあるということです。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：ネットワーク通信も、Express全体を起こすこともせず、ミドルウェアだけをテストする

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

:white_check_mark: **すべきこと：** 静的解析ツールを使えば、客観的な方法でコードの品質を改善し、保守しやすい状態に保てます。CIのビルドに組み込み、コードの不吉なにおいを見つけたら中断することもできます。通常のリントに対する主な強みは、複数のファイルをまたいで品質を調べられること（重複の検出など）、高度な解析ができること（コードの複雑度など）、コードの問題の履歴と改善状況を追えることです。使えるツールの例に、[SonarQube](https://www.sonarqube.org/)（[スター](https://github.com/SonarSource/sonarqube)4,900以上）や[Code Climate](https://codeclimate.com/)（[スター](https://github.com/codeclimate/codeclimate)2,000以上）があります。

協力：[Keith Holliday](https://github.com/TheHollidayInn)

<br/>

❌ **そうしないと：** コードの品質が低ければ、バグと性能はいつまでも問題になります。どんな新しいライブラリや最先端の機能でも、解決してはくれません。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：複雑なメソッドを見つけられる商用ツール、Code Climate

![CodeClimateを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Code%20Climate-blue.svg "CodeClimateを使った例")

![Code Climateによる複雑なメソッドの検出](assets/bp-16-yoni-goldberg-quality.png "複雑なメソッドを見つけられる商用ツール、Code Climate")

</details>

<br/><br/>

<a id="practice-2-6"></a>

## ⚪️ 2.6 Node.js特有のカオスに備えられているか確かめる

:white_check_mark: **すべきこと：** 不思議なことに、ソフトウェアのテストはほとんどがロジックとデータのことばかりです。でも、最悪の出来事の中には、インフラに起因し、しかも影響を抑えるのがひどく難しいものがあります。プロセスのメモリがいっぱいになったら、あるいはサーバーやプロセスが死んだら、何が起こるか試したことはありますか？ APIが50%遅くなったら、監視システムは気付くでしょうか？ こうした厄介な事態をテストし、影響を和らげるために、Netflixで[カオスエンジニアリング](https://principlesofchaos.org/)が生まれました。アプリケーションがカオスにどれだけ耐えられるかを試すことへの理解を広め、そのためのフレームワークやツールを提供するのが狙いです。有名なツールの1つ、[Chaos Monkey](https://github.com/Netflix/chaosmonkey)は、サーバーをランダムに停止させます。それでもユーザーへのサービスを続けられ、1台のサーバーに依存していないことを確かめるためです。Podを停止させるKubernetes版の[kube-monkey](https://github.com/asobti/kube-monkey)もあります。ただ、これらはすべてホスティングやプラットフォームの層で動きます。Node.jsそのもののカオスを起こして試したいときはどうでしょう？ 捕捉されていないエラー、処理されていないPromiseの拒否、V8のメモリが上限の1.7GBまで埋まったときにNode.jsのプロセスがどう対処するか、イベントループがたびたびブロックされてもUXは満足できるものか、といったことです。このために、私は[node-chaos](https://github.com/i0natan/node-chaos-monkey)（アルファ版）を書きました。Node.jsにまつわる、さまざまなカオスを起こせます。
<br/>

❌ **そうしないと：** 逃げ道はありません。マーフィーの法則が、あなたの本番環境を容赦なく襲います。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：node-chaosにNode.jsのさまざまないたずらをさせ、アプリケーションがカオスにどれだけ耐えられるかを試す

![node-chaosでアプリケーションの耐性を試す](assets/bp-17-yoni-goldberg-chaos-monkey-nodejs.png "node-chaosはNode.jsのさまざまないたずらを起こし、アプリケーションのカオスへの耐性を試せる")

</details>

<br/>

## ⚪️ 2.7 グローバルなフィクスチャやシードを避け、テストごとにデータを追加する

:white_check_mark: **すべきこと：** 黄金律（項目0）に従えば、各テストは自分専用のDBレコードを追加し、それだけを操作するべきです。テスト同士の結び付きを防ぎ、流れも理解しやすくなります。現実には、性能を上げようとして、テスト前にDBへ共通データを投入することがよくあります。「テストフィクスチャ」とも呼ばれるこの方法は、その原則に反しています。もちろん性能は気にすべきことですが、改善する手段はあります。「コンポーネントテスト」の項目を参照してください。それよりも、テストの複雑さのほうがずっとつらい問題で、たいていの場合は、ほかの事情より優先して考えるべきです。各テストケースが、必要なDBレコードを明示的に追加し、そのレコードだけを操作するようにしてください。性能がどうしても重大な問題になるなら、問い合わせのようにデータを変更しないテストスイートだけに共通データを投入するのが、折り合いの付け方かもしれません。
<br/>

❌ **そうしないと：** いくつかのテストが落ち、デプロイが中止されました。これからチームの貴重な時間を使うことになります。「バグだろうか？ 調べよう。……ああ、どうやら2つのテストが同じシードデータを書き換えていたらしい」。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：テストが独立しておらず、グローバルなフックがDBに投入する共通データに依存している

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

### :clap: 良い例：テストの外を見に行かずに済む。各テストが、自分専用のデータを操作している

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

## ⚪️ 2.8 データをいつ削除するか決める：全テスト後（推奨）か、各テスト後か

:white_check_mark: **すべきこと：** テストでDBをいつ空にするかによって、テストの書き方は決まります。現実的な選択肢は、すべてのテストの後に削除するか、個々のテストの後に削除するかの2つです。後者なら、毎回まっさらなテーブルから始められ、開発者には便利です。テスト開始時にほかのレコードがないので、どのデータを問い合わせているか確実にわかりますし、アサーションで行数を数えたくなるかもしれません。ただし、大きな欠点があります。マルチプロセスで動かすと、テスト同士が干渉しやすいのです。プロセス1がテーブルを空にしているまさにその瞬間、プロセス2が問い合わせて失敗します。プロセス1に、いきなりDBを消されてしまったからです。そのうえ、失敗したテストの原因も追いにくくなります。DBをのぞいても、レコードは残っていません。

もう1つは、全テストファイルの実行後に削除する方法です。1日1回でもかまいません！ この方法では、既存のレコードが入った同じDBを、すべてのテストとプロセスで使います。互いの足を踏まないよう、各テストは自分でレコードを追加し、その特定のレコードだけを操作しなければなりません。レコードが追加されたか確かめたい？ ほかにも何千ものレコードがあるものとして、自分が追加したものを明示的に検索してください。削除されたか確かめたい？ テーブルが空だと決めつけず、そのレコードがないことを調べてください。この方法には強みがいくつかあります。そのままマルチプロセスで使えますし、何が起きたかを調べたいときも、データは消えずに残っています。人工的に空にしたDBではなく、レコードがたくさん入ったDBを使うので、バグに出会う機会も増えます。[詳しい比較表はこちらです](https://github.com/testjavascript/nodejs-integration-tests-best-practices/blob/master/graphics/db-clean-options.png)。
<br/>

❌ **そうしないと：** レコードを分離したり削除したりする方針がなければ、テスト同士が足を踏み合います。トランザクションで対処する方法はリレーショナルDBでしか使えず、内部にもトランザクションがあると複雑になりがちです。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: すべてのテストが終わってから削除する。毎回削除する必要はない。テスト中のデータが多いほど、本番の条件に近付く

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

## ⚪️ 2.9 HTTPインターセプターで、コンポーネントを外の世界から隔離する

:white_check_mark: **すべきこと：** 外向きのHTTPリクエストをすべて捕捉し、望む応答を返すことで、連携先のHTTP APIを実際には呼ばずに、テスト対象のコンポーネントを隔離します。この仕事にはNockがぴったりです。外部サービスの振る舞いを、使いやすい構文で定義できます。隔離は、ノイズや遅さを防ぐためにも必要ですが、何より、さまざまなシナリオや応答を再現するために欠かせません。優れたフライトシミュレーターは、澄んだ青空を描くものではなく、嵐や混乱を安全に体験させてくれるものです。これは、外の世界を巻き込まず、常に1つのコンポーネントに集中すべきマイクロサービス構成で、ますます重要になります。テストダブル、つまりモックで外部サービスを模擬することもできますが、純粋なブラックボックステストを保つには、デプロイするコードには触れず、ネットワーク層で操作するほうがよいでしょう。隔離の弱点は、連携先の変更や、2つのサービス間の認識違いに気付けないことです。少数のコントラクトテストやE2Eテストで、必ず補ってください。
<br/>

❌ **そうしないと：** 呼び出し側がローカルに配置できる代替版を、通常はDockerで提供しているサービスもあります。準備は楽になり、実行も速くなりますが、いろいろな応答の再現には役立ちません。「サンドボックス」環境を提供するサービスもあります。本物を呼んでも課金や副作用が発生しないため、外部サービスを用意する煩わしさは減りますが、これもさまざまなシナリオの再現はできません。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 外部コンポーネントへの通信を止めれば、シナリオを再現でき、ノイズも最小限に抑えられる

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

## ⚪️ 2.10 応答のスキーマをテストする：自動生成されるフィールドがあるときは特に

:white_check_mark: **すべきこと：** 特定の値を検証できないなら、必須フィールドの存在と型を確かめます。応答には、日付や連番のように、テストを書く時点では予測できない動的な値を持つ、重要なフィールドが含まれることがあります。APIの契約で、そのフィールドはnullにならず、正しい型を持つと約束しているなら、必ずテストしなければなりません。大半のアサーションライブラリは型の検証に対応しています。応答が小さければ、下のコード例のように、返された値と型を同じアサーションで確かめてください。OpenAPI文書（Swagger）に照らして応答全体を検証する方法もあります。ほとんどのテストランナーには、API応答をドキュメントと照合するコミュニティ製の拡張があります。


<br/>

❌ **そうしないと：** コードやAPIの呼び出し側が、IDや日付などの動的なフィールドを当てにしているのに、それが応答に含まれず、契約を破ってしまいます。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 動的な値のフィールドが存在し、正しい型であることを確かめる

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

## ⚪️ 2.11 外部連携のコーナーケースやカオスを確かめる

:white_check_mark: **すべきこと：** 連携を調べるときは、通常の成功・失敗のパターンだけで終わらせないでください。HTTP 500などのエラー応答に加え、応答の遅延やタイムアウトといったネットワーク層の異常も試します。そうすれば、タイムアウト後に正しい処理へ進む、危うい競合状態がない、再試行用のサーキットブレーカーがあるなど、さまざまな通信状況にコードが耐えられることを確かめられます。実績のあるインターセプターなら、ときどき失敗する不安定なサービスなど、多様なネットワークの振る舞いを簡単に再現できます。HTTPクライアントの既定のタイムアウト値が、模擬した応答時間より長いことを検知して、実際には待たず、その場でタイムアウト例外を投げることさえできます。


<br/>

❌ **そうしないと：** テストは全部通ります。ところが外部サービスが例外的な応答を返すと、本番だけがクラッシュしたり、エラーを正しく報告できなかったりします。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 通信障害が起きても、サーキットブレーカーが窮地を救ってくれることを確かめる

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

:white_check_mark: **すべきこと：** テストを計画するときは、典型的な処理が生む5種類の結果をカバーすることを考えてください。テストがAPI呼び出しなどの操作を起こすと、何らかの反応があります。意味のある何かが起きるので、そこをテストする必要があるのです。注目したいのは、内部でどう動くかではありません。外から見えて、ユーザーに影響しうる結果です。こうした結果や反応は、5つに分けられます。

• 応答 — テストがAPIなどを通じて操作を行い、応答を受け取ります。ここで調べるのは、応答データの正しさ、スキーマ、HTTPステータスです。

• 新しい状態 — 操作した後には、**外部からアクセスできる**何らかのデータが変更されているでしょう。

• 外部呼び出し — 操作した後に、アプリケーションがHTTPなどを通じて外部コンポーネントを呼ぶことがあります。SMSやメールの送信、クレジットカードへの課金などです。

• メッセージキュー — 一連の処理の結果が、キューに入るメッセージになることもあります。

• 可観測性 — エラーや重要な業務イベントなど、監視しなければならないものがあります。トランザクションが失敗したとき、期待するのは正しい応答だけではありません。適切なエラー処理と、ログやメトリクスへの正しい記録も必要です。その情報が直接届く相手は、とても重要な利用者です。運用担当者、つまり本番のSREや管理者です。


<br/><br/>

<a id="section-3"></a>

# 第3章：フロントエンドのテスト

## ⚪️ 3.1 UIと機能を切り離す

:white_check_mark: **すべきこと：** コンポーネントのロジックをテストするとき、UIの細部はノイズです。データそのものに集中できるよう、切り離すべきです。具体的には、見た目の実装に結び付きすぎない、抽象化した方法でマークアップから必要なデータを取り出します。HTMLやCSSの見た目ではなく、そのデータだけを検証し、実行を遅くするアニメーションは無効にします。描画をやめて、サービス、アクション、ストアなど、UIの裏側だけをテストしたくなるかもしれません。しかし、それでは実際とは違う、架空のテストになってしまいます。正しいデータがそもそもUIに届いていないケースも、見つけられません。

<br/>

❌ **そうしないと：** 計算したデータは10ミリ秒で用意できているのに、無関係な凝ったアニメーションのせいで、テスト全体は500ミリ秒かかるかもしれません。100件なら1分です。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：UIの細部を切り離す

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

### :thumbsdown: アンチパターン：アサーションにUIの細部とデータが混ざっている

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

:white_check_mark: **すべきこと：** HTML要素は、CSSセレクターとは違い、見た目が変わっても残りそうな属性、たとえばフォームのラベルで取得してください。対象の要素にそうした属性がなければ、`test-id-submit-button`のようなテスト専用の属性を作ります。こうすれば、見た目の変更で機能やロジックのテストが壊れなくなるだけでなく、この要素と属性はテストに使っているので削除してはいけない、とチーム全体にはっきり伝わります。

<br/>

❌ **そうしないと：** 多数のコンポーネント、ロジック、サービスにまたがるログイン機能をテストしようとしています。スタブもスパイも準備し、Ajax呼び出しも隔離しました。何もかも完璧に見えます。ところが、デザイナーがdivのCSSクラスを`thick-border`から`thin-border`に変えただけで、テストが落ちてしまいます。

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

## ⚪️ 3.3 できる限り、完全に描画したコンポーネントで、実際に近いテストをする

:white_check_mark: **すべきこと：** 無理のない規模であれば、ユーザーと同じように、コンポーネントを外側からテストしてください。UIを完全に描画して操作し、描画されたUIが期待どおりに振る舞うことを確かめます。モックも、部分的な描画も、シャローレンダリングも避けてください。そうした方法では細部が欠けてバグを見逃すおそれがあり、テストが内部実装をいじるため、保守も難しくなります（[「ブラックボックステストに徹する」](#practice-1-4)を参照）。子コンポーネントの1つが、たとえばアニメーションによって大幅に実行を遅くしたり、準備を複雑にしたりする場合は、その子を明示的に代替物へ置き換えることを検討します。

とはいえ、注意も必要です。この方法がうまくいくのは、適度な数の子を持つ、小規模から中規模のコンポーネントです。子が多すぎるコンポーネントを完全に描画すると、テストが失敗した理由、つまり根本原因を追いにくくなりますし、遅すぎることもあります。そういう場合は、その大きな親には少数のテストだけを書き、子に対するテストを増やしてください。

<br/>

❌ **そうしないと：** 非公開メソッドを呼び、内部状態を調べるようなテストでは、コンポーネントの実装をリファクタリングするたびに、全テストも直さなければなりません。それだけの保守を引き受ける余裕が、本当にありますか？

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

### :thumbsdown: アンチパターン：シャローレンダリングで、実際の構成をモックに置き換えてしまう

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

## ⚪️ 3.4 sleepせず、フレームワークの非同期イベント対応を使う。高速化も試みる

:white_check_mark: **すべきこと：** テスト対象の処理がいつ終わるかは、わからないことが多いものです。たとえば、アニメーションのために要素がなかなか現れない場合です。そんなときは`setTimeout`などでsleepせず、多くのプラットフォームが用意している、より確実な方法を使ってください。[Cypressの`cy.request('url')`](https://docs.cypress.io/guides/references/best-practices.html#Unnecessary-Waiting)のように操作の完了を待てるライブラリもあれば、[@testing-library/domの`wait(expect(element))`](https://testing-library.com/docs/guide-disappearance)のような待機APIを備えるものもあります。APIなどの遅いリソースをスタブにし、応答のタイミングを決められるようにしてから、コンポーネントを明示的に再描画するほうが、すっきりする場合もあります。sleepする外部コンポーネントに依存しているなら、[時計を早送りする](https://jestjs.io/docs/en/timer-mocks)方法も役立つかもしれません。sleepは、テストを遅くするか、待ち時間を短くしすぎて危うくするかのどちらかなので、避けるべきパターンです。sleepやポーリングを避けられず、テストフレームワークにも支援機能がないときは、[wait-for-expect](https://www.npmjs.com/package/wait-for-expect)などのnpmライブラリで、ある程度確実な待機を実装できます。
<br/>

❌ **そうしないと：** 長くsleepすれば、テストは桁違いに遅くなります。短くしようとすると、テスト対象の応答が間に合わず、失敗します。結局、不安定さと遅さのどちらを取るか、という話になってしまいます。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：非同期処理が終わるまで解決しない、E2E用のAPI（Cypress）

![Cypressを使った例](https://img.shields.io/badge/🔨%20Example%20using%20Cypress-blue.svg "Cypressを使った例")
![react-testing-libraryを使った例](https://img.shields.io/badge/🔧%20Example%20using%20React%20Testing%20Library-blue.svg "react-testing-libraryを使った例")

```javascript
// using Cypress
cy.get("#show-products").click(); // navigate
cy.wait("@products"); // wait for route to appear
// this line will get executed only when the route is ready
```

### :clap: 良い例：DOM要素を待ってくれるテストライブラリ

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

### :thumbsdown: アンチパターン：自前のsleep処理

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

## ⚪️ 3.5 コンテンツがネットワーク越しにどう配信されるかを監視する

![Lighthouseを使った例](https://img.shields.io/badge/🔧%20Example%20using%20Google%20LightHouse-blue.svg "Lighthouseを使った例")

✅ **すべきこと：** 実際のネットワークでページの読み込みが最適化されているか、能動的に監視する仕組みを入れてください。ページの読み込みが遅い、バンドルがminifyされていないなど、UXに関わる問題も含みます。検査ツールには事欠きません。[Pingdom](https://www.pingdom.com/)、AWS CloudWatch、[GCP Stackdriver](https://cloud.google.com/monitoring/uptime-checks/)のような基本的なツールなら、サーバーが生きていて、妥当なSLAの範囲で応答するかを簡単に監視できます。ただ、それでは起こりうる問題の表面をなぞっているだけです。[Lighthouse](https://developers.google.com/web/tools/lighthouse/)や[PageSpeed](https://developers.google.com/speed/pagespeed/insights/)など、フロントエンドに特化したツールで、もっと詳しく分析するほうがよいでしょう。目を向けるべきなのは、ユーザーに現れる症状です。ページの読み込み時間、[意味のある内容が描画されるまでの時間](https://scotch.io/courses/10-web-performance-audit-tips-for-your-next-billion-users-in-2018/fmp-first-meaningful-paint)、[ページが操作可能になるまでの時間（TTI）](https://calibreapp.com/blog/time-to-interactive/)など、UXに直接響く指標を見ます。そのうえで、コンテンツの圧縮、最初の1バイトが届くまでの時間、画像の最適化、適切なDOMサイズ、SSLなど、技術的な原因も調べられます。こうした詳しい監視は、開発中やCIの一部として、そして何より、本番のサーバーやCDNに対して24時間365日、行うことを勧めます。

<br/>

❌ **そうしないと：** UIをあれほど丁寧に作り、機能テストは100%通り、バンドルにも工夫を凝らしたのに、CDNの設定ミスでひどく遅く、使いにくいとわかったら、がっかりするはずです。

<br/>

<details><summary>✏ <b>コード例</b></summary>

### :clap: 良い例：Lighthouseによるページ読み込みの検査レポート

![Lighthouseによるページ読み込みの検査レポート](/assets/lighthouse2.png "Lighthouseによるページ読み込みの検査レポート")

</details>

<br/>

<a id="practice-3-6"></a>

## ⚪️ 3.6 バックエンドAPIなど、不安定で遅いリソースはスタブにする

:white_check_mark: **すべきこと：** 普段のテスト、つまりE2Eではないテストを書くときは、バックエンドAPIのように、自分の責任も制御も及ばないリソースを巻き込まず、スタブなどのテストダブルを使ってください。具体的には、APIを実際に呼ぶ代わりに、[Sinon](https://sinonjs.org/)や[testdouble](https://www.npmjs.com/package/testdouble)などのライブラリで応答をスタブに置き換えます。いちばんの利点は、結果の不安定さを防げることです。テストやステージングのAPIは、性質上、それほど安定しているものではありません。**あなたの**コンポーネントは正しく動いていても、ときどきテストを失敗させます。本番環境もテスト用ではなく、通常はリクエストが制限されます。スタブなら、データが見つからない、APIがエラーを投げるといった、コンポーネントの振る舞いを左右するさまざまな状況を再現できます。最後に、これも重要ですが、ネットワーク通信はテストを大幅に遅くします。

<br/>

❌ **そうしないと：** 平均的なテストは長くても数ミリ秒ですが、一般的なAPI呼び出しは100ミリ秒を超えます。各テストが約20倍遅くなる計算です。

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

## ⚪️ 3.7 システム全体を通すE2Eテストは、ごく少数だけにする

:white_check_mark: **すべきこと：** E2E（エンドツーエンド）は、通常、実ブラウザーでUIだけをテストすることを指します（[3.6参照](#practice-3-6)）。一方で、実際のバックエンドも含め、システム全体にまたがるテストを指す人もいます。後者のテストは非常に有益です。やり取りするデータのスキーマに対する認識の違いで起きる、フロントエンドとバックエンドの連携バグを確認できるからです。マイクロサービスAがBに誤ったメッセージを送るような、バックエンド同士の連携問題や、デプロイの失敗を見つけるにも有効です。バックエンドのE2Eテストには、[Cypress](https://www.cypress.io/)や[Puppeteer](https://github.com/GoogleChrome/puppeteer)のようなUI向けのものほど、使いやすく成熟したフレームワークがありません。こうしたテストの欠点は、多数のコンポーネントをそろえた環境を作る費用と、何よりその壊れやすさです。50個のマイクロサービスがあれば、たった1つが失敗するだけでE2E全体が失敗します。ですから、この手法は控えめに使い、おそらく1〜10件ほどにとどめるべきです。とはいえ、少数のE2Eテストでも、狙っているデプロイや連携の不具合は見つけられるはずです。本番に似たステージング環境での実行を勧めます。

<br/>

❌ **そうしないと：** UIの機能テストに大きな労力をかけたのに、バックエンドから返るペイロード、つまりUIが扱うデータのスキーマが想定とまるで違うことに、かなり後になって気付くかもしれません。

<br/>

## ⚪️ 3.8 ログイン情報を再利用してE2Eテストを速くする

:white_check_mark: **すべきこと：** 実際のバックエンドを使い、API呼び出しに有効なユーザートークンが必要なE2Eテストでは、リクエストごとにユーザーを作ってログインするほど分離しても、割に合いません。代わりに、全テストの実行前、つまりbefore-allフックで一度だけログインし、ローカルにトークンを保存して、各リクエストで使い回します。これは、リソースを共有せずテストを独立させる、という基本原則に反するように見えます。その心配はもっともですが、E2Eでは実行速度が重要です。各テストの前に1〜3回APIを呼ぶだけで、実行時間はひどく長くなりえます。認証情報を再利用するからといって、同じユーザーレコードを操作する必要はありません。支払い履歴のテストなどでユーザーのデータに依存するなら、そのデータは必ずテストの中で作り、ほかのテストと共有しないでください。バックエンドを代替物にできることも忘れずに。フロントエンドに集中するテストなら、隔離してバックエンドAPIをスタブにするほうがよいかもしれません（[3.6参照](#practice-3-6)）。

<br/>

❌ **そうしないと：** 200件のテストケースがあり、ログインに100ミリ秒かかるとすれば、同じログインの繰り返しだけで20秒を使います。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：before-eachではなく、before-allでログインする

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

## ⚪️ 3.9 サイトマップを巡るだけのE2Eスモークテストを1つ用意する

:white_check_mark: **すべきこと：** 本番の監視と開発中の簡単な動作確認のために、サイトのすべて、または大半のページを回り、どれも壊れていないことを確かめるE2Eテストを1つ実行してください。こうしたテストは書くのも保守するのも簡単なのに、機能、ネットワーク、デプロイなど、あらゆる種類の失敗を検出できるため、投資に対する見返りが大きいのです。ほかのスモークテストや簡易確認は、これほど確かでも網羅的でもありません。たとえば、本番のトップページにpingするだけの運用チームもいますし、統合テストを大量に実行していても、パッケージングやブラウザーの問題を見つけられない開発者もいます。言うまでもありませんが、スモークテストは機能テストの代わりではありません。いち早く煙を見つける検知器の役目を果たすだけです。

<br/>

❌ **そうしないと：** 何もかも完璧に見え、全テストが成功し、本番のヘルスチェックも正常です。それでも、Paymentコンポーネントのパッケージングに問題があり、`/Payment`だけ描画されないかもしれません。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：全ページを巡るスモークテスト

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

:white_check_mark: **すべきこと：** テストには、アプリケーションの信頼性を上げるほかにも、魅力的な使い道があります。生きたドキュメントにするのです。テストは本来、技術の細部よりもプロダクトやUXの言葉で語るものです。適切なツールを使えば、開発者と顧客を含む関係者の認識をそろえる、優れたコミュニケーションの道具になります。たとえば、人が読める言葉で処理の流れと期待する結果、つまりテスト計画を表現できるフレームワークがあります。プロダクトマネージャーを含む誰もが読んで承認し、一緒に作業できれば、そのテストは生きた要件書になります。顧客が平易な言葉で受け入れ条件を定められるため、この手法は「受け入れテスト」とも呼ばれます。これが、最も純粋な形の[BDD（振る舞い駆動テスト）](https://en.wikipedia.org/wiki/Behavior-driven_development)です。これを可能にする人気のフレームワークの1つが、[JavaScript版もあるCucumber](https://github.com/cucumber/cucumber-js)です。下の例をご覧ください。似ていますが違う使い道として、[Storybook](https://storybook.js.org/)もあります。UIコンポーネントを視覚的なカタログとして公開し、各コンポーネントのさまざまな状態を見て回れます。たとえば、フィルターのない表、複数行のある表、行のない表を表示し、それぞれの見た目と、その状態の作り方を確かめられます。プロダクト担当者にも魅力的でしょうが、主には、そのコンポーネントを使う開発者にとっての生きたドキュメントです。

❌ **そうしないと：** テストにこれだけの人手や時間をかけたのに、その投資を生かして大きな価値を得ないのは、もったいないことです。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：cucumber-jsで、人が読める言葉でテストを記述する

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

### :clap: 良い例：Storybookで、コンポーネントとそのさまざまな状態・入力を可視化する

![StoryBookを使った例](https://img.shields.io/badge/🔨%20Example%20using%20StoryBook-blue.svg "StoryBookを使った例")

![Storybook](assets/story-book.jpg "Storybook")

</details>

<br/><br/>

## ⚪️ 3.11 自動化ツールで見た目の問題を検出する

:white_check_mark: **すべきこと：** 変更があったときにUIのスクリーンショットを撮り、内容の重なりや表示崩れなどを見つける自動化ツールを設定してください。正しいデータが用意されているだけでなく、ユーザーがそれを無理なく見られることも確かめられます。この手法は、まだ広く使われていません。私たちはテストというと機能に目を向けがちですが、ユーザーが体験するのは見た目です。これだけ多くの種類の端末があると、厄介なUIのバグは簡単に見落とされます。無料のツールにも、スクリーンショットを作って保存し、人が目で調べるための基本機能を備えたものがあります。小さなアプリケーションなら十分かもしれませんが、ほかの手動テストと同じく、何か変わるたびに人手がかかるのが難点です。一方、何を問題とするかの明確な定義がないため、UIの不具合を自動で見つけるのはかなり大変です。ここで出番となるのが「ビジュアルリグレッション」です。以前のUIと最新の変更を比べ、差分を見つけることで、この難問に対処します。[Wraith](https://github.com/BBC-News/wraith)や[PhantomCSS](https://github.com/HuddleEng/PhantomCSS)など、OSSや無料のツールでも一部の機能は使えますが、設定には相当の時間がかかるかもしれません。[Applitools](https://applitools.com/)や[Percy.io](https://percy.io/)などの商用ツールは、さらに先へ進んでいます。導入が容易で、管理UI、アラート、広告やアニメーションといった「視覚的ノイズ」を取り除く賢い撮影機能、さらには問題を引き起こしたDOMやCSSの変更を突き止める根本原因の分析まで備えています。

<br/>

❌ **そうしないと：** 内容は素晴らしく、テストは100%通り、一瞬で読み込まれるページでも、コンテンツの半分が隠れていたら、何になるでしょうか？

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：内容は正しいのに表示が悪い、典型的なビジュアルリグレッション

![表示が崩れたAmazonのページ](assets/amazon-visual-regression.jpeg "Amazonのページの表示崩れ")

<br/>

### :clap: 良い例：WraithでUIのスナップショットを撮って比較する設定

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

### :clap: 良い例：Applitoolsでスナップショットの比較などの高度な機能を使う

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

## ⚪️ 4.1 自信を持てるだけのカバレッジを確保する：どうやら80%あたりが吉

:white_check_mark: **すべきこと：** テストの目的は、素早く進むために必要な自信を得ることです。もちろん、テストしたコードが多いほど、チームも自信を持てます。カバレッジは、テストがコードの何行、あるいは分岐や文のどれだけを通ったかを測る指標です。では、どこまであれば十分でしょうか？ 10〜30%では、ビルドが正しいかどうかを判断するには明らかに低すぎます。一方、100%を目指すと費用がかさみ、重要な経路ではなく、めったに使わない隅のコードへ目が向いてしまうかもしれません。詳しく答えるなら、アプリケーションの種類など、多くの要因によります。次世代のAirbus A380を作るなら100%は必須ですが、漫画の画像を載せるサイトなら50%でも多すぎるかもしれません。テストの愛好家の多くは、適切な下限は状況次第だと言いますが、その多くが経験則として80%という数字も挙げています。おそらく、ほとんどのアプリケーションにはそれで十分だからでしょう（[Fowlerは「80%台後半か90%台」としています](https://martinfowler.com/bliki/TestCoverage.html)）。

実装のヒント：CIにカバレッジの下限を設定し、基準に達しないビルドを止めるとよいでしょう（[Jestの設定](https://jestjs.io/docs/en/configuration.html#collectcoverage-boolean)）。コンポーネントごとに下限を指定することもできます。下の例を参照してください。さらに、新しくコミットされたコードでカバレッジが下がったことを検出する仕組みも検討しましょう。開発者がテスト済みのコードを増やす、少なくとも減らさないようにする動機になります。ただし、カバレッジは量に基づく指標の1つにすぎません。これだけでは、テストがどれほど確かなものかはわかりませんし、次の項目で示すように、数字にだまされることもあります。

<br/>

❌ **そうしないと：** 自信と数字は切り離せません。システムの大半をテストしたと本当にわかっていなければ、不安が残ります。そして、不安はあなたの歩みを遅くします。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 例：一般的なカバレッジレポート

![一般的なカバレッジレポート](assets/bp-18-yoni-goldberg-code-coverage.png "一般的なカバレッジレポート")

<br/>

### :clap: 良い例：Jestでコンポーネントごとにカバレッジを設定する

![Jestを使った例](https://img.shields.io/badge/🔨%20Example%20using%20Jest-blue.svg "Jestを使った例")

![コンポーネントごとのカバレッジ設定](assets/bp-18-code-coverage2.jpeg "Jestでコンポーネントごとにカバレッジを設定する")

</details>

<br/><br/>

## ⚪️ 4.2 カバレッジレポートを調べ、未テストの箇所や不自然な点を見つける

:white_check_mark: **すべきこと：** 普通のツールではなかなか見つからず、監視の目をかいくぐる問題があります。バグというより、深刻な影響を及ぼしかねない、予想外の振る舞いです。たとえば、まったく、あるいはめったに呼ばれないコードがあることは珍しくありません。商品価格はいつも`PricingCalculator`クラスが設定していると思っていたのに、実は一度も呼ばれていなかった。DBには1万件の商品があり、販売実績もたくさんあるというのに……。カバレッジレポートは、アプリケーションが自分の思っているとおりに動いているかを教えてくれます。どんな種類のコードがテストされていないかも、はっきりします。80%をテストしたと聞いただけでは、肝心な部分が含まれるのかわかりません。レポートを作るのは簡単です。本番またはテスト中にカバレッジを記録しながらアプリケーションを動かし、各箇所がどれくらい呼ばれたかを色分けしたレポートを見ればよいのです。このデータに少し目を通せば、思わぬ落とし穴が見つかるかもしれません。
<br/>

❌ **そうしないと：** コードのどこが未テストかわからなければ、どこから問題が起こるかもわかりません。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：このカバレッジレポート、何がおかしい？

QA環境でアプリケーションの使われ方を追い、興味深いログインの傾向を見つけた実例です。ヒント：ログイン失敗の数が不釣り合いに多く、明らかに何かがおかしい。結局、フロントエンドのバグで、バックエンドのログインAPIが繰り返し呼ばれているとわかりました。

![このカバレッジレポート、何がおかしい？](assets/bp-19-coverage-yoni-goldberg-nodejs-consultant.png "このカバレッジレポート、何がおかしい？")

</details>

<br/><br/>

## ⚪️ 4.3 ミューテーションテストで、ロジックのカバレッジを測る

:white_check_mark: **すべきこと：** 従来のカバレッジ指標は、よく嘘をつきます。カバレッジ100%と表示されていても、正しい応答を返す関数が、ただの1つもないかもしれません。どうしてでしょう？ 測っているのはテストがどの行を通ったかだけで、実際に何かを確かめたか、つまり正しい応答をアサーションで検証したかは調べていないからです。出張した人が、パスポートのスタンプを見せるようなものです。仕事をした証拠にはなりません。いくつかの空港とホテルを訪れたことがわかるだけです。

そこで役立つのがミューテーションテストです。単に**通った**だけでなく、実際に**検証した**コードの量を測ります。JavaScript用のミューテーションテストライブラリ[Stryker](https://stryker-mutator.io/)は、実にうまくできています。

(1) コードをわざと書き換えて、「バグを仕込み」ます。たとえば`newOrder.price===0`を`newOrder.price!=0`に変えます。この「バグ」をミューテーションと呼びます。

(2) テストを実行します。全部通ったら問題です。バグを見つけるという役目を、テストが果たせていません。こうしたミューテーションは「生き残った」と呼ばれます。テストが失敗したなら、やりました！ ミューテーションを「殺せた」のです。

すべて、あるいは大半のミューテーションを殺せたとわかれば、従来のカバレッジよりもずっと自信を持てます。しかも、設定にかかる時間は同じくらいです。
<br/>

❌ **そうしないと：** カバレッジ85%なら、コードの85%にあるバグを見つけられるのだと、思い込まされてしまいます。

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

### :clap: 良い例：ミューテーションテストツールStrykerのレポートは、テストされていないコードを見つけ、その量をミューテーションの数で示す

![Strykerのミューテーションテストレポート](assets/bp-20-yoni-goldberg-mutation-testing.jpeg "Strykerのレポートは、テストされていないコードを見つけ、その量をミューテーションの数で示す")

</details>

<br/><br/>

## ⚪️ 4.4 テスト用リンターで、テストコードの問題を防ぐ

:white_check_mark: **すべきこと：** テストコードのパターンを検査し、問題を見つけるためのESLintプラグインがあります。たとえば[eslint-plugin-mocha](https://www.npmjs.com/package/eslint-plugin-mocha)は、`describe()`の子ではなくグローバルにテストを書いたときや、テストが[スキップされている](https://mochajs.org/#inclusive-tests)ときに警告します。スキップに気付かないと、全テストが通っていると誤解しかねません。同じように、[eslint-plugin-jest](https://github.com/jest-community/eslint-plugin-jest)は、たとえばアサーションがまったくなく、何も確かめていないテストを警告できます。

<br/>

❌ **そうしないと：** カバレッジ90%、テストは100%緑。それを見て満面の笑みを浮かべるのも、多くのテストが何も確かめておらず、多くのスイートがただスキップされていたと気付くまでです。その思い違いをもとに、何もデプロイしていなければよいのですが。

<br/>
<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：間違いだらけのテストケース。幸い、リンターがすべて見つけてくれる

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

## ⚪️ 5.1 リンターを充実させ、リントの問題があればビルドを止める

:white_check_mark: **すべきこと：** リンターは、使うだけ得です。5分設定するだけで、コードを見張り、入力しているそばから重大な問題を見つける自動操縦装置が、無料で手に入るのです。リントが見た目の問題だけを扱っていた時代は終わりました。「セミコロン禁止！」だけではないのです。今のリンターは、エラーを正しくthrowせず情報を失ってしまうような、深刻な問題も検出できます。[ESLint standard](https://www.npmjs.com/package/eslint-plugin-standard)や[Airbnbスタイル](https://www.npmjs.com/package/eslint-config-airbnb)といった基本ルールに加え、専用のリンターを入れることも検討してください。[eslint-plugin-chai-expect](https://www.npmjs.com/package/eslint-plugin-chai-expect)はアサーションのないテストを、[eslint-plugin-promise](https://www.npmjs.com/package/eslint-plugin-promise?activeTab=readme)はresolveされないPromiseを検出できます。resolveされなければ、コードはいつまでも先へ進みません。[eslint-plugin-security](https://www.npmjs.com/package/eslint-plugin-security?activeTab=readme)はDoS攻撃に使われかねない、貪欲な正規表現を見つけます。[eslint-plugin-you-dont-need-lodash-underscore](https://www.npmjs.com/package/eslint-plugin-you-dont-need-lodash-underscore)は、Lodashの`_map(…)`のように、V8の標準メソッドでできることをユーティリティライブラリに頼っていると警告できます。
<br/>

❌ **そうしないと：** ついていない日を想像してください。本番が何度も落ちるのに、ログにはエラーのスタックトレースが出てきません。何が起きたのでしょう？ コードが誤ってErrorではないオブジェクトをthrowし、スタックトレースを失ったのです。壁に頭を打ち付けたくもなります。5分かけてリンターを設定していれば、その書き間違いを見つけ、こんな1日を救えたかもしれません。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :thumbsdown: アンチパターン：誤ったエラーオブジェクトをthrowしてしまい、スタックトレースが出ない。幸い、ESLintが次の本番バグを見つけてくれる

![誤ったエラーのthrowを検出するESLint](assets/bp-21-yoni-goldberg-eslint.jpeg "誤ったエラーオブジェクトをthrowすると、スタックトレースが出ない。幸い、ESLintが本番に出る前に見つけてくれる")

</details>

<br/><br/>

## ⚪️ 5.2 開発者の手元でCIを実行し、フィードバックループを短くする

:white_check_mark: **すべきこと：** CIでテスト、リント、脆弱性チェックなど、頼もしい品質検査をしていますか？ 開発者がそのパイプラインをローカルでも動かせるようにして、すぐに結果を受け取り、[フィードバックループ](https://www.gocd.org/2016/03/15/are-you-ready-for-continuous-delivery-part-2-feedback-loops/)を短くしましょう。なぜか？ 効率のよいテストでは、(1)試す → (2)結果を受け取る → (3)リファクタリングする、という流れを何度も回すからです。結果が早く返るほど、1つのモジュールを何度も改善し、仕上がりをよくできます。逆に結果が遅ければ、1日にできる改善の回数は減ります。チームはもう別の話題や作業、モジュールに移っていて、元のモジュールを磨き込む気にはならないかもしれません。

具体的には、[CircleCIのローカルCLI](https://circleci.com/docs/2.0/local-cli/)のように、パイプラインをローカルで実行できるCIサービスがあります。[Wallaby](https://wallabyjs.com/)などの商用ツールなら、開発者が試作している最中に、役立つテストの情報を得られます。私は同ツールと利害関係はありません。もっと単純に、テスト、リント、脆弱性検査など、品質に関するコマンドを全部動かすnpmスクリプトをpackage.jsonに追加するだけでもかまいません。[concurrently](https://www.npmjs.com/package/concurrently)などで並列実行し、どれかが失敗したら0以外の終了コードを返すようにします。これで開発者は、`npm run quality`のような1つのコマンドを打つだけで、すぐに結果を得られます。Gitフックを使い、品質チェックに失敗したらコミットを中止することも検討してください（[Husky](https://github.com/typicode/husky)が役立ちます）。
<br/>

❌ **そうしないと：** コードを書いた翌日に検査結果が届くようでは、テストは開発の流れに溶け込まず、後から形式を整えるための作業になってしまいます。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：コードの品質を調べるnpmスクリプトを、必要に応じて、または新しいコードをpushしようとしたときに、まとめて並列実行する

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

## ⚪️ 5.3 本番を忠実に再現した環境でE2Eテストをする

:white_check_mark: **すべきこと：** E2Eテストは、どのCIパイプラインでも大きな課題です。関連するクラウドサービスを全部含めて、本番と同じ使い捨ての環境をその場で作るのは、手間も費用もかかります。どこで折り合いを付けるかが腕の見せどころです。[Docker Compose](https://serverless.com/)なら、1つのテキストファイルで、同じコンテナーを使った隔離環境を作れます。ただし、ネットワークやデプロイ方式などの基盤技術は、実際の本番環境と違います。[AWS Local](https://github.com/localstack/localstack)と組み合わせれば、実際のAWSサービスのスタブを使えます。[サーバーレス](https://serverless.com/)を採用したなら、Serverlessや[AWS SAM](https://docs.aws.amazon.com/lambda/latest/dg/serverless_app.html)など、FaaSのコードをローカルで呼び出せるフレームワークもいくつもあります。

Kubernetesの巨大なエコシステムでは、新しいツールが次々と出ていますが、ローカルやCIで本番を再現するための、標準的で使いやすいツールはまだ定まっていません。1つの方法は、[Minikube](https://kubernetes.io/docs/setup/minikube/)や[MicroK8s](https://microk8s.io/)で「小さなKubernetes」を動かすことです。本物によく似ていて、負担は軽くなります。もう1つは、リモートの「本物のKubernetes」でテストする方法です。[Codefresh](https://codefresh.io/)など、Kubernetes環境との連携を標準で備え、本物の環境でCIパイプラインを動かしやすいサービスもあります。リモートのKubernetesに対して独自のスクリプトを実行できるサービスもあります。
<br/>

❌ **そうしないと：** 本番とテストで異なる技術を使うと、2つのデプロイ方式を保守しなければならず、開発チームと運用チームの分断も続きます。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 例：その場でKubernetesクラスターを作るCIパイプライン（[出典：Dynamic Environments Kubernetes](https://container-solutions.com/dynamic-environments-kubernetes/)）

<pre name="38d9" id="38d9" class="graf graf--pre graf-after--p">deploy:<br>stage: deploy<br>image: registry.gitlab.com/gitlab-examples/kubernetes-deploy<br>script:<br>- ./configureCluster.sh $KUBE_CA_PEM_FILE $KUBE_URL $KUBE_TOKEN<br>- kubectl create ns $NAMESPACE<br>- kubectl create secret -n $NAMESPACE docker-registry gitlab-registry --docker-server="$CI_REGISTRY" --docker-username="$CI_REGISTRY_USER" --docker-password="$CI_REGISTRY_PASSWORD" --docker-email="$GITLAB_USER_EMAIL"<br>- mkdir .generated<br>- echo "$CI_BUILD_REF_NAME-$CI_BUILD_REF"<br>- sed -e "s/TAG/$CI_BUILD_REF_NAME-$CI_BUILD_REF/g" templates/deals.yaml | tee ".generated/deals.yaml"<br>- kubectl apply --namespace $NAMESPACE -f .generated/deals.yaml<br>- kubectl apply --namespace $NAMESPACE -f templates/my-sock-shop.yaml<br>environment:<br>name: test-for-ci</pre>

</details>

<br/><br/>

## ⚪️ 5.4 テストを並列実行する

:white_check_mark: **すべきこと：** うまく作れば、テストは24時間365日、ほぼ即座に結果を知らせてくれる友人です。しかし実際には、CPU負荷の高いユニットテストを500件、1つのスレッドで実行すると、時間がかかりすぎることがあります。幸い、[Jest](https://github.com/facebook/jest)、[AVA](https://github.com/avajs/ava)、[Mochaの拡張](https://github.com/yandex/mocha-parallel-tests)といった今のテストランナーやCI環境なら、テストを複数プロセスで並列実行し、結果が返るまでの時間を大幅に縮められます。コンテナーをまたいで（！）並列実行し、フィードバックループをさらに短くしてくれるCIサービスもあります。ローカルの複数プロセスであれ、クラウドのCLIから使う複数マシンであれ、並列化するなら各テストを独立させなければなりません。それぞれが別のプロセスで動く可能性があるからです。

❌ **そうしないと：** 新しいコードをpushして1時間、すでに次の機能を書いているところへテスト結果が届く。テストの意味を薄れさせるには、うってつけのやり方です。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：Mochaの並列実行版とJestは、並列化のおかげで従来のMochaを軽々と追い抜く（[出典：JavaScript Test-Runners Benchmark](https://medium.com/dailyjs/javascript-test-runners-benchmark-3a78d4117b4)）

![Mochaの並列実行版とJestのベンチマーク](assets/bp-24-yonigoldberg-jest-parallel.png "Mochaの並列実行版とJestは、並列化のおかげで従来のMochaを軽々と追い抜く。出典：JavaScript Test-Runners Benchmark")

</details>

<br/><br/>

## ⚪️ 5.5 ライセンスと盗用をチェックし、法的な問題を避ける

:white_check_mark: **すべきこと：** ライセンスや盗用は、今いちばんの気掛かりではないでしょう。でも、10分で済むなら、これも確認しておきませんか？ [license-checker](https://www.npmjs.com/package/license-checker)や[plagiarism-checker](https://www.npmjs.com/package/plagiarism-checker)（無料プランのある商用ツール）など、いくつかのnpmパッケージはCIに簡単に組み込めます。制約の厳しいライセンスの依存パッケージや、Stack Overflowからコピーしたために著作権に触れていそうなコードなど、厄介な問題を調べられます。

❌ **そうしないと：** 開発者が意図せず不適切なライセンスのパッケージを使ったり、商用コードをコピーしたりして、法的な問題に巻き込まれるかもしれません。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 良い例：

```shell
# install license-checker in your CI environment or also locally
npm install -g license-checker

# ask it to scan all licenses and fail with exit code other than 0 if it found unauthorized license. The CI system should catch this failure and stop the build
license-checker --summary --failOn BSD
```

<br/>

![ライセンス検査の結果](assets/bp-25-nodejs-licsense.png)

</details>

<br/><br/>

## ⚪️ 5.6 依存パッケージの脆弱性を継続的に調べる

:white_check_mark: **すべきこと：** Expressのように評判のよい依存パッケージにも、既知の脆弱性があります。[npm audit](https://docs.npmjs.com/getting-started/running-a-security-audit)などのコミュニティのツールや、コミュニティ向け無料版もある商用ツール[Snyk](https://snyk.io/)を使えば、簡単に対処できます。どちらも、ビルドのたびにCIから呼び出せます。

❌ **そうしないと：** 専用のツールを使わずにコードを脆弱性から守り続けるには、新しい脅威についての情報を、ずっとネットで追いかけなければなりません。かなり面倒です。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 例：npm auditの結果

![npm auditの結果](assets/bp-26-npm-audit-snyk.png "npm auditの結果")

</details>

<br/><br/>

<a id="practice-5-7"></a>

## ⚪️ 5.7 依存パッケージの更新を自動化する

:white_check_mark: **すべきこと：** Yarnやnpmに最近導入されたpackage-lock.jsonは、深刻な課題を持ち込みました。「地獄への道は善意で舗装されている」とは、このことです。今や、既定ではパッケージが更新されません。`npm install`や`npm update`を使って何度も新しくデプロイしているチームでさえ、新しい更新を取り込めないのです。その結果、よくても見劣りするバージョンの依存パッケージ、悪ければ脆弱なコードが残ります。package.jsonを手で更新するか、[ncu](https://www.npmjs.com/package/npm-check-updates)などを手動で使うかは、開発者の善意と記憶頼みです。もっと確実な方法は、最も信頼できるバージョンの依存パッケージを取得する手順を、自動化することかもしれません。まだ銀の弾丸はありませんが、自動化には2つの道があります。

(1) [`npm outdated`](https://docs.npmjs.com/cli/outdated)や`npm-check-updates（ncu）`を使って、古くなった依存パッケージがあるビルドをCIで失敗させます。こうすれば、開発者は更新せざるを得ません。

(2) コードを調べ、依存パッケージを更新したプルリクエストを自動で送る、商用ツールを使います。ここで残る面白い問題は、どんな更新方針にするかです。パッチのたびに更新すると手間が増えすぎますし、メジャー版が出てすぐ更新すると、不安定な版を使うことになるかもしれません。公開からわずか数日で脆弱性が見つかったパッケージは、たくさんあります（[eslint-scopeの事件](https://nodesource.com/blog/a-high-level-post-mortem-of-the-eslint-scope-security-incident/)を参照）。

効率のよい更新方針として、一定の待機期間を設けてもよいでしょう。手元の版を古いと判断するまでに、`@latest`からしばらく、あるいは何バージョンか遅れることを許容するのです。たとえば、ローカルが1.3.1で、公開版が1.3.8という状態です。
<br/>

❌ **そうしないと：** 作者自身が危険だとはっきり示したパッケージを、本番で動かすことになります。

<br/>

<details><summary>✏ <b>コード例</b></summary>

<br/>

### :clap: 例：[ncu](https://www.npmjs.com/package/npm-check-updates)を手動またはCIで実行し、コードが最新版からどれくらい遅れているかを調べる

![ncuによる更新の確認](assets/bp-27-yoni-goldberg-npm.png "ncuを手動またはCIで実行し、コードが最新版からどれくらい遅れているかを調べる")

</details>

<br/><br/>

## ⚪️ 5.8 Node.jsに限らない、CIのそのほかのヒント

:white_check_mark: **すべきこと：** この記事は、Node.jsに関係する、あるいは少なくともNode.jsで例を示せるテストの助言を中心にしています。ただ、この項目ではNode.jsに限らない、よく知られた助言をいくつかまとめます。

<ol><li>宣言的な構文を使います。大半のサービスではそれしか選べませんが、古いJenkinsではコードやUIも使えます。</li><li>Dockerを標準でサポートするサービスを選びます。</li><li>失敗は早く見つけましょう。いちばん速いテストから実行します。リントやユニットテストなど、短時間で済む検査を「スモークテスト」のステップにまとめ、コミットした人へすばやく結果を返します。</li><li>テスト、カバレッジ、ミューテーションテストの各レポートやログなど、ビルドの成果物をすべて、簡単に見渡せるようにします。</li><li>イベントごとにパイプラインやジョブを分け、ステップは再利用します。たとえば、機能ブランチへのコミット用とmasterへのプルリクエスト用に、別のジョブを用意します。共通のステップを使って、それぞれで処理を再利用してください。大半のサービスには、コードを再利用する仕組みがあります。</li><li>ジョブ定義にシークレットを埋め込んではいけません。シークレットストアか、ジョブの設定から取得してください。</li><li>リリースビルドでは明示的にバージョンを上げるか、少なくとも開発者が上げたことを確認します。</li><li>ビルドは一度だけ行い、Dockerイメージなど、その1つの成果物に対してすべての検査を実行します。</li><li>ビルド間で状態が持ち越されない、使い捨ての環境でテストします。例外になりそうなのは、node_modulesのキャッシュだけです。</li></ol>
<br/>

❌ **そうしないと：** 長年の知恵を取り逃してしまいます。

<br/><br/>

<a id="practice-5-9"></a>

## ⚪️ 5.9 ビルドマトリックス：複数のNode.jsバージョンで同じCI手順を実行する

:white_check_mark: **すべきこと：** 品質チェックでは、思いがけない発見がものをいいます。調べる範囲が広いほど、問題を早く見つける幸運にも恵まれます。再利用できるパッケージを作るときや、顧客ごとに設定やNode.jsバージョンの違う本番環境を運用するときは、その設定の組み合わせすべてで、CIのテストパイプラインを動かさなければなりません。たとえば、MySQLを使う顧客も、Postgresを使う顧客もいるとします。一部のCIサービスが備える「マトリックス」機能なら、MySQL・Postgresと、Node.js 8・9・10などのバージョンをすべて組み合わせ、テストスイートを実行できます。テストなどの品質チェックがすでにあれば、設定だけで済み、それ以上の作業は要りません。マトリックスを備えていないCIでも、拡張機能や工夫で対応できる場合があります。
<br/>

❌ **そうしないと：** あれだけ苦労してテストを書いたのに、設定の違いだけでバグを忍び込ませてしまうのでしょうか？

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
<img width="480px" src="assets/yoni-goldberg.jpg" alt="Yoni Goldberg"/>
<br/>

**役割：** 執筆

**紹介：** 独立したコンサルタントとして、Fortune 500企業からガレージで始めたスタートアップまで、JavaScript・Node.jsアプリケーションの改善を手伝っています。何よりテストに夢中で、その技を極めたいと思っています。[Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices)の著者でもあります。

**📗 オンライン講座：** このガイドを気に入り、テストの技術をとことん突き詰めたくなりましたか？ テストを網羅した私の講座 [Testing Node.js & JavaScript From A To Z](https://www.testjavascript.com) も、ぜひのぞいてみてください。

<br/>

**フォロー：**

- [🐦 Twitter](https://twitter.com/goldbergyoni/)
- [📞 お問い合わせ](https://testjavascript.com/contact-2/)
- [✉️ ニュースレター](https://testjavascript.com/newsletter//)

<br/>
<hr/>
<br/>

## [Bruno Scheufler](https://github.com/BrunoScheufler)

**役割：** 技術レビューと助言

全文の見直し、改善、リント、仕上げを担当しました。

**紹介：** フルスタックのWebエンジニア。Node.jsとGraphQLの愛好家です。

<hr/>
<br/>

## [Ido Richter](https://github.com/idori)

**役割：** 構想、デザイン、素晴らしい助言

**紹介：** 腕の立つフロントエンド開発者で、CSSの専門家。絵文字マニアでもあります。

## [Kyle Martin](https://github.com/js-kyle)

**役割：** プロジェクトの運営を支え、セキュリティに関わるプラクティスをレビューしています。

**紹介：** Node.jsのプロジェクトとWebアプリケーションのセキュリティに取り組むのが好きです。

## コントリビューター ✨

このリポジトリに貢献してくださった、素晴らしい皆さんに感謝します！

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
