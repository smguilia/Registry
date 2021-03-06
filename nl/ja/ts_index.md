---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}


# トラブルシューティング
{: #ts_index}

ここでは、{{site.data.keyword.registrylong}} の使用に関する一般的なトラブルシューティングの質問への回答を示します。
{:shortdesc}


## {{site.data.keyword.registrylong_notm}} のヘルプとサポートの入手
{: #gettinghelp}

{{site.data.keyword.registrylong_notm}} を使用していて問題や疑問が生じた場合は、情報を検索するか、フォーラムを通じて質問することにより、ヘルプを利用できます。 また、{{site.data.keyword.IBM_notm}} サポート・チケットをオープンすることもできます。

フォーラムを使用して質問するときは、{{site.data.keyword.registrylong_notm}} 開発チームの目に留まるように、質問にタグを付けてください。

-   {{site.data.keyword.registrylong_notm}} でのアプリの開発またはデプロイに関する技術的な質問がある場合は、[スタック・オーバーフロー](http://stackoverflow.com/search?q=+ibm-bluemix)で質問を投稿し、質問に `ibm-bluemix` および `container-registry` のタグを付けてください。
-   サービスおよび概説の指示に関する質問については、[IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/container-registry/?smartspace=bluemix) フォーラムを使用してください。 `bluemix` タグと `container-registry` タグを含めてください。

フォーラムの使用について詳しくは、[サポート・センターの使用](../../get-support/howtogetsupport.html#using-avatar)を参照してください。
{{site.data.keyword.IBM_notm}} サポート・チケットを開く方法や、サポート・レベルとチケットの重大度については、[サポート・チケットのオープン](../../get-support/howtogetsupport.html#open-ticket)を参照してください。

## {{site.data.keyword.registrylong_notm}} へのログインが失敗する
{: #ts_login}

{{site.data.keyword.registrylong_notm}} にログインできません。

{: tsSymptoms}
`bx cr login` コマンドが失敗します。

{: tsCauses}
-   container-registry プラグインが古いため、更新する必要がある。
-   Docker がローカル・マシンにインストールされていないか、稼働していない。
-   {{site.data.keyword.Bluemix_notm}} ログイン資格情報の有効期限が切れている。

{: tsResolve}
この問題は、以下の方法で修正できます。

-   {{site.data.keyword.registryshort_notm}} プラグインの最新バージョンにアップグレードします。[">{{site.data.keyword.registrylong_notm}} (`bx cr`) プラグインの更新](registry_setup_cli_namespace.html#registry_cli_update)を参照してください。
-   Docker がマシンにインストールされていることを確認します。 既にインストールされている場合、Docker デーモンを再始動します。
-   `bx login` コマンドを再実行して、{{site.data.keyword.Bluemix_notm}} ログイン資格情報をリフレッシュします。
  
## {{site.data.keyword.registrylong_notm}} に対してコマンドを実行すると`「FAILED You are not logged in to IBM Cloud.」`で失敗する 
{: #ts_login_cloud}

{{site.data.keyword.Bluemix_notm}} にログインしているのに、{{site.data.keyword.registrylong_notm}} でコマンドを実行することができません。

{: tsSymptoms}
すべての `bx cr` コマンドが失敗します。

{: tsCauses}
-   container-registry プラグインが古いため、更新する必要がある。

{: tsResolve}
この問題は、以下の方法で解決できます。

-   {{site.data.keyword.registryshort_notm}} プラグインの最新バージョンにアップグレードします。[">{{site.data.keyword.registrylong_notm}} (`bx cr`) プラグインの更新](registry_setup_cli_namespace.html#registry_cli_update)を参照してください。



## {{site.data.keyword.registrylong_notm}} コマンドが `'cr' is not a registered command. See 'bx help'.` で失敗する
{: #ts_login_error}

`cr` は登録された `bx` コマンドではないため、`bx cr` コマンドを実行できません。

{: tsSymptoms}
以下のいずれかのエラー・メッセージと同じエラー・メッセージが表示されます。

```
bx cr login
'cr' is not a registered command. See 'bx help'.
```
{: pre}

```
bx cr namespace
'cr' is not a registered command. See 'bx help'.
```
{: pre}

{: tsCauses}
-   The container-registry plug-in is not installed.


{: tsResolve}
この問題は、以下の方法で解決できます。

-   container-registry プラグインをインストールします。[{{site.data.keyword.registryshort_notm}} CLI (bx cr) プラグインのインストール](registry_setup_cli_namespace.html#registry_cli_install)を参照してください。


## 名前空間のセットアップが失敗する
{: #ts_problem}

{: tsSymptoms}
`bx cr namespace-add` を実行するときに、入力した値を名前空間として設定できない。

{: tsCauses}
-   別の {{site.data.keyword.Bluemix_notm}} 組織によって既に使用されている名前空間値を入力した。
-   名前空間は最近削除されており、その名前を再使用している。 削除された名前空間に多くのリソースが含まれていた場合、その削除が {{site.data.keyword.registrylong_notm}} によってまだ完全に処理されていない可能性があります。
-   名前空間値に無効な文字を使用した。

{: tsResolve}
この問題は、以下の方法で修正できます。

-   返されたエラー・メッセージに示されている指示に従います。
-   以下を参照して、有効な名前空間を入力したか確認します。
    -   名前空間は、4 文字から 30 文字の長さでなければなりません。
    -   名前空間は、文字または数字で始まる必要があります。
    -   名前空間には、小文字、数字、またはアンダースコアー (_) のみを使用できます。
-   名前空間に別の値を選択します。
-   削除された名前空間を再作成しており、その名前空間に多くのイメージが含まれていた場合は、後で再試行してください。

## Docker イメージのプッシュまたはプルが失敗する
{: #ts_pushpull}

{: tsSymptoms}
Docker イメージをプッシュまたはプルするコマンドを実行すると、エラー・メッセージを受け取る。 このエラー・メッセージは、根本原因によって異なります。 受け取る可能のあるエラー・メッセージとしては、以下のようなものがあります。

```
You have exceeded your storage quota. Delete one or more images, or review your storage quota and pricing plan
```
{: screen}

```
You have exceeded your pull traffic quota for the current month. Review your pull traffic quota and pricing plan
```
{: screen}

```
unauthorized: authentication required
```
{: screen}

```
denied: requested access to the resource is denied
```
{: screen}

{: tsCauses}
-   Docker がインストールされていない。
-   Docker クライアントが {{site.data.keyword.registrylong_notm}} にログインしていない。
-   {{site.data.keyword.Bluemix_notm}} アクセス・トークンの有効期限が切れている可能性がある。
-   {{site.data.keyword.Bluemix_notm}} アカウントに設定されているストレージまたはプル・トラフィックの割り当て量制限を超えた。

{: tsResolve}
この問題は、以下の方法で修正できます。

-   [Docker がマシンにインストールされていることを確認します](index.html#registry_cli_install)。
-   Docker のインストール・パスを確認します。
-   `bx login` を実行して {{site.data.keyword.Bluemix_notm}} にログインします。 次に、`bx cr login` を実行して {{site.data.keyword.registrylong_notm}} CLI にログインします。
-   [{{site.data.keyword.registrylong_notm}} で Docker イメージを保管およびプルするための割り当て量制限と使用量を検討します](registry_quota.html#registry_quota_get)。

## latest タグを使用して最新イメージをプルできない
{: #ts_docker_latest}

{: tsSymptoms}
コマンド `docker pull` を実行しようとしているが、最新バージョンのビルドではないイメージのバージョンが返される。

{: tsCauses}
タグ値を指定せずに Docker コマンドを実行すると、デフォルトでは、イメージを参照するために `latest` タグが適用されます。 `latest` タグは、タグ値を明示的に設定せずに実行された最新の `docker build` コマンドまたは `docker tag` コマンドに適用されます。 したがって、`docker` コマンドの実行順序が適切でなかったり、一部のイメージに対してタグが明示的に設定されたり、`latest` タグが、最新でないビルドを参照する可能性があります。

{: tsResolve}
通常は、`latest` タグに頼らずに、イメージに毎回別の順次タグを明示的に定義する方が得策です。


## 他の IBM イメージをレジストリーに追加できない
{: #ts_ppa}


{: tsSymptoms}
他の IBM 製品 ({{site.data.keyword.Bluemix_notm}} Private など) で使用したコンテンツをインポートしようとすると、自分のイメージや、[IBM パスポート・アドバンテージ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www-01.ibm.com/software/passportadvantage/index.html) から入手したその他のライセンス適用済みのソフトウェアをレジストリーに保管できません。

{: tsCauses}
イメージや IBM パスポート・アドバンテージから取得した Helm チャートなどのソフトウェア・パッケージは、`bx cr ppa-archive-load` コマンドを使用してレジストリーにインポートする必要があります。

{: tsResolve}
開始前に、以下のことを行います。
* `bx login [--sso]` を実行して {{site.data.keyword.Bluemix_notm}} にログインします。
* `bx cr login` を実行して {{site.data.keyword.registrylong_notm}} にログインします。
* クラスターを [`kubectl` CLI のターゲットとして設定](../../containers/cs_cli_install.html#cs_cli_configure)します。
* クラスターにまだ Helm をセットアップしていない場合は、[ここでクラスターに Helm をセットアップします](../../containers/cs_integrations.html#helm)。
* 組織内でチャートを共有する場合は、[Chart Museum オープン・ソース・プロジェクト ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/kubernetes/charts/tree/master/stable/chartmuseum) をインストールできます。

### {{site.data.keyword.Bluemix_notm}} で使用するための IBM パスポート・アドバンテージ製品のインポート

1.  インポートする圧縮ファイルを [IBM パスポート・アドバンテージ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www-01.ibm.com/software/passportadvantage/index.html) から入手します。

2.  使用する地域をターゲットにします。地域名がわからない場合は、地域を指定せずにコマンドを実行してから、地域を選択します。

    ```
    bx cr region-set <region>
    ```
    {: pre}

3.  圧縮アーカイブ・ファイルをインポートします。 圧縮ファイルのパスと、イメージのプッシュ先のレジストリー名前空間を指定します。

    ```
    bx cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace>
    ```
    {: pre}

    このコマンドは、圧縮ファイルを解凍し、中に含まれているイメージをローカル Docker クライアントにロードしてから、イメージをレジストリー内の名前空間にプッシュします。
    
    IBM パスポート・アドバンテージ・アーカイブの Helm チャートを Chart Museum にアップロードする場合は、コマンドに次のオプションを含めます: `bx cr ppa-archive-load --archive </path/to/archive.tgz> --namespace <namespace> --chartmuseum-uri <URI> --chartmuseum-user <user_name> --chartmuseum-password <password>`
    {: tip}

    **出力例**:
    ```
    user:~ user$ bx cr ppa-archive-load --archive IBM_INTEGRATION_BUS_V10.0.0.10_FO.tar.gz  --namespace mynamespace
    Unpacking archive to '/Users/user/Downloads/ppa-import/50ab12ea-2d4e-402b-9d9c-61708fcb0720'...
    Found 1 image(s) and 1 chart(s) to import.
    Importing 'iib-prod:10.0.0.10' and pushing it to 'registry.ng.bluemix.net/mynamespace/iib-prod:10.0.0.10'...
    Loaded image: iib-prod:10.0.0.10
    The push refers to repository [registry.ng.bluemix.net/mynamespace/iib-prod]
    1ecda25d51a8: Preparing
    369bf331939e: Preparing
    ...
    369bf331939e: Pushed
    1ecda25d51a8: Pushed
    10.0.0.10: digest: sha256:8fbe4b0a33b061da38c0081ca86673f24073fbafeca3b49099367e70a20f88cz size: 3444

    Extracting chart 'charts/ibm-integration-bus-prod-1.0.0.tgz' to '/Users/user/Downloads/ppa-import/charts'.

    OK
    ```
    {: screen}

4.  圧縮ファイルに Helm チャートが含まれている場合、それらのチャートは、現行作業ディレクトリーに作成される `ppa-import` というアーカイブ・ディレクトリーに置かれます。そのディレクトリーを開いて Helm チャートの名前 `<helm_chart>` を確認してから、その値の詳細を表示します。

    ```
    helm inspect values ppa-import/charts/<helm_chart>.tgz
    ```
    {: pre}
    
    前の手順でチャートを Chart Museum にアップロードした場合は、`helm inspect` を使用して Chart Museum 内のチャートの詳細を表示できます。
    {: tip}

5.  `helm inspect values` コマンドにより出力された値にしたがって、Helm チャート `<helm_chart>` を構成します。

6.  Helm チャート `<helm_chart>` を、`helm install` コマンドを使用してデプロイします。必要に応じて、`--set` オプションを使用してチャート内の値をオーバーライドできます。

    ```
    helm install ppa-import/charts/<helm_chart>.tgz --set license=accept
    ```
    {: pre}


## カスタム・ファイアウォールを設定したレジストリーへのアクセスが失敗する
{: #ts_firewall}

{: tsSymptoms}
開発環境において、インバウンドとアウトバウンドのネットワーク・トラフィック用に、カスタム設定を行った追加ファイアウォールをセットアップします。 {{site.data.keyword.registrylong_notm}} にアクセスしようとすると、接続は失敗します。

{: tsCauses}
インバウンドとアウトバウンドのネットワーク・トラフィックでレジストリーとの間の通信を可能にするには、カスタム・ファイアウォールにおいて特定のネットワーク・グループを開く必要があります。

{: tsResolve}
カスタマイズしたファイアウォールで次のネットワーク・グループを開きます。

1.  {{site.data.keyword.registrylong_notm}} に接続するために使用するマシンのパブリック IP アドレスをメモしておいてください。 Kubernetes を使用する場合、ワーカー・ノードのパブリック IP アドレスを使用します。 `bx cs workers <cluster_name_or_id>` を実行して、ワーカー・ノードのパブリック IP アドレスを取得します。*&lt;cluster_name_or_id&gt;* はクラスターの名前または ID です。
2.  ファイアウォールで、マシンとの間の次の接続を許可します。
    -   マシンへの INBOUND 接続については、次のソース・ネットワーク・グループからマシンの宛先パブリック IP アドレスへの着信ネットワーク・トラフィックを許可します。

        `registry.bluemix.net`:

        ```
        169.60.72.144/28
        169.61.76.176/28
        ```
        {: codeblock}

        `registry.au-syd.bluemix.net`:

        ```
        168.1.45.160/27
        168.1.139.32/27
        ```
        {: codeblock}

        `registry.eu-de.bluemix.net`:

        ```
        169.50.56.144/28
        159.8.73.80/28
        ```
        {: codeblock}

        `registry.eu-gb.bluemix.net`:

        ```
        159.8.188.160/27
        169.50.153.64/27
        ```
        {: codeblock}

        `registry.ng.bluemix.net`:

        ```
        169.55.39.112/28
        169.46.9.0/27
        169.55.211.0/27
        ```
        {: codeblock}

    -   マシンからの OUTBOUND 接続については、同じネットワーク・グループを使用し、マシンの送信元パブリック IP アドレスからこれらのネットワーク・グループへの発信ネットワーク・トラフィックを許可します。

## 失われた鍵または改ざんされた鍵のリカバリー
{: #ts_recoveringtrustedcontent}

{: tsSymptoms}
[信頼できるコンテンツ](registry_trusted_content.html)を使用している場合に、署名鍵を失われたり改ざんされたりすると、信頼できるイメージを管理できなくなります。

{: tsCauses}
リポジトリー鍵またはルート鍵が失われたか、改ざんされました。

{: tsResolve}
失われた鍵または影響を受けた鍵をリカバリーするための方法は、鍵のタイプ (リポジトリーまたはルート) によって異なります。

*  [リポジトリー鍵](#trustedcontent_lostrepokey)の場合は、リポジトリーの署名鍵のセットを新たに生成できます。
*  [ルート鍵](#trustedcontent_lostrootkey)の場合は、リポジトリーの削除を要求してから、新規リポジトリーを作成できます。

### リポジトリー鍵
{: #trustedcontent_lostrepokey}

リポジトリー鍵が失われた場合または改ざんされた場合は、リポジトリーの署名鍵のセットを新たに生成します。
{:shortdesc}

**注**: ローテーションできる署名役割は、リポジトリー管理者である `targets` だけです。その他の役割が影響を受けた場合は、それらの役割のために新規鍵を生成し、古い役割を削除し、新しい役割を署名者として追加してください。

始める前に、[署名付きのイメージを初めてプッシュ](registry_trusted_content.html#trustedcontent_push)したときに作成したルート鍵のパスフレーズを取得しておいてください。

1.  [Notary プロジェクト](https://github.com/theupdateframework/notary#getting-started-with-the-notary-cli)の CLI バージョンをインストールします。

2.  [信頼できるコンテンツ環境をセットアップします](registry_trusted_content.html#trustedcontent_setup)。

3.  前の手順の export コマンドの URL をメモします。 例えば、`https://registry.ng.bluemix.net:4443` です。

4.  レジストリー・トークンを生成します。

    ```
    bx cr token-add --readwrite
    ```
    {: pre}

5.	問題の鍵で署名されたコンテンツが信頼されなくなるように、鍵をローテーションします。 _&lt;URL&gt;_ を、手順 2 でメモした export コマンドの URL に置き換え、_&lt;image&gt;_ を、リポジトリー鍵が影響を受けたイメージに置き換えます。

    ```
    notary -s <URL> -d ~/.docker/trust key rotate <image> targets
    ```
    {: pre}

6.	プロンプトが出たら、ルート鍵のパスフレーズを入力します。 次に、新しいリポジトリー鍵のための新しいルート鍵のパスフレーズをプロンプトに応じて入力します。

7.	新しい署名鍵を使用する[署名付きのイメージをプッシュ](registry_trusted_content.html#trustedcontent_push)します。

### ルート鍵
{: #trustedcontent_lostrootkey}

ルート鍵が失われたり改ざんされたりした場合、そのルート鍵を使用した信頼できるコンテンツ・リポジトリーは更新できません。
{:shortdesc}

影響を受けたルート鍵を使用するリポジトリーが含まれている[名前空間を削除](registry_setup_cli_namespace.html#registry_remove)できます。これにより、イメージとトラスト・データが削除されます。

実動イメージ用の名前空間のように、ルート鍵が影響を受けていないリポジトリーが名前空間に含まれている場合、影響を受けたルート鍵に関連付けられているトラスト・データだけを削除する必要があります。サポート・チケットをオープンしてください。

1.  [{{site.data.keyword.Bluemix_notm}} サポートにお問い合わせください](../../get-support/howtogetsupport.html)。問題の簡単な説明、アカウント ID、ルート鍵が影響を受けたイメージ・リポジトリーが含まれている名前空間のリストをお知らせください。

2.  {{site.data.keyword.Bluemix_notm}} で問題が解決されたら、ローカル・マシン上の Docker コンテント・トラストのリポジトリーを削除します。

    * Linux および Mac ディレクトリー: `~/.docker/trust/private` および `~/.docker/trust/tuf`

    * Windows ディレクトリー: `%HOMEPATH%&#xa5;.docker&#xa5;trust&#xa5;private` および `%HOMEPATH%&#xa5;.docker&#xa5;trust&#xa5;tuf`

    **注**: ルート鍵が影響を受けたため、この手順では、他のトラスト・サーバーのものを含め、すべての署名鍵を削除します。

3.  {{site.data.keyword.containershort_notm}} クラスターで [{{site.data.keyword.Bluemix_notm}} Image Enforcement](registry_security_enforce.html) を使用する場合は、各イメージ制約ポッドを再始動します。Kubernetes にポッドのローリング再始動を自動実行させるには、ポッド上の一部のメタデータを変更します。 例えば、[クラスターを Kubernetes CLI のターゲットとして設定](../../containers/cs_cli_install.html#cs_cli_configure)し、デプロイメントを変更します。
    ```
    kubectl patch deployment $(helm list | grep "ibmcloud-image-enforcement" | awk '{print $1;}')-ibmcloud-image-enforcement -p'{"spec":{"template":{"metadata":{"annotations":{"restarted":"'$(date +%s)'"}}}}}}' -n ibm-system
    ```
    {: pre}

4.  信頼できるコンテンツ・リポジトリーを生成します。

    *  信頼できるコンテンツを新規作成する場合は、[新しく署名したイメージをプッシュします](registry_trusted_content.html#trustedcontent_push)。

    *  以前の信頼できるコンテンツを変更しない場合は、レジストリー内の最新のイメージに署名を追加します。

       ```
       docker trust sign <image>:<tag>
       ```
       {: pre}
       

## Container Image Security Enforcement のインストールが、`「helm install ibm-incubator/ibmcloud-image-enforcement --name cise Error: jobs.batch "create-crds" already exists」`で失敗する
{: #ts_install_cise_fail}


{: tsSymptoms}
Container Image Security Enforcement のインストールが失敗し、以下のメッセージを受け取りました。

```
helm install ibm-incubator/ibmcloud-image-enforcement --name cise 
Error: jobs.batch "create-crds" already exists
```
{: screen}

{: tsCauses}
前のインストールが失敗し、その後のアンインストールで、インストールに関連付けられた一部の Kubenetes ジョブが削除されませんでした。

{: tsResolve}
次のコマンドを実行して、残りの Kubenetes ジョブを削除します。

```
kubectl delete jobs -n ibm-system create-admission-webhooks create-armada-image-policies create-crds validate-crd-creation --ignore-not-found=true
```
{: pre}
