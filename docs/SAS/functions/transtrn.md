## transtrn関数

- 文字列の置き換えを行う。

### dataステップでの利用

``` sas
data _null_;
  text = 'hogehoge';
  text_replaced = transtrn(text, 'ge', 'ku');
  put text_replaced=;
run;
```

### マクロ内での利用

``` sas
%macro test();
  %let text = 'hogehoge';
  %let text_replaced = %sysfunc(transtrn(&text, 'ge', 'ku'));
  %put text_replaced = &text_replaced;
%mend;

%test();
```

### メモ
#### 文字リテラルの扱いについて（SAS言語の仕様に関するもの。別のところに記載を移管予定）

- SASは文字列内の最初の文字をチェックし、それが数値または算術演算子の場合はパラメータを%eval()する
