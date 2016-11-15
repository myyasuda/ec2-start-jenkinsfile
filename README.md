# ec2を起動してパブリックIPをメール通知するJenkinsfile

## 前提

aws-cliを利用できるスレーブを用意しておく必要があります。  
ノード名（ラベル）に「aws-cli」を指定します。  

## 設定

1. 「Pipeline」ジョブを作成します。
2. 「ビルドのパラメータ化」をチェックし、以下のパラメータを設定します。

|type|name|notes|
|----|----|-----|
|文字列/選択値|EC2_INSTANCE_ID|起動対象のインスタンスIDを設定します。|
|文字列/選択値|AWS_PROFILE|AWSのプロファイル名を指定します。|
|文字列/選択値|MAIL_TO|送信先のメールアドレスを指定します。|
|文字列|MAIL_SUBJECT|メール件名を入力します。|
|テキスト|MAIL_BODY|メール本文を入力します。「publicIpAddress」という文字列をインスタンスのパブリックIPに置き換えます。|
