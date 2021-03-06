---

copyright:
  years: 2017, 2018
lastupdated: "2018-05-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}



# Erste Schritte mit {{site.data.keyword.registrylong_notm}}
{: #index}

{{site.data.keyword.registrylong}} bietet eine private Multi-Tenant-Registry für Images, mit der Sie Ihre Docker-Images sicher speichern und mit Benutzern in Ihrem {{site.data.keyword.Bluemix_notm}}-Konto gemeinsam nutzen können.
{:shortdesc}

Die {{site.data.keyword.Bluemix_notm}}-Konsole enthält eine kurze Anleitung zum Schnelleinstieg. Weitere Informationen zu Verwendung der {{site.data.keyword.Bluemix_notm}}-Konsole finden Sie in [Sicherheitslücken bei Images überwachen](registry_ui.html).

**Hinweis**: Beziehen Sie keine personenbezogenen Daten in Ihre Container-Images, Namensbereichsnamen, Beschreibungsfelder (z. B. in Registry-Tokens) oder in Image-Konfigurationsdaten (z. B. Imagenamen oder Imagebezeichnungen) ein.



## {{site.data.keyword.registrylong_notm}}-CLI installieren
{: #registry_cli_install}

1.  Installieren Sie die [{{site.data.keyword.Bluemix_notm}}-CLI, ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://clis.ng.bluemix.net/ui/home.html) um die **bx**-Befehle von {{site.data.keyword.Bluemix_notm}} ausführen zu können.
2.  Installieren Sie das Container-Registry-Plug-in:

    ```
    bx plugin install container-registry -r Bluemix
    ```
    {: pre}


## Namensbereich einrichten
{: #registry_namespace_add}

1.  Melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an.

    ```
    bx login
    ```
    {: pre}

2.  Fügen Sie einen Namensbereich hinzu, um Ihr eigenes Image-Repository zu erstellen. Ersetzen Sie hierbei _&lt;eigener Namensbereich&gt;_ durch den gewünschten Namen für Ihren Namensbereich.

    ```
    bx cr namespace-add <eigener Namensbereich>
    ```
    {: pre}

3.  Führen Sie den Befehl `bx cr namespace-list` aus, um sicherzustellen, dass der Namensbereich erstellt wurde.

    ```
    bx cr namespace-list
    ```
    {: pre}



## Images mit einer Pull-Operation aus einer anderen Registry auf die lokale Maschine mit Pull-Operation extrahieren
{: #registry_images_pulling}

1.  [Installieren Sie die Docker-CLI ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.docker.com/community-edition#/download). Für Windows 8 oder OS X Yosemite 10.10.x oder frühere Versionen installieren Sie stattdessen die [Docker-Toolbox ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.docker.com/products/docker-toolbox).

2.  Melden Sie sich an der CLI an:

    ```
    bx cr login
    ```
    {: pre}

    **Hinweis:** Sie müssen sich anmelden, wenn Sie ein Image aus Ihrer privaten {{site.data.keyword.registrylong_notm}} mit Pull-Operation extrahieren.

3.  Laden Sie das Image auf Ihre lokale Maschine herunter (_mit Pull-Operation extrahieren_). Ersetzen Sie _&lt;quellenimage&gt;_ durch das Repository des Images und _&lt;tag&gt;_ durch den Tag des Images, das Sie verwenden möchten, z. B. _latest_.

    ```
    docker pull <quellenimage>:<tag>
    ```
    {: pre}

    Beispiel, bei dem _&lt;Quellenimage&gt;_ `hello-world` und _&lt;Tag&gt;_ `latest` ist:

    ```
    docker pull hello-world:latest
    ```
    {: pre}

4.  Kennzeichnen Sie das Image. Ersetzen Sie _&lt;quellenimage&gt;_ durch das Repository und _&lt;tag&gt;_ durch den Tag des lokalen Image, das Sie zuvor mit einer Pull-Operation extrahiert haben. Ersetzen Sie _&lt;Region&gt;_ durch den Namen der jeweiligen [Region](registry_overview.html#registry_regions). Ersetzen Sie _&lt;eigener Namensbereich&gt;_ durch den Namensbereich, den Sie in [Namensbereich einrichten](index.html#registry_namespace_add) erstellt haben. Definieren Sie das Repository und den Tag des Images, die Sie in Ihrem Namensbereich verwenden wollen, indem Sie _&lt;neues_image-repository&gt;_ und _&lt;neuer_tag&gt;_ durch die entsprechenden Werte ersetzen.

    ```
    docker tag <Quellenimage>:<tag> registry.<region>.bluemix.net/<eigener Namensbereich>/<neues_Image-Repository>:<neuer Tag>
    ```
    {: pre}

    Beispiel, bei dem _&lt;Quellenimage&gt;_ `hello-world`, _&lt;Tag&gt;_ `latest`, _&lt;Region&gt;_ `eu-gb`, _&lt;eigener Namensbereich&gt;_ `Namespace1`, _&lt;neuer Imagebericht&gt;_ `hw_repo` und _&lt;neues Tag&gt;_ `1` ist:

    ```
    docker tag hello-world:latest registry.eu-gb.bluemix.net/Namespace1/hw_repo:1
    ```
    {: pre}



## Docker-Images mit Push-Operation in den eigenen Namensbereich übertragen
{: #registry_images_pushing}

1.  Laden Sie das Image in Ihren Namensbereich hoch (_mit Push-Operation übertragen_). Ersetzen Sie _&lt;eigener Namensbereich&gt;_ durch den Namensbereich,  den Sie in [Namensbereich einrichten](index.html#registry_namespace_add) erstellt haben, und _&lt;Imagebericht&gt;_ und _&lt;Tag&gt;_ durch das Repository und den Tag des Image, das Sie beim Tagging ausgewählt haben.

    ```
    docker push registry.<region>.bluemix.net/<eigener Namensbereich>/<Image-Repository>:<tag>
    ```
    {: pre}

    Beispiel, bei dem _&lt;Region&gt;_ `eu-gb`, _&lt;eigener Namensbereich&gt;_ `Namespace1`,
_&lt;Imagebericht&gt;_ `hw_repo` und _&lt;Tag&gt;_ `1` ist:

    ```
    docker push registry.eu-gb.bluemix.net/Namespace1/hw_repo:1
    ```
    {: pre}

2.  Überprüfen Sie, ob das Image erfolgreich mit der Push-Operation übertragen wurde, indem Sie den folgenden Befehl ausführen.

    ```
    bx cr image-list
    ```
    {: pre}


Herzlichen Glückwunsch! Sie haben einen Namensbereich in {{site.data.keyword.registrylong_notm}} konfiguriert und mit Push-Operation Ihr erstes Image an Ihren Namensbereich übertragen.


**Wie geht es weiter?**

-   [Imagesicherheit mit Vulnerability Advisor verwalten](../va/va_index.html).
-   [Servicepläne und Nutzung überprüfen](registry_overview.html#registry_plans).
-   [Weitere Images in Ihrem Namensbereich speichern und verwalten](registry_images_.html).
-   [Container aus Ihrem Image erstellen und in einem Kubernetes-Cluster bereitstellen](../../containers/cs_clusters.html).


