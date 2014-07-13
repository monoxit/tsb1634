# _Attiny 1634 シリアル ブート ローダー_

_オリジナル TinySafeBoot http://jtxp.org/tech/tinysafeboot_en.htm._  
_Attiny1634対応_
_Bluetooth接続対応_

## プロジェクトセットアップ

### _開発環境_

* TinySafeBoot http://jtxp.org/tech/tinysafeboot_en.htm
* Atmel Studio 6.2
* AVRライター (例 AdafruitのUSBtinyISP)
* FreeBasic
* Ruby (hexコードのフォーマットに使用)

### _ビルドから動作確認の手順_

1. Atmel Studioで tsb1634.atsln を開き、プロジェクトをビルド。
2. hexコードをフォーマット。例）>ruby -i.bak -pe '$_.gsub!(/(.+)/,"data \"\\1\"")' tsb1634.hex
3. TinySafeBootのdata.bas内のtn1634部をフォーマット済のhexコードと入れ替え。
4. FreeBasicでTSBソフトウェア(ホスト側のツール）をコンパイル。例）>fbc tsb.bas
5. TSBソフトウェアでブートローダーコード（.hexファイル）を作成。例）>tsb tn1634 a7b0
6. AVRライターでターゲットの自己プログラミングを有効に。例） >avrdude -c usbtiny -p t1634 -U efuse:w:0xFE:m
7. AVRライターでターゲットにブートローダーを書き込む。例）>avrdude -c usbtiny -p t1634 -U flash:w:tsb_tn1634_a7b0_20140619.hex
8. USB (またはBluetooth) UART変換モジュールのTX/RXをターゲットのPA7:RX/PB0:TXに接続。
9. 接続の確認。例）ターゲットリセット後、 >tsb com5 i
10. アプリケーションの書き込み。ターゲットリセット後、 >tsb com5 fw MI100R6.cpp.hex

## ライセンス
GPLv3

