## 良く使う機能
### 文字列から特定の文字列・パターンを探す
- 特定の文字列を探す
  - [find関数](./SAS/functions/find.md)
- 正規表現を用い、文字列がパターンと一致するかを判定する
  - [prxmatch関数](./SAS/functions/prxmatch.md)

### 文字列を加工する
- 文字列を切り出す
  - [substr関数 / %substrマクロ関数](./SAS/functions/substr.md)
- 文字列を取り除く
  - [compress関数](./SAS/functions/compress.md)
- 文字列に含まれる特定の文字を計上する
  - [count関数](./SAS/functions/count.md)
- 任意の文字列を指定文字で区切った際のN番目の文字列を取得する
  - [scan関数 / %scanマクロ関数](./SAS/functions/scan.md)

### 任意のデータセットを作成する
- [datalinesステートメント](./SAS/statements/datalines.md)

### dataステップ内でマクロ変数に値を代入する
- [symputxマクロ関数](./SAS/macrofunction/symputx.md)

### データセットを縦方向に結合する
- [proc appendプロシジャ](./SAS/procedures/append.md)
- [table.appendアクション](./SAS/casl/table.append.md)

## Tips

### forループを回す

#### dataステップ内での利用
``` sas
data _null_;
  do i=1 to 10;
    put index=;
  end;
run;
```

#### マクロ内での利用

``` sas
%macro test();
  %let count = 10;
  %let index;
  %do index = 1 %to &count;
    %put index is &index;
  %end;
%mend;
```

### 行数を指定してデータセットを読み込む

- firstobsオプションおよびobsオプションを使用する。
  - firstobsは「読み込み始める行位置」を、obsオプションで「読み込みを止める行位置」を指定できる。
- `obs - firstobs + 1`の行数を持つデータセットが取得できる。

``` sas
data work.t;
  set sashelp.cars(firstobs=3 obs=5);
run;
```

- [firstobsデータセットオプション](./SAS/dataset_options/firstobs.md)
- [obsデータセットオプション](./SAS/dataset_options/obs.md)


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

### マクロ関数の一覧
- https://support.sas.com/documentation/cdl_alternate/ja/mcrolref/67912/HTML/default/n1qqdn7r170c30n197p4jfufv1yy.htm
