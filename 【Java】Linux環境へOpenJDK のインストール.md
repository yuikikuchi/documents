# Linux環境へOpenJDK のインストール

<div style="text-align: right;">2020/11/04</div>

## 1. JRE/JDKのインストール

まずパッケージインデックスを更新.
```
$ sudo apt-get update
```



JRE/JDKがインストールされているか確認.
```
$ java -version
```
`Command 'java' not found, but can be installed with:`と出力された.
Javaがインストールされていないぽい.



JRE/JDKのインストールを実行.

```
$ sudo apt-get install default-jre
$ sudo apt-get install default-jdk
```

```
$ java -version
openjdk version "11.0.9" 2020-10-20
OpenJDK Runtime Environment (build 11.0.9+11-Ubuntu-0ubuntu1.20.04)
OpenJDK 64-Bit Server VM (build 11.0.9+11-Ubuntu-0ubuntu1.20.04, mixed mode, sharing)
```
成功.



##  2. Open JDK

Open JDKは、Ubuntu の universe リポジトリで提供されている.
先の手順でデフォルトのJRE/JDKとしてOpen JDKのどれかがすでにインストールされているかもしれない.
その他に必要であれば、バージョンに応じてコマンドを実行.

下記の必要なバージョンのみ実行でOK.
* JRE

```
$ sudo apt-get install openjdk-8-jre
$ sudo apt-get install openjdk-7-jre
$ sudo apt-get install openjdk-6-jre
```
* JDK

```
$ sudo apt-get install openjdk-8-jdk
$ sudo apt-get install openjdk-7-jdk
$ sudo apt-get install openjdk-6-jdk
```



## 3. Javaの管理

複数のJavaの中から、デフォルトとして使用するJavaを選択する.
```
$ sudo update-alternatives --config java
There are 2 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                            Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      auto mode
  1            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      manual mode
  2            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      manual mode

Press <enter> to keep the current choice[*], or type selection number:
```
今回はJava8を使用したいため、`2`を選択.



```
$ java -version
openjdk version "1.8.0_272"
OpenJDK Runtime Environment (build 1.8.0_272-8u272-b10-0ubuntu1~20.04-b10)
OpenJDK 64-Bit Server VM (build 25.272-b10, mixed mode)
```

デフォルトから指定されたバージョンのOpenJDKに変更されたことを確認.



javacも同様にしてデフォルトの選択が可能.
```
$ sudo update-alternatives --config javac
There are 2 choices for the alternative javac (providing /usr/bin/javac).

  Selection    Path                                          Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-11-openjdk-amd64/bin/javac   1111      auto mode
  1            /usr/lib/jvm/java-11-openjdk-amd64/bin/javac   1111      manual mode
  2            /usr/lib/jvm/java-8-openjdk-amd64/bin/javac    1081      manual mode

Press <enter> to keep the current choice[*], or type selection number:
```



## 4. 環境変数 JAVA_HOME の設定

インストール済みのJavaを確認.
```
$ sudo update-alternatives --list java
/usr/lib/jvm/java-11-openjdk-amd64/bin/java
/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java
```



環境変数へ`JAVA_HOME`を設定
```
$ export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
```
完了.



もしくは、、、

システム全体の環境変数は /etc/profile.d/ で設定できる.

例えば java.shファイルを作成.

```
$ vi /etc/profile.d/java.sh
JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
```



現在のシェルに作成したファイルを読み込む.
```
$ source /etc/profile.d/java.sh
```



環境変数 JAVA_HOME が設定されたか確認.
```
$ echo $JAVA_HOME
/usr/lib/jvm/java-8-openjdk-amd64
```
OK.


