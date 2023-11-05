## compress関数

- 文字列に含まれる特定の文字列の数を計上する。

### dataステップでの利用

``` sas
data _null_;
  text = 'aaa, bbb, ccc, ddd';
  count = count(text, ',');
  put count=;
run;
```

### マクロ内での利用

``` sas
%macro test();
  %let text = 'aaa, bbb, ccc, ddd';
  %let count = %sysfunc(count(&text, ','));
  %put count is &count;
%mend;

%test();
```
