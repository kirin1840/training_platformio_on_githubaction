# training_platformio_on_githubaction

## 目的
組込み開発でのCI/CT環境を構築するにあたり、
PlatformIOとGithub　Actionでのトレーニング資料を作成する。

## PlatformIOのコマンド調査

## Reference
https://docs.platformio.org/en/latest/integration/ci/github-actions.html

## ２つのコマンド存在
どちらかを選択して、

### Using pio run command
pio run コマンドは、PlatformIOのビルド、書き込みを実行するためのコマンド
-e のオプションで、Target環境を指定することができる。
通常ターゲット環境は “platformio.ini”　で定義されていることが多い。

### Using pio ci command
pio ci コマンドは、継続的インテグレーションを支援するためのコマンド。pio runと同じく、ビルド、書き込みが可能
通常、platformio.iniでデバイス等の構成を決めているが、pio ciコマンドで、
環境およびライブラリの組み合わせを任意に設定できるので、複数のプロジェクトを作成しなくても、
一括でのビルドが可能になる。

フォーマット
~~~
 - name: Run PlatformIO
  run: pio ci path/to/test/file.c --lib="/tmp/OneWire-master" --board=<ID_1> --board=<ID_2> --board=<ID_N>
~~~  
サンプルコード
~~~  
- name: Run PlatformIO
      run: pio ci --lib="." --lib="/tmp/spi4teensy3-master" --board=uno --board=teensy31 --board=due
      env:
        PLATFORMIO_CI_SRC: ${{ matrix.example }}
~~~  

--lib ・・・利用するライブラリを指定
--board ・・・ 実行環境をしている。


