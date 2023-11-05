

## dataステッププログラミング

### 任意のデータセットを作成する
- [datalinesステートメント](./SAS/statements/datalines.md)

### 正規表現を用い、文字列がパターンと一致するかを判定する
- [prxmatch関数](./SAS/functions/prxmatch.md)

### dataステップ内でマクロ変数に値を代入する
- [symputxマクロ関数](./SAS/macrofunction/symputx.md)


## Tips

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
