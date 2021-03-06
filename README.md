


# CARD4_CPU
  
## ワンボードリレー式コンピュータ


![enter image description here](https://imgur.com/d8OO1Yi.jpg)
  
## ・ファイルのディレクトリ構成
  
  
![enter image description here](https://imgur.com/DqaWnND.jpg)
  
  
## ・開発コンセプト
  
  
  
  (1) 　 CPUにはリレーを使用　(I/O・メモリは半導体使用可)
  
  (2) 　使用素子を可能な限り少なく抑える(実効速度等は二の次)　
  
  (3) 　パソコンと通信してプログラムのダウンロードやデバッグができるようにする

  
![enter image description here](https://imgur.com/dl9AJPW.jpg)


  まず、一般的なCPUの構成を以下に示します
  
## ・一般的なCPUの構成
   
![enter image description here](https://imgur.com/lGrUWV1.jpg) 
  
  



  このCPUの構成から、あまり必要ではない要素を削除して使用素子数を削減していきます。
  
###  (1) 命令デコーダは必要か？
    
  ・・・命令コードの各ビットを直接制御信号に割り当てるので必要ない
  
###  (2) プログラムカウンタは必要か？
  
  ・・・全ての命令をジャンプ命令(+副作用)とするので必要ない
  
###  (3) ALUは必要か？
  
  ・・・メモリテーブルのインデックス参照で演算を代行するので必要ない
  
例えば、C言語風に記述すると
  
  
  　int x;
  
  
  　int inc[16]={1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,0};
  
  
   とおいて
  
  　x=inc[x];
  
　とすると変数xを+1することができます  　
  
  
###  (4) レジスタは必要か？
  
  ・・・メモリは読み出し・書き込みが同時に出来ないので必要
  
  
  結局必要なのはレジスタ類と簡単な制御回路だけということになります。
  
  
  この結果をもとにCPUを再構成してみると以下のようになりました。
  
  
## ・新しく考えた CPUの構成
  
![enter image description here](https://imgur.com/tk3P1o5.jpg)  

  
  この新しく再構成したCPUを『CARD4』と名付けました。
  
  
  これをさらにもう少し詳細に描くと以下のようになります。
  
  


  
  

  
  
  
  
  
## ・CARD4 CPUのブロック図
  
![enter image description here](https://imgur.com/IUl5qlI.jpg)  
 
  
  
  
## ・外観
  
###  (1) レジスタ(4ビット分)
  
![enter image description here](https://imgur.com/zHtFXes.jpg)
  
###  (2) バッファ
  
![enter image description here](https://imgur.com/JmSPqQP.jpg)
  
###  (3) セレクタ
  
![enter image description here](https://imgur.com/Q9V3wOw.jpg)
  
###  (4) 周辺回路(メモリ＋入出力)
  
![enter image description here](https://imgur.com/hhhFdSw.jpg)
  
  
###  表示装置
  
![enter image description here](https://imgur.com/H4PImIJ.jpg)

    
###  全体
  
![enter image description here](https://imgur.com/d8OO1Yi.jpg)
  



## ・シミュレータ
  
  
  実機のない環境でも開発/実行を体験できるようにシミュレータが用意されています。
  
  
  CPUのシミュレーション、アセンブル、ソースコードの編集、デバッグ等がパソコン上で行えます。
  

    
###  ・実行画面
  
![enter image description here](https://imgur.com/PyoqBlu.jpg)  
  

### ・アセンブラソースコードの編集画面
  
![enter image description here](https://imgur.com/xseChi5.jpg)  
  
  
  
### ・実行結果
  
  
![enter image description here](https://imgur.com/23sktb7.jpg)
  
  
## ・アセンブラの命令
  
  org xxx
  
   ・・・カレントアドレスを数値xxxにセットする

  align16
  
   ・・・カレントアドレスを16ワード境界に揃える

  align256
  
   ・・・カレントアドレスを256ワード境界に揃える

  read xxx
  
   ・・・アドレスxxxのデータを読み出してカレントアドレスのdフィールドにセットする

  read@
  
  ・・・H,M,Lレジスタで指定されたアドレスのデータを読み出してカレントアドレスのdフィールドにセットする

  write xxx
  
  ・・・カレントアドレスのdフィールドの内容を指定アドレスxxxのデータフィールドにセットする


  write@
  
  ・・・カレントアドレスのdフィールドの内容をのH,M,Lレジスタで指定されたアドレスのデータフィールドにセットする


  set.h
  
  ・・・カレントアドレスのdフィールドの内容をHレジスタにセットする


  set.m
  
  ・・・カレントアドレスのdフィールドの内容をMレジスタにセットする


  set.l
  
  ・・・カレントアドレスのdフィールドの内容をLレジスタにセットする


  jmp  xxx
  
  ・・・指定アドレスxxxにジャンプする

  jmp@
  
  ・・・H,M,Lレジスタで指定されたアドレスにジャンプする


  data xxx
  
  ・・・Dレジスタに数値xxxをセットする
  
  
  data.h xxx
  
  ・・・Hレジスタに数値xxxをセットする
  
  
  data.m xxx
  
  ・・・Mレジスタに数値xxxをセットする
  
  
  data.l xxx
  
  ・・・Lレジスタに数値xxxをセットする
  
  
## ・コーディング例

### ・データ移動
  
  　  //　アドレスxxxの内容をアドレスyyyにコピーする
  
  　read xxx
  
  　write yyy
  
  ・
  
  ・
  
  ・
    
xxx:
  
  　  data 0
  
yyy:
  
  　data 1
  
  　
  
  　
  
  　
### ・演算

  
  
 　 //　アドレスxxxの値を+1する
  
　 read 　inc_table_h
  
　 read 　inc_table_m
  
　 read 　xxx
  
　 set.l
  
　 read@
  
　 write 　xxx
  
  
  ・
  
  ・
  
  ・
    

  
xxx:
  
　 data 0

  
// インクリメント演算用テーブルのアドレス(H)
  
inc_table_h:
  
　 data.h　 inc_table.h
  

// インクリメント演算用テーブルのアドレス(M)
  
inc_table_m:
  
　 data.m　 inc_table.m
  
// インクリメント演算用テーブル
  
　 align16
   
inc_table:
  
 　data 1
  
 　data 2
  
 　data 3
  
 　data 4
  
 　data 5
  
 　data 6
  
 　data 7
  
 　data 8
  
 　data 9
  
 　data 10
  
 　data 11
  
 　data 12
  
 　data 13
  
 　data 14
  
 　data 15
  
 　data 0
  
  　
  
  　
  
  　
### ・条件分岐
  
// アドレスxxxの内容が0ならyyyにジャンプして1ならzzzにジャンプする
  
  
  
  ・
  
  ・
  
  ・
    

  
  　 read 　jump_table_h
  
  　 read 　jump_table_m
  
  　 read 　xxx
  
  　 set.l
  
  　 jump@
  
  
  ・
  
  ・
  
  ・
    

  
  
xxx:
  
  　data 0
  
  
jump_table_h:
  
  　data.h　 jump_table.h
  
jump_table_m:
  
  　data.m　 jump_table.m
  
  　align16
  
jump_table:
  
  　 jmp yyy
  
  　 jmp zzz
  
  　
  
###  ・演算子について
  
  基本的な演算の他に以下のような演算子が用意されています。
  
  xxx.h
  
  ・・・数値xxxの12ビット中の上位4ビットを与える
  
  xxx,m
  
  ・・・数値xxxの12ビット中の中位4ビットを与える
  
  xxx.l
  
  ・・・数値xxxの12ビット中の下位4ビットを与える
    
  
  
## ・実機における動作の様子
  
  実機においても操作はシミュレータと同じくパソコン上でおこないます。
  
  
### ・操作画面
  
 画面構成や操作感はシミュレータの画面とほぼ同じです
  
  
![enter image description here](https://imgur.com/4A5fhDC.jpg)
    
  
## ・実行環境について
  シミュレータ等の実行やソースコード閲覧のためには
  Javaと[ObjectEditor](https://github.com/kousoz80/ObjectEditor)のインストールが必要です。
  
    
## ・動画
  
  実機の動作する様子をYouTubeで公開しています
  
https://www.youtube.com/watch?v=qONswbnE61M

