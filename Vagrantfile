Vagrant.configure("2") do |config|

  # Vagrant Box で 「bento/ubuntu-18.04」を指定
  config.vm.box = "bento/ubuntu-18.04"

  # IPアドレスの設定
  config.vm.network "private_network", ip: "192.168.33.10"

  # ホストのポート1234へのアクセスをVMのポート22に転送
  # ※127.0.0.1:1234 が 192.168.33.10:22 へ転送される
  # ※vagrant up 時に利用される
  # ※設定しない場合、guest:22, host: 2222 がデフォルトで割り当たる
  # ※適宜ホストで空いているポートに変更してください
  config.vm.network "forwarded_port", guest: 22, host: 1234, id: 'ssh'

  # SSH 秘密鍵を利用しない（所詮ローカルの確認環境のため）
  config.ssh.insert_key = false
  config.ssh.username = 'vagrant'
  config.ssh.password = 'vagrant'

  # ディレクトリをマウント
  config.vm.synced_folder "./data", "/vagrant_data"

  # シェルスクリプトの実行
  # ※privileged は sudo で実行するかのフラグ（デフォルトは true）
  config.vm.provision :shell, privileged: false, inline: $script
end

$script = <<SCRIPT

######################################################################
# Docker リポジトリの登録

# パッケージの更新
sudo apt-get update

# HTTPS利用のためのパッケージをインストール
sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common

# Docker公式の GPG を追加
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# リポジトリの設定
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

######################################################################
# Docker CE のインストール
# （https://docs.docker.com/install/linux/docker-ce/ubuntu/）

# パッケージの更新
sudo apt-get update

# Docker CE のインストール
sudo apt-get install -y docker-ce

######################################################################
# Docker Compose のインストール
# （https://docs.docker.com/compose/install）

# Docker compose のダウンロード
# ※適宜 https://github.com/docker/compose/releases の最新バージョンへ書き換えてください
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# 実行権限の付与
sudo chmod +x /usr/local/bin/docker-compose

######################################################################
# vagrant ユーザーを docker グループへ追加

sudo usermod -aG docker vagrant

SCRIPT