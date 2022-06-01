# .dotfiles

***

# Surface Pro 7 環境構築メモ

Ubuntu-20.04 LTS on WSL2

## WSL2の導入
### 1. GPUドライバーのインストール
[WSL で Linux GUI アプリを実行する | Microsoft Docs](https://docs.microsoft.com/ja-jp/windows/wsl/tutorials/gui-apps)の前提条件を見て、システムに一致するGPUドライバーをインストールする。  

### 2. WSL2のインストール
`wsl --install -d Ubuntu20.04`  
-d で使用するディストリビューションを指定すると、それのインストールも付随して行われる。

### 3. WSLgの動作確認
`sudo apt update` パッケージリストを更新  
`sudo apt upgrade -y` パッケージを更新  
`sudo apt install x11-apps -y` X11アプリのインストール  
`xeyes`  
xeyesが起動することを確認する。

### 4. Visual Studio Codeの導入
[Download Visual Studio Code - Mac, Linux, Windows](https://code.visualstudio.com/download)  
インストールしたら、GitHubと連携して設定を同期する。  
拡張機能「Remote Development」をインストールする。

### 5. VSCodeとWSL2の接続
「Remote Explorer」からUbuntuに接続する。この際、接続時に必要なコンポーネントがUbuntuにインストールされる。  
`code . ` と、Ubuntu側からVSCodeを起動してもよい。


## Anaconda on Linuxの導入
### 1. 導入前の準備
[Installing on Linux — Anaconda documentation](https://docs.anaconda.com/anaconda/install/linux/)  
`sudo apt install libgl1-mesa-glx libegl1-mesa libxrandr2 libxrandr2 libxss1 libxcursor1 libxcomposite1 libasound2 libxi6 libxtst6`  
で、GUIアプリを利用するために必要なパッケージをインストールする。

### 2. インストーラーのダウンロード、実行
[Anaconda | Anaconda Distribution](https://www.anaconda.com/products/distribution)から、「Linux 64-Bit(x86) Installer」のリンクをコピーする。  
`wget` でコピーしたリンクを指定し、インストール用ファイルをダウンロードする。  
`bash` でダウンロードしたインストール用ファイルを指定し実行する。  
表示に従い、Enterやyesと入力する。  
※ conda initを実行しますか。という問いかけにnoと答えると、手動でconda initすることになり二度手間なので注意。  
インストール終了後、ターミナルを再起動する。

### 3. condaのアップデート
`conda update conda`
condaを最新のバージョンにアップデートできる。


