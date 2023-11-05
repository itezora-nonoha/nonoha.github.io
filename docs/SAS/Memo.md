### transtrn

文字列の置き換えを行う。

``` sas
data _null_;
  text = 'hogehoge';
  text_replaced = transtrn(text, 'g', 'm');
run;
```

> SASは文字列内の最初の文字をチェックし、それが数値または算術演算子の場合はパラメータを%evals()する



### CASアクション

#### テーブルを縦方向に結合する

``` sas
libname casuser cas caslib="casuser";
proc cas;
  table.append /
    source={caslib='casuser', name='t1', where="age < 15"},
    target={caslib='casuser', name='t2};
run;
```

### データセットを縦報告に結合する（proc append）

``` sas
proc append base=work.t1 data=work.2;
run;
```

### データセットが最後まで読み込まれたときに処理をする
- `end = 一時変数名`とすることで、最後のオブザベーション読み込んだときに1が設定される一時変数を作成することができる。
 
``` sas
data work.t2
  set sashelp.cars end = eof;
  if (eof) then do;
    put '最後のオブザベーションが読み込まれました。'
  end;
run;
```

### dataステップ内でマクロ変数に値を代入する

- `call symputx()`を使用する。
- 第三引数に'G'を設定することで、グローバル変数として設定・代入できる。

``` sas
data _null_;
  set sashelp.car end = eof;
  retain model_list;
  model_list = catx(',', model_list, model);
  if (eof) then do;
    call symputx('model_list', model_list);
    call symputx('model_list_global', model_list, 'G');
  end;
run;

```

### 部分文字列を検索する(find Function)

``` sas
data _null_;
  find_text = 'wo';
  text = 'hello world';
  result = find(text, find_text);  
run;
```
> 第三引数として「検索開始位置」を指定することも可能。

### 全てのCASライブラリを現在のセッションに読み込む

``` sas
caslib _all_ assign;
```

### 行数を指定してデータセットを読み込む

firstobsは「読み込み始める行位置」を、obsオプションで「読み込みを止める行位置」を指定できる。
両方のオプションを指定した場合は、`obs - firstobs + 1`の行数を持つがデータセットが取得される。

``` sas
data work.t;
  set sashelp.cars(firstobs=3 obs=5);
run;
```

### 指定文字列を全て取り除いた文字列を取得する（compress Function）

``` sas
data _null_;
  text_before = 'aaa, bbb, ccc, ddd';
  text_after = compress(text_before, ',');
run;
```

### 文字列に含まれる特定の文字列の数を計上する（count Function）

``` sas
data _null_;
  text = 'aaa, bbb, ccc, ddd';
  count = count(text, ',');
run;
```

### 各用語について
- データセットオプション
  - dataステップ内の「set」ステートメントの直後（セミコロンの前）の丸括弧内に記述するオプション。keepやdrop、firstobsなどをよく使う。
  - こちらのkeep/dropは「dataステップ内で使用せず、処理開始時点で不要な変数を取り除く」ために使用する。
- ステートメント
  - dataステップ内に記述する「処理に関する内容」。setやwhere、keepなどをよく使う。
  - こちらのkeep/dropは「dataステップ内で作成・使用し、出力するデータセットにも含みたい(外したい)」ときに使用する。
 
### 任意の文字列を指定文字で区切った際のN番目の文字列を取得する（scan Function / %scan MacroFunction）

``` sas
data _null_;
  text = 'aaa, bbb, ccc, ddd';
  word = scan(text, 3, ',');
  put word; /" 3番目の文字列「ccc」が出力される */
run;
``` 
> 第三引数における「区切り文字」の指定は「文字のリスト」として解釈されるため、'.,'と指定した場合は','および'.'の2つが区切り文字として解釈される。
> また、区切り文字としてマルチバイト文字は指定できない。（マルチバイト文字を使用したい場合はkscan関数を使用する）
> 第四引数を指定しない場合、先頭の区切り文字は無視される」「連続した区切り文字は1津の区切り文字として解釈される」仕様のため、これを避けたい場合にはとして'M'を指定してあげる必要がある。

### 任意のデータセットを作成する
- datalineステートメントを使用する。

``` sas
data work.t;
  input aaa $4 bbb $4;
  datalines;
B01 1234
B02 2345
B03 3456
;
run;

> データを記述する「datalines;から;まで」の部分について、インデントは不可。
> inputで指定した長さで固定長区切りを行ってデータセットを作成するため、カラム長を適切に設定する必要がある。

### dataステップ内のoutputステートメントについて

- 基本的には「現在のオブザベーションをすぐにデータセットに書き込む」ための「暗黙的なoutputステートメント」が存在している。
- しかし、if文の中などで「特定の条件においてのみ、outputを行う」ような記述とすると、前述の「暗黙的なoutputステートメント」が消滅する。


### caslプログラミングのメモ
- table.promote
- table.altertable
