
### prxmatch関数

正規表現によりパターンマッチを行う。
処理結果は「見つからなければ0」「見つかった場合は文字列の位置」が返り値として設定される。

#### dataステップでの利用
``` sas
find_pos = prxmatch()
```

#### マクロ内での利用

``` sas

%let prx_pattern = /[A-Z0-9_]+/;
%let target_text = ABC_123;
%let find_pos = %sysfunc(prxmatch(&prx_pattern, &target_text);
```
