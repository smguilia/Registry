---

copyright:
  years: 2017, 2018
lastupdated: "2017-10-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# 管理儲存空間及取回資料流量的配額限制
{: #registry_quota}

您可以設定及管理自訂配額限制，來限制可在 {{site.data.keyword.Bluemix}} 帳戶中使用的儲存空間量及取回資料流量。
{:shortdesc}


## 設定儲存及取回映像檔的配額限制
{: #registry_quota_set}

您可以設定自己的配額限制，來限制專用映像檔的儲存空間量及取回資料流量。
{:shortdesc}

開始之前，請確定您是要設定配額的 [{{site.data.keyword.Bluemix_notm}} 帳戶的擁有者或帳單管理員](../../iam/users_roles.html#userroles)。

當您升級至 {{site.data.keyword.registryshort_notm}} 標準方案時，可以受益於專用映像檔的無限制儲存空間量及取回資料流量。若要避免超出偏好的付費等級，您可以設定儲存空間量及取回資料流量的個別配額。配額限制會套用至您在 {{site.data.keyword.registrylong_notm}} 中設定的所有名稱空間。如果您使用的是免費服務方案，則也可以設定免費儲存空間量及取回資料流量內的自訂配額。

若要設定配額，請執行下列動作：

1.  登入 {{site.data.keyword.Bluemix_notm}}。

    ```
        bx login
    ```
    {: pre}

2.  檢閱儲存空間及取回資料流量的現行配額限制。

    ```
        bx cr quota
    ```
    {: pre}

    您的輸出會與下列內容類似。

    ```
        Getting quotas and usage for the current month, for account '<account_owner> Account'...

    

    QUOTA          LIMIT    USED   
    Pull traffic   5.1 GB   0 B   
    Storage        512 MB   511 MB   

    

    OK
    ```
    {: screen}

3.  變更儲存空間及取回資料流量的配額限制。若要變更取回資料流量用量，請指定 **traffic** 選項，並將 _&lt;traffic_quota&gt;_ 取代為您要針對取回資料流量配額設定的值（以 MB 為單位）。如果您要變更帳戶中的儲存空間量，請指定 **storage** 選項，並將 _&lt;storage_quota&gt;_ 取代為您要設定的值（以 MB 為單位）。

    **附註：**如果您使用免費方案，則無法將配額設為超出免費方案的數量。儲存空間的免費層額度是 512 MB，而資料流量是 5120 MB。

    ```
        bx cr quota-set --traffic <traffic_quota> --storage <storage_quota>
    ```
    {: pre}

    將儲存空間的配額限制設為 600 MB 並將取回資料流量設為 7000 GB 的範例：

    ```
        bx cr quota-set --storage 600 --traffic 7000
    ```
    {: pre}


## 檢閱儲存及取回映像檔的配額限制及用量
{: #registry_quota_get}

您可以檢閱配額限制，以及檢查帳戶的現行儲存空間及取回資料流量用量。
{:shortdesc}

1.  登入 {{site.data.keyword.Bluemix_notm}}。

    ```
        bx login
    ```
    {: pre}

2.  檢閱儲存空間及取回資料流量的現行配額限制。

    ```
        bx cr quota
    ```
    {: pre}

    您的輸出會與下列內容類似。

    ```
        Getting quotas and usage for the current month, for account '<account_owner> Account'...

    

    QUOTA          LIMIT    USED   
    Pull traffic   5.1 GB   0 B   
    Storage        512 MB   511 MB   

    

    OK
    ```
    {: screen}


## 釋放已使用的儲存空間以及變更服務方案或配額限制以保持在給定配額限制內
{: #registry_quota_freeup}

如果您已超出針對 {{site.data.keyword.Bluemix_notm}} 帳戶所設定的配額限制，則可以釋放儲存空間，並變更服務方案或配額限制以繼續從名稱空間推送及取回映像檔。
{:shortdesc}

釋放 {{site.data.keyword.Bluemix_notm}} 帳戶中的映像檔儲存空間：

1.  列出 {{site.data.keyword.Bluemix_notm}} 帳戶的所有名稱空間中的所有映像檔。

    ```
        bx cr images
    ```
    {: pre}

2.  移除名稱空間中的映像檔。請將 _&lt;image_name&gt;_ 取代為您要移除的映像檔名稱。

    ```
        bx cr image-rm <image_name>
    ```
    {: pre}

    **附註：**根據映像檔大小，可能需要一些時間，才能移除映像檔，並且儲存空間變為可用。

3.  檢閱儲存空間配額用量。

    ```
        bx cr quota
    ```
    {: pre}

4. **附註：**您無法減少計費期間中的取回資料流量用量。

    若要繼續從名稱空間取回映像檔，請從下列選項之間進行選擇：

    -   等到下一個計費週期開始。
    -   如果您有免費方案，請[升級至標準服務方案](registry_overview.html#registry_plan_upgrade)。
    -   如果您已有標準方案，請[設定取回資料流量的新配額限制](#registry_quota_set)。
