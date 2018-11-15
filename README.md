# Re:ゼロから始めるテスト駆動開発

# 目的

実践テスト駆動開発

# 前提

| ソフトウェア       | バージョン | 備考 |
| :----------------- | :--------- | :--- |
| Visual Studio Code |            |      |
| vagrant            | 2.0.3      |      |
| Ruby               | 2.5.3      |      |
| Node.js            | 8.10.0     |      |
| Python             | 3.6.0      |      |

# 構成

1. [構築](#構築)
1. [配置](#配置)
1. [運用](#運用)
1. [開発](#開発)

## 構築

### エディタの用意

- [Visual Studio Code のインストール](https://code.visualstudio.com/)
- [VS Live Share Extension Pack のセットアップ](https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare-pack)

### 開発用仮想マシンの起動・プロビジョニング

```bash
vagrant up
vagrant ssh
```

### ドキュメント環境構築セットアップ

```bash
curl -s api.sdkman.io | bash
source "/home/vagrant/.sdkman/bin/sdkman-init.sh"
sdk list maven
sdk use maven 3.5.4
sdk list java
sdk use java 8.0.181-zulu
sdk list gradle
sdk use gradle 4.10
```

### 開発パッケージのセットアップ

#### 共通ライブラリのセットアップ

```
sudo yum update -y
sudo yum install -y build-essential \
                   libssl-dev \
                   gcc-c++  \
                   openssl-devel  \
                   bzip2-devel  \
                   zlib-devel  \
                   readline-devel  \
                   sqlite-devel  \
                   python-devel  \
                   python3-dev
```

#### Ruby のセットアップ

- rbenv のインストール
- ruby-build のインストール
- Ruby のインストール

```bash
cd /vagrant
git clone https://github.com/sstephenson/rbenv ~/.rbenv
git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
sudo ~/.rbenv/plugins/ruby-build/install.sh
echo 'export PATH="~/.rbenv/bin:$PATH"' >> ~/.bash_profile
echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
source ~/.bash_profile
rbenv install --list
rbenv install 2.5.3
rbenv local 2.5.3
```

#### Node.js のセットアップ

- nvm のインストール
- Node.js のインストール

```bash
cd /vagrant
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.3/install.sh | bash
source ~/.bashrc
nvm install v8.10
nvm alias default v8.10
```

#### Python のセットアップ

- pyenv のインストール
- Python のインストール

```bash
curl -L https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer | bash
```

`~/.bashrc`に以下を追加して`source ~/.bashrc`

```
export PATH="/home/vagrant/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

利用する Python のバージョンをインストールする

```
cd /vagrant
pyenv install -l
pyenv install 3.6.0
pyenv local 3.6.0
```

**[⬆ back to top](#構成)**

## 配置

ドキュメントの生成

```
cd /vagrant
gradle build
gradle asciidoctor
gradle livereload
```

[http://localhost:35729/](http://localhost:35729/)に接続して確認する

**[⬆ back to top](#構成)**

## 運用

**[⬆ back to top](#構成)**

## 開発

**[⬆ back to top](#構成)**

# 参照

- [AWS SAM Node.js Hands-on](https://github.com/hiroshima-arc/aws_sam_nodejs_hands-on)
- [AWS SAM Python Hands-on](https://github.com/hiroshima-arc/aws_sam_python_hands-on)
