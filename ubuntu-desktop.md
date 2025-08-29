
```
# パッケージ更新
sudo apt update && sudo apt upgrade -y

# Ubuntu Desktopをインストール（最小版）
sudo apt install ubuntu-desktop -y

```

ubuntu-desktop は重いので、軽量なGUIなら xfce4 または lxde を推奨。

```
sudo apt install xfce4 xfce4-goodies -y

```

# リモートアクセス方法の選択

X2Go（おすすめ）

VNCより高速でセキュア。

サーバ側

```
sudo apt install x2goserver x2goserver-xsession -y

```

クライアント側

X2Go Client
https://wiki.x2go.org/doku.php/doc:installation:x2goclient
をローカルにインストール。

接続設定

SSHの認証情報で接続。

セッションタイプは XFCE など軽量デスクトップを選択。

