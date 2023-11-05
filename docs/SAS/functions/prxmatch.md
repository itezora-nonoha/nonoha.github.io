## prxmatch関数

- 正規表現によりパターンマッチを行う。
- 返り値
  - 指定パターンが見つかった場合 ... 1以上の整数
  - 指定パターンが見つからなかった場合 ... 0

> [PRXMATCH Function - SAS Help Center](https://documentation.sas.com/doc/en/pgmsascdc/v_044/ds2ref/p0m49np18q0pdxn1laab98pazajo.htm)

### dataステップでの利用

``` sas
data _null_;
  prx_pattern = /[A-Z0-9_]+/;
  target_text = ABC_123;
  find_pos = prxmatch(prx_pattern, target_text);
  put find_pos=;
run;
```

### マクロ内での利用

``` sas

%macro test();
  %let prx_pattern = /[A-Z0-9_]+/;
  %let target_text = ABC_123;
  %let find_pos = %sysfunc(prxmatch(&prx_pattern, &target_text);
  %put find_pos is &find_pos;
%mend;

%test();
```

### メモ
- 正規表現の始端終端を表現するスラッシュ`/`を入れると、スラッシュ自身がパターン内の文字列として認識されてしまうことがある。そういう時はprxparseを挟むと確実。
``` sas

%let prx_pattern = %sysfunc(prxparse(/[A-Z0-9_]+/));
%let target_text = ABC_123;
%let find_pos = %sysfunc(prxmatch(&prx_pattern, &target_text));
```
