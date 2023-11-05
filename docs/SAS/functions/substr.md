## substr関数 / %substrマクロ関数

- 任意の文字列から文字列を切り出す。

### dataステップでの利用

``` sas
data _null_;
  text = 'aaa, bbb, ccc, ddd';
  word = substr(text, 6, 3);
  put word=; /" 6文字目から3文字分の「ccc」が出力される */
run;
```

### マクロ内での利用

``` sas
%macro test();
  text = 'aaa, bbb, ccc, ddd';
  word = %substr(&text, 6, 3);
  %put word = &word; /" 6文字目から3文字分の「ccc」が出力される */
%mend;

%test();
```
