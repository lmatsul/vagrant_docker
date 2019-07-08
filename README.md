Docker で開発環境を構築したい方向けに、  
vagrant コマンドで Docker や Docker Compose が動作する環境を立ち上げる Vagrantfile を用意しました

### 環境

- VirtualBox をインストールしていない方
https://www.virtualbox.org/wiki/Downloads  
上記URLからダウンロードしてきてインストールしてください  
※VirtualBox とは仮想環境を構築するためのツールです  
※試したのは バージョン 6.0.8

- Vagrant をインストールしていない方
https://www.vagrantup.com/downloads.html  
上記URLからダウンロードしてきてインストールしてください  
※Vagrant とは仮想環境の構築をサポートするツールです  
※試したのは バージョン 2.2.4

### 構成
```
data/         ・・・ ソースコードなどのマウント用ディレクトリ
Vagrantfile   ・・・ vagrant 用
```

### 使い方

適当な場所へ ディレクトリを作成し、コマンドプロンプト や PowerShell などを起動して、以下のコマンドを実行します

```sh
$ cd [作成したディレクトリパス]
$ git clone https://github.com/lmatsul/vagrant_docker.git
$ vagrant up
```
 
### SSH 接続してみる
無事、vagrant up による仮想環境の構築・起動が終わったら、以下のコマンドで SSH 接続してみます
 
```sh
 $ vagrant ssh
```

> もしくは別でターミナルを立ち上げて 127.0.0.1 の ポート 1234 へ SSH 接続する
 
接続出来たら、  
ユーザー名 `vagrant`  
パスワード `vagrant`  
を入力してログインします
 
### Docker、Docker Compser コマンドの確認
```bash
 # Docker のバージョン確認
 $ docker version
 
 # Docker Composer のバージョン確認
 $ docker-composer --version
```

無事、バージョンの確認が出来たら、環境の構築は完了です。