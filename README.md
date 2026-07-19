# azure-lamp-bicep

Bicep(ARMテンプレート)を使い、Azure仮想マシン上にLAMP環境を構築するIaCコードです。VM・NSG・NIC・VNet・パブリックIPをすべてコードで定義し、cloud-init(customData)によってApache/PHP/MySQLのインストールとWebページ配置を自動化しています。手動構築の`azure-lamp-setup-guide`をコード化したものにあたり、AWSでの`aws-lamp-terraform`に対応するAzure版です。

## 構成内容

- `main.bicep` — VM、NSG(SSH制限/HTTP開放)、VNet、パブリックIP、NICの定義
- cloud-initによるApache/PHP/MySQLの自動インストールとWebページ配置
- SSH公開鍵・送信元IP制限をパラメータとして外部から注入(秘密情報はリポジトリに含めない)

## 使い方

```bash
az group create --name <リソースグループ名> --location japaneast
az deployment group create \
  --resource-group <リソースグループ名> \
  --template-file main.bicep \
  --parameters sshPublicKey=@<公開鍵ファイル> allowedSshSourceIp="<自分のIP>/32" adminUsername=azureuser
```

## 関連リポジトリ

- [azure-lamp-setup-guide](https://github.com/saki-nya1539/azure-lamp-setup-guide) — 手動構築の手順書
- [azure-fundamentals-notes](https://github.com/saki-nya1539/azure-fundamentals-notes) — Azure基礎知識まとめ
- [aws-lamp-terraform](https://github.com/saki-nya1539/aws-lamp-terraform) — AWS版のIaCコード(Terraform)
