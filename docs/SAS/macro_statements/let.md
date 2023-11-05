## letマクロステートメント

- マクロ変数に値を代入する。

### dataステップでの利用

- `call symputx`ルーチンを使用する。
  - [symputxルーチン](/docs/SAS/call_routine/symputx.md)

### マクロ内での利用

``` sas
%macro test();
  %let text = 'hogehoge';
  %put text = &text;
%mend;

%test();
```
