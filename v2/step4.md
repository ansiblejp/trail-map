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
  - 仮想メモリー: 8GB以上
  - 仮想ディスク: 20GB以上
  - インターネットへの接続が可能なこと

- その他の必要物
  - Red Hat Customer Portal のアカウントを作成するためのメールアドレス

## 進め方の概要

1. [Red Hat Customer Portal のアカウントを作成する](#Red-Hat-Customer-Portal-のアカウントを作成する)
1. [Red Hat Enterprise Linux(以下RHEL) と Red Hat Ansible Automation Platform の試用サブスクリプションを取得する](#試用サブスクリプションを取得する)
1. [RHELをインストールする](#RHELのインストール)
1. [Red Hat Ansible Automation Platform をインストールする](#Red-Hat-Ansible-Automation-Platform-のインストール)
1. [動作確認](#動作確認)


## Red Hat Customer Portal のアカウントを作成する

まず Red Hat Customer Portal のアカウントを作成します。このアカウントに必要な試用サブスクリプションを関連付けて環境を構築します。

作成方法に関しては [こちら](https://jp-redhat.com/pdf/Create_newID_and_subuser.pdf) を参照してください。作成にはメールアドレスが必要となります。


## 試用サブスクリプションを取得する

次に作成したアカウントに試用版のサブスクリプションを関連付けます。以下のサイトから簡単に取得することが可能です。それぞれのページで「無料で試用する」や「無料で試す」を選択します。手続きの途中でログインを求められる場合がありますので、先程作成した Red Hat Customer Portal のアカウントを入力してください。

- [RHELの試用サブスクリプションを取得する](https://www.redhat.com/ja/technologies/linux-platforms/enterprise-linux)
- [Red Hat Ansible Automation Platform の試用サブスクリプションを取得する](https://www.redhat.com/ja/technologies/management/ansible)

### RHELの例

[https://www.redhat.com/ja/technologies/linux-platforms/enterprise-linux](https://www.redhat.com/ja/technologies/linux-platforms/enterprise-linux) へアクセスし、「無料で試用する」をクリックします。

<img src="./images/subs-rhel1.png" width=50%>


### STEP1
「START YOUR TRIAL」をクリックします。

<img src="./images/subs-rhel2.png" width=50%>


### STEP2
ログインが求められますので、作成した Red Hat Customer Portal のアカウントでログインしてください。その後、ライセンスへの同意を求められますので内容を確認してから同意すると試用サブスクリプションが取得できます。

<img src="./images/subs-rhel3.png" width=50%>

### STEP3
取得に成功するとインストールメディアのダウンロードが始まります。始まらない場合はリンクをクリックしてインストールメディアを取得しましょう。

> Note: ここでダウンロードされるRHELのインストールメディアの容量は8GB前後になるため、モバイル回線を使用している方は注意してください。

<img src="./images/subs-rhel4.png" width=50%>

2021/2/14時点では以下のファイルがダウンロードされます。後続のインストール手順の中で利用します。

RHELのインストールメディア
```
rhel-8.3-x86_64-dvd.iso
```


Red Hat Ansible Automation Platform のインストールファイル
```
ansible-automation-platform-setup-bundle-1.2.1-1.tar.gz
```

### STEP4
取得した試用版は Red Hat Customer Portal から確認することができます。以下の例ではRHELの試用サブスクリプションが割り当てられています。

<img src="./images/subs-rhel5.png" width=50%>

### STEP5
Red Hat Ansible Automation Platform もほぼ同様の手順となります。こちらも取得後にRed Hat Customer Portal から試用サブスクリプションが確認できます。2つの試用サブスクリプションが取得できたらインストールの準備は完了です。


## RHELのインストール

お使いのハイパーバイザーに合わせて仮想マシンを作成し、ダウンロードしたインストールメディアから起動するように設定してください。仮想マシンを起動するとインストーラーが起動します。


<img src="./images/install-rhel1.png" width=50%>


<img src="./images/install-rhel2.png" width=50%>


<img src="./images/install-rhel3.png" width=50%>


<img src="./images/install-rhel4.png" width=50%>


<img src="./images/install-rhel5.png" width=50%>


<img src="./images/install-rhel6.png" width=50%>


<img src="./images/install-rhel7.png" width=50%>


<img src="./images/install-rhel8.png" width=50%>


<img src="./images/install-rhel9.png" width=50%>


インストールが終了したら仮想マシンが再起動されます。ログイン可能な状態になったら root ユーザーでログインしてください。

まずインストールしたRHELに試用サブスクリプションを関連付けます。まず以下のコマンドを実行してCustomer PortalとRHELを接続します。xxxx, yyyy の部分にはCustomer Portalのユーザー名とパスワードを指定してください。
```bash
[root@localhost ~]# subscription-manager register --username='xxxx' --password='yyyy'
登録中: subscription.rhsm.redhat.com:443/subscription
このシステムは、次の ID で登録されました: xxxxx-yyyy-zzzz-aaaa-bbbbbbbbbb
登録したシステム名: localhost.localdomain
```

利用可能なサブスクリプションを表示します。試用サブスクリプションが確認できるはずです。ここでプールIDをメモしておきます。
```bash
[root@localhost ~]# subscription-manager list --available
+-------------------------------------------+
    利用可能なサブスクリプション
+-------------------------------------------+
サブスクリプション名:     30 Day Red Hat Enterprise Linux Server Self-Supported Evaluation
提供:                     Red Hat Beta
                          Oracle Java (for RHEL Server)
                          Red Hat Enterprise Linux Server
                          Red Hat CodeReady Linux Builder for x86_64
                          Red Hat Enterprise Linux for x86_64
                          Red Hat Ansible Engine
                          Red Hat Container Images Beta
                          Red Hat Enterprise Linux Atomic Host Beta
                          Red Hat Enterprise Linux Atomic Host
                          Red Hat Container Images
SKU:                      RH00065
契約:                     xxxxxxxxx
プール ID:                2c92808177826aeb017785db02f108ce ← このIDをメモしておきます。
管理の提供:               いいえ
数量:                     2
推奨:                     1
サービスタイプ:           L1-L3
ロール:                   Red Hat Enterprise Linux Server
サービスレベル:           Self-Support
使用方法:                 Development/Test
アドオン:
サブスクリプションタイプ: Instance Based
開始:                     2021年02月09日
終了:                     2021年03月11日
エンタイトルメントタイプ: 物理
```

先程のプールIDを指定してこのRHELと試用サブスクリプションを関連付けます。サブスクリプションと関連付けられたRHELはパッケージリポジトリへアクセス可能になり、dnf(yum)コマンドを利用してパッケージの操作ができるようになります。
```bash
[root@localhost ~]# subscription-manager attach --pool='2c92808177826aeb017785db02f108ce'
サブスクリプションが正しく割り当てられました: 30 Day Red Hat Enterprise Linux Server Self-Supported Evaluation
```

ためしに tar コマンドをインストールしてみましょう（最小インストールではインストールされません）。このコマンドが成功すれば設定はうまくいっています。
```
[root@localhost ~]# dnf install -y tar
```

## Red Hat Ansible Automation Platform のインストール


```
[root@localhost ~]# tar zxvf ansible-automation-platform-setup-bundle-1.2.1-1.tar.gz
[root@localhost ~]# cd ansible-automation-platform-setup-bundle-1.2.1-1
[root@localhost ansible-automation-platform-setup-bundle-1.2.1-1]# ls
README.md  backup.yml  bundle  collections  group_vars  install.yml  inventory  licenses  rekey.yml  restore.yml  roles  setup.sh
```

```
[root@localhost ansible-automation-platform-setup-bundle-1.2.1-1]# vi inventory
```

```
[tower]
localhost ansible_connection=local

[automationhub]

[database]

[all:vars]
admin_password='pass-ansible-tower'

pg_host=''
pg_port=''

pg_database='awx'
pg_username='awx'
pg_password='pass-ansible-tower'
pg_sslmode='prefer'  # set to 'verify-full' for client-side enforced SSL
```

```
[root@localhost ansible-automation-platform-setup-bundle-1.2.1-1]# ./setup.sh

[warn] Will install bundled Ansible
Updating Subscription Management repositories.
メタデータの期限切れの最終確認: 0:42:38 時間前の 2021年02月14日 21時39分58秒 に実施しました。
依存関係が解決しました。
========================================================================================================================================
 パッケージ                        アーキテクチャー    バージョン                   リポジトリー                                  サイズ
========================================================================================================================================
インストール:
 ansible                           noarch              2.9.15-1.el8ae               @commandline                                   17 M
 sshpass                           x86_64              1.06-3.el8ae                 @commandline                                   27 k
 
 
 
PLAY RECAP *****************************************************************************************************************************
localhost                  : ok=176  changed=76   unreachable=0    failed=0    skipped=85   rescued=0    ignored=2

The setup process completed successfully.
Setup log saved to /var/log/tower/setup-2021-02-14-22:39:03.log.
```


```
TASK [postgres : Make sure PostgreSQL is started] **************************************************************************************
fatal: [localhost]: FAILED! => {"changed": false, "msg": "Unable to start service postgresql: Job for postgresql.service failed because the control process exited with error code.\nSee \"systemctl status postgresql.service\" and \"journalctl -xe\" for details.\n"}
```

```
[root@localhost ansible-automation-platform-setup-bundle-1.2.1-1]# dnf install glibc-langpack-en
```

<img src="./images/install-tower1.png" width=50%>


<img src="./images/install-tower2.png" width=50%>


<img src="./images/install-tower3.png" width=50%>


<img src="./images/install-tower4.png" width=50%>

## 動作確認

(作成中)

