# 環境を準備する

本ドキュメントは [Ansible Trail Map 牡丹山]() の一部となります。
Red Hat Ansible Automation Platform の環境を構築し、自動化のボタン化の準備を整えます。ここで構築する環境は体験とデモを目的としておりますので、本番の自動化環境としては利用しないでください。

## 必要な環境

ここでは仮想環境の中で Red Hat Ansible Automation Platform を構築します。仮想環境は自分の環境に適したものを選択してください。

- 仮想マシンを起動できるノートPCやサーバー
  - x86_64アーキテクチャ
  - VirtualBox, VMware, KVM 等

- 仮想マシンの必要スペック
  - vCPU: 2core以上
  - 仮想メモリー: 4GB以上
  - 仮想ディスク: 20GB以上
  - インターネットへの接続が可能なこと

- その他の必要物
  - Red Hat Customer Portal のアカウントを作成するためのメールアドレス

## 進め方の概要

1. Red Hat Customer Portal のアカウントを作成する
1. Red Hat Enterprise Linux(以下RHEL) と Red Hat Ansible Automation Platform の試用サブスクリプションを取得する
1. RHELをインストールする
1. Red Hat Ansible Automation Platform をインストールする
1. 動作確認


## Red Hat Customer Portal のアカウントを作成する

まず Red Hat Customer Portal のアカウントを作成します。このアカウントに必要な試用サブスクリプションを関連付けて環境を構築します。

作成方法に関しては [こちら](https://jp-redhat.com/pdf/Create_newID_and_subuser.pdf) を参照してください。


## 試用サブスクリプションを取得する

次に作成したアカウントに試用版のサブスクリプションを関連付けます。以下のサイトから簡単に取得することが可能です。それぞれのページで「無料で試用する」や「無料で試す」を選択します。手続きの途中でログインを求められる場合がありますので、先程作成した Red Hat Customer Portal のアカウントを入力してください。

- [RHELの試用サブスクリプションを取得する](https://www.redhat.com/ja/technologies/linux-platforms/enterprise-linux)
- [Red Hat Ansible Automation Platform の試用サブスクリプションを取得する](https://www.redhat.com/ja/technologies/management/ansible)

### RHELの例

[https://www.redhat.com/ja/technologies/linux-platforms/enterprise-linux](https://www.redhat.com/ja/technologies/linux-platforms/enterprise-linux) へアクセスし、「無料で試用する」をクリックします。

<img src="./images/subs-rhel1.png" width=50%>


「START YOUR TRIAL」をクリックします。

<img src="./images/subs-rhel2.png" width=50%>


ログインが求められますので、作成した Red Hat Customer Portal のアカウントでログインしてください。その後、ライセンスへの同意を求められますので内容を確認してから同意すると試用サブスクリプションが取得できます。

<img src="./images/subs-rhel3.png" width=50%>


取得した試用版は Red Hat Customer Portal から確認することができます。

<img src="./images/subs-rhel4.png" width=50%>


Red Hat Ansible Automation Platform もほぼ同様の手順となります。こちらも取得後にRed Hat Customer Portal から試用サブスクリプションが確認できます。2つの試用サブスクリプションが取得できたらインストールの準備は完了です。

## RHELのインストール

(作成中)

## Red Hat Ansible Automation Platform のインストール

(作成中)

## 動作確認

(作成中)

