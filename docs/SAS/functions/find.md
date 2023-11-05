## find関数

- 部分文字列を検索する。

> 第三引数として「検索開始位置」を指定することも可能。

### dataステップでの利用

``` sas
data _null_;
  find_text = 'wo';
  text = 'hello world';
  result = find(text, find_text);  
  put result=;
run;
```

### マクロ内での利用

``` sas
%macro test();
  %let find_text = 'wo';
  %let text = 'hello world';
  %let result = %sysfunc(find(&text, &find_text));
  %put result is &result;
%mend;

%test();
```
