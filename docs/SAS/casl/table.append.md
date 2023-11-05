## table.appendアクション

- テーブルを縦方向に結合する。

``` sas
libname casuser cas caslib="casuser";
proc cas;
  table.append /
    source={caslib='casuser', name='t1', where="age < 15"},
    target={caslib='casuser', name='t2};
run;
```

