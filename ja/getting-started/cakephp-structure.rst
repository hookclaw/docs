CakePHP の構造
##############

CakePHP には、コントローラ、モデル、ビューのクラスがあります。その他にも MVC での開発を
よりすばやく、楽しめるものにするために、幾つかの追加クラスとオブジェクトがあります。
コンポーネント (*Components*)、ビヘイビア (*Behaviors*)、ヘルパー (*Helpers*) は、
拡張性と再利用性を実現するクラスで、アプリケーションの MVC 基礎クラスにすばやく機能を追加できます。
今は大枠をつかむだけにして、後で各ツールの詳細を調べましょう。

.. _application-extensions:

アプリケーションの拡張
======================

コントローラ、ヘルパー、モデルには親クラスがあり、アプリケーション全体に変更を加えることができます。
AppController (``/app/Controller/AppController.php`` に配置) 、
AppHelper (``/app/View/Helper/AppHelper.php`` に配置) と、
AppModel (``/app/Model/AppModel.php`` に配置) は、すべてのコントローラ、
ヘルパー、モデルで共有するようなメソッドを置くのに良い場所です。

クラスやファイルではありませんがルートは、CakePHP にリクエストを送る役割を果たしています。
ルートを定義することによって、URL とコントローラのアクションをどのように結びつける (*map*) が
CakePHP に伝えられます。 URL ``/controller/action/var1/var2`` は、デフォルトの動作では、
Controller::action($var1, $var2) にマップされます。しかし、ルートを使うと URL をカスタマイズでき、
アプリケーション内でどのように解釈するかを設定できます。

アプリケーション内の機能の中には、そっくりそのままパッケージ化してしまうと便利なものもあります。
プラグイン (*plugin*) はモデル、コントローラ、ビューをパッケージ化したもので、ある特定の目的のために
複数のアプリケーションで使えるようにしたものです。ユーザ管理システムや簡単なブログシステムなどを、
CakePHP のプラグインにできるでしょう。


コントローラの拡張 ("コンポーネント")
=====================================

コンポーネントは、コントローラのロジック内で手伝いをするクラスのことです。
もし、複数のコントローラ（またはアプリケーション）で共通に使いたいロジックがあれば、通常、
コンポーネントにするのがいちばん良い方法です。例えば、コアに含まれる EmailComponent クラスは、
Email を簡単に作成、送信することができます。一つのコントローラの中にこのロジックを
書いてしまうのではなく、ロジックをパッケージ化して、共通に使えるようにできるわけです。

コントローラには、幾つかのコールバック (*callbacks*) もあります。
CakePHP コアの動作中に自分のロジックを割り込ませたい場合、コールバックを使うことができます。
使用できるコールバックには次のものがあります:

-  :php:meth:`~Controller::afterFilter()` 、 ビューの表示 (*render*) を含むすべての
   コントローラのロジックの後に実行されます。
-  :php:meth:`~Controller::beforeFilter()` 、 コントローラのアクションロジックの実行前に
   呼ばれます。
-  :php:meth:`~Controller::beforeRender()` 、 コントローラロジックの実行後、しかしビューの
   表示(*render*)前に実行されます。

モデルの拡張 ("ビヘイビア")
===========================

同様に、ビヘイビアはモデル間で共通の機能を追加する方法として利用できます。例えば、ユーザデータを
ツリー構造で保存する場合、User モデルをツリーのように動作させるよう指定し、ツリー構造の中での
ノードの削除、追加、移動などの機能を使うことができます。

モデルは、データソース (*DataSource*) と呼ばれるもう一つのクラスによっても支えられています。
データソースは、異なるタイプの一連のデータについて、モデルがそれを操作できるように抽象化するものです。
CakePHP アプリケーションの主なソースは、通常データベースですが、RSS フィード、CVS ファイル、
LDAP エントリ、iCal イベントなどをモデルが扱えるようなデータソースを追加することもできます。
データソースは、異なるソースからのレコードを関連づけることも可能になっています。つまり、SQL の
Join だけに制限されているわけではなく、LDAP モデルに多くの iCal イベントを関連付けるようなことも
可能です。

コントローラと同じように、モデルにもコールバックがあります:

-  beforeFind()
-  afterFind()
-  beforeValidate()
-  afterValidate()
-  beforeSave()
-  afterSave()
-  beforeDelete()
-  afterDelete()

これらのメソッドの名前を見れば、何をするものか分かるはずです。
モデルの章で詳細について調べてください。

ビューの拡張("ヘルパー")
========================

ヘルパーは、ビューのロジックを手伝うクラスのことです。コンポーネントがコントローラ内で使用されるのと
同じように、ヘルパーによって、複数のビューから共通の表現用ロジックにアクセスできるようにします。
コアに含まれるヘルパーのひとつ、JsHelper を使うと、ビュー内での Ajax リクエストを非常に簡単に扱えます。
JsHelper は、jQuery (デフォルト)、Prototype、Mootools をサポートしています。

たいていのアプリケーションには、繰り返し利用されるビューのコードがあります。
CakePHP はレイアウト (*layout*) とエレメント (*element*) によってビューコードの再利用を促進します。
デフォルトでは、コントローラによって表示されるすべてのビューは、レイアウトの中に配置して表示されます。
エレメントは、切れはし (*snippet*) を作って複数のビューの中で繰り返し利用したい時に使用できます。


.. meta::
    :title lang=ja: CakePHP Structure
    :keywords lang=ja: user management system,controller actions,application extensions,default behavior,maps,logic,snap,definitions,aids,models,route map,blog,plugins,fit
