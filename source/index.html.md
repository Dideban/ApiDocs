---
title: Dideban API Documentation

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell: cURL
  - php: Php
  - csharp : .Net
  - javascript: Javascript 

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Dideban API Documentation
---

# Introduction

Welcome to the Dideban API documentation! At Dideban, we are dedicated to providing powerful, flexible, and easy-to-use no-code web scraping solutions for businesses of all sizes. While our platform is designed to be accessible and user-friendly, we understand that our enterprise plan customers may require deeper integration and customization. That's where our API comes in.

This API enables B2B clients to harness the full power of Dideban's web scraping capabilities and seamlessly integrate them into their own systems, applications, or services. By utilizing our API, you can automate your data extraction processes, streamline workflows, and scale your business operations with ease.

In this documentation, you'll find detailed information on how to authenticate, make API calls, and work with the data returned by the API. We've included step-by-step guides, sample code snippets, and best practices to help you get started quickly and efficiently.

Whether you're looking to extract valuable insights from the web or build innovative data-driven solutions, the Dideban API is your key to unlocking the true potential of web scraping. Let's get started!
# Environments
At Dideban, we provide two separate environments for our API to accommodate different stages of your application development and deployment process: Staging and Production.

## Staging Environment
The Staging environment is designed for testing and development purposes. It allows you to experiment with the API, develop your integrations, and validate your implementation without affecting your Production data or usage limits. The Staging environment is accessible at the following base URL:

<aside class="success">
https://stageapi.dideban.live
</aside>

Keep in mind that the Staging environment may not always have the same level of performance, stability, or uptime as the Production environment. It is not recommended to use the Staging environment for production applications.

## Production Environment
The Production environment is intended for live applications and services. It provides optimal performance, stability, and uptime to ensure your application runs smoothly. Once you have completed development and testing, switch to the Production environment to go live. The Production environment is accessible at the following base URL:

<aside class="success">
https://api.dideban.live
</aside>

Make sure to update your application's API endpoint URLs accordingly when switching between environments. We recommend using separate API keys for each environment to prevent accidental data manipulation and to manage access control effectively.

Always exercise caution when working with live data in the Production environment, and ensure you have thoroughly tested your integration in the Staging environment before deploying your application.

# Authentication

```json
#Sample API response:
{
    "access_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6IkE3N0NERTUyREJDRTgxRjFDNDRERDkzRDM5NUQ5MUI0IiwidHlwIjoiYXQrand0In0.....",
    "expires_in": 36000,
    "token_type": "Bearer",
    "refresh_token": "843649A1ACD4663E67820C68CC15.....",
    "scope": "api offline_access openid"
}
```

The Dideban API uses API keys to authenticate requests. This method ensures a secure and straightforward way to access our services. API keys are only available to users who have created one for themselves. To get started with the API, you must first generate your unique API key.

Please note that your API key grants access to your Dideban account and should be treated as a sensitive credential. Keep your API key secure and do not share it with unauthorized parties.
## Using Your API Key
Once you have generated your API key, to access the Dideban API, you need to use your API key to obtain a JWT access token. This access token is then used as a Bearer token in the header of each API request.

Please ensure you include the Authorization header with the correct jwt token in every request. Failing to do so will result in an authentication error, and your request will be denied.

If you believe your API key has been compromised or you need to revoke access for any reason, you can change the key in the "API Keys" section of your account settings and generate a new one. Remember to update your application with the new API key to continue using the Dideban API.
## Obtain Access Token

```shell
curl --location 'https://stageapi.dideban.live/v1/auth/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'api_key=<YOUR_API_KEY>' \
--data-urlencode 'client_id=apiClient' \
--data-urlencode 'client_secret=secret' \
--data-urlencode 'grant_type=api_key'

```

```php

<?php
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://stageapi.dideban.live/v1/auth/token',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => array(
    'api_key' => '<YOUR_API_KEY>',
    'client_id' => 'apiClient',
    'client_secret' => 'secret',
    'grant_type' => 'api_key'
  ),
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/x-www-form-urlencoded'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
?>
```

```csharp
using System;
using System.Net.Http;
using System.Collections.Generic;
using System.Net.Http.Headers;
using System.Threading.Tasks;

namespace DidebanAuthSample
{
    class Program
    {
        static async Task Main(string[] args)
        {
            var client = new HttpClient();
            var content = new FormUrlEncodedContent(new[]
            {
                new KeyValuePair<string, string>("api_key", "<YOUR_API_KEY>"),
                new KeyValuePair<string, string>("client_id", "apiClient"),
                new KeyValuePair<string, string>("client_secret", "secret"),
                new KeyValuePair<string, string>("grant_type", "api_key")
            });

            content.Headers.ContentType = new MediaTypeHeaderValue("application/x-www-form-urlencoded");
            var response = await client.PostAsync("https://stageapi.dideban.live/v1/auth/token", content);

            var result = await response.Content.ReadAsStringAsync();
            Console.WriteLine(result);
        }
    }
}
```

```javascript
const axios = require('axios');
const qs = require('qs');

const data = qs.stringify({
  'api_key': '<YOUR_API_KEY>',
  'client_id': 'apiClient',
  'client_secret': 'secret',
  'grant_type': 'api_key'
});

const config = {
  method: 'post',
  url: 'https://stageapi.dideban.live/v1/auth/token',
  headers: { 
    'Content-Type': 'application/x-www-form-urlencoded'
  },
  data: data
};

axios(config)
.then(function (response) {
  console.log(JSON.stringify(response.data));
})
.catch(function (error) {
  console.log(error);
});
```
To obtain an access token, make a POST request to the `/auth/token` endpoint with your `api_key`, `client_id`, `client_secret`, and `grant_type`.

## Refresh Access Token

```shell
curl --location 'https://stageapi.dideban.live/v1/auth/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'client_id=apiClient' \
--data-urlencode 'client_secret=secret' \
--data-urlencode 'grant_type=refresh_token' \
--data-urlencode 'refresh_token=<YOUR_REFRESH_TOKEN>'
```

```php
<?php
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://stageapi.dideban.live/v1/auth/token',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS => array(
    'client_id' => 'apiClient',
    'client_secret' => 'secret',
    'grant_type' => 'refresh_token',
    'refresh_token' => '<YOUR_REFRESH_TOKEN>'
  ),
  CURLOPT_HTTPHEADER => array(
    'Content-Type: application/x-www-form-urlencoded'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
?>
```

```csharp
using System;
using System.Net.Http;
using System.Collections.Generic;
using System.Net.Http.Headers;
using System.Threading.Tasks;

namespace DidebanRefreshTokenSample
{
    class Program
    {
        static async Task Main(string[] args)
        {
            var client = new HttpClient();
            var content = new FormUrlEncodedContent(new[]
            {
                new KeyValuePair<string, string>("client_id", "apiClient"),
                new KeyValuePair<string, string>("client_secret", "secret"),
                new KeyValuePair<string, string>("grant_type", "refresh_token"),
                new KeyValuePair<string, string>("refresh_token", "<YOUR_REFRESH_TOKEN>")
            });

            content.Headers.ContentType = new MediaTypeHeaderValue("application/x-www-form-urlencoded");
            var response = await client.PostAsync("https://stageapi.dideban.live/v1/auth/token", content);

            var result = await response.Content.ReadAsStringAsync();
            Console.WriteLine(result);
        }
    }
}
```

```javascript
const axios = require('axios');
const qs = require('qs');

const data = qs.stringify({
  'client_id': 'apiClient',
  'client_secret': 'secret',
  'grant_type': 'refresh_token',
  'refresh_token': '<YOUR_REFRESH_TOKEN>'
});

const config = {
  method: 'post',
  url: 'https://stageapi.dideban.live/v1/auth/token',
  headers: { 
    'Content-Type': 'application/x-www-form-urlencoded'
  },
  data: data
};

axios(config)
.then(function (response) {
  console.log(JSON.stringify(response.data));
})
.catch(function (error) {
  console.log(error);
});
```
Access tokens have a limited lifespan, and you'll need to refresh them periodically to maintain an active session. To refresh your access token, make a POST request to the `/auth/token` endpoint with your `client_id`, `client_secret`, `grant_type`, and `refresh_token`.

Replace YOUR_REFRESH_TOKEN with your actual refresh token in each code sample. This will ensure that you maintain a valid session and can continue making requests to the Dideban API without interruption.

# Subscriptions List

```json
#Sample API response:

[
    {
        "type": "ExternalApiConfig",
        "configId": "644ff890a41411ece9bd0b2f",
        "subscriptionId": "644ff920a41411ece9bd0b32",
        "interval": "00:01:00",
        "baseUrl": null,
        "sourceUrls": [
            "https://sample.ir"
        ],
        "urlAbbreviation": "di",
        "scrapeInstruction": null,
        "externalApiInstruction": {
            "id": "644ff890a41411ece9bd0b2e",
            "variableValue": "https://api.sample.ir/v8/web-search/sample",
            "options": null
        },
        "selectedOptions": null,
        "triggerValue": {
            "mainStringValue": null,
            "secondStringValue": null,
            "mainNumberValue": null,
            "secondNumberValue": null,
            "previousFetchedDataId": "6453a1360141cdcbd454bba1",
            "previousFetchedData": null
        },
        "triggerType": "A_NewRow",
        "customTriggerCode": 0,
        "method": "Element",
        "status": "Active",
        "name": "دیوار - ویلاهای استان البرز",
        "websiteId": null,
        "notificationSetting": {
            "receivePush": true,
            "receiveTelegram": true,
            "receiveSMS": false,
            "receiveEmail": true
        },
        "lastFetchDate": "2023-05-04T12:12:38.616Z",
        "lastChangeDate": "2023-05-04T12:12:38.616Z",
        "previousFetchedDataSummary": "نمونه داده ها | و 23 مورد دیگر",
        "lastChangeType": "Auxilary"
    },
    //Other subscriptions you might have...
]
```
With the Subscriptions List API, you can fetch a list of scraping configurations that you have subscribed to, along with their details. The API returns various attributes, such as `configId`, `subscriptionId`, `interval`, `baseUrl`, `sourceUrls`, `scrapeInstruction`, `externalApiInstruction`, and more.
## Get All Config Subscriptions

```shell
curl --location 'https://stageapi.dideban.live/v1/configSubscription/getAll?OrderBy=BaseUrl' \
--header 'Authorization: Bearer <YOUR_ACCESS_TOKEN>'
```

```php
<?php
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://stageapi.dideban.live/v1/configSubscription/getAll?OrderBy=BaseUrl',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'GET',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer <YOUR_ACCESS_TOKEN>'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
?>
```

```csharp
using System;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Threading.Tasks;

namespace DidebanSubscriptionsListSample
{
    class Program
    {
        static async Task Main(string[] args)
        {
            var client = new HttpClient();
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", "<YOUR_ACCESS_TOKEN>");

            var response = await client.GetAsync("https://stageapi.dideban.live/v1/configSubscription/getAll?OrderBy=BaseUrl");

            var result = await response.Content.ReadAsStringAsync();
            Console.WriteLine(result);
        }
    }
}
```

```javascript
const axios = require('axios');

const config = {
  method: 'get',
  url: 'https://stageapi.dideban.live/v1/configSubscription/getAll?OrderBy=BaseUrl',
  headers: { 
    'Authorization': 'Bearer <YOUR_ACCESS_TOKEN>'
  }
};

axios(config)
.then(function (response) {
  console.log(JSON.stringify(response.data));
})
.catch(function (error) {
  console.log(error);
});
```
To fetch the list of subscriptions, make a GET request to the `/configSubscription/getAll` endpoint with the OrderBy parameter set to the desired ordering attribute (`BaseUrl` or `LastChangeDate`).

Here are the code samples in cURL, PHP, .NET (C#), and JavaScript for fetching the subscriptions list. Just remember to replace the `YOUR_ACCESS_TOKEN` placeholder with your actual access token.

# Analyze Results

```json
[
    {
        "type":"ExternalApiConfig",
        "id": "6453a1360141cdcbd454bba2",
        "scrapeConfigId": null,
        "externalApiConfigId": "644ff890a41411ece9bd0b2f",
        "scrapeSubscriptionId": null,
        "externalApiSubscriptionId": "644ff920a41411ece9bd0b32",
        "analyseStartDate": "2023-05-04T12:12:38.65Z",
        "analyseEndDate": "2023-05-04T12:12:38.65Z",
        "fetchStartDate": "2023-05-04T12:12:36.595Z",
        "fetchEndDate": "2023-05-04T12:12:38.616Z",
        "result": {
            "newTextSummary": "۲۳۵ متر با جواز ساخت لاین ۳ | ۱۹,۰۰۰,۰۰۰,۰۰۰ تومان | آژانس املاک نمونه در کرج | و 2 مورد دیگر",
            "oldTextSummary": null,
            "documentDifferences": [
                {
                    "oldRow": null,
                    "newRow": {
                        "image_src": "",
                        "title": "۲۳۵ متر با جواز ساخت لاین ۳",
                        "price": "۱۹,۰۰۰,۰۰۰,۰۰۰ تومان",
                        "description": "آژانس املاک نمونه در کرج",
                        "link": "https://sample.ir/v/AZJx230b",
                        "date": "1683201306261392"
                    }
                },
                {
                    "oldRow": null,
                    "newRow": {
                        "image_src": "",
                        "title": "۲۳۵ متر با جواز ساخت لاین ۳",
                        "price": "۱۹,۰۰۰,۰۰۰,۰۰۰ تومان",
                        "description": "آژانس املاک نمونه در کرج",
                        "link": "https://sample.ir/v/AZJx230b",
                        "date": "1683201306261392"
                    }
                }
            ]
        },
        "status": "Done",
        "triggerStatus": "Met"
    },
    //Other analyse results you might have...
]
```

The "analyse orders" are a set of results generated from the processing of scraping requests in a scraping configuration. These orders are based on the interval and triggers set in the configuration. The main purpose of analyze orders is to identify and track changes in the scraped data over time.

When a scraping request is processed, the system analyzes the fetched data to look for differences based on the triggers set in the configuration. These differences are then stored as analyse results, which can be retrieved through the provided API.

An analyse result typically contains information such as the start and end time of the analysis, the fetched data, and the differences found between the old and new data. In the given example, the result shows that there are two new rows added, along with their respective details such as the title, price, description, and link.

To retrieve all the analyse results, you can use the API endpoint https://stageapi.dideban.live/v1/analyseResult/getAll, with the required parameters and filters such as TriggeredOnly, PageSize, CurrentPage, ScrapeSubscriptionId, ExternalApiSubscriptionId, From, and To. Make sure to replace <YOUR_ACCESS_TOKEN> with your actual access token in the API request.

In summary, the analyse orders are a way to track and monitor changes in scraped data based on the triggers set in a scraping configuration. These orders can be retrieved and analyzed through the provided API to help users understand and act upon any significant changes in the data.

## Get All Analyse Results

Replace `YOUR_ACCESS_TOKEN` with your actual access token in each example.


```shell
curl --location 'https://stageapi.dideban.live/v1/analyseResult/getAll?TriggeredOnly=true&PageSize=10&CurrentPage=0&ScrapeSubscriptionId=63999fd71d200b38fa7521d7&ExternalApiSubscriptionId=63999fd71d200b38fa7521d7&From=2023-02-07T14%3A19%3A13.574Z&To=2023-05-07T14%3A19%3A13.574Z' \
--header 'Authorization: Bearer <YOUR_ACCESS_TOKEN>'
```

```php
$curl = curl_init();

curl_setopt_array($curl, [
  CURLOPT_URL => "https://stageapi.dideban.live/v1/analyseResult/getAll?TriggeredOnly=true&PageSize=10&CurrentPage=0&ScrapeSubscriptionId=63999fd71d200b38fa7521d7&From=2023-02-07T14%3A19%3A13.574Z&To=2023-05-07T14%3A19%3A13.574Z",
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_CUSTOMREQUEST => "GET",
  CURLOPT_HTTPHEADER => [
    "Authorization: Bearer <YOUR_ACCESS_TOKEN>"
  ],
]);

$response = curl_exec($curl);
$err = curl_error($curl);

curl_close($curl);

if ($err) {
  echo "cURL Error #:" . $err;
} else {
  echo $response;
}
```

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main(string[] args)
    {
        using (var httpClient = new HttpClient())
        {
            httpClient.DefaultRequestHeaders.Authorization =
                new System.Net.Http.Headers.AuthenticationHeaderValue("Bearer", "<YOUR_ACCESS_TOKEN>");

            var url = "https://stageapi.dideban.live/v1/analyseResult/getAll?TriggeredOnly=true&PageSize=10&CurrentPage=0&ScrapeSubscriptionId=63999fd71d200b38fa7521d7&From=2023-02-07T14%3A19%3A13.574Z&To=2023-05-07T14%3A19%3A13.574Z";
            HttpResponseMessage response = await httpClient.GetAsync(url);

            if (response.IsSuccessStatusCode)
            {
                string content = await response.Content.ReadAsStringAsync();
                Console.WriteLine(content);
            }
            else
            {
                Console.WriteLine($"Error: {response.StatusCode}");
            }
        }
    }
}
```

```javascript
const axios = require('axios');

const config = {
  method: 'get',
  url: 'https://stageapi.dideban.live/v1/analyseResult/getAll?TriggeredOnly=true&PageSize=10&CurrentPage=0&ScrapeSubscriptionId=63999fd71d200b38fa7521d7&From=2023-02-07T14%3A19%3A13.574Z&To=2023-05-07T14%3A19%3A13.574Z',
  headers: {
    'Authorization': 'Bearer <YOUR_ACCESS_TOKEN>'
  }
};

axios(config)
  .then(response => {
    console.log(JSON.stringify(response.data));
  })
  .catch(error => {
    console.log(error);
  });
```


To fetch the list of subscriptions, make a GET request to the `/configSubscription/getAll` endpoint with the optional query parameters below:

1. TriggeredOnly: When set to true, it will only return the results where the trigger conditions are met.
2. PageSize: Determines the number of analyze results returned per page.
3. CurrentPage: Specifies the current page number for the paginated results.
4. ScrapeSubscriptionId: An optional filter for analyze results based on a specific Scrape Subscription ID.
5. ExternalApiSubscriptionId: An optional filter for analyze results based on a specific External API Subscription ID.
6. From: The start date for the date range filter (in ISO 8601 format).
7. To: The end date for the date range filter (in ISO 8601 format).

<aside class="notice">
You can use either ScrapeSubscriptionId or ExternalApiSubscriptionId in the request, but not both at the same time.
</aside>

### PageSize and CurrentPage
PageSize and CurrentPage are used for pagination. PageSize determines the number of analyze results to display per page, while CurrentPage specifies which page of the results you want to retrieve. 

For example, if there are 100 results and you set PageSize to 10, you will have 10 pages of results. By changing the CurrentPage parameter, you can navigate through these pages.

<aside class="notice">
PageSize should be between 10 and 100.
</aside>

### From and To
The From and To query parameters are used to filter the analyze results based on a date range. The results will only include those that fall within the specified range.

<aside class="notice">
 The date values should be in ISO 8601 format (e.g., "2023-02-07T14:19:13.574Z").
</aside>
