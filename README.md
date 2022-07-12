# .dotfiles

***

# 環境構築メモ

## Surface Pro7
Ubuntu-20.04 LTS on WSL2  
Python: pyenv + poetry, ~~Anaconda~~

### WSL2
#### 1. GPUドライバーのアップデート
「インテル® グラフィックス・コマンド・センター」経由で、GPUドライバーをアップデートする。

#### 2. WSL2のインストール
「コマンドプロンプト」を管理者権限で開き、下記のコマンドを実行する。  
```
wsl --install -d Ubuntu-20.04
```
(`wsl -l -o`でインストールするディストリビューションが最新であるか、あらかじめ確認しておくこと。)  
-d で使用するディストリビューションを指定すると、それのインストールも付随して行われる。  
再起動後Ctrl+Cで新規ユーザー作成を抜けることで、デフォルトユーザーをrootにすることができる。

##### WSLgの動作確認
`sudo apt update` パッケージリストを更新  
`sudo apt upgrade -y` パッケージを更新  
`sudo apt install x11-apps -y` X11アプリのインストール  
`xeyes`  
xeyesが起動することを確認する。

#### 3. Visual Studio Codeの導入
VSCodeをインストールし、GitHubと連携して設定を同期する。  
拡張機能「Remote Development」をインストールして、リモートエクスプローラーからUbuntu(WSL2)に接続する。

#### ref
[WSL のインストール | Microsoft Docs](https://docs.microsoft.com/ja-jp/windows/wsl/install)


### Python
#### 1. pyenvのインストール
[公式](https://github.com/pyenv/pyenv/wiki#suggested-build-environment)より推奨されるビルド環境を満たすため、下記のコマンドを実行する。
```
sudo apt-get update; sudo apt-get install make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
```
`cd ~` でホームディレクトリに移動してから、下記のコマンドでインストールする。
```
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```
パスを通すために、`.bashrc`に以下を追加する。
```
export PYENV_ROOT="$HOME/.pyenv"
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
```

#### 2. Pythonのインストール
`pyenv install --list`  
`pyenv install 3.○.○`  
`pyenv global 3.○.○`

#### 3. poetryのインストール
```
curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python -
```
下記のコマンドで、プロジェクトフォルダ直下に仮想環境が作られるようにする。これによりVSCodeが自動で仮想環境を認識するようになる。
```
poetry config virtualenvs.in-project true
```

#### ref
[pyenv/pyenv: Simple Python version management](https://github.com/pyenv/pyenv)  
[Introduction | Documentation | Poetry - Python dependency management and packaging made easy](https://python-poetry.org/docs/)


#### ~~Anaconda on Linux~~
##### 1. 導入前の準備
[公式](https://docs.anaconda.com/anaconda/install/linux/)より、GUIアプリを利用するために必要なパッケージをインストールする。
```
sudo apt install libgl1-mesa-glx libegl1-mesa libxrandr2 libxrandr2 libxss1 libxcursor1 libxcomposite1 libasound2 libxi6 libxtst6
```

##### 2. インストーラーのダウンロード、実行
[Anaconda | Anaconda Distribution](https://www.anaconda.com/products/distribution)から、「Linux 64-Bit(x86) Installer」のリンクをコピーする。  
`wget` でコピーしたリンクを指定し、インストール用ファイルをダウンロードする。  
`bash` でダウンロードしたインストール用ファイルを指定し実行する。  
表示に従い、Enterやyesと入力する。  
※ conda initを実行しますか。という問いかけにnoと答えると、手動でconda initすることになり二度手間なので注意。  
インストール終了後、ターミナルを再起動する。

##### 3. condaのアップデート
`conda update conda` condaを最新のバージョンにアップデートできる。
