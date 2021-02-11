# covid19-chiba-tools

千葉県版のツール

## setup

```bash
git clone https://github.com/civictechzenchiba/covid19-chiba-tools.git
cd covid19-chiba-tools
python3 -m venv venv
source venv/bin/activate
pip install -U pip
pip install -r requirements.txt
```
## debug

```
% python download_pubdata.py                                                                                                          (git)-[feature-main-summary-format-changed]
0211 0210
We failed to reach a server.
Reason:  Not Found https://www.pref.chiba.lg.jp/shippei/press/2019/documents/0211chiba_corona_data.xlsx
download success:https://www.pref.chiba.lg.jp/shippei/press/2019/documents/0210chiba_corona_data.xlsx

% python convert_pubdata.py | jq . > data/DataPub.json

```

## deploy to aws lambda

### setup
* AWS アカウントを作成し、そのなかに結果出力用のS3bucketと、covid19chiba-deployというlambda functionを作成しておく
* 現在はweb front側から下記のS3bucketにあるデータをDownloadする設定になっている
  - https://covid19chiba.s3-ap-northeast-1.amazonaws.com/DataPub.json
* 上記は　現状 kozayupapaの個人アカウント上で構築している　移行する場合はWebFront側の参照パスもあわせて更新する必要あるので注意


* Test
  - `./deploy-aws-lambda.sh covid19chiba-tool ap-northeast-1 Test_1 covid19chiba-deploy`

* Prod
  - `% ./deploy-aws-lambda.sh covid19chiba-tool ap-northeast-1 Prod covid19chiba-deploy  `