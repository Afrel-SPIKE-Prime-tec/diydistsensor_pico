# diydistsensor_pico

![2022-02-21_15-47-27_881](https://user-images.githubusercontent.com/5597377/154905247-233a7a38-cc52-4383-bda5-a77daba564c4.jpg)

## 概要
LEGO(R) SPIKE Prime用のDistance Sensorとして認識される自作のセンサーです。 1～9のダミーデータを返します。

## 材料
・Raspberry Pi Pico。

・SPIKE用カードエッジ　https://github.com/Afrel-SPIKE-Prime-tec/spikeconnector

・ジャンパーワイヤー

## 組み立てと実行
以下の回路図の通りに接続します。

![diy_distance_pico_sch](https://user-images.githubusercontent.com/5597377/154905261-ef6340d6-0085-4a5c-b20f-fb17dea6bce3.png)

・Raspberry Pi PicoにMicroPythonのファームウェアを書き込みます。

・Thonnyなどを使って、Pythonのコードを実行します。

## プロトコル
(1)接続の開始
通信速度は2400bps。 20ms周期で、Hub→Sensorへ0xF0を送信。 受信するとセンサー側がHubの存在を確認。Sensor→Hubへ約500ms Low信号を送る。

(2)センサー情報を送信
Sensor→Hubへセンサー情報を送信。

(3)接続の完了待ち
Hub→Sensorに0x04が送信されたら、接続の成功。以後、ボーレートを115200bpsに変更する。 0x04が送信されない場合、(1)へ戻る。

(4)コマンド受信＆レスポンス返信
Hub→Sensorにコマンド送信。Sensor→Hubへレスポンス返信。返信後、(4)を繰り返す。 一定時間コマンドが到着しない場合はエラーとして、(1)へ戻る。

## 参考資料
https://github.com/sonoisa/cheese/

https://github.com/ahmedjouirou/legopup_arduino

https://www.philohome.com/wedo2reverse/protocol.htm

