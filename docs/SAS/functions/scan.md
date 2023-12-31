## scan関数 / %scanマクロ関数

- 任意の文字列を指定文字で区切った際のN番目の文字列を取得する。

### dataステップでの利用

``` sas
data _null_;
  text = 'aaa, bbb, ccc, ddd';
  word = scan(text, 3, ',');
  put word=; /" 3番目の文字列「ccc」が出力される */
run;
```

### マクロ内での利用

``` sas
%macro test();
  %let text = 'aaa, bbb, ccc, ddd';
  %let word = %scan(&text, 3, ',');
  %put word = &word; /" 3番目の文字列「ccc」が出力される */
%mend;

%test();
```

### メモ

#### 区切り文字の指定について
- 第三引数における「区切り文字」の指定は「文字のリスト」として解釈されるため、'.,'と指定した場合は','および'.'の2つが区切り文字として解釈される。
- また、区切り文字としてマルチバイト文字は指定できない。（マルチバイト文字を使用したい場合はkscan関数を使用する）

#### 第四引数について
  - 第四引数を指定しない場合、先頭の区切り文字は無視される」「連続した区切り文字は1津の区切り文字として解釈される」仕様のため、これを避けたい場合にはとして'M'を指定してあげる必要がある。
