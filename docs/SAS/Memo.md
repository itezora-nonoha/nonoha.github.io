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
