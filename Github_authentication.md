# Authentication
- 基本：ユーザーネームとパスワード
- 問題：basicHTTP認証のため、セキュリティリスクがある

1. Personal access tokens(Pats)
    - APIを使うためのもの、
2. SSH keys
    - 設定したら毎回のユーザーネームやトークンを入れる必要がなくなる
    - 組織によってSSH証明書が提供されるなら、その証明書をアカウントに追加することなくアクセスできる。
3. Deploy key
    - 1つのリポジトリへのアクセス権をユーザーに付与するSSHキー

## 追加のセキュリティオプション
1. 2要素認証(2FA) (MFAの一種)
    - パスワードの後に、もう一つ認証を追加するもの
    - SMSのコード
    - エンタープライズ所有者はエンタープライズアカウントによって所有される全ての組織に特定のセキュリテキーポリシーを科せられる
2. SAML SSO
    - IDプロパイダー(IdP)を利用してユーザいのIDとアプリケーションを一元的に管理している場合は、Github内で組織のリソースを保護するために、Security Assertion Markup Language(SAML)　SSOを構成できる。
3. LDAP
    - サードパーティのソフトウェアを大規模な企業ユーザーディレクトリと統合するために最もよく使われるプロトコル

# Github accounts
GitHubのアカウントは３種類ある
1. Personal
2. Organization
3. Enterprise

### Personal
2つのプランがある
- GitHub Free
- GitHub Pro
Freeだとプライベートリポジトリの数が制限されるらしい

### Organization
無制限の数のユーザが一度に多くのプロジェクトで共同作業できる共有アカウント<br>
サービスレベルのアクセス許可<br>
Organizationのさまざまなロールを付与してデータに異なるレベルのアクセス権を付与できる。<br>
Organizationの設定を管理したり、データへのアクセスを制御できるのは、Organization OwnerとSecurity Managerのみ

### Enterprise
複数のOrganizationのポリシーと請求を管理できる<br>
Organization間のInner Sourcing(?)を可能にする。<br>
Enterpriseアカウントを使用すると、所有するすべての組織に対してポリシーを管理適用できる。

## plan
### Github Free
**Personal account**
**Organization account**<br>
- publicリポジトリは全機能、無制限
- privateは機能制限
- 無制限のコラボレーターと作業可能
- Personalに加えて、グループを管理するためのTeamアクセスコントロール

### Github Pro
- Github Freeに加えて以下の機能がある
    - メールのGithubサポート
    - 3000分/月 のGithub Action
    - 2GBのGithub Packagesストレージ
    - 180/月のGithub Codespacesコア時間
    - 20GB/月のGithub Codespaseストレージ
    - プライベートリポジトリのツールと分析機能

### Github Team ???
Organization向けのProバージョン
- GitHub Action分が増加
- GitHub Packagesストレージが追加される

### Github Enterprise
より高いレベルのサポートに加えて、追加のセキュリティ、コンプライアンス、デプロイコントロールを利用できる。<br>
Github Enterprise製品にサインアップして1つ以上のEnterpriseアカウントを作成できる。<br>
作成者は"Enterprise Owner"のロールが割り当てられる。<br>
以下の機能が使える
- Github Enterprise サポート
- セキュリティ、コンプラ、デプロイコントロールの強化
- SAMLシングルサインオンによる認証
- SAMLまたはSCIMを使用したアクセスのプロビジョニング
- デプロイ保護規則
- Github Advanced Securituの購入オプション

**2つの異なるEnterpriseオプションが利用できる**<br>
- Github enterprise Service
    - Organizationがインフラ全体を完全に制御できるセルフホステッドソリューションであること
- Github enterprise Cloud
    - Actionsとpackagesストレージが大幅ぞうか

## Github Mobileでできること
- 通知の管理、トリアージ、クリア
- issueとpull requestの読み取り、レビュー、コラボレーション
- pull requestでのファイルの編集 ..

## Github Desktopでできること
- リポジトリの追加と複製
- インタラクティブな方法でコミットに変更を加える
- 共同作成者をcommitに簡単に追加する
- pull requestを使用したブランチのチェックアウトとCLステータスの表示
- 変更された画像の比較

## 請求について
アカウントごとに請求する。以下の2つを組み合わせた料金
- サブスクごとの請求
- 使用量ベースの請求


# GitHub copilot
GitHub EnterpriseはGithub Businessと比べてpersonalizationできるらしい