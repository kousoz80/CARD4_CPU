


# CARD4_CPU
  
## リレー式コンピュータ


![enter image description here](https://imgur.com/d8OO1Yi.jpg)
  
### ・ファイルのディレクトリ構成
  
  
![enter image description here](https://imgur.com/DqaWnND.jpg)
  
  
### ・開発コンセプト
  
  
  
  (1) 　 CPUにはリレーを使用　(I/O・メモリは半導体使用可)
  
  (2) 　使用素子を可能な限り少なく抑える(実効速度等は二の次)　
  
  (3) 　パソコンと通信してプログラムのダウンロードやデバッグができるようにする

  
![enter image description here](https://imgur.com/dl9AJPW.jpg)


  まず、一般的なCPUの構成を以下に示します
  
### ・一般的なCPUの構成
   
![enter image description here](https://imgur.com/lGrUWV1.jpg) 
  
  



  このCPUの構成をあまり必要ではない要素を削除して使用素子数を削減していきます。
  
  (1) 命令デコーダは必要か？
命令コードの各ビットを直接制御信号に割り当てるので必要ない。
  
  (2) プログラムカウンタは必要か？
全ての命令をジャンプ命令(+副作用)とするので必要ない
  
  (3) ALUは必要か？
メモリテーブルのインデックス参照で演算を代行するので必要ない(下図参照)
  
  
(図)
  
  
  (4) レジスタは必要か？
  メモリは読み出し・書き込みが同時に出来ないので必要です。
  
  
  結局必要なのはレジスタ類と簡単な制御回路だけということになります。
  
  
  この結果をもとにCPUを再構成してみると以下のようになりました。
  
  
### ・新しく考えた CPUの構成
  
![enter image description here](https://imgur.com/tk3P1o5.jpg)  

  
  この新しく再構成したCPUをCARD4と名付けることにします。
  
  
  これをさらにもう少し詳細に描くと以下のようになります。
  
  


  
  

  
  
  
  
  
### ・CARD4 CPUのブロック図
  
![enter image description here](https://imgur.com/IUl5qlI.jpg)  
 
  
  
  
### ・外観
  
  (1) レジスタ(4ビット分)
  
![enter image description here](https://imgur.com/zHtFXes.jpg)
  
  (2) バッファ
  
![enter image description here](https://imgur.com/JmSPqQP.jpg)
  
  (3) セレクタ
  
![enter image description here](https://imgur.com/Q9V3wOw.jpg)
  
  (4) 周辺回路(メモリ＋入出力)
  
![enter image description here](https://imgur.com/hhhFdSw.jpg)
  
  
  表示装置
  
![enter image description here](https://imgur.com/H4PImIJ.jpg)

    
  全体
  
![enter image description here](https://imgur.com/d8OO1Yi.jpg)
  



### ・シミュレータ
  
  
  実機のない環境でも体験できるようにシミュレータが用意されています。
  
  
  CPUのシミュレーション、アセンブル、ソースコードの編集、デバッグ等がパソコン上で行えます。
  

    
  ・実行画面
  
![enter image description here](https://imgur.com/PyoqBlu.jpg)  
  

・アセンブラソースコードの編集画面
  
![enter image description here](https://imgur.com/xseChi5.jpg)  
  

### ・アセンブラの命令
  
  read xxx
  
   ・・・アドレスxxxのデータを読み出してカレントデータフィールドにセット

  read (hml)
  
  ・・・H,M,Lレジスタで指定されたアドレスのデータを読み出してカレントデータフィールドにセット

  write xxx
  
  ・・・カレントデータフィールドの内容を指定アドレスxxxのデータフィールドにセット


  write (hml)
  
  ・・・カレントデータフィールドの内容をのH,M,Lレジスタで指定されたアドレスのデータフィールドにセット


  jmp  xxx
  
  ・・・指定アドレスxxxにジャンプ

  jmp (hml)
  
  ・・・H,M,Lレジスタで指定されたアドレスにジャンプ


  data xxx
  
  ・・・カレントアドレスのデータフィールドに数値xxxをセットする
  
  
### ・コーディング例

・データ移動

・演算
  
  
  
・条件分岐
  
  
  
  
  
  ※演算子について
  
  基本的な演算の他に以下のような演算子が用意されています。
  
  xxx.h
  
  ・・・数値xxxの12ビット中の上位4ビットを与える
  
  xxx,m
  
  ・・・数値xxxの12ビット中の中位4ビットを与える
  
  xxx.l
  
  ・・・数値xxxの12ビット中の下位4ビットを与える
    
  
  
### ・実機における動作の様子
  
  実機においても操作はシミュレータと同じくパソコン上でおこないます。
  
  
・操作画面
  
 画面構成や操作感はシミュレータの画面とほぼ同じです
  
  
![enter image description here](https://imgur.com/4A5fhDC.jpg)
  
  
・動画
  
  実機の動作する様子をYoutubeで公開しています
  
https://www.youtube.com/watch?v=qONswbnE61M

