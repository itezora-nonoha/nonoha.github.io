## compress関数

- 指定文字列を全て取り除いた文字列を取得する。

### dataステップでの利用

``` sas
data _null_;
  text_before = 'aaa, bbb, ccc, ddd';
  text_after = compress(text_before, ',');
  put text_after=;
run;
```

### マクロ内での利用

``` sas

%macro test();
  %let text_before = 'aaa, bbb, ccc, ddd';
  %let text_after = %sysfunc(compress(&text_before., ','));
  %put text_after is &text_after;
%mend;

%test();
```
