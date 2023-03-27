---
title: Net Zero Insights API documentation

language_tabs:
  - shell

toc_footers:
  - <a href='https://netzeroinsights.com'>Visit our website</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: api documentation
    content: Documentation for the Net Zero Insights API
---

# Introduction

Our REST APIs give all the functionalities needed to interact with our database. All these services are exclusively usable with https standard, and only after having been authenticated.

For brevity, the possible error codes for all the calls are at the bottom of the document.

Every endpoint is to be called starting with the domain https://api.netzeroinsights.com

# Security

## Login

> To login, use this code:

```shell
curl -v -X POST "https://api.netzeroinsights.com/security/formLogin" \
-H "Content-Type: application/x-www-form-urlencoded" \
-d "username=YOUR_USERNAME&password=YOUR_PASSWORD"
```

> Make sure to replace `YOUR_USERNAME` and `YOUR_PASSWORD` with your credentials.
> 
> Using the -v ("verbose") flag lets you see the full response, in which you can find the **Session Cookie**.

Before using any other API, you should first login using the following endpoint:

`POST /security/formLogin`

With the following two parameters:

Parameter name | Parameter value
--------- | -----------
username | provided by Net Zero Insights
password | provided by Net Zero Insights

The possible response codes are:

Response code | Meaning
--------- | -----------
200 | Login successful

Please note that in case of a 200 response, you will also get a **Session Cookie**. You should save this,
as it will be needed for using all the other endpoints. The session cookie expires after 30 minutes of
session inactivity.

Our API expects the **Session Cookie** to be included in all API requests to the server, like this:

`JSESSIONID=EXAMPLE_SESSION_ID`

<aside class="notice">
You must replace <code>EXAMPLE_SESSION_ID</code> with your **Session Cookie**.
</aside>

## Logout

> To logout, use this code:

```shell
curl -v --cookie "JSESSIONID=EXAMPLE_SESSION_ID" \
 -X GET "https://api.netzeroinsights.com/security/logout"
```

> Make sure to replace `EXAMPLE_SESSION_ID` with your **Session Cookie**

To close the session, you should use the following endpoint:

`GET /security/logout`

It takes no parameter, and has the following response code:

Response code | Meaning
--------- | -----------
200 | Session terminated

<aside class="notice">
Please note that manually closing a session is not required, since it will be closed bye the server after
30 minutes. This endpoint is mainly used if you need to use different accounts.
</aside>

# Startup List

> To get startup list, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X POST 'https://api.netzeroinsights.com/getStartupList' \
-H 'Content-Type: application/json' \                 
-d '{"limit": 5, "offset": 0, "include":{}, "exclude": {}, "sorting": {}}'
```

> In case of a 200 response, the response body will contain the startups matching your request, with the format specified at section [Startup Search](#startup-search).

```json
{
  "count": 5,
  "results": [
    {
      "clientID": 72592,
      "name": "Net Zero Insights",
      "logo": "https://res.cloudinary.com/eutop-1/image/upload/v1679698613/Startups/egykhqdli5njwqeqgdgb.jpg",
      "website": "https://netzeroinsights.com/",
      "domain": "netzeroinsights.com",
      "pitchLine": "Net Zero Insights develops and operates the Net Platform: a market intelligence platform for climate tech startups and SMEs.<br><br>It offers access to the largest climate tech startup database, allowing users to stay up-to-date on the latest innovation, trends and deals in the climate tech industry. The platform covers organizations globally and provides data-points, such as funding rounds, patents, and direct contacts to founders and C-Suite, to help users make well-informed decisions. The platform's smart search features and email notifications make it easy for users to track organizations.<br><br>The platform is also supported by a team of analysts who ensure data accuracy and are available for technical support within the subscription.",
      "description": "Provider of a web platform to access information about climate tech startups such as climate impact, patents, financials, traction, contacts, and more. The Net0 market intelligence platform enables decision makers and market players to gain insight into the climate technology VC space. A platform matching greentech project to the resources they need - for free. A platform to connect greentech projects with the resources they need to take off. Data, insights and updates on the climate tech venture space. We help decision makers scout and assess the climate tech solutions they need to make the transition happen. \n \nSort over 45K+ climate startups in Europe and North America, and gain access to hard-to-find data such as patents, contacts, impact metrics, traction, fundings and deals. \n \nOur end goal is to simplify access to meaningful data about climate innovation to investors, governments, policy makers, researchers and business developers.\n \nWhy don't you give a try for free and share your feedback later with us  https://bit.ly/netzero-freetrial We help decision makers scout and assess the climate tech solutions they need to make the transition happen.  Sort over 45K+ climate startups in Europe and North America, and gain access to hard-to-find data such as patents, contacts, impact metrics, traction, fundings and deals.  Our end goal is to simplify access to meaningful data about climate innovation to investors, governments, policy makers, researchers and business developers. Why dont you give a try for free and share your feedback later with us  https://bit.ly/netzero-freetrial  Provider of a web platform to access information about climate tech startups such as climate impact, patents, financials, traction, contacts, and more. I get back to you as we've just launched an AI-powered platform to access information about thousands of climate startups in. Eutopia is an AI-powered platform to access information about thousands of green startups in Europe. The most comprehensive database of climate tech startups and SMEs in Europe and North America. Provider of a web platform to access information about climate tech startups such as climate impact, patents, financials, traction, contacts, and more. ket A social business mapping innovative green startups to provide market players with insights, analytics, and consulting on the future of green technology.We are working on a platform to find information about green startups and technologies with the aim of putting greentech innovation in front of decision-makers Eutopia is a social business mapping innovative green startups to provide market players with insights, analytics, and consulting on the future of green technology. We have developed a web-based platform to find information about green startups and technologies with the aim of putting green innovation in front of decision-makers. Book a demo at: ??????????://??????????.??????/????1??????????????????????????5 For each venture, the platform includes information such as sector of activity, technologies employed, climate impact, SDGs, and generic info like financials, commercial stage, founded date, employees number and more. Eutopia sources its data by crawling news, company websites on the internet, asking directly to startups, establishing key partnerships with green accelerators and events and thanks to its in-house data team. ?????? ?????? ?? ?????????? ??????????????? ?????? ???????????????? ???? ??????????????: ??????????://????????????????????????.??????/????????????????",
      "fundingAmount": 320000.0,
      "fundingString": "320K",
      "fundingAmountUSD": 326273.0,
      "fundingStringUSD": "326.3K",
      "fundingRangeID": 1,
      "fundingRange": "0 - 500K",
      "lastRoundDate": "2022-07-01T02:00:00.000+00:00",
      "sustainabilityMetric": 0.41335288,
      "foundedDate": 2020,
      "countryID": 172,
      "country": "Portugal",
      "city": "Lisbon",
      "continent": "Europe",
      "email": "info@netzeroinsights.com",
      "phone": "+351 934 529 622",
      "sizeID": 2,
      "size": "11-50",
      "stageID": 2,
      "stage": "Early",
      "linkedinURL": "https://www.linkedin.com/company/12649435/",
      "twitterURL": "https://twitter.com/netzeroinsights/",
      "facebookURL": "https://facebook.com/netzeroinsights/",
      "directURL": "net-zero-insights-72592",
      "sustainabilityMetricID": 2,
      "lastRoundAmount": 320000,
      "lastRoundAmountUSD": 326273,
      "lastRoundAmountString": "320K",
      "lastRoundAmountStringUSD": "326.3K",
      "lastRoundType": "Pre-Seed",
      "tags": [
        {
          "tagTypeId": 74,
          "definition": "Storage, manipulation, management, movement, control, display, switching, interchange, transmission or processing of data through data centres, including edge computing.",
          "tagType": {
            "id": 74,
            "tagType": "EU activity",
            "platformOrder": 9,
            "tagFamily": {
              "id": 1,
              "tagFamily": "EU taxonomy",
              "platformOrder": 1
            }
          },
          "id": 488,
          "filterable": true,
          "label": "Data processing, hosting and related activities"
        },
        {
          "tagTypeId": 3,
          "tagType": {
            "id": 3,
            "tagType": "technology",
            "platformOrder": 3,
            "tagFamily": {
              "id": 2,
              "tagFamily": "Solutions",
              "platformOrder": 2
            }
          },
          "id": 14,
          "filterable": true,
          "label": "artificial intelligence (AI)"
        }
      ],
      "fundingTypes": [
        "Equity"
      ],
      "sdgs": [
        {
          "id": 13,
          "label": "13. Climate action"
        }
      ],
      "note": "",
      "fundingRangeUSD": "0 - 500K",
      "fundingRangeIDUSD": 1,
      "alternativeNames": [
        "Eutopia Green",
        "Net0i",
        "Eutopia"
      ],
      "legalNames": [
        " Net Zero Insights Unipessoal Lda",
        "Net Zero Insights Holding Limited"
      ],
      "numberOfGrants": 1,
      "id": 42080,
      "eutopiaScore": 41
    },
    {
      [omissis...]
    },
    [omissis...]
  ]
}
```

To search our startup database you should use the following endpoint:

`POST /getStartupList`

With a JSON request body in the format specified at the section [Main Filter](#main-filter).

The possible response codes are:

Response code | Meaning
--------- | -----------
200 | Request successful

# Startup Detail

All the information related to a startup is divided into different sections: 

1. [Overview and Taxonomy](#startup-overview-and-taxonomy)
2. [Patents](#startup-patents)
3. [Investors](#startup-investors)
4. [Contacts](#startup-contacts)
5. [Funding Rounds](#startup-funding-rounds)

Additionally, for each funding round, you can get the investors and the sources using the following endpoints:

1. [Investors](#funding-round-investors)
2. [Sources](#funding-round-sources)

## Startup Overview and Taxonomy

> To get a startup overview and taxonomy, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET "https://api.netzeroinsights.com/getStartup/net-zero-insights-72592"
```

> In case of a 200 response, the response body will contain the requested startup, with the format specified at section [Startup](#startup).

```json
  {
  "clientID": 72592,
  "name": "Net Zero Insights",
  "logo": "https://res.cloudinary.com/eutop-1/image/upload/v1679698613/Startups/egykhqdli5njwqeqgdgb.jpg",
  "website": "https://netzeroinsights.com/",
  "domain": "eutopiagreen.com",
  "pitchLine": "Net Zero Insights develops and operates the Net Platform: a market intelligence platform for climate tech startups and SMEs.<br><br>It offers access to the largest climate tech startup database, allowing users to stay up-to-date on the latest innovation, trends and deals in the climate tech industry. The platform covers organizations globally and provides data-points, such as funding rounds, patents, and direct contacts to founders and C-Suite, to help users make well-informed decisions. The platform's smart search features and email notifications make it easy for users to track organizations.<br><br>The platform is also supported by a team of analysts who ensure data accuracy and are available for technical support within the subscription.",
  "description": "Provider of a web platform to access information about climate tech startups such as climate impact, patents, financials, traction, contacts, and more. The Net0 market intelligence platform enables decision makers and market players to gain insight into the climate technology VC space. A platform matching greentech project to the resources they need - for free. A platform to connect greentech projects with the resources they need to take off. Data, insights and updates on the climate tech venture space. We help decision makers scout and assess the climate tech solutions they need to make the transition happen. \n \nSort over 45K+ climate startups in Europe and North America, and gain access to hard-to-find data such as patents, contacts, impact metrics, traction, fundings and deals. \n \nOur end goal is to simplify access to meaningful data about climate innovation to investors, governments, policy makers, researchers and business developers.\n \nWhy don't you give a try for free and share your feedback later with us  https://bit.ly/netzero-freetrial We help decision makers scout and assess the climate tech solutions they need to make the transition happen.  Sort over 45K+ climate startups in Europe and North America, and gain access to hard-to-find data such as patents, contacts, impact metrics, traction, fundings and deals.  Our end goal is to simplify access to meaningful data about climate innovation to investors, governments, policy makers, researchers and business developers. Why dont you give a try for free and share your feedback later with us  https://bit.ly/netzero-freetrial  Provider of a web platform to access information about climate tech startups such as climate impact, patents, financials, traction, contacts, and more. I get back to you as we've just launched an AI-powered platform to access information about thousands of climate startups in. Eutopia is an AI-powered platform to access information about thousands of green startups in Europe. The most comprehensive database of climate tech startups and SMEs in Europe and North America. Provider of a web platform to access information about climate tech startups such as climate impact, patents, financials, traction, contacts, and more. ket A social business mapping innovative green startups to provide market players with insights, analytics, and consulting on the future of green technology.We are working on a platform to find information about green startups and technologies with the aim of putting greentech innovation in front of decision-makers Eutopia is a social business mapping innovative green startups to provide market players with insights, analytics, and consulting on the future of green technology. We have developed a web-based platform to find information about green startups and technologies with the aim of putting green innovation in front of decision-makers. Book a demo at: ??????????://??????????.??????/????1??????????????????????????5 For each venture, the platform includes information such as sector of activity, technologies employed, climate impact, SDGs, and generic info like financials, commercial stage, founded date, employees number and more. Eutopia sources its data by crawling news, company websites on the internet, asking directly to startups, establishing key partnerships with green accelerators and events and thanks to its in-house data team. ?????? ?????? ?? ?????????? ??????????????? ?????? ???????????????? ???? ??????????????: ??????????://????????????????????????.??????/????????????????",
  "fundingAmount": 320000.0,
  "fundingString": "320K",
  "fundingAmountUSD": 326273.0,
  "fundingStringUSD": "326.3K",
  "fundingRangeID": 1,
  "fundingRange": "0 - 500K",
  "lastRoundDate": "2022-07-01T02:00:00.000+00:00",
  "sustainabilityMetric": 0.41335288,
  "foundedDate": 2020,
  "countryID": 172,
  "country": "Portugal",
  "city": "Lisbon",
  "continent": "Europe",
  "email": "info@netzeroinsights.com",
  "phone": "+351 934 529 622",
  "sizeID": 2,
  "size": "11-50",
  "stageID": 2,
  "stage": "Early",
  "linkedinURL": "https://www.linkedin.com/company/12649435/",
  "twitterURL": "https://twitter.com/netzeroinsights/",
  "facebookURL": "https://facebook.com/netzeroinsights/",
  "directURL": "net-zero-insights-72592",
  "sustainabilityMetricID": 2,
  "lastRoundAmount": 320000,
  "lastRoundAmountUSD": 326273,
  "lastRoundAmountString": "320K",
  "lastRoundAmountStringUSD": "326.3K",
  "lastRoundType": "Pre-Seed",
  "tags": [
    {
      "tagTypeId": 74,
      "definition": "Storage, manipulation, management, movement, control, display, switching, interchange, transmission or processing of data through data centres, including edge computing.",
      "tagType": {
        "id": 74,
        "tagType": "EU activity",
        "platformOrder": 9,
        "tagFamily": {
          "id": 1,
          "tagFamily": "EU taxonomy",
          "platformOrder": 1
        }
      },
      "id": 488,
      "filterable": true,
      "label": "Data processing, hosting and related activities"
    },
    {
      "tagTypeId": 3,
      "tagType": {
        "id": 3,
        "tagType": "technology",
        "platformOrder": 3,
        "tagFamily": {
          "id": 2,
          "tagFamily": "Solutions",
          "platformOrder": 2
        }
      },
      "id": 14,
      "filterable": true,
      "label": "artificial intelligence (AI)"
    }
  ],
  "fundingTypes": [
    "Equity"
  ],
  "sdgs": [
    {
      "id": 13,
      "label": "13. Climate action"
    }
  ],
  "note": "",
  "fundingRangeUSD": "0 - 500K",
  "fundingRangeIDUSD": 1,
  "alternativeNames": [
    "Eutopia Green",
    "Net0i",
    "Eutopia"
  ],
  "legalNames": [
    " Net Zero Insights Unipessoal Lda",
    "Net Zero Insights Holding Limited"
  ],
  "numberOfGrants": 1,
  "id": 42080,
  "eutopiaScore": 41
}
```

To get a startup overview and taxonomy you should use the following endpoint:

`GET /getStartup/[directLink]`

It takes a single parameter, indicated as ”[directLink]” in the example, which is taken from a previous call of the endpoint at [Startup List](#startup-list), variable ”directLink”, and has the following response codes:

Response code | Meaning
--------- | -----------
200 | Request successful

## Startup Patents

> To get a startup overview and taxonomy, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET "https://api.netzeroinsights.com/patents/668"
```

> In case of a 200 response, the response body will contain the requested patents, with the format specified at section [Patent](#patent).
     
```json
[
  {
    "id": 54136,
    "googlePatentsUrl": "https://patents.google.com/patent/DE112015006427A5/",
    "filingDate": "2015-04-07T22:00:00.000+00:00",
    "publicationDate": "2017-12-27T23:00:00.000+00:00",
    "patentAbstract": "A Process For The Production Of Synthetically Produced Methane (57)/Gaseous And/Or Liquid Hydrocarbons (114, 115, 116, 117). For This Purpose, Hydrogen (44, 84, 150) From An Electrolytic Arrangement (41, 81, 151, 159) Which Is Operated By Means Of Regeneratively Generated Electric Energy And Carbon Dioxide (19, 46, 86) Are Synthesized In A Methane Synthesis (Figs. 2-48) Or Fischer-Tropsch Synthesis (Figs. 3-96) Or Other Suitable Hydrocarbon Synthesis, The Carbon Dioxide (19, 46, 86) Being Produced From An Air/Gas Flow (3, 134) By Means Of A Carbon Dioxide Recovery System (Fig. 1). The Carbon Dioxide (19, 46, 86) Is Obtained From The Air/Gas Flow (3, 134) In The Carbon Dioxide Recovery System (Fig. 1) By Way Of A Reversible Adsorption Process. Also A Production System (57) For The Production Of Synthetically Produced Methane/Gaseous And/Or Liquid Hydrocarbons (114, 115, 116, 117), In Particular For Carrying Out The Production Process According To The Invention, Comprising An Electrolytic Arrangement (41, 81, 151, 159) Which Is Operated By Means Of Regeneratively Generated Electric Energy (42, 82, 153) For Producing Hydrogen (44, 84, 150), A Carbon Dioxide Recovery System (Fig. 1) For Producing Carbon Dioxide (19, 46, 86) From An Air/Gas Flow (3, 134) And A Methane (Fig. 2) Or Fischer-Tropsch Synthesis (Fig. 3) Or Any Other Suitable Hydrocarbon Synthesis For Synthesizing Hydrogen (44, 84, 150) And Carbon Dioxide (19, 45, 86) To Methane (57)/Gaseous And/Or Liquid Hydrocarbons (114, 115, 116, 117).",
    "title": "Production Process And Production System For Producing Methane / Gaseous And/Or Liquid Hydrocarbons",
    "jurisdiction": 80,
    "publicationNumber": "DE-112015006427-A5",
    "familyId": 1078,
    "clientId": 668,
    "jurisdictionName": "Germany",
    "status": "pending"
  },
  {
    "id": 54137,
    "googlePatentsUrl": "https://patents.google.com/patent/WO2016161998A1/",
    "filingDate": "2015-04-07T22:00:00.000+00:00",
    "publicationDate": "2016-10-12T22:00:00.000+00:00",
    "patentAbstract": "A Process For The Production Of Synthetically Produced Methane (57)/Gaseous And/Or Liquid Hydrocarbons (114, 115, 116, 117). For This Purpose, Hydrogen (44, 84, 150) From An Electrolytic Arrangement (41, 81, 151, 159) Which Is Operated By Means Of Regeneratively Generated Electric Energy And Carbon Dioxide (19, 46, 86) Are Synthesized In A Methane Synthesis (Figs. 2-48) Or Fischer-Tropsch Synthesis (Figs. 3-96) Or Other Suitable Hydrocarbon Synthesis, The Carbon Dioxide (19, 46, 86) Being Produced From An Air/Gas Flow (3, 134) By Means Of A Carbon Dioxide Recovery System (Fig. 1). The Carbon Dioxide (19, 46, 86) Is Obtained From The Air/Gas Flow (3, 134) In The Carbon Dioxide Recovery System (Fig. 1) By Way Of A Reversible Adsorption Process. Also A Production System (57) For The Production Of Synthetically Produced Methane/Gaseous And/Or Liquid Hydrocarbons (114, 115, 116, 117), In Particular For Carrying Out The Production Process According To The Invention, Comprising An Electrolytic Arrangement (41, 81, 151, 159) Which Is Operated By Means Of Regeneratively Generated Electric Energy (42, 82, 153) For Producing Hydrogen (44, 84, 150), A Carbon Dioxide Recovery System (Fig. 1) For Producing Carbon Dioxide (19, 46, 86) From An Air/Gas Flow (3, 134) And A Methane (Fig. 2) Or Fischer-Tropsch Synthesis (Fig. 3) Or Any Other Suitable Hydrocarbon Synthesis For Synthesizing Hydrogen (44, 84, 150) And Carbon Dioxide (19, 45, 86) To Methane (57)/Gaseous And/Or Liquid Hydrocarbons (114, 115, 116, 117).",
    "title": "Production Process And Production System For Producing Methane / Gaseous And/Or Liquid Hydrocarbons",
    "jurisdiction": 241,
    "publicationNumber": "WO-2016161998-A1",
    "familyId": 1078,
    "clientId": 668,
    "jurisdictionName": "World",
    "status": "pending"
  } 
]
```

To get all the patents of a startup, you should use the following endpoint:

`GET /patents/[clientID]`

It takes a single parameter, indicated as ”[clientID]” in the example, which is taken from a previous call of the endpoint at [Startup List](#startup-list), variable ”clientID”, and has the following response codes:

Response code | Meaning
--------- | -----------
200 | Request successful

## Startup Investors

> To get all the investors of a startup, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET "https://api.netzeroinsights.com/investors/72592"
```

> In case of a 200 response, the response body will contain the requested investors, with the format specified at section [Investor](#investor).

```json
[
  {
    "id": 15265,
    "name": "Chris Goodall",
    "firstRoundDate": "Jul 2022",
    "roundTypes": "Pre-Seed"
  },
  {
    "id": 15316,
    "name": "Miguel de Ros",
    "firstRoundDate": "Jul 2022",
    "roundTypes": "Pre-Seed"
  }
]
```

To get all the investors of a startup, you should use the following endpoint:

`GET /investors/[clientID]`

It takes a single parameter, indicated as ”[clientID]” in the example, which is taken from a previous call of the endpoint at [Startup List](#startup-list), variable ”clientID”, and has the following response codes:

Response code | Meaning
--------- | -----------
200 | Request successful

## Startup Contacts

> To get all the contacts of a startup, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X POST "https://api.netzeroinsights.com/contacts" \
-H "Content-Type: application/json" \
-d "{'clientID': 72592, 'decisionMaker': false, 'roleID': 5}"
```

> In case of a 200 response, the response body will contain all the requested contacts, with the format specified at section [Contact](#contact).

```json
[
  {
    "name": "Aafia Tehrim",
    "role": "Climate Tech Analyst",
    "department": "Tech",
    "email": "aafia@netzeroinsights.com",
    "linkedinURL": "http://www.linkedin.com/in/aafia-tehrim-36856920a",
    "decisionMaker": false,
    "id": 1112723
  }
]
```

To get all contacts of a startup, you should use the following endpoint:

`POST /contacts`

With a JSON request body in the format specified at the Section [Contacts Filter](#contacts-filter), and has the following response codes:

Response code | Meaning
--------- | -----------
200 | Request successful

## Startup Funding rounds

> To get all the funding rounds of a startup, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET https://api.netzeroinsights.com/fundingRoundsPrints/72592
```

> In case of a 200 response, the response body will contain the requested funding rounds, with the format specified at section [Funding Round](#funding-round).

```json
[
  {
    "clientId": 72592,
    "roundDate": "2022-07-01T02:00:00.000+00:00",
    "roundType": "Pre-Seed",
    "roundAmount": 320000.0,
    "roundAmountUSD": 326273.0,
    "roundAmountId": 1,
    "coFundingRoundId": 168677,
    "fundingRange": "0 - 500K",
    "roundInvestors": [
      15265,
      15266,
      15317,
      18450,
      15316
    ],
    "roundNews": [
      86510,
      87287
    ],
    "roundCurrency": "EUR",
    "source": "andrea_canepa",
    "originalRoundAmount": 320000.0,
    "valuationAmount": "1600000",
    "valuationCurrency": "EUR",
    "valuationType": "post-money",
    "financingInstrument": "Grant",
    "equityStageID": 2,
    "exitStageID": 1,
    "id": 152398
  }
]
```

To get all the funding rounds of a startup, you should use the following endpoint:

`GET /fundingRoundsPrints/[clientID]`

It takes a single parameter, indicated as ”[clientID]” in the example, which is taken from a previous call of the endpoint at [Startup List](#startup-list), variable ”clientID”, and has the following response codes:

Response code | Meaning
--------- | -----------
200 | Request successful

## Funding round investors

> To get all the investors of a given set of funding rounds, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X POST https://api.netzeroinsights.com/getFundingRoundInvestors \
-H "Content-Type: application/json" \
-d "{[168677]}"
```

> In case of a 200 response, the response body will contain all the investors of the requested funding rounds, with the format specified at section [Funding Round Investor](#funding-round-investor).

```json
[
  {
    "id": 15265,
    "name": "Chris Goodall",
    "website": "https://uk.linkedin.com/in/chris-goodall-b2a51510",
    "fundingRoundId": 168677
  },
  {
    "id": 15266,
    "name": "Tony Lent",
    "website": "https://www.linkedin.com/in/tony-lent-80096a",
    "fundingRoundId": 168677
  }
]
```

To get all the investors of a given set of funding rounds, you should use the following endpoint:

`POST /getFundingRoundInvestors`

The request body should be a list of round IDs, which you can get from previous calls of [Startup Funding Rounds](#startup-funding-rounds), variable ”coFundingRoundId”, and has the following response codes:

Response code | Meaning
--------- | -----------
200 | Request successful

## Funding round sources

> To get all the sources of a funding round, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
 -X GET https://api.netzeroinsights.com/roundNewsByRoundID/168677
```

> In case of a 200 response, the response body will contain all the sources of a funding rounds, with the format specified at section [Funding round source](#funding-round-source).

```json
[
  {
    "id": 86510,
    "googleTitle": "",
    "url": "https://netzeroinsights.com/resources/our-updates/net-zero-insights-raises-320k-in-pre-seed-funding-to-develop-climate-tech-market-intelligence-software/",
    "fundingRoundId": 168677
  }
]
```

To get all the sources of a funding round, you should use the following endpoint:

`GET /roundNewsByRoundID/[coFundingRoundId]`

It takes a single parameter, indicated as ”[coFundingRoundId]” in the example, which is taken from a previous call of the endpoint at Section [Startup Funding Rounds](#startup-funding-rounds), variable ”coFundingRoundId”, and has the following response codes:

Response code | Meaning
--------- | -----------
200 | Request successful

# Filters structure

## Main Filter

This is the main filter used when searching for startups. It contains two simple fields (”offset” and ”limit”) and some complex ones (i.e.: ”include”, ”sorting”) defined further in this document.

Parameter name | Parameter type | Description
--------- | ----------- | -------------------
limit | int | Maximum number of results shown
offset | int | Number of pages (of size "limit") skipped
sorting | Section [Sorting](#sorting) | Order of the results
include | Section [Startups Filter](#startups-filter) | Filters related to startups which should be included in the result
exclude | Section [Startups Filter](#startups-filter) | Filters related to startups which should be excluded in the result

## Sorting

Parameter name | Parameter type | Description
--------- | ----------- | -------------------
column | string | See Section [Sortable Columns](#sortable-columns) for the available options
direction | string | The only options available are ”ASC” and ”DESC”

## Startups Filter

Parameter name | Parameter type | Description
--------- | ----------- | -------------------
searchableLocations | List of int | See Section [Searchable Locations](#searchable-locations) for the accepted values
sizes | List of Section [Size](#size) | Number of employees
stages | List of int | Growth stage, see Section [Stages](#stages) for accepted values
fundings | List of int | Total funding range, see Section [Fundings](#fundings) for accepted val- ues
fundingsFrom | int | Minimum total funding
fundingsTo | int | Maximum total funding
tags | List of int | See Section [Tags](#tags) for accepted values
sustainabilities | List of int | See Section [Sustainabilities](#sustainabilities) for accepted values
foundedDates | List of Section [Founded Date](#founded-date) | Startup founded date
acquisitionDateFrom | date | Starting date for when the startup has been inserted into our database
acquisitionDateTo | date | Maximum date for when the startup has been in- serted into our database
foundedDatesFrom | date | Starting founded date
foundedDatesTo | date | Maximum founded date
raisedDateFrom | date | Starting date for any round
raisedDateTo | date | Maximum date for any round
lastRoundDates | List of Section [Last Round Date](#last-round-date) | Date range for last round
lastRoundDatesFrom | date | Starting date for last round
lastRoundDatesTo | date | Maximum date for last round
fundingTypes | List of Section [Funding Type](#funding-type) | Funding type for any round
sdgs | List of int | Sustainable development goals, see Section [SDGs](#sdgs) for accepted values
wildcards | List of string | Any match of the keywords in the name/pitchline/description
wildcardsFields | List of Section [Wildcard Fields](#wildcard-fields) | Select on which fields to match the wildcards
investors | List of int | See Section [Investors](#investors) for the accepted values
lastFundingTypes | List of Section [Funding Type](#funding-type) | Funding type for last round
lastFundingsFrom | List of int | Minimum last round amount
lastFundingsTo | List of int | Maximum last round amount
patentSearch | List of string | Any match of the keywords in any patent description
patentsStatus | List of Section [Patent Status](#patent-status) | Status of any patent
applicationDateFrom | Date | Starting application date for any patent
applicationDateTo | Date | Maximum application date for any patent
grantedDateFrom | Date | Starting granted date for any patent
grantedDateTo | Date | Maximum granted date for any patent
patentOffice | List of int | See Section [Searchable Locations](#searchable-locations) for the accepted values
patentsCountFrom | int | Minimum number of patents
patentsCountTo | int | Maximum number of patents
fundRaising | List of string | Use ”fundRaising” to see all the companies likely to fundraise

## Contacts Filter

Parameter name | Parameter type | Description
--------- |----------------| -------------------
clientID | int            | ClientID of the requested startup, taken from a previous call of [Startup List](#startup-list)
decisionMaker | boolean        | Optional, if true only returns contacts with decision making capabilities
roleID | int            | Optional, contact role, see Section [Role](#role) for accepted values

# Additional Tables

## Sortable Columns

Value | Usable for | Description
--------- | ----------- | -------------------
name | startup | Startup name
country | startup | Startup country
website | startup | Startup website
foundedDate | startup | Startup founded date
size | startup | Number of employees
stage | startup | Startup growth stage
lastRoundDate | startup | Startup last round date
acquisitionDate | startup | Date of startup insertion into our database
fundingString | startup | Startup total funding
lastRoundAmount | startup | Startup last round amount
lastRoundType | startup | Startup last round type
sustainabilityMetricID | startup | Startup impact on the ecosystem
tags | startup | Startup tags
fundingTypes | startup | Startup funding types
sdgs | startup | Startup Sustainable Development Goals

## Size

ID | Label
--- | ---- 
1 | 1-10
2 | 11-50
3 | 51-100
4 | 101-200
5 | 201-500
6 | 501-1000
7 | 1001-5000
8 | 5001-10000
9 | 10000+

## Founded Date

ID | Label
--- | ----
1 | This year
2 | Last year
3 | Last 3 years
4 | Last 5 years

## Last Round Date

ID | Label
--- | ----
1 | Last month
2 | Last semester
3 | Last year

## Wildcard Fields

Label |
------ |
pitchLine |
description | 
websiteContent |

## Patent Status

Label |
------ |
granted |
pending |

## Stages

ID | Label
--- | ----
1 | Ideation
2 | Early
3 | Growth
4 | Scaling

## Fundings

ID | Label
--- | ----
1 | 0 - 500K
2 | 500K - 1M
3 | 1M-5M
4 | 5M-10M
5 | 10M - 25M
6 | 25M - 50M
7 | 50M - 100M
8 | 100M - 250M
9 | 250+M

## Sustainabilities

ID | Label
--- | ----
1 | Low impact
2 | Average impact
3 | High impact
4 | Very high impact

## Round Date

ID | Label
--- | ----
1 | Last Month
2 | Last Quarter
3 | Last Semester
4 | Last Year
5 | YTD

## SDGs

ID | Label
--- | ----
1 | 1. No poverty
2 | 2. Zero hunger
3 | 3. Good health and well-being
4 | 4. Quality education
5 | 5. Gender equality
6 | 6. Clean water and sanitation
7 | 7. Affordable and clean energy
8 | 8. Decent work and economic growth
9 | 9. Industry, innovation, and infrastructure
10 | 10. Reduced inequalities
11 | 11. Sustainable cities and communities
12 | 12. Responsible consumption and production
13 | 13. Climate action
14 | 14. Life below water
15 | 15. Life on land
16 | 16. Peace justice and strong institutions
17 | 17. Partenrships

## Financing Instrument

Label |
------ |
Debt |
Equity | 
Grant |

## Equity Stage

ID | Label
--- | ----
1 | Other
2 | Pre-seed and seed
3 | Early stage
4 | Late stage

## Exit Stage

ID | Label
--- | ----
1 | Venture
2 | Exit
3 | Post Exit

## Role

ID | Label
--- | ----
1 | Fouder
2 | HR
3 | Sales
4 | Marketing / PR
5 | Tech
6 | C-Suite

## Tags

> To get the list of the currently available tags, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET "https://api.netzeroinsights.com/getEnabledTags"
```

> In case of a 200 response, the response body will contain all the available tags, with the JSON structured like the following:
     
```json
[
  {
    "name": "3d printing",
    "id": 1
  },
  {
    "name": "advanced material",
    "id": 2
  }
]
```

To get the list of the currently available tags, you should use the following endpoint:

`GET /getEnabledTags`

It takes no parameter, and has the following response codes:

Response code | Meaning
--------- | -----------
200 | Request successful

## Investors

> To get the list of the currently available investors, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET "https://api.netzeroinsights.com/getInvestorsForFilter"
```

> In case of a 200 response, the response body will contain all the available investors, with the JSON structured like the following:
     
```json
[
  {
    "id": 142,
    "name": "Hevella Capital",
    "website": "https://www.hevella-capital.com/"
  },
  {
    "id": 143,
    "name": "IBB Ventures",
    "website": "https://www.ibbventures.de/"
  }
]
```

To get the list of the currently available investors, you should use the following endpoint:

`GET /getInvestorsForFilter`

It takes no parameter, and has the following response codes:

Response code | Meaning
--------- | -----------
200 | Request successful

## Funding Type

> To get the list of the currently available funding types, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET "https://api.netzeroinsights.com/getFundingTypes"
```

> In case of a 200 response, the response body will contain all the available funding types, with the JSON structured like the following:
     
```json
[
  {
    "name": "Accelerator/incubator",
    "id": 65
  },
  {
    "name": "Acquisition",
    "id": 66
  }
]
```

To get the list of the currently available funding types, you should use the following endpoint:

`GET /getFundingTypes`

It takes no parameter, and has the following response codes:

Response code | Meaning
--------- | -----------
200 | Request successful

## Searchable Locations

> To get the list of the searchable locations, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X GET "https://api.netzeroinsights.com/searchLocation/london"
```

> In case of a 200 response, the response body will contain all the matching searchable locations, with the JSON structured like the following:
     
```json
[
  {
    "cityID": 112253,
    "cityName": "London",
    "adminID4": 3113,
    "adminName4": "England",
    "countryID": 225,
    "countryName": "United Kingdom",
    "continentID": 3,
    "continentName": "Europe",
    "id": 928071
  },
  {
    "cityID": 14534,
    "cityName": "London",
    "adminID4": 514,
    "adminName4": "Ontario",
    "countryID": 38,
    "countryName": "Canada",
    "continentID": 4,
    "continentName": "North America",
    "id": 775779
  }
]
```

To get the list of the searchable locations, you should use the following endpoint:

`GET /searchLocation/[location]`

It takes a single parameter, indicated as ”[location]” in the example, which is a string used to filter the locations and has the following response codes:

Response code | Meaning
--------- | -----------
200 | Request successful

# Responses structure

## Startup search

Name | Content
--------- | -----------
results | List of Section [Startup](#startup)
count | Total number of results, regardless of the ”limit” parameter

## Startup

Name | Content
--------- | -----------
id | Internal ID
clientID | Startup ID
name | Name
logo | URL to company’s logo
website | Company website
domain | Company website domain
pitchLine | Pitchline
description | Description fetched from the company website
fundingAmount | Company total funding in EUR
fundingString | Company total funding in EUR, formatted
fundingAmountUSD | Company total funding in USD
fundingStringUSD | Company total funding in USD, formatted
fundingRangeID | Company total funding range ID
fundingRange | Company total funding range
fundingRangeUSD | Company total funding range in USD
fundingRangeIDUSD | Company total funding range ID in USD
lastRoundDate | Date of the last round
foundedDate | Founded date
countryID | Country ID
country | Country name
city | City name
continent | Continent name
email | Company main email
phone | Company main phone
sizeID | Company number of employees range ID
size | Company number of employees range
stageID | Company growth stage ID
stage | Company growth stage
linkedinURL | URL to company LinkedIn
twitterURL | URL to company Twitter
facebookURL | URL to company Facebook
directURL | URL to our company page
sustainabilityMetric | Company climate impact metric
sustainabilityMetricID | Company climate impact metric range ID
lastRoundAmount | Last round amount in EUR
lastRoundAmountUSD | Last round amount in USD
lastRoundAmountString | Last round amount in EUR, formatted
lastRoundAmountStringUSD | Last round amount in USD, formatted
lastRoundType | Last round type
revenueEuro | Total company revenue
revenueYear | Year related to the ”revenueEuro” field
tags | Company tags
fundingTypes | Funding types of any round
sdgs | Sustainable Development Goals
isFundRaising | Company likelihood to fundraise
roundCount | Number of rounds
roundWithDateCount | Number of rounds with a date available
reviewDate | Date of latest company review by our analysts




## Funding round

Name | Content
--------- | -----------
id | Internal funding round ID
clientID | Startup ID
roundDate | Date of the round
roundType | Type of the round
roundAmount | Amount of the round (EUR)
roundAmountUSD | Amount of the round (USD)
roundAmountId | ID of the amount range
coFundingRoundId | Additional internal funding round ID
fundingRange | Amount range
roundInvestors | List of IDs of all the investors of the round
roundNews | List of IDs of all the sources of the round
roundCurrency | Original currency of the round
originalAmount | Round amount in original currency
source | Name of the analyst who inserted the round
financingInstrument | Financing instrument
equityStageID | Equity stage ID, see Section [Equity Stage](#equity-stage)
exitStageID | Exit stage ID, see Section [Exit Stage](#exit-stage)

## Funding round investor

Name | Content
--------- | -----------
id | Internal investor ID
name | Investor name
website | Investor website
fundingRoundId | Funding round ID

## Funding round source

Name | Content
--------- | -----------
id | Internal source ID
url | Source url
fundingRoundId | Funding round ID

## Patent

Name | Content
--------- | -----------
id | Internal patent ID
googlePatentsUrl | Patent url
filingDate | Filing date
publicationDate | Pubblication date
patentAbstract | Patent abstract
title | Patent title
jurisdiction | Country ID where the patent has been filed
jurisdictionName | Name of the country where the patent has been filed
publicationNumber | External patent ID
familyId | Internal patent family ID
clientId | Client ID of the startup
status | Patent status, see Section [Patent Status](#patent-status)

## Investor

Name | Content
--------- | -----------
id | Internal investor ID
name | Investor name
firstRoundDate | Date of the first round of the company in which the in- vestor made an appearance
roundTypes | Types of round in which the investor appeared

## Contact

Name | Content
--------- | -----------
name | Person name
role | Person role
department | Person department
email | Person email
linkedinURL | Person LinkedIn URL
decisionMaker | True if the person has decision making capabilities
id | Internal person ID
