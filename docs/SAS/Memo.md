### 大事なこと

- マクロの世界とdataステップの世界の違いを意識する。
  - マクロの定義や呼び出しではあくまでも「コード自体の繰り返し・条件分岐」のみを行っており、実際の処理は行っていない。（実際の処理はprocステップやdataステップ内で行われる）
  - 

### それぞれの繋がり方

- マクロプログラミング
  - マクロ関数（Macro Function）
  - マクロステートメント（Macro Statement）
- dataステッププログラミング
  - データセットオプション（Dataset Options）
  - 関数
  - CALLルーチン
- procステッププログラミング
  - プロシジャ（Procedure）
- CASLプログラミング
  - CASアクション

### 各用語について

#### データセットオプション
- dataステップ内の「set」ステートメントの直後（セミコロンの前）の丸括弧内に記述するオプション。keepやdrop、firstobsなどをよく使う。
- こちらのkeep/dropは「dataステップ内で使用せず、処理開始時点で不要な変数を取り除く」ために使用する。

#### ステートメント
- dataステップ内に記述する「処理に関する内容」。setやwhere、keepなどをよく使う。
- こちらのkeep/dropは「dataステップ内で作成・使用し、出力するデータセットにも含みたい(外したい)」ときに使用する。

- 


#### CASライブラリの情報を表示する
``` sas
cas casauto;
proc cas;
  %local _tmp_result;
  table.caslibinfo result = rs / caslib = "casuser";
  symputx('_tmp_result', rs['caslibinfo'][1]['Path'], 'L') /* rsデータセットから値を取得し、マクロ変数に格納　*/
quit;
```

> https://go.documentation.sas.com/doc/ja/pgmsascdc/9.4_3.5/caspg/cas-table-caslibinfo.htm

#### テーブルを「セッションスコープ」から「グローバルスコープ」に格上げする

``` sas
cas casauto;
proc cas;
  table.promote /
    name="mytable"
    caslib="TEST" /* sourceCaslib= でもOK */
    targetlib="TARGET"; /* targetCaslib= でもOK */
quit;
```
