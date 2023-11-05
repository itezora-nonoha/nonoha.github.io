
### call symputxルーチン

- dataステップ内でマクロ変数に値を代入する。
  - 第三引数に'G'を設定することで、グローバル変数として設定・代入できる。

### dataステップ内での使用
``` sas
data _null_;
  call symputx('model_list', model_list);
  call symputx('model_list_global', model_list, 'G');
run;
```

### マクロ内での利用
- `%let`ステートメントを使用する。
  - [letマクロステートメント](/docs/SAS/macro_statements/let.md)
