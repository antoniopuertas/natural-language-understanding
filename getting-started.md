---

copyright:
  years: 2015, 2020
lastupdated: "2020-02-24"

keywords: natural language understanding,getting started,analyze content,analyze text,text analysis

subcollection: natural-language-understanding

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:go: .ph data-hd-programlang='go'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:apikey: data-credential-placeholder='apikey'}
{:url: data-credential-placeholder='url'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}

# Getting started with {{site.data.keyword.nlushort}}
{: #getting-started}

This short tutorial introduces the {{site.data.keyword.nlushort}} API with example requests and links to additional resources.
{:shortdesc}

## Before you begin
{: #before-you-begin}

- {: hide-dashboard} Create an instance of the service:
    1.  Go to the [{{site.data.keyword.nlushort}}](https://{DomainName}/catalog/natural-language-understanding){: external} page in the {{site.data.keyword.cloud_notm}} catalog.
    1.  Sign up for a free {{site.data.keyword.cloud_notm}} account or log in.
    1.  Click **Create**.
- {: hide-dashboard} Copy the credentials to authenticate to your service instance:
    1.  On the **Manage** page, click **Show Credentials**.
    1.  Copy the `API Key` and `URL` values.
- Make sure that you have the `curl` command.
    - Test whether `curl` is installed. Run the following command on the command line. If the output lists the `curl` version with SSL support, you are set for the tutorial.

        ```sh
        curl -V
        ```
        {: pre}

    - If necessary, install a version with SSL enabled from [curl.haxx.se](https://curl.haxx.se/){: external}. Add the location of the file to your PATH environment variables if you want to run `curl` from any command-line location.

This tutorial shows you how to use the {{site.data.keyword.nlushort}} API from a command-line interface. To download client libraries for various programming languages, check out the [Watson SDKs](/docs/natural-language-understanding?topic=watson-using-sdks#using-sdks).
{:tip}

## Step 1: Analyze a webpage
{: #analyze-sample}

Run the following command to analyze a webpage to get sentiment, concepts, categories, entities, and keywords. <span class="hide-dashboard">Replace `{apikey}` and `{url}` with your service credentials.</span>

```sh
curl -X POST -u "apikey:{apikey}"{: apikey} \
--header "Content-Type: application/json" \
--data '{
  "url": "http://newsroom.ibm.com/Guerbet-and-IBM-Watson-Health-Announce-Strategic-Partnership-for-Artificial-Intelligence-in-Medical-Imaging-Liver",
  "features": {
    "sentiment": {},
    "categories": {},
    "concepts": {},
    "entities": {},
    "keywords": {}
  }
}' \
"{url}/v1/analyze?version=2019-07-12"{: url}
```
{:pre}

Windows users: This command might not run on Windows. Run the following command instead:

```sh
curl -X POST -u "apikey:{apikey}"{: apikey} --header "Content-Type: application/json" --data "{\"url\":\"http://newsroom.ibm.com/Guerbet-and-IBM-Watson-Health-Announce-Strategic-Partnership-for-Artificial-Intelligence-in-Medical-Imaging-Liver\",\"features\":{\"sentiment\":{},\"categories\":{},\"concepts\":{},\"entities\":{},\"keywords\":{}}}" "{url}/v1/analyze?version=2019-07-12"{: url}
```
{: pre}

The next step demonstrates how to specify options that customize the analysis for each feature.

## Step 2: Analyze target phrases and keywords
{: #analyze-phrase}

{{site.data.keyword.nlushort}} can analyze target phrases in context of the surrounding text for focused sentiment and emotion results. The **targets** option for sentiment in the following example tells the service to search for the targets "apples", "oranges", and "broccoli". Since "apples" and "oranges" are located in the text, sentiment scores are returned for those targets.

You can also get sentiment and emotion results for entities and keywords that are detected in your text. In the example, the **emotion** option for keywords tells the service to analyze each detected keyword for emotion results.

```sh
curl -X POST -u "apikey:{apikey}"{: apikey} \
--header "Content-Type: application/json" \
--data '{
  "text": "I love apples! I do not like oranges.",
  "features": {
    "sentiment": {
      "targets": [
        "apples",
        "oranges",
        "broccoli"
      ]
    },
    "keywords": {
      "emotion": true
    }
  }
}' \
"{url}/v1/analyze?version=2019-07-12"{: url}
```
{:pre}

Runnable command for Windows users:

```sh
curl -X POST -u "apikey:{apikey}"{: apikey} --header "Content-Type: application/json" --data "{\"text\":\"I love apples! I do not like oranges.\",\"features\":{\"sentiment\":{\"targets\":[\"apples\",\"oranges\",\"broccoli\"]},\"keywords\":{\"emotion\":true}}}" "{url}/v1/analyze?version=2019-07-12"{: url}
```
{:pre}

## Next steps
{: #next-steps}

- View the [API reference](https://{DomainName}/apidocs/natural-language-understanding){: external}.
- Learn how to identify [custom entities and relations](/docs/natural-language-understanding?topic=natural-language-understanding-customizing).
