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

For brevity, the possible error codes for all endpoints are at the end of the document.

Each endpoint in this documentation should be called using the appropriate domain for the environment and API version you are integrating with.

| Environment           | Domain                                  | Description                                |
|-----------------------|-----------------------------------------|--------------------------------------------|
| System 1.0 Production | `https://api.netzeroinsights.com`       | Base URL for the legacy System 1.0 API     |
| System 2.0 Production | `https://api-new.netzeroinsights.com`   | Base URL for the System 2.0 production API |
| System 2.0 Stage      | `https://api-stage.netzeroinsights.com` | Base URL for the System 2.0 staging API    |

# Security System 2.0

## Login

> To login, use this code:

```shell
curl -v -X POST 'https://api-new.netzeroinsights.com/auth/login?email={YOUR_EMAIL}&password={YOUR_PASSWORD}' \
-d '' 
```

> Make sure to replace `YOUR_EMAIL` and `YOUR_PASSWORD` with your credentials.
>
> Using the -v ("verbose") flag lets you see the full response, in which you can find the **access_token** in the headers.

System 2.0 APIs use **JWT Bearer Token** authentication instead of session-based authentication.

Before using any other API, you should first login using the following endpoint:

`POST /auth/login?email={YOUR_EMAIL}&password={YOUR_PASSWORD}`

With the following two query parameters:

| Parameter name | Parameter value               |
|----------------|-------------------------------|
| email          | provided by Net Zero Insights |
| password       | provided by Net Zero Insights |

The possible response codes are:

| Response code | Meaning                              |
|---------------|--------------------------------------|
| 200           | Login successful                     |
| 403           | Forbidden, insufficient access level |

Please note that in case of a 200 response, you will also get an **access_token** with an expiration duration of 30 days.
You should save this, as it will be needed for using all the other endpoints.

Our API expects the **access_token** to be included in all API requests to the server by the authorization header, like this:

`Authorization: Bearer EXAMPLE_ACCESS_TOKEN`

<aside class="notice">
You must replace <code>EXAMPLE_ACCESS_TOKEN</code> with your **access_token**.
JWT access tokens expire after a configurable period. When the token expires, authenticate again to obtain a new access token.
</aside>

## Logout

> To logout, use this code:

```shell
curl -v -X POST 'https://api-new.netzeroinsights.com/auth/logout' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN'
```

> Make sure to replace `EXAMPLE_ACCESS_TOKEN` with your **access_token**

To invalidate the access token, you should use the following endpoint:

`GET /auth/logout`

It takes no parameter, and has the following response code:

| Response code | Meaning                              |
|---------------|--------------------------------------|
| 200           | Login successful                     |
| 403           | Forbidden, insufficient access level |


# Startup List System 2.0

> To get startup list, use this code:

```shell
curl -v -X POST 'https://api-new.netzeroinsights.com/advanced-filters/companies?pageNumber=0&pageSize=1' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN'
-H 'Content-Type: application/json' \                 
-d '{"companyInclude": {}, "companyExclude": {}}'
```

> In case of a 200 response, the response body will contain all the startups matching your request, with the format specified at section [Startup Search](#startup-search).

```json
{
  "content": [
    {
      "acquisitionDate": "2023-09-07T08:33:18.797",
      "updatedDate": "2026-07-24T11:18:30.783171",
      "name": "Spiritus",
      "description": "Developer of direct air capture carbon removal process We re a climate tech company at the forefront of DAC technology dedicated to sustainable stewardship of our environment Developer of a Direct Air Capture technology designed to offer a scalable and modular system Spiritus is a climate tech company at the forefront of Direct Air Capture DAC technology Critically Spiritus has developed a particular architecture that mimics the alveoli in the lungs in order to maximize the surface area for carbon dioxide to make contact with the material Developer of a Direct Air Capture technology designed to offer a scalable and modular system The company s system achieves sorption and desorption rates at a fraction of the sorbent cost versus state of the art sorbents under passive DAC conditions enabling clients to experience sustainable stewardship Spiritus Accelerating sustainable stewardship of our climate Spiritus has built a novel approach to direct air carbon capture that relies on a material that absorbs carbon dioxide passively Spiritus is committed to making carbon removal an accessible and practical tool in the global fight against climate change For more information visit Spiritus com Spiritus has built a novel approach to direct air carbon capture that relies on a material that absorbs carbon dioxide passively The company s approach combines the Spiritus Sorbent and the Spiritus Carbon Orchard offering a scalable and modular system for low cost DAC and sequestration DAC S",
      "pitchLine": "Spiritus specializes in direct-air capture (DAC) carbon removal. <br><br>Spiritus offers a novel approach to direct air carbon capture that relies on a material that absorbs carbon dioxide passively. They provide a particular architecture that mimics the alveoli in the lungs to maximize the surface area for carbon dioxide to make contact with the material.<br><br>Opna develops an innovation that contributes to:<br>Climate change mitigation by enabling GHG emissions reduction.",
      "pitchLineNoPunctuation": "spiritus specializes in direct air capture  dac  carbon removal   br  br spiritus offers a novel approach to direct air carbon capture that relies on a material that absorbs carbon dioxide passively  they provide a particular architecture that mimics the alveoli in the lungs to maximize the surface area for carbon dioxide to make contact with the material  br  br opna develops an innovation that contributes to  br climate change mitigation by enabling ghg emissions reduction",
      "website": "https://spiritus.com/en",
      "domain": "spiritus.com",
      "email": "contact@spiritus.com",
      "phone": "+1(800) 952 5210",
      "logoUrl": "https://d1gpx4pnpaaoyd.cloudfront.net/Startups/client_921400.png",
      "foundedYear": 2022,
      "searchableLocation": {
        "continent": {
          "name": "North America",
          "id": 4
        },
        "country": {
          "name": "United States",
          "continent": {
            "name": "North America",
            "id": 4
          },
          "alpha2": "US",
          "id": 226
        },
        "cityName": "White Rock",
        "cityAsciiName": "White Rock",
        "adminID4": 3152,
        "adminName4": "New Mexico",
        "platformOrder": 1060,
        "isSearchable": true,
        "id": 953852
      },
      "linkedinUrl": "https://www.linkedin.com/company/spiritus-cdr",
      "twitterUrl": "https://twitter.com/SpiritusCDR",
      "fundingAmountEUR": 39334712,
      "fundingStringEUR": "39.3M",
      "fundingAmountUSD": 42475000,
      "fundingStringUSD": "42.5M",
      "fundingRangeEUR": {
        "rangeFrom": 25000000,
        "rangeTo": 50000000,
        "rangeTextFormat": "25M - 50M",
        "id": 6
      },
      "fundingRangeUSD": {
        "rangeFrom": 25000000,
        "rangeTo": 50000000,
        "rangeTextFormat": "25M - 50M",
        "id": 6
      },
      "lastDealAmountEUR": 427528,
      "lastDealAmountStringEUR": "428K",
      "lastDealAmountUSD": 500000,
      "lastDealAmountStringUSD": "500K",
      "lastDealType": {
        "label": "Grant",
        "filterable": false,
        "assignable": true,
        "id": 79
      },
      "lastDealDate": "2025-07-09T06:57:00",
      "dealCount": 7,
      "dealWithDateCount": 6,
      "lastEquityDeal": {
        "acquisitionDate": "2025-04-11T06:40:47.64",
        "updatedDate": "2026-06-16T07:49:34.941696",
        "status": "COMPLETED",
        "connectedToInfrastructure": "NO",
        "assetClass": {
          "label": "Venture",
          "id": 1
        },
        "id": 610331
      },
      "lastEquityDealType": {
        "label": "Early VC",
        "id": 76
      },
      "growthStage": {
        "label": "Growth",
        "id": 3
      },
      "financialStage": {
        "label": "Series A & B",
        "id": 3
      },
      "lastReviewer": {
        "name": "Amirhossein",
        "surname": "Mohammadghasemi",
        "email": "amirhossein@netzeroinsights.com",
        "id": 949
      },
      "lastReviewDate": "2023-09-14T09:49:05.333",
      "dealsLastReviewer": {
        "name": "Sharmila",
        "surname": "Bojan",
        "email": "sharmila@netzeroinsights.com",
        "id": 262
      },
      "dealsLastReviewDate": "2025-10-03T10:33:47.557",
      "sizeRange": {
        "rangeTextFormat": "11 - 50",
        "id": 2
      },
      "currentEmployeesCount": 50,
      "yoYEmployeesGrowth": 0.08695652173913043,
      "qoQEmployeesGrowth": 0.0,
      "yoYCorrespondingQuarter": "Q4 2025 vs Q4 2024",
      "qoQCorrespondingQuarter": "Q4 2025 vs Q3 2025",
      "trl": {
        "label": "7-8",
        "description": "Finalizing",
        "referenceYear": 2026,
        "id": 11
      },
      "trlReviewDate": "2025-08-11T11:02:20.867",
      "isChampion": false,
      "isEmerging": true,
      "isNewEntrant": false,
      "isAcquired": false,
      "isCommercialBuyer": false,
      "isCommercialPartner": true,
      "commercialPartnershipCount": 1,
      "commercialBuyCount": 0,
      "commercialAgreementCount": 1,
      "isStrategic": false,
      "isProjectDeveloper": false,
      "trlThreeYearsHorizonPrior": {
        "label": "4-6",
        "description": "Mid stage",
        "id": 10
      },
      "trlThreeYearsPrior": {
        "label": "4-6",
        "description": "Mid stage",
        "id": 10
      },
      "lastCommercialDeal": {
        "title": "Memorandum of Understanding between Aramco and Spiritus",
        "description": "Spiritus has signed a memorandum of understanding with Aramco to establish a framework for strategic collaboration in the direct air capture carbon removal sector. Under the terms of this agreement, the two counterparties intend to explore opportunities to enhance Spiritus' direct air capture technology, initiate potential piloting programs, and execute large-scale deployment of the technology. Additionally, the memorandum outlines mutual efforts to localize Spiritus' supply chain infrastructure within Saudi Arabia, contributing to regional climate initiatives and carbon management goals. The formal signing ceremony was conducted in Riyadh in the presence of the United States Secretary of Energy, Jennifer Granholm, and Saudi Arabia's Energy Minister, Abdulaziz bin Salman Al-Saud. Spiritus' technical approach addresses cost and energy challenges associated with standard carbon removal by reducing power requirements, utilizing passive air collection systems, and deploying a proprietary sorbent material designed to remove carbon from the atmosphere with a tenfold increase in adsorption efficiency.",
        "announcedDate": "2024-05-24T00:00:00",
        "id": 39679
      },
      "totalEquityFundingEUR": 38036605,
      "totalEquityFundingUSD": 41000000,
      "totalNonDilutiveFundingEUR": 1298107,
      "totalNonDilutiveFundingUSD": 1475000,
      "isActive": true,
      "isFundraising": false,
      "webtext": "Where innovation meets sustainability and the future is carbon neutral WE ARE ON A MISSION TO RESHAPE THE WORLD S APPROACH TO CLIMATE CHANGE Spiritus Spiritus stands at the forefront of high quality direct air capture DAC carbon removal bringing to life a groundbreaking solution that captures and sequesters megaton scale CO2 from the atmosphere This is an incredibly hard problem that will require new innovations to bring down cost and accelerate scale With real time monitoring and verification our carbon removal goes beyond estimation it s measurable and provable Scalable DAC on Renewables Our modular design facilitates rapid scale up all while relying on renewable energy sources and existing supply chains to maximum carbon dioxide removal potential Our modular design facilitates rapid scale up all while relying on renewable energy sources and existing supply chains to maximum carbon dioxide removal potential The Carbon Orchard Approach Achieving DAC at high quality and low cost requires a Rubik s Cube solution all key parameters need to be optimized concurrently and complementary to each other In Spiritus we have a combination of a strong approach and team to solve this climate challenge making it our first investment in the DAC area JESSY RIVEST PARTNER AT KHOSLA VENTURES Contact Us Thank you Khosla Ventures has been looking closely at the direct air capture space for years Something went wrong while submitting the form This approach paired with our modular framework enables us to scale quickly to set new standards for sustainability and redefine the DAC landscape Unique Sorbent Process Technology Our novel solid sorbent material drives efficient adsorption and a novel low temperature desorption process capturing carbon dioxide at an unprecedented pace while minimizing energy consumption Measurement Reporting Verification Trust transparency and impact This 30M Series A investment will catalyze the widespread deployment of DAC ensuring that growth does not come at the expense of our environment David Delfassy TDK Ventures Our novel solid sorbent material drives efficient adsorption and a novel low temperature desorption process capturing carbon dioxide at an unprecedented pace while minimizing energy consumption Spiritus represents a unique fusion of cutting edge material science and scalable cost efficient carbon removal making it a key enabler of the world s industrial future In Spiritus we have a combination of a strong approach and team to solve this climate challenge making it our first investment in the DAC area Jessy Rivest Partner at Khosla Ventures Direct Air Capture has the potential to play an important role in decarbonizing hard to abate sectors of the economy but until now it has been too expensive to be meaningful Energy Saving Spiritus has innovated on a novel non TVSA desorption process that cuts energy usage by more than half when compared to current methods Faster Adsorption Rapid sorption and desorption rates at a fraction of the sorbent cost versus state of the art sorbents under passive DAC conditions It s exciting to see Spiritus pioneer new technologies for direct air capture that can drive progress for the field and dramatically expand access to the highest quality carbon dioxide removals Trust transparency and impact Investors Khosla Ventures has been looking closely at the direct air capture space for years Breakthrough approaches like Spiritus are needed Our Approach Our approach integrates a novel sorbent material an innovative process design and a modular approach that promises cost efficient and scalable carbon dioxide removal To prevent the worst harms from climate change we will need to remove gigatons of CO2 from the atmosphere annually Your submission has been received Peter Minor PhD Co Founder of Absolute Climate former Director of Science Innovation at Carbon180 Khosla Ventures has been looking closely at the direct air capture space for years Our innovations in sorbent technology and a low temperature desorption process optimize all major drivers of cost energy input sorbent cost and durability adsorption desorption kinetics and facility capex We are excited to partner with Spiritus and bring this important technology to market Bruce Niven Aramco Ventures We are witnessing a pivotal moment in the journey to decarbonize our economies In Spiritus we have a combination of a strong approach and team to solve this climate challenge making it our first investment in the DAC area JESSY RIVEST PARTNER AT KHOSLA VENTURES ACCELERATING SUSTAINABLE STEWARDSHIP OF OUR CLIMATE Where innovation meets sustainability and the future is carbon neutral This 30M Series A investment will catalyze the widespread deployment of DAC ensuring that growth does not come at the expense of our environment David Delfassy TDK Ventures Why Spiritus",
      "platformOrder": 1,
      "entityTypes": [
        {
          "label": "Company",
          "id": 1
        }
      ],
      "tags": [
        {
          "label": "Business to Business (B2B)",
          "tagType": {
            "label": "Customer Type",
            "id": 125
          },
          "source": "pooneh_amini_naeini",
          "id": 237
        },
        {
          "label": "Hardware",
          "tagType": {
            "label": "buzzword",
            "id": 5
          },
          "source": "pooneh_amini_naeini",
          "id": 240
        }
      ],
      "fundingTypes": [
        {
          "label": "Equity",
          "id": 1
        },
        {
          "label": "Grant",
          "id": 3
        }
      ],
      "numberOfEquityDeals": 4,
      "numberOfDebtDeals": 0,
      "numberOfGrantDeals": 3,
      "id": 117556
    }
  ],
  "pageSize": 1,
  "pageNumber": 0,
  "totalElements": 129877,
  "numberOfElements": 1,
  "totalPages": 129877
}
```

To search our startup database you should use the following endpoint:

`POST /advanced-filters/companies?pageNumber={PAGE_NUMBER}&pageSize={PAGE_SIZE}&sortField={SORT_FIELD}&sortDirection={SORT_DIR}`

With the following optional query parameters:

| Parameter name | Parameter value                                                                 |
|----------------|---------------------------------------------------------------------------------|
| pageNumber     | Zero-based page number to retrieve (by default 0)                               |
| pageSize       | Number of records to return per page (by default 15)                            |
| sortField      | See Section [Company Sort Fields](#company-sort-fields) for the accepted values |
| sortDirection  | ASC or DESC (by default ASC)                                                    |

And a JSON request body in the format specified at the section [Main Filter](#mainfilter).

The possible response codes are:

| Response code | Meaning                              |
|---------------|--------------------------------------|
| 200           | Request successful                   |
| 400           | Bad request, invalid fields          |
| 403           | Forbidden, insufficient access level |

# Filters structure System 2.0

## Company Sort Fields

The following sort fields are supported for the listing endpoints. If no **sortField** is specified as a query parameter, the results are sorted by **PLATFORM_ORDER** by default.

| Name                    | Content                                              |
|-------------------------|------------------------------------------------------|
| NAME                    | Sort by company name                                 |
| WEBSITE                 | Sort by company website                              |
| COUNTRY                 | Sort by the company’s country                        |
| CITY                    | Sort by the company’s city                           |
| FOUNDED_YEAR            | Sort by the company’s founding year                  |
| ACQUISITION_DATE        | Sort by the date of insertion into our database      |
| UPDATED_DATE            | Sort by the date the company was last updated        |
| SIZE                    | Sort by company size                                 |
| GROWTH_STAGE            | Sort by the company’s growth stage                   |
| LAST_DEAL_DATE          | Sort by the date of the company’s most recent deal   |
| LAST_DEAL_TYPE          | Sort by the type of the company’s most recent deal   |
| LAST_DEAL_AMOUNT        | Sort by the amount of the company’s most recent deal |
| TOTAL_FUNDING_AMOUNT    | Sort by the company’s total funding amount           |
| YOY_EMPLOYEE_GROWTH     | Sort by year-over-year employee growth               |
| QOQ_EMPLOYEE_GROWTH     | Sort by quarter-over-quarter employee growth         |
| CURRENT_EMPLOYEES_COUNT | Sort by the current number of employees              |
| TRL                     | Sort by Technology Readiness Level                   |
| PLATFORM_ORDER          | Sort by the default platform order                   |  

## MainFilter

This is the main filter used when searching for startups, investors, or deals.

| Parameter name  | Parameter type                                | Description                                                         |
|-----------------|-----------------------------------------------|---------------------------------------------------------------------|
| companyInclude  | Section [Company Filter](#company-filter)     | Filters related to startups which should be included in the result  |
| companyExclude  | Section [Company Filter](#company-filter)     | Filters related to startups which should be excluded in the result  |
| investorInclude | Section [Investors Filter](#investors-filter) | Filters related to investors which should be included in the result | 
| investorExclude | Section [Investors Filter](#investors-filter) | Filters related to investors which should be excluded in the result |
| dealInclude     | Section [Deals Filter](#deals-filter)         | Filters related to deals which should be included in the result     |
| dealExclude     | Section [Deals Filter](#deals-filter)         | Filters related to deals which should be excluded in the result     |

## Company Filter

| Parameter name               | Parameter type                                      | Description                                                                                     |
|------------------------------|-----------------------------------------------------|-------------------------------------------------------------------------------------------------|
| name                         | string                                              | Startup name                                                                                    |
| domain                       | string                                              | Startup domain                                                                                  |
| searchableLocationIDs        | List of int                                         | See Section [Searchable Locations](#searchable-locations) for the accepted values               |
| financialStageIDs            | List of int                                         | See Section [Financial Stages](#financial-stages) for accepted values                           |
| sizeRangeIDs                 | List of int                                         | See Section [Size Ranges](#size-ranges) for accepted values                                     |
| revenueRangeIDs              | List of int                                         | See Section [Revenue Ranges](#revenue-ranges) for accepted values                               |
| trlIDs                       | List of int                                         | See Section [TRLs](#trls) for accepted values                                                   |
| foundedYearFrom              | int                                                 | Starting founded year                                                                           |
| foundedYearTo                | int                                                 | Maximum founded year                                                                            |
| totalFundingAmountFrom       | int                                                 | Minimum total funding amount                                                                    |
| totalFundingAmountTo         | int                                                 | Maximum total funding amount                                                                    |
| numberOfDealsFrom            | int                                                 | Minimum number of deals done by the company                                                     |
| numberOfDealsTo              | int                                                 | Maximum number of deals done by the company                                                     |
| commercialAgreementCountFrom | int                                                 | Minimum number of commercial agreements                                                         |
| commercialAgreementCountTo   | int                                                 | Maximum number of commercial agreements                                                         |
| employeesCountFrom           | int                                                 | Minimum number of employee count                                                                |
| employeesCountTo             | int                                                 | Maximum number of employee count                                                                |
| acquisitionDateFrom          | date                                                | Starting date for when the startup has been inserted into our database                          |
| acquisitionDateTo            | date                                                | Maximum date for when the startup has been inserted into our database                           |
| employeesGrowthPeriod        | string                                              | Employee growth period (`"Q"` (quarter-over-quarter) or `"Y"` (year-over-year). Default: `"Q"`) |
| employeesGrowthFrom          | int                                                 | Minimum employee growth for the selected period                                                 |
| employeesGrowthTo            | int                                                 | Maximum employee growth for the selected period                                                 |
| tagsConceptsMode             | string                                              | Logical `"AND"` or `"OR"` operators for filtering startups by the given tags. Default: `"AND"`  |
| tagIDs                       | List of int                                         | See Section [Tags](#tags) for accepted values                                                   |
| wildcards                    | List of string                                      | Any match of the keywords in the name/pitchline/description                                     |
| wildcardsFields              | List of Section [Wildcard Fields](#wildcard-fields) | Select on which fields to match the wildcards                                                   |
| regexps                      | List of string                                      | Any match of the keywords in the name/pitchline/description                                     |
| regexpFields                 | List of Section [Regexp Fields](#wildcard-fields)   | Select on which fields to match the regexps                                                     |
| onlyActive                   | boolean                                             | If `"true"`, returns only active startups                                                       |
| viewed                       | boolean                                             | Filters startups based on whether they have been viewed                                         |
| viewedDateFrom               | date                                                | Earliest viewed date                                                                            |
| viewedDateTo                 | date                                                | Latest viewed date                                                                              |
| topViewed                    | boolean                                             | If `"true"`, returns only top viewed startups                                                   |
| hasNotes                     | boolean                                             | If `"true"`, returns only the startups with notes                                               |
| champions                    | boolean                                             | If `"true"`, returns only champion startups                                                     |
| newEntrants                  | boolean                                             | If `"true"`, returns only new entrant startups                                                  |
| emerging                     | boolean                                             | If `"true"`, returns only emerging startups                                                     |
| acquired                     | boolean                                             | If `"true"`, returns only acquired startups                                                     |
| strategic                    | boolean                                             | If `"true"`, returns only strategic startups                                                    |

# Response structures System 2.0

## Company Search

| Name             | Content                                        |
|------------------|------------------------------------------------|
| content          | List of Section Company                        |
| pageSize         | Number of records returned per page            |
| pageNumber       | Zero-based index of the current page           |
| totalElements    | Total number of records matching the query     |
| numberOfElements | Number of records returned in the current page |
| totalPages       | Total number of available pages                |






# Security System 1.0

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

| Parameter name | Parameter value               |
|----------------|-------------------------------|
| username       | provided by Net Zero Insights |
| password       | provided by Net Zero Insights |

The possible response codes are:

| Response code | Meaning          |
|---------------|------------------|
| 200           | Login successful |

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

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Session terminated |

<aside class="notice">
Please note that manually closing a session is not required, since it will be closed bye the server after
30 minutes. This endpoint is mainly used if you need to use different accounts.
</aside>

# Startup List System 1.0

> To get startup list, use this code:

```shell
curl -v --cookie 'JSESSIONID=EXAMPLE_SESSION_ID' \
-X POST 'https://api.netzeroinsights.com/companies' \
-H 'Content-Type: application/json' \                 
-d '{"limit": 1, "offset": 0, "include":{}, "exclude": {}, "fundingRoundInclude":{}, "fundingRoundExclude": {}, "investorInclude":{}, "investorExclude": {}, "sorting": {}}'
```

> In case of a 200 response, the response body will contain all the startups matching your request, with the format specified at section [Startup Search](#startup-search).

```json
{
  "count": 54856,
  "results": [
    {
      "clientID": 668,
      "name": "Sunfire",
      "website": "http://www.sunfire.de"
    }
  ]
}
```

To search our startup database you should use the following endpoint:

`POST /companies`

With a JSON request body in the format specified at the section [Main Filter](#main-filter).

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

# Deals List

> To get the deals list, use this code:

```shell
curl -v -X POST 'https://api-new.netzeroinsights.com/fundingRounds' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN'
-H 'Content-Type: application/json' \                 
-d '{"limit": 1, "offset": 0, "include":{}, "exclude": {}, "fundingRoundInclude":{}, "fundingRoundExclude": {}, "investorInclude":{}, "investorExclude": {}, "sorting": {}}'
```

> In case of a 200 response, the response body will contain all the deals matching your request, with the format specified at section [Deals Search](#deal-search).

```json
{
  "count": 52018,
  "results": [
    {
      "dealID": 425794,
      "clientID": 5051,
      "clientName": "Lightmatter"
    }
  ]
}
```

To search our deals database you should use the following endpoint:

`POST /fundingRounds`

With a JSON request body in the format specified at the section [Main Filter](#main-filter).

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

# Investors List

> To get the investors list, use this code:

```shell
curl -v -X POST 'https://api-new.netzeroinsights.com/investors' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN'
-H 'Content-Type: application/json' \                 
-d '{"limit": 1, "offset": 0, "include":{}, "exclude": {}, "fundingRoundInclude":{}, "fundingRoundExclude": {}, "investorInclude":{}, "investorExclude": {}, "sorting": {}}'
```

> In case of a 200 response, the response body will contain all the investors matching your request, with the format specified at section [Investors Search](#investor-search).

```json
{
  "count": 22736,
  "results": [
    {
      "investorID": 9156,
      "name": "The Carlyle Group",
      "website": "https://www.carlyle.com/"
    }
  ]
}
```

To search our investors database you should use the following endpoint:

`POST /investors`

With a JSON request body in the format specified at the section [Main Filter](#main-filter).

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

# Commercial Deals List

> To get the commercial deals list, use this code:

 ```shell
curl -v -X POST 'https://api-new.netzeroinsights.com/commercial-deals/filter?pageSize=1' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN' \
-H 'Content-Type: application/json' \                 
-d '{"primaryTypeIDs": [1, 7], "pricingFrom": 15000000, "pricingTo": 20000000}'
```

> In case of a 200 response, the response body will contain all the commercial deals matching your request, with the format specified at section [Commercial Deals Filter](#commercial-deals-filter).

```json
{
  "content": [
    {
      "title": "Supply Agreement between Regional Government of Extremadura and Iberdrola",
      "description": "The Regional Government of Extremadura has awarded Iberdrola Clientes a public procurement contract for the supply of electricity to government buildings, public institutions, and educational centres across Extremadura, Spain. The agreement covers electricity delivery across multiple consumption points and includes additional services such as grid access contract management, meter reading representation, consumption monitoring, and energy management tools, with all supplied electricity backed by guarantees of origin certifying renewable or high-efficiency sources. The contract is valued at €19,287,643.02 (excluding VAT) for a two-year period, with an option to extend for one additional year, and applies to distributed supply points across the regional public sector infrastructure in Extremadura.",
      "currency": "EUR",
      "announcedDate": "2026-03-30T00:00:00",
      "duration": 2,
      "pricing": 19287643.02,
      "pricingEUR": 19287643.02,
      "pricingUSD": 22477288.77,
      "news": [],
      "searchableLocations": [
        {
          "continent": {
            "name": "Europe",
            "id": 3
          },
          "country": {
            "name": "Spain",
            "continent": {
              "name": "Europe",
              "id": 3
            },
            "alpha2": "ES",
            "id": 199
          },
          "platformOrder": 10,
          "isSearchable": true,
          "id": 915829
        }
      ],
      "primaryTypes": [
        {
          "label": "Supply Agreement",
          "id": 7
        }
      ],
      "secondaryTypes": [],
      "connectedCompanies": [],
      "connectedInvestors": [
        {
          "name": "Regional Government of Extremadura",
          "logoUrl": "https://d1gpx4pnpaaoyd.cloudfront.net/Startups/New_Empty_Logo_xqsrak.png",
          "investorID": 64106,
          "directUrl": "investor/64106",
          "commercialDealRole": "Buyer",
          "entityTypes": [
            {
              "label": "Government",
              "id": 4
            }
          ],
          "id": 54018
        },
        {
          "name": "Iberdrola",
          "logoUrl": "https://d1gpx4pnpaaoyd.cloudfront.net/Investors/Inv_client_503256.jpg",
          "investorID": 1693,
          "directUrl": "investor/1693",
          "commercialDealRole": "Seller",
          "entityTypes": [
            {
              "label": "Company",
              "id": 1
            }
          ],
          "id": 54019
        }
      ],
      "tags": [],
      "id": 39470
    }
  ],
  "pageSize": 1,
  "pageNumber": 0,
  "totalElements": 111,
  "numberOfElements": 1,
  "totalPages": 111
}
```
To search our commercial deals database, you should use the following endpoint:

`POST /commercial-deals/filter`

With a JSON request body in the format specified at the section [Commercial Deals Filter](#commercial-deals-filter).

The possible response codes are:

| Response code | Meaning                              |
|---------------|--------------------------------------|
| 200           | Request successful                   |
| 400           | Bad Request                          |
| 403           | Forbidden, insufficient access level |
| 404           | Resource not found                   |

# Startup Detail

All the information related to a startup is divided into different sections: 

1. [Overview and Taxonomy](#startup-overview-and-taxonomy)
2. [Patents](#startup-patents)
3. [Investors](#startup-investors)
4. [Contacts](#startup-contacts)
5. [Funding Rounds](#startup-funding-rounds)
6. [Commercial Deals](#startup-commercial-deals)

Additionally, for each funding round, you can get the investors and the sources using the following endpoints:

1. [Investors](#funding-round-investors)
2. [Sources](#funding-round-sources)

## Startup Overview and Taxonomy

> To get a startup overview and taxonomy, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/getStartup/sunfire-668' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN'
```

> In case of a 200 response, the response body will contain the requested startup, with the format specified at section [Startup](#startup).

```json
{
  "clientID": 668,
  "name": "Sunfire",
  "logo": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1695114255/Startups/pwiujiclbklqjftnt16h.jpg",
  "website": "http://www.sunfire.de",
  "domain": "sunfire.de",
  "pitchLine": "Sunfire develops and manufactures industrial electrolysers for the production of renewable hydrogen and syngas.<br><br>The electrolyzers - based on alkaline and solid oxide technologies - are producing hydrogen and Syngas and are meant to decarbonize energy-intensive and climate-conscious businesses. The company either uses renewable electricity and water to produce green hydrogen, or includes captured CO2 in the process to produce renewable syngas which can be transferred into hydrocarbon products. Main applications for the produced fuels are refineries, steel manufacturing, chemicals, mobility, and the utility sector.<br><br>Sunfire develops an innovation that contributes to:<br>Climate change mitigation by producing green hydrogen and renewable syngas.<br>",
  "description": "Sunfire develops and produces high temperature electrolyzers SOEC and high temperature fuel cells SOFC Provider of energy conversion technologies including solid oxide fuel cells and renewable synthetic fuels based on solid oxide electrolyzers The solid oxide cells SOCs used for the conversion process are also used as generators to provide electricity and heat Sunfire has been named Global Cleantech 100 company for six consecutive years and is backed by leading strategic and financial investors such as Neste and SMS Group global leaders in the renewable fuel and steel business Innovative technology Sunfire offers modular power plants and electrolysis systems to produce renewable energy hydrogen and syngas Energy suppliers can work on a more efficient supply at certain points as the fuel cells can also use hydrocarbons Business ModelSunfire offers its technology in the fields of CHP off grid production and hydrogen fuels",
  "fundingAmount": 449000000,
  "fundingString": "449M",
  "fundingAmountUSD": 501968139,
  "fundingStringUSD": "502M",
  "fundingRangeID": 9,
  "fundingRange": ">250M",
  "lastRoundDate": "2023-08-31T06:52:00.000+00:00",
  "acquisitionDate": "2021-05-25T00:00:00.000+00:00",
  "sustainabilityMetric": 0.9335,
  "foundedDate": 2010,
  "georowID": 814818,
  "countryID": 80,
  "country": "Germany",
  "city": "Dresden",
  "continent": "Europe",
  "email": "info@sunfire.de",
  "phone": "+49 351 8967970",
  "sizeID": 5,
  "size": "201 - 500",
  "stageID": 4,
  "stage": "Scaling",
  "linkedinURL": "https://www.linkedin.com/company/sunfire-gmbh/",
  "twitterURL": "https://twitter.com/sunfire_dresden/",
  "facebookURL": "https://facebook.com/sunfire.dresden/",
  "directURL": "sunfire-668",
  "sustainabilityMetricID": 4,
  "lastRoundAmount": 169000000,
  "lastRoundAmountUSD": 184431559,
  "lastRoundAmountString": "169M",
  "lastRoundAmountStringUSD": "184M",
  "lastRoundType": "Grant",
  "revenuesRange": ">500M",
  "tags": [
    {
      "tagTypeId": 11,
      "tagType": {
        "tagType": "environmental objective",
        "platformOrder": 7,
        "tagFamily": {
          "tagFamily": "EU taxonomy",
          "platformOrder": 1,
          "id": 1
        },
        "id": 11
      },
      "filterable": true,
      "id": 374,
      "label": "climate change mitigation"
    },
    {
      "tagTypeId": 74,
      "tagType": {
        "tagType": "EU activity",
        "platformOrder": 9,
        "tagFamily": {
          "tagFamily": "EU taxonomy",
          "platformOrder": 1,
          "id": 1
        },
        "id": 74
      },
      "filterable": true,
      "id": 405,
      "label": "Manufacture of equipment for the production and use of hydrogen"
    }
  ],
  "trls": [
    {
      "date": "2023-12-06T12:36:34.167+00:00",
      "label": "6-8",
      "id": 4
    }
  ],
  "fundingTypes": [
    "Grant",
    "Equity"
  ],
  "sdgs": [
    {
      "id": 7,
      "label": "7. Affordable and clean energy"
    },
    {
      "id": 13,
      "label": "13. Climate action"
    }
  ],
  "piFrameworks": [
    {
      "label": "Adoption",
      "definition": "",
      "id": 2
    },
    {
      "label": "Physical offer",
      "definition": "",
      "id": 4
    }
  ],
  "note": "",
  "roundCount": 11,
  "fundingRangeUSD": ">250M",
  "fundingRangeIDUSD": 9,
  "reviewDate": "2023-09-13T08:23:40.747+00:00",
  "lastReviewer": "pratibha_agarwal",
  "lastSeenDate": "2024-01-12T07:47:14.580+00:00",
  "numberOfEquityRounds": 8,
  "numberOfGrants": 3,
  "sustainabilityMetricLabel": "Very high impact",
  "employeesGrowthJSON": "[\n  {\n    \"dateOn\": {\n      \"month\": 12,\n      \"year\": 2021,\n      \"day\": 1\n    },\n    \"employeeCount\": 152\n  },\n  {\n    \"dateOn\": {\n      \"month\": 1,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 3,\n    \"employeeCount\": 157\n  },\n  {\n    \"dateOn\": {\n      \"month\": 2,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 1,\n    \"employeeCount\": 158\n  },\n  {\n    \"dateOn\": {\n      \"month\": 3,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 4,\n    \"employeeCount\": 164\n  },\n  {\n    \"dateOn\": {\n      \"month\": 4,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 2,\n    \"employeeCount\": 168\n  },\n  {\n    \"dateOn\": {\n      \"month\": 5,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 5,\n    \"employeeCount\": 177\n  },\n  {\n    \"dateOn\": {\n      \"month\": 6,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 5,\n    \"employeeCount\": 186\n  },\n  {\n    \"dateOn\": {\n      \"month\": 7,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 4,\n    \"employeeCount\": 194\n  },\n  {\n    \"dateOn\": {\n      \"month\": 8,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 5,\n    \"employeeCount\": 204\n  },\n  {\n    \"dateOn\": {\n      \"month\": 9,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 6,\n    \"employeeCount\": 216\n  },\n  {\n    \"dateOn\": {\n      \"month\": 10,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 11,\n    \"employeeCount\": 239\n  },\n  {\n    \"dateOn\": {\n      \"month\": 11,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 6,\n    \"employeeCount\": 253\n  },\n  {\n    \"dateOn\": {\n      \"month\": 12,\n      \"year\": 2022,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 3,\n    \"employeeCount\": 261\n  },\n  {\n    \"dateOn\": {\n      \"month\": 1,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 2,\n    \"employeeCount\": 266\n  },\n  {\n    \"dateOn\": {\n      \"month\": 2,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 3,\n    \"employeeCount\": 275\n  },\n  {\n    \"dateOn\": {\n      \"month\": 3,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 4,\n    \"employeeCount\": 285\n  },\n  {\n    \"dateOn\": {\n      \"month\": 4,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 1,\n    \"employeeCount\": 289\n  },\n  {\n    \"dateOn\": {\n      \"month\": 5,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 3,\n    \"employeeCount\": 298\n  },\n  {\n    \"dateOn\": {\n      \"month\": 6,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 4,\n    \"employeeCount\": 311\n  },\n  {\n    \"dateOn\": {\n      \"month\": 7,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 2,\n    \"employeeCount\": 318\n  },\n  {\n    \"dateOn\": {\n      \"month\": 8,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 2,\n    \"employeeCount\": 323\n  },\n  {\n    \"dateOn\": {\n      \"month\": 9,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 4,\n    \"employeeCount\": 336\n  },\n  {\n    \"dateOn\": {\n      \"month\": 10,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 5,\n    \"employeeCount\": 354\n  },\n  {\n    \"dateOn\": {\n      \"month\": 11,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 1,\n    \"employeeCount\": 359\n  },\n  {\n    \"dateOn\": {\n      \"month\": 12,\n      \"year\": 2023,\n      \"day\": 1\n    },\n    \"monthlyPercentageDifference\": 0,\n    \"employeeCount\": 359\n  }\n]",
  "currentEmployeesCount": 431,
  "active": true,
  "id": 527,
  "eutopiaScore": 93
}
```

To get a startup overview and taxonomy you should use the following endpoint:

`GET /getStartup/[clientID]`

It takes a single parameter, indicated as ”[clientID]” in the example, which is taken from a previous call of the endpoint at [Startup List](#startup-list), variable ”clientID”, and has the following response codes:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Startup Patents

> To get a startup overview and taxonomy, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/patents/668'
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN'
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

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Startup Investors

> To get all the investors of a startup, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/investors/668'
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN'
```

> In case of a 200 response, the response body will contain the requested investors, with the format specified at section [Investor](#investor-core).

```json
[
  {
    "id": 13333,
    "name": "Amazon Climate Pledge Fund",
    "firstRoundDate": "Jul 2022",
    "roundTypes": "Late VC"
  },
  {
    "id": 19364,
    "name": "IPCEI",
    "firstRoundDate": "Jun 2022",
    "roundTypes": "Grant"
  }
]
```

To get all the investors of a startup, you should use the following endpoint:

`GET /investors/[clientID]`

It takes a single parameter, indicated as ”[clientID]” in the example, which is taken from a previous call of the endpoint at [Startup List](#startup-list), variable ”clientID”, and has the following response codes:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Startup Contacts

> To get all the contacts of a startup, use this code:

```shell
curl -v -X POST 'https://api-new.netzeroinsights.com/contacts/company' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN' \
-H "Content-Type: application/json" \
-d "{'clientID': 668, 'decisionMaker': false, 'roleID': 5}"
```

> In case of a 200 response, the response body will contain all the requested contacts, with the format specified at section [Contact](#contact).

```json
[
  {
    "name": "Hergen Wolf",
    "role": "Director Product Management",
    "department": "Tech",
    "email": "hergenthore.wolf@sunfire.de",
    "linkedinURL": "http://www.linkedin.com/in/hergen-wolf",
    "decisionMaker": true,
    "id": 1170662
  },
  {
    "name": "David Hering",
    "role": "Head Of Production",
    "department": "Tech",
    "email": "david.hering@sunfire.de",
    "linkedinURL": "http://www.linkedin.com/in/david-hering-07a169247",
    "decisionMaker": true,
    "id": 1170669
  }
]
```

To get all contacts of a startup, you should use the following endpoint:

`POST /contacts/company`

With a JSON request body in the format specified at the Section [Contacts Filter](#contacts-filter), and has the following response codes:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Startup Funding rounds

> To get all the funding rounds of a startup, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/fundingRoundsPrints/668' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN'
```

> In case of a 200 response, the response body will contain the requested funding rounds, with the format specified at section [Funding Round](#funding-round).

```json
[
  {
    "clientId": 668,
    "roundDate": "2022-07-14T00:00:00.000+00:00",
    "roundType": "Late VC",
    "roundAmount": 0.0,
    "coFundingRoundId": 138720,
    "roundInvestors": [
      13333
    ],
    "roundNews": [
      58824,
      58825,
      58826
    ],
    "source": "pratik_gohil",
    "financingInstrument": "Equity",
    "equityStageID": 4,
    "exitStageID": 1,
    "id": 143791
  },
  {
    "clientId": 668,
    "roundDate": "2022-07-01T00:00:00.000+00:00",
    "roundType": "Grant",
    "roundAmount": 0.0,
    "coFundingRoundId": 177701,
    "roundInvestors": [
      19364
    ],
    "roundNews": [
      72998
    ],
    "source": "sharmila_bojan",
    "financingInstrument": "Grant",
    "equityStageID": 5,
    "exitStageID": 1,
    "id": 154414
  }
]
```

To get all the funding rounds of a startup, you should use the following endpoint:

`GET /fundingRoundsPrints/[clientID]`

It takes a single parameter, indicated as ”[clientID]” in the example, which is taken from a previous call of the endpoint at [Startup List](#startup-list), variable ”clientID”, and has the following response codes:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Funding round investors

> To get all the investors of a given set of funding rounds, use this code:

```shell
curl -v -X POST 'https://api-new.netzeroinsights.com/getFundingRoundInvestors' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN' \
-H "Content-Type: application/json" \
-d "{[86971]}"
```

> In case of a 200 response, the response body will contain all the investors of the requested funding rounds, with the format specified at section [Funding Round Investor](#funding-round-investor).

```json
[
  {
    "id": 10140,
    "name": "Blue Earth Capital",
    "website": "https://blueearth.capital/",
    "fundingRoundId": 86971
  },
  {
    "id": 3222,
    "name": "Carbon Direct Capital Management",
    "website": "https://carbon-direct.com/",
    "fundingRoundId": 86971
  },
  {
    "id": 6970,
    "name": "Copenhagen Infrastructure Partners",
    "website": "https://cipartners.dk/",
    "fundingRoundId": 86971
  }
]
```

To get all the investors of a given set of funding rounds, you should use the following endpoint:

`POST /getFundingRoundInvestors`

The request body should be a list of round IDs, which you can get from previous calls of [Startup Funding Rounds](#startup-funding-rounds), variable ”coFundingRoundId”, and has the following response codes:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Funding round sources

> To get all the sources of a specific funding round, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/roundNewsByRoundID/86971' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN'
```

> In case of a 200 response, the response body will contain all the sources of a funding rounds, with the format specified at section [Funding round source](#funding-round-source).

```json
[
  {
    "id": 50021,
    "url": "https://www.sunfire.de/en/news/detail/sunfire-secures-further-growth-capital-and-an-agreement-for-up-to-640-mw-electrolysis-offtake",
    "fundingRoundId": 86971
  },
  {
    "id": 39628,
    "url": "https://tech.eu/2022/03/24/sunfire-gets-eur195-million-backing-to-support-european-energy-independence",
    "fundingRoundId": 86971
  },
  {
    "id": 39629,
    "url": "https://renewablesnow.com/news/sunfire-raises-eur-86m-to-scale-electrolysers-production-778402/",
    "fundingRoundId": 86971
  }
]
```

To get all the sources of a funding round, you should use the following endpoint:

`GET /roundNewsByRoundID/[coFundingRoundId]`

It takes a single parameter, indicated as ”[coFundingRoundId]” in the example, which is taken from a previous call of the endpoint at Section [Startup Funding Rounds](#startup-funding-rounds), variable ”coFundingRoundId”, and has the following response codes:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Startup Commercial Deals

> To get all the commercial deals of a startup, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/commercial-deals/connected-entities/company/37090' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN'
```

> In case of a 200 response, the response body will contain the requested commercial deals, with the format specified at section [Commercial Deal](#commercial-deal).

```json
[
  {
    "title": "Strategic Partnership between Groupe Sorégies and Ze Energy",
    "description": "ZE Energy and Groupe Sorégies have partnered to equip the Senillé-Saint-Sauveur solar park in Vienne, France, with a battery storage system, making it the first of its kind in continental France. This innovation, supported by the Nouvelle-Aquitaine region, addresses the challenge of solar energy intermittency by storing energy for use when needed, even when the sun isn't shining. ZE Energy's economic model enables the efficient integration and valorization of solar energy into the grid, optimizing its cost-effectiveness and environmental benefits. This collaboration, which includes a successful bid for a long-term RTE tender, involved a two-month installation process with technology partners Entech and Emerson. The project is expected to improve grid stability, enhance the value of solar energy, and pave the way for similar initiatives in France and internationally.",
    "announcedDate": "2020-10-08T00:00:00",
    "news": [
      {
        "url": "https://ze-energy.com/admin/wp-content/uploads/2021/04/5f7f33137ff6c9b97667c6f8-cpzeenergysaintsauveurvdef.pdf",
        "title": "The sorégies group and the startup ze energy inaugurate the first photovoltaic park equipped with a storage battery",
        "newsDate": "2020-10-08T00:00:00",
        "id": 56979
      },
      {
        "url": "https://ze-energy.com/admin/wp-content/uploads/2021/04/5f7f33137ff6c9b97667c6f8-cpzeenergysaintsauveurvdef.pdf",
        "title": "The sorégies group and the startup ze energy inaugurate the first photovoltaic park equipped with a storage battery",
        "newsDate": "2020-10-08T00:00:00",
        "id": 74682
      }
    ],
    "searchableLocations": [
      {
        "continent": {
          "name": "Europe",
          "id": 3
        },
        "country": {
          "name": "France",
          "continent": {
            "name": "Europe",
            "id": 3
          },
          "alpha2": "FR",
          "id": 73
        },
        "platformOrder": 10,
        "isSearchable": true,
        "id": 806702
      }
    ],
    "primaryTypes": [
      {
        "label": "Strategic Partnership",
        "id": 1
      }
    ],
    "secondaryTypes": [],
    "connectedCompanies": [
      {
        "name": "Ze Energy",
        "logoUrl": "https://d1gpx4pnpaaoyd.cloudfront.net/Startups/client_1789635.png",
        "companyID": 37090,
        "directUrl": "organization/37090",
        "commercialDealRole": "Partner",
        "entityTypes": [
          {
            "label": "Company",
            "id": 1
          }
        ],
        "id": 33385
      }
    ],
    "connectedInvestors": [
      {
        "name": "Groupe Sorégies",
        "logoUrl": "https://d1gpx4pnpaaoyd.cloudfront.net/Investors/Inv_client_509704.jpg",
        "investorID": 12271,
        "directUrl": "investor/12271",
        "commercialDealRole": "Partner",
        "entityTypes": [
          {
            "label": "Company",
            "id": 1
          }
        ],
        "id": 26248
      }
    ],
    "id": 1257
  }
]
```

To get all the commercial deals of a startup, you should use the following endpoint:

`GET /connected-entities/company/{companyID}`

It takes a single parameter, indicated as “companyID” in the example, which is taken from a previous call of the endpoint at [Startup List](#startup-list), variable “id”, and has the following response codes:

| Response code | Meaning                              |
|---------------|--------------------------------------|
| 200           | Request successful                   |
| 403           | Forbidden, insufficient access level |

# Deal Detail

> To get the details of a Deal, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/fundingRound/42643' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN'
```

> In case of a 200 response, the response body will contain the requested deal, with the format specified at section [Deal](#deal).

```json
{
  "clientId": 45891,
  "clientName": "Ecohelix",
  "clientLogoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1704479512/Startups/p2epr8fhratvldckqbxv.jpg",
  "clientPitchLine": "Manufacturer of amphiphilic polymers intended for packaging, construction, and cosmetics sectors.",
  "clientHQ": "Sweden",
  "clientCityHQ": "Stockholm",
  "clientCountryCode": "SE",
  "clientCountryID": 205,
  "clientContinentID": 3,
  "clientFoundedDate": "2014",
  "roundDate": "2021-05-13T00:00:00.000+00:00",
  "roundType": "Seed",
  "roundAmount": 1972593.0,
  "roundAmountUSD": 2395397.0,
  "roundAmountString": "1.97M",
  "roundAmountStringUSD": "2.4M",
  "roundAmountRangeID": 3,
  "roundAmountRangeIDUSD": 3,
  "roundInvestorIDs": [
    136,
    1811,
    3686,
    14896
  ],
  "roundInvestors": [
    {
      "id": 136,
      "name": "Molindo Energy",
      "website": "https://www.molindo.se/",
      "fundingRoundId": 42643,
      "logoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1687952923/Investors/orwa0yiqmkjkcdvgo9ec.jpg",
      "investorSince": "2021-05-13T00:00:00.000+00:00"
    },
    {
      "id": 1811,
      "name": "European Innovation Council Fund",
      "website": "https://eic.ec.europa.eu/select-language?destination=/node/1",
      "fundingRoundId": 42643,
      "logoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1687345554/Investors/vsvgdeqplej2qwt6vhxe.jpg",
      "investorSince": "2007-01-01T00:00:00.000+00:00"
    },
    {
      "id": 3686,
      "name": "Lärarnas Riksförbunds Studerandeförening",
      "website": "http://ww.lr.se/lrstud",
      "fundingRoundId": 42643,
      "logoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1705075824/Investors/ifig49nujrf75l2cy5ow.jpg",
      "investorSince": "2018-12-14T00:00:00.000+00:00"
    },
    {
      "id": 14896,
      "name": "Almi",
      "website": "https://www.almi.se/",
      "fundingRoundId": 42643,
      "logoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1690947644/Investors/mhqlfur7jtx2frmxwln6.png",
      "investorSince": "2009-01-01T00:00:00.000+00:00"
    }
  ],
  "roundNews": [
    {
      "id": 1654,
      "url": "https://nordic9.com/news/ecohelix-announced-raising-sek-20-million/",
      "title": "Ecohelix announced raising SEK 20 million. | Nordic 9",
      "coFundingRoundID": 42643
    },
    {
      "id": 47334,
      "url": "https://www.breakit.se/artikel/28902/ecohelix-ska-gora-din-plast-mindre-dum-mot-miljon-plockar-in-20-miljoner",
      "coFundingRoundID": 42643
    }
  ],
  "roundCurrency": "SEK",
  "originalRoundAmount": 2.0E7,
  "numberOfRounds": 4,
  "totalFunding": 8172438.0,
  "totalFundingUSD": 8984881.0,
  "totalFundingString": "8.17M",
  "totalFundingStringUSD": "8.98M",
  "roundNumber": 2,
  "financingInstrument": "Equity",
  "lastRound": false,
  "sizeID": 2,
  "size": "11 - 50",
  "trlID": 4,
  "trl": "6-8",
  "status": "COMPLETED",
  "equityStageID": 2,
  "exitStageID": 1,
  "id": 42643
}
```

To get the deal information, you should use the following endpoint:

`GET /fundingRound/[fundingRoundID]`

It takes a single parameter, indicated as ”[fundingRoundID]” in the example, and has the following response codes:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |


# Investor Detail

> To get the details of an Investor, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/getInvestor/10000' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN'
```

> In case of a 200 response, the response body will contain the requested investor, with the format specified at section [Investor](#investor).

```json
{
  "investorID": 10000,
  "name": "Intergen",
  "description": "InterGen is a private ScaleUp fund and talent matching program based in Calgary, Canada.<br><br>The company was founded in 2018 with a belief that the talent and expertise responsible for making Alberta the economic envy of the entire continent for the last twenty years can be leveraged to build the companies that will define the next twenty years - and beyond. InterGen only invests in companies and CEOs that meet the criteria of having revenue of approximately $1M-$5M per year, with rare exceptions below $1M. The firm prefers to invest in seed-stage, early-stage, and later-stage companies in information technology, SaaS, TMT, oil, and gas sectors in Alberta. InterGen offers educational programming, events, and networking opportunities to help businesses learn as they grow. The company has a strong network of retired and transitioning executives looking to engage with innovative companies emerging from start-up to scale-up.",
  "website": "https://intergenconnect.com",
  "city": "Calgary",
  "country": "Canada",
  "continent": "North America",
  "linkedInURL": "https://www.linkedin.com/company/intergencanada/",
  "twitterURL": "https://twitter.com/intergenscaleup/",
  "email": "marcy@intergenconnect.com",
  "logoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1692058153/Investors/q3r0z1bzarioblbxnjmn.jpg",
  "size": "1 - 10",
  "sizeID": 1,
  "foundedDate": 2018,
  "numberOfDeals": 1,
  "numberOfDealsFiltered": 1,
  "lastDealType": "Late VC",
  "lastDealDate": "2018-12-14T00:00:00.000+00:00",
  "lastRoundAmount": 3294864,
  "lastRoundAmountUSD": 3750000,
  "note": "",
  "primaryTypeID": 10,
  "primaryType": "Venture Capital",
  "secondaryTypes": [],
  "investments": [
    {
      "id": 16936,
      "clientID": 31143,
      "url": "osperity-31143",
      "logoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1680109363/Startups/ihumccybullkimhjsinh.jpg",
      "name": "Osperity",
      "pitchline": "Osperity develops a cloud-based platform designed to offer intelligent visual monitoring services.<br><br>Osperity is a leading provider of AI-driven intelligent visual monitoring and alerting solutions for industrial operations. Their platform offers customizable exception-based management, remote site inspections, automated asset monitoring, and seamless integration with industrial sensors and systems, delivering business cost savings, risk mitigation, and operational efficiency.<br><br>Osperity develops an innovation that contributes to:<br>Climate change mitigation by providing a platform that offers visual monitoring services.",
      "country": "Canada",
      "totalFunding": 6283832,
      "totalFundingUSD": 7200000,
      "lastRoundType": "Late VC",
      "lastRoundAmount": 3294864,
      "lastRoundAmountUSD": 3750000,
      "lastRoundDate": "2018-12-14",
      "investorSince": "2018-12-14T00:00:00.000+00:00"
    }
  ],
  "coInvestors": [
    {
      "id": 16495,
      "investorID": 6998,
      "name": "Evok Innovations",
      "logoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1692355453/Investors/eek442rreqwc5qnaqtyw.jpg",
      "investorType": "Venture Capital",
      "country": "United States",
      "numberOfCoInvestments": 1
    },
    {
      "id": 5573,
      "investorID": 15357,
      "name": "Shell",
      "logoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1691834266/Investors/ov8ccgpalypyqaofecwl.jpg",
      "country": "United Kingdom",
      "numberOfCoInvestments": 1
    }
  ]
}
```

To get the investor information, you should use the following endpoint:

`GET /getInvestor/[investorID]`

It takes a single parameter, indicated as ”[investorID]” in the example, and has the following response codes:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Investor Commercial Deals

> To get all the commercial deals of an investor, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/commercial-deals/connected-entities/investor/43939' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN'
```

> In case of a 200 response, the response body will contain the requested commercial deals, with the format specified at section [Commercial Deal](#commercial-deal).

```json
[
  {
    "title": "Supply Agreement between Evlox and Recover",
    "description": "In April 2023, Evlox, a prominent denim fabric manufacturer, entered into a three-year partnership with Recover™, a producer of recycled cotton fiber. This agreement commits Evlox to integrating Recover's sustainably produced, high-quality recycled cotton fiber—derived entirely from textile waste—into their denim fabrics. The collaboration aims to advance Evlox's sustainability objectives, particularly those outlined in their 2025 corporate social responsibility program, by reducing reliance on virgin materials and promoting a circular production model. As part of this initiative, Evlox plans to launch \"Re-Iconics by Evlox,\" a capsule collection that pays homage to classic denim styles while incorporating Recover's recycled fiber, thereby significantly minimizing environmental impact.",
    "announcedDate": "2023-04-14T00:00:00",
    "startYear": 2023,
    "endYear": 2026,
    "duration": 3,
    "news": [
      {
        "url": "https://recoverfiber.com/newsroom/evlox-signs-three-year-deal-with-recover",
        "title": "Evlox signs three-year deal with Recover™",
        "newsDate": "2023-04-14T00:00:00",
        "id": 74634
      },
      {
        "url": "https://www.businesswire.com/news/home/20230418005189/en/Evlox-Signs-a-Three-year-Agreement-to-Incorporate-Recover%E2%84%A2-Recycled-Cotton-Fiber-in-Their-Denim-Production",
        "title": "Evlox Signs a Three-year Agreement to Incorporate Recover™ Recycled Cotton Fiber in Their Denim Production\r\n ",
        "newsDate": "2023-04-18T00:00:00",
        "id": 74635
      }
    ],
    "searchableLocations": [
      {
        "continent": {
          "name": "Europe",
          "id": 3
        },
        "country": {
          "name": "Spain",
          "continent": {
            "name": "Europe",
            "id": 3
          },
          "alpha2": "ES",
          "id": 199
        },
        "platformOrder": 10,
        "isSearchable": true,
        "id": 915829
      }
    ],
    "primaryTypes": [
      {
        "label": "Supply Agreement",
        "id": 7
      }
    ],
    "secondaryTypes": [
      {
        "label": "Sustainability Partnership",
        "id": 13
      }
    ],
    "connectedCompanies": [
      {
        "name": "Recover",
        "logoUrl": "https://d1gpx4pnpaaoyd.cloudfront.net/Startups/matpkxj4ergscseibcro.png",
        "companyID": 75094,
        "directUrl": "organization/75094",
        "commercialDealRole": "Seller",
        "entityTypes": [
          {
            "label": "Company",
            "id": 1
          }
        ],
        "id": 33352
      }
    ],
    "connectedInvestors": [
      {
        "name": "Evlox",
        "logoUrl": "https://d1gpx4pnpaaoyd.cloudfront.net/Investors/Inv_client_514764.jpg",
        "investorID": 43939,
        "directUrl": "investor/43939",
        "commercialDealRole": "Buyer",
        "entityTypes": [
          {
            "label": "Investor",
            "id": 2
          }
        ],
        "id": 26227
      }
    ],
    "id": 1231
  }
]
```

To get all the commercial deals of an investor, you should use the following endpoint:

`GET /connected-entities/investor/{investorID}`

It takes a single parameter, indicated as “investorID” in the example, which is taken from a previous call of the endpoint at [Investors List](#investors-list), variable “investorID”, and has the following response codes:

| Response code | Meaning                              |
|---------------|--------------------------------------|
| 200           | Request successful                   |
| 403           | Forbidden, insufficient access level |

## Investor Contacts

> To get all the contacts of an investor, use this code:

```shell
curl -v -X POST 'https://api-new.netzeroinsights.com/contacts/investor' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN' \
-H "Content-Type: application/json" \
-d "{'investorID': 16328, 'decisionMaker': false}"
```

> In case of a 200 response, the response body will contain all the requested contacts, with the format specified at section [Investor Contact](#investor-contact).

```json
[
  {
    "name": "Lewis Liu",
    "role": "Venture Partner",
    "linkedinURL": "http://www.linkedin.com/in/lewisliu",
    "decisionMaker": true,
    "id": 2317638
  },
  {
    "name": "Arielle Schacter",
    "role": "Investor",
    "linkedinURL": "http://www.linkedin.com/in/arielle-schacter-26b8192b",
    "decisionMaker": false,
    "id": 2317639
  },
  {
    "name": "Monika Burniston",
    "role": "Executive Assistant",
    "linkedinURL": "http://www.linkedin.com/in/monika-burniston-83702840",
    "decisionMaker": false,
    "id": 2317640
  }
]
```

To get all contacts of an investor, you should use the following endpoint:

`POST /contacts/investor`

With a JSON request body in the format specified at the Section [Investor Contacts Filter](#investor-contacts-filter), and has the following response codes:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

# Commercial Deal Details

> To get the details of a commercial deal, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/commercial-deals/1230' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN'
```

> In case of a 200 response, the response body will contain the requested commercial deal, with the format specified at section [Commercial Deal](#commercial-deal).

```json
{
  "title": "Offtake Agreement between Orange and Ze Energy",
  "description": "Orange and ZE Energy have signed a 15-year corporate power purchase agreement (CPPA) for 90 GWh of solar energy annually. This agreement involves a hybrid solar park under construction in Vert, Landes, France, which combines a 77 MW solar park with a 15 MW/34 MWh battery storage system. This setup allows ZE Energy to provide Orange with stable, competitive renewable energy throughout the day, mitigating the intermittency of solar power. The project, a first in France, is expected to be operational in 2025 and achieve a competitive electricity price by leveraging grid connection savings to finance the battery system. This \"hybrid\" model is anticipated to gain traction as solar energy expands and influences electricity prices.",
  "volume": "90 GWh of solar energy annually",
  "announcedDate": "2024-05-14T00:00:00",
  "startYear": 2026,
  "endYear": 2041,
  "duration": 15.00,
  "news": [
    {
      "url": "https://in.marketscreener.com/quote/stock/ORANGE-4649/news/Orange-solar-power-purchase-agreement-with-ZE-Energy-46716737/",
      "title": "Orange: solar power purchase agreement with ZE Energy",
      "newsDate": "2024-05-14T00:00:00",
      "id": 74632
    },
    {
      "url": "https://web.archive.org/web/20240516091840/https://www.lesechos.fr/industrie-services/energie-environnement/electricite-comment-orange-contourne-les-montagnes-russes-du-solaire-2095140",
      "title": "Electricity: how Orange is avoiding the solar roller coaster",
      "newsDate": "2024-05-16T00:00:00",
      "id": 74633
    }
  ],
  "searchableLocations": [
    {
      "continent": {
        "name": "Europe",
        "id": 3
      },
      "country": {
        "name": "France",
        "continent": {
          "name": "Europe",
          "id": 3
        },
        "alpha2": "FR",
        "id": 73
      },
      "platformOrder": 10,
      "isSearchable": true,
      "id": 806702
    }
  ],
  "primaryTypes": [
    {
      "label": "Offtake Agreement",
      "id": 6
    }
  ],
  "secondaryTypes": [],
  "connectedCompanies": [
    {
      "name": "Ze Energy",
      "logoUrl": "https://d1gpx4pnpaaoyd.cloudfront.net/Startups/client_1789635.png",
      "companyID": 37090,
      "directUrl": "organization/37090",
      "commercialDealRole": "Seller",
      "entityTypes": [
        {
          "label": "Company",
          "id": 1
        }
      ],
      "id": 33351
    }
  ],
  "connectedInvestors": [
    {
      "name": "Orange",
      "logoUrl": "https://d1gpx4pnpaaoyd.cloudfront.net/Investors/Inv_client_514709.png",
      "investorID": 43829,
      "directUrl": "investor/43829",
      "commercialDealRole": "Buyer",
      "entityTypes": [
        {
          "label": "Company",
          "id": 1
        }
      ],
      "id": 26226
    }
  ],
  "id": 1230
}
```

To get the commercial deal information, you should use the following endpoint:

`GET /commercial-deals/{commercialDealID}`

It takes a single parameter, indicated as “commercialDealID” in the example, and has the following response codes:

| Response code | Meaning                              |
|---------------|--------------------------------------|
| 200           | Request successful                   |
| 403           | Forbidden, insufficient access level |
| 404           | Resource not found                   |

## Connected Entities

> To get all the connected entities of a commercial deal, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/commercial-deals/connected-entities/1230/2' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN'
```

```json
{
  "connectedInvestors": [],
  "connectedCompanies": [
    {
      "name": "Ze Energy",
      "logoUrl": "https://d1gpx4pnpaaoyd.cloudfront.net/Startups/client_1789635.png",
      "companyID": 37090,
      "directUrl": "organization/37090",
      "commercialDealRole": "Seller",
      "entityTypes": [
        {
          "label": "Company",
          "id": 1
        }
      ],
      "id": 33351
    }
  ]
}
```

To get the connected entities of a commercial deal, you should use the following endpoint:

`GET /commercial-deals/connected-entities/{commercialDealID}/{commercialDealRoleID}`

It takes two parameters, indicated as “commercialDealID” and “commercialDealRoleID” in the example, and has the following response codes:

| Response code | Meaning                              |
|---------------|--------------------------------------|
| 200           | Request successful                   |
| 403           | Forbidden, insufficient access level |

## Tags

> To get all the tags of connected entities of a commercial deal, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/commercial-deals/connected-entities/taxonomy/1230' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN'
```

```json
[
  {
    "label": "Battery",
    "visibilityStatus": {
      "visibleTo": "ALL",
      "id": 1
    },
    "description": "Battery refers to energy storage technologies that store electrical energy for later use. Battery solutions play a crucial role in enabling energy storage, and management of renewable energy storage and electric vehicles. This solution covers a wide range of aspects within the battery industry, including battery and battery component manufacturers, battery management systems, and solutions for the end-of-life stage of batteries.",
    "isCustomCompany": false,
    "isCustomMap": false,
    "isUmbrella": false,
    "isVisibleCompany": true,
    "isVisibleMap": true,
    "isSearchable": true,
    "isGrouping": false,
    "isAdvancedFilters": true,
    "tagType": {
      "label": "technology",
      "platformOrder": 3,
      "tagFamily": {
        "label": "Solutions",
        "platformOrder": 1,
        "id": 2
      },
      "id": 3
    },
    "synonyms": [],
    "rawSearches": [
      {
        "acquisitionDate": "2024-04-04T17:03:20.177",
        "text": "{\"companyInclude\":{\"tagIDs\":[191]},\"companyExclude\":{},\"investorInclude\":{},\"investorExclude\":{},\"dealInclude\":{},\"dealExclude\":{},\"forScheduledSavedSearchEmail\":false,\"sortDirection\":\"ASC\",\"dealSortDirection\":\"DESC\",\"companySortField\":\"PLATFORM_ORDER\",\"investorSortField\":\"PLATFORM_ORDER\",\"dealSortField\":\"DEAL_DATE\"}",
        "strong": false,
        "id": 9162
      }
    ],
    "platformOrder": 160,
    "id": 191
  }
]
```

To get the tags of connected entities of a commercial deal, you should use the following endpoint:

`GET /commercial-deals/connected-entities/taxonomy/{commercialDealID}`

It takes a single parameter, indicated as “commercialDealID” in the example, and has the following response codes:

| Response code | Meaning                              |
|---------------|--------------------------------------|
| 200           | Request successful                   |
| 403           | Forbidden, insufficient access level |


## Mappings

> To get all the commercial deal mappings, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/commercial-deals/mappings/1230' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN'
```

```json
[
  {
    "title": "Supply Agreement between Evlox and Recover",
    "description": "In April 2023, Evlox, a prominent denim fabric manufacturer, entered into a three-year partnership with Recover™, a producer of recycled cotton fiber. This agreement commits Evlox to integrating Recover's sustainably produced, high-quality recycled cotton fiber—derived entirely from textile waste—into their denim fabrics. The collaboration aims to advance Evlox's sustainability objectives, particularly those outlined in their 2025 corporate social responsibility program, by reducing reliance on virgin materials and promoting a circular production model. As part of this initiative, Evlox plans to launch \"Re-Iconics by Evlox,\" a capsule collection that pays homage to classic denim styles while incorporating Recover's recycled fiber, thereby significantly minimizing environmental impact.",
    "announcedDate": "2023-04-14T00:00:00",
    "startYear": 2023,
    "endYear": 2026,
    "duration": 3,
    "news": [
      {
        "url": "https://recoverfiber.com/newsroom/evlox-signs-three-year-deal-with-recover",
        "title": "Evlox signs three-year deal with Recover™",
        "newsDate": "2023-04-14T00:00:00",
        "id": 74634
      },
      {
        "url": "https://www.businesswire.com/news/home/20230418005189/en/Evlox-Signs-a-Three-year-Agreement-to-Incorporate-Recover%E2%84%A2-Recycled-Cotton-Fiber-in-Their-Denim-Production",
        "title": "Evlox Signs a Three-year Agreement to Incorporate Recover™ Recycled Cotton Fiber in Their Denim Production\r\n ",
        "newsDate": "2023-04-18T00:00:00",
        "id": 74635
      }
    ],
    "searchableLocations": [
      {
        "continent": {
          "name": "Europe",
          "id": 3
        },
        "country": {
          "name": "Spain",
          "continent": {
            "name": "Europe",
            "id": 3
          },
          "alpha2": "ES",
          "id": 199
        },
        "platformOrder": 10,
        "isSearchable": true,
        "id": 915829
      }
    ],
    "primaryTypes": [
      {
        "label": "Supply Agreement",
        "id": 7
      }
    ],
    "secondaryTypes": [
      {
        "label": "Sustainability Partnership",
        "id": 13
      }
    ],
    "connectedCompanies": [
      {
        "name": "Recover",
        "logoUrl": "https://d1gpx4pnpaaoyd.cloudfront.net/Startups/matpkxj4ergscseibcro.png",
        "companyID": 75094,
        "directUrl": "organization/75094",
        "commercialDealRole": "Seller",
        "entityTypes": [
          {
            "label": "Company",
            "id": 1
          }
        ],
        "id": 33352
      }
    ],
    "connectedInvestors": [
      {
        "name": "Evlox",
        "logoUrl": "https://d1gpx4pnpaaoyd.cloudfront.net/Investors/Inv_client_514764.jpg",
        "investorID": 43939,
        "directUrl": "investor/43939",
        "commercialDealRole": "Buyer",
        "entityTypes": [
          {
            "label": "Investor",
            "id": 2
          }
        ],
        "id": 26227
      }
    ],
    "id": 1231
  }
]
```

To get the mappings of a commercial deal, you should use the following endpoint:

`GET /commercial-deals/mappings/{commercialDealID}`

It takes a single parameter, indicated as “commercialDealID” in the example, and has the following response codes:

| Response code | Meaning                              |
|---------------|--------------------------------------|
| 200           | Request successful                   |
| 403           | Forbidden, insufficient access level |

## News

> To get all the news of a commercial deal, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/commercial-deals/news/1230' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN'
```

```json
{
  "content": [
    {
      "url": "https://in.marketscreener.com/quote/stock/ORANGE-4649/news/Orange-solar-power-purchase-agreement-with-ZE-Energy-46716737/",
      "title": "Orange: solar power purchase agreement with ZE Energy",
      "newsDate": "2024-05-14T00:00:00",
      "id": 74632
    },
    {
      "url": "https://web.archive.org/web/20240516091840/https://www.lesechos.fr/industrie-services/energie-environnement/electricite-comment-orange-contourne-les-montagnes-russes-du-solaire-2095140",
      "title": "Electricity: how Orange is avoiding the solar roller coaster",
      "newsDate": "2024-05-16T00:00:00",
      "id": 74633
    }
  ],
  "pageSize": 15,
  "pageNumber": 0,
  "totalElements": 2,
  "numberOfElements": 2,
  "totalPages": 1
}
```

To get the news of a commercial deal, you should use the following endpoint:

`GET /commercial-deals/news/{commercialDealID}`

It takes a single parameter, indicated as “commercialDealID” in the example, and has the following response codes:

| Response code | Meaning                              |
|---------------|--------------------------------------|
| 200           | Request successful                   |
| 403           | Forbidden, insufficient access level |

# Deprecated Endpoints

`POST /getStartupList` was replaced with `POST /companies` and it'll will no longer be supported after 1st of August

`POST /getInvestorList` was replaced with `POST /investors` and it'll will no longer be supported after 1st of August

`POST /getFundingRoundList` was replaced with `POST /fundingRounds` and it'll will no longer be supported after 1st of August

# Filters structure

## Main Filter

This is the main filter used when searching for startups. It contains two simple fields (”offset” and ”limit”) and some complex ones (i.e.: ”include”, ”sorting”) defined further in this document.

| Parameter name      | Parameter type                                | Description                                                         |
|---------------------|-----------------------------------------------|---------------------------------------------------------------------|
| limit               | int                                           | Maximum number of results shown                                     |
| offset              | int                                           | Number of pages (of size "limit") skipped                           |
| sorting             | Section [Sorting](#sorting)                   | Order of the results                                                |
| include             | Section [Startups Filter](#startups-filter)   | Filters related to startups which should be included in the result  |
| exclude             | Section [Startups Filter](#startups-filter)   | Filters related to startups which should be excluded in the result  |
| fundingRoundInclude | Section [Deals Filter](#deals-filter)         | Filters related to deals which should be included in the result     |
| fundingRoundExclude | Section [Deals Filter](#deals-filter)         | Filters related to deals which should be excluded in the result     |
| investorInclude     | Section [Investors Filter](#investors-filter) | Filters related to investors which should be included in the result | 
| investorExclude     | Section [Investors Filter](#investors-filter) | Filters related to investors which should be excluded in the result |

## Sorting

| Parameter name | Parameter type | Description                                                                 |
|----------------|----------------|-----------------------------------------------------------------------------|
| column         | string         | See Section [Sortable Columns](#sortable-columns) for the available options |
| direction      | string         | The only options available are ”ASC” and ”DESC”                             |

## Startups Filter

| Parameter name      | Parameter type                                      | Description                                                                       |
|---------------------|-----------------------------------------------------|-----------------------------------------------------------------------------------|
| name                | string                                              | Startup name                                                                      |
| ids                 | List of int                                         | Startup ids                                                                       |
| searchableLocations | List of int                                         | See Section [Searchable Locations](#searchable-locations) for the accepted values |
| stages              | List of int                                         | Growth stage, see Section [Stages](#stages) for accepted values                   |
| fundings            | List of int                                         | Total funding range, see Section [Fundings](#fundings) for accepted val- ues      |
| employeesFrom       | int                                                 | Minimum number of employees                                                       |
| employeesTo         | int                                                 | Maximum number of employees                                                       |
| fundingsFrom        | int                                                 | Minimum total funding                                                             |
| fundingsTo          | int                                                 | Maximum total funding                                                             |
| tags                | List of int                                         | See Section [Tags](#tags) for accepted values                                     |
| tagsMode            | string                                              | Logical AND or OR operators for filtering startups by the given tags              |
| trls                | List of int                                         | See Section [TRLs](#trls) for accepted values                                     |
| financialStageIDs   | List of int                                         | See Section [Financial Stages](#financial-stages) for accepted values             |
| sustainabilities    | List of int                                         | See Section [Sustainabilities](#sustainabilities) for accepted values             |
| foundedDates        | List of Section [Founded Date](#founded-date)       | Startup founded date                                                              |
| acquisitionDateFrom | date                                                | Starting date for when the startup has been inserted into our database            |
| acquisitionDateTo   | date                                                | Maximum date for when the startup has been inserted into our database             |
| foundedDatesFrom    | date                                                | Starting founded date                                                             |
| foundedDatesTo      | date                                                | Maximum founded date                                                              |
| raisedDateFrom      | date                                                | Starting date for any round                                                       |
| raisedDateTo        | date                                                | Maximum date for any round                                                        |
| lastRoundDates      | List of Section [Last Round Date](#last-round-date) | Date range for last round                                                         |
| lastRoundDatesFrom  | date                                                | Starting date for last round                                                      |
| lastRoundDatesTo    | date                                                | Maximum date for last round                                                       |
| numberOfRoundFrom   | int                                                 | Minimum number of rounds done by the company                                      |
| numberOfRoundTo     | int                                                 | Maximum number of rounds done by the company                                      |
| fundingTypes        | List of Section [Funding Type](#funding-type)       | Funding type for any round                                                        |
| sdgs                | List of int                                         | Sustainable development goals, see Section [SDGs](#sdgs) for accepted values      |
| wildcards           | List of string                                      | Any match of the keywords in the name/pitchline/description                       |
| wildcardsFields     | List of Section [Wildcard Fields](#wildcard-fields) | Select on which fields to match the wildcards                                     |
| lastFundingTypes    | List of Section [Funding Type](#funding-type)       | Funding type for last round                                                       |
| lastFundingsFrom    | List of int                                         | Minimum last round amount                                                         |
| lastFundingsTo      | List of int                                         | Maximum last round amount                                                         |
| patentSearch        | List of string                                      | Any match of the keywords in any patent description                               |
| patentsStatus       | List of Section [Patent Status](#patent-status)     | Status of any patent                                                              |
| applicationDateFrom | Date                                                | Starting application date for any patent                                          |
| applicationDateTo   | Date                                                | Maximum application date for any patent                                           |
| grantedDateFrom     | Date                                                | Starting granted date for any patent                                              |
| grantedDateTo       | Date                                                | Maximum granted date for any patent                                               |
| patentOffice        | List of int                                         | See Section [Searchable Locations](#searchable-locations) for the accepted values |
| patentsCountFrom    | int                                                 | Minimum number of patents                                                         |
| patentsCountTo      | int                                                 | Maximum number of patents                                                         |
| fundRaising         | List of string                                      | Use ”fundRaising” to see all the companies likely to fundraise                    |
| taxonomyItems       | List of int                                         | See Section [Taxonomy Items](#Taxonomy-Item) for accepted values                  |
| taxonomyItemsMode   | string                                              | Logical AND or OR operators for filtering startups by the given taxonomy items    |

## Deals Filter
 
| Parameter name       | Parameter type | Description                                                                                                     |                                                                                                    
|----------------------|----------------|-----------------------------------------------------------------------------------------------------------------|
| acquisitionDateFrom  | Date           | Starting date for when the deal has been inserted into our database                                             |                                            
| acquisitionDateTo    | Date           | Maximum date for when the deal has been inserted into our database                                              |                                             
| datesFrom            | Date           | Starting date for when the deal has been closed                                                                 |                                                                
| datesTo              | Date           | Maximum date for when the deal has been closed                                                                  |                                                                 
| lastRoundDays        | List of int    | Maximum number of days passed since the deal was closed                                                         |
| amountFrom           | int            | Minimum deal amount                                                                                             |                                                                                            
| amountTo             | int            | Maximum deal amount                                                                                             |                                                                                            
| types                | List of string | See Section [Deal Type](#deal-type) for the accepted values                                                     |                                                  
| allowNullAmounts     | boolean        | When searching with deal amount filters, if true, include deals with no deal amount                             |                            
| numberFrom           | int            | Minimum deal number for the company                                                                             |                                                                            
| numberTo             | int            | Maximum deal number for the company                                                                             |                                                                            
| investors            | List of int    | Using the [Investor List](#investors-list) endpoints, it is possible to fetch the investors' IDs to insert here |
| totalFundingFrom     | int            | Minimum total funding of the company                                                                            |                                                                           
| totalFundingTo       | int            | Maximum total funding of the company                                                                            |                                                                           
| financingInstruments | List of string | See Section [Financing Instruments](#financing-instrument) for the accepted values                              |                             
| equityStages         | List of int    | See Section [Equity Stage](#equity-stage) for the accepted values                                               |                                              
| exitStages           | List of int    | See Section [Exit Stage](#exit-stage) for the accepted values                                                   |                                                  

## Investors Filter

| Parameter name              | Parameter type | Description                                                                                                                  |
|-----------------------------|----------------|------------------------------------------------------------------------------------------------------------------------------|
| investorTypeIDs             | List of int    | See Section [Investor Types](#investor-types) for the accepted values                                                        |
| includeOtherInvestorTypes   | boolean        | When filtering for investor types, if true, include investors whose secondary types match at least one of the selected types |
| investorDealsFrom           | int            | Minimum number of deals                                                                                                      |
| investorDealsTo             | int            | Maximum number of deals                                                                                                      |
| investorSearchableLocations | List of int    | See Section [Searchable Locations](#searchable-locations) for the accepted values                                            |
| investorRegions             | List of int    | See Section [Investor Regions](#investor-regions) for accepted values                                                        |
| coInvestors                 | List of int    | See Section [Investors](#investors) for accepted values                                                                      |
| investments                 | List of int    | Using the endpoint [Startup List](#startup-list) it's possible to fetch their clientIDs to be used here                      |
| investorIDs                 | List of int    | See Section [Investors](#investors) for accepted values                                                                      |
| investorFoundedDatesFrom    | date           | Starting founded date of the investor                                                                                        |
| investorFoundedDatesTo      | date           | Maximum founded date of the investor                                                                                         |

## Contacts Filter

| Parameter name | Parameter type | Description                                                                                    |
|----------------|----------------|------------------------------------------------------------------------------------------------|
| clientID       | int            | ClientID of the requested startup, taken from a previous call of [Startup List](#startup-list) |
| decisionMaker  | boolean        | Optional, if true only returns contacts with decision making capabilities                      |
| roleID         | int            | Optional, contact role, see Section [Role](#role) for accepted values                          |

## Investor Contacts Filter

| Parameter name | Parameter type | Description                                                                                          |
|----------------|----------------|------------------------------------------------------------------------------------------------------|
| investorID     | int            | InvestorID of the requested investor, taken from a previous call of [Investor List](#investors-list) |
| decisionMaker  | boolean        | Optional, if true only returns contacts with decision making capabilities                            |

## Tag Filter

This is the tag filter used when searching for tags.

| Parameter name      | Parameter type                                | Description                                |
|---------------------|-----------------------------------------------|--------------------------------------------|
| limit               | int                                           | Maximum number of results shown            |
| offset              | int                                           | Number of pages (of size "limit") skipped  |
| name                | string                                        | Fetch only the tags containing this string |

## Commercial Deals Filter

This is the commercial deal filter used when searching for commercial deals.

| Parameter name        | Parameter type | Description                                                                                       |
|-----------------------|----------------|---------------------------------------------------------------------------------------------------|
| title                 | string         | Filters deals by title (partial or full match)                                                    |
| announcedDateFrom     | date           | Earliest announced date of the deal                                                               |
| announcedDateTo       | date           | Latest announced date of the deal                                                                 |
| announcedDaysFrom     | int            | Filters deals announced within the last specified number of days                                  |
| startYearFrom         | int            | Minimum start year of the deal                                                                    |
| startYearTo           | int            | Maximum start year of the deal                                                                    |
| endYearFrom           | int            | Minimum end year of the deal                                                                      |
| endYearTo             | int            | Maximum end year of the deal                                                                      |
| durationFrom          | int            | Minimum duration of the deal                                                                      |
| durationTo            | int            | Maximum duration of the deal                                                                      |
| pricingFrom           | int            | Minimum deal pricing                                                                              |
| pricingTo             | int            | Maximum deal pricing                                                                              |
| primaryTypes          | List of int    | See Section [Commercial Deal Types](#commercial-deal-types) for the accepted values               |
| secondaryTypes        | List of int    | See Section [Commercial Deal Types](#commercial-deal-types) for the accepted values               |
| searchableGeographies | List of int    | See Section [Searchable Locations](#searchable-locations) for the accepted values                 |
| buyerCompanyIDs       | List of int    | See Section [Commercial Deal Participants](#commercial-deal-participants) for the accepted values |
| buyerInvestorIDs      | List of int    | See Section [Commercial Deal Participants](#commercial-deal-participants) for the accepted values |
| sellerCompanyIDs      | List of int    | See Section [Commercial Deal Participants](#commercial-deal-participants) for the accepted values |
| sellerInvestorIDs     | List of int    | See Section [Commercial Deal Participants](#commercial-deal-participants) for the accepted values |
| partnerCompanyIDs     | List of int    | See Section [Commercial Deal Participants](#commercial-deal-participants) for the accepted values |
| partnerInvestorIDs    | List of int    | See Section [Commercial Deal Participants](#commercial-deal-participants) for the accepted values |
| advisorCompanyIDs     | List of int    | See Section [Commercial Deal Participants](#commercial-deal-participants) for the accepted values |
| advisorInvestorIDs    | List of int    | See Section [Commercial Deal Participants](#commercial-deal-participants) for the accepted values |
| participantCompanyIDs | List of int    | See Section [Commercial Deal Participants](#commercial-deal-participants) for the accepted values |
| participantCompanyIDs | List of int    | See Section [Commercial Deal Participants](#commercial-deal-participants) for the accepted values |
| tagsMode              | string         | Specifies how multiple tags are matched (for example, AND or OR)                                  |
| tagIDs                | List of int    | See Section [Tags](#tags) for accepted values                                                     |

# Additional Tables

## Sortable Columns

| Value                  | Usable for | Description                                 |
|------------------------|------------|---------------------------------------------|
| name                   | startup    | Startup name                                |
| country                | startup    | Startup country                             |
| website                | startup    | Startup website                             |
| foundedDate            | startup    | Startup founded date                        |
| size                   | startup    | Number of employees                         |
| stage                  | startup    | Startup growth stage                        |
| lastRoundDate          | startup    | Startup last round date                     |
| acquisitionDate        | startup    | Date of startup insertion into our database |
| fundingString          | startup    | Startup total funding                       |
| lastRoundAmount        | startup    | Startup last round amount                   |
| lastRoundType          | startup    | Startup last round type                     |
| sustainabilityMetricID | startup    | Startup impact on the ecosystem             |
| tags                   | startup    | Startup tags                                |
| fundingTypes           | startup    | Startup funding types                       |
| sdgs                   | startup    | Startup Sustainable Development Goals       |

## Founded Date

| ID | Label        |
|----|--------------|
| 1  | This year    |
| 2  | Last year    |
| 3  | Last 3 years |
| 4  | Last 5 years |

## Last Round Date

| ID | Label         |
|----|---------------|
| 1  | Last month    |
| 2  | Last semester |
| 3  | Last year     |

## Wildcard Fields

| Label          |
|----------------|
| pitchLine      |
| description    | 
| websiteContent |

## Regexp Fields

| Label          |
|----------------|
| pitchLine      |
| description    | 
| websiteContent |

## Patent Status

| Label   |
|---------|
| granted |
| pending |

## Stages

| ID | Label    |
|----|----------|
| 1  | Ideation |
| 2  | Early    |
| 3  | Growth   |
| 4  | Scaling  |

## TRLs

| ID | Label |
|----|-------|
| 2  | 9     |
| 3  | 1-5   |
| 4  | 6-8   |

## Financial Stages

| ID | Label               |
|----|---------------------|
| 1  | Pre-Seed stage (VC) |
| 2  | Seed stage (VC)     |
| 3  | Early stage (VC)    |
| 4  | Late stage (VC)     |
| 5  | PE-growth stage     |

## Size Ranges

| ID | Label        |
|----|--------------|
| 1  | 1 - 10       |
| 2  | 11 - 50      |
| 3  | 51 - 100     |
| 4  | 101 - 200    |
| 5  | 201 - 500    |
| 6  | 501 - 1000   |
| 7  | 1001 - 5000  |
| 8  | 5001 - 10000 |
| 9  | 10001+       |

## Revenue Ranges

| ID | Label       |
|----|-------------|
| 1  | 500K - 1M   |
| 2  | 50M - 100M  |
| 3  | 10M - 20M   |
| 4  | 5M - 10M    |
| 5  | 500M - 1B   |
| 6  | 2.5M - 5M   |
| 7  | 20M - 50M   |
| 8  | 1M - 2.5M   |
| 9  | 1B+         |
| 10 | 0 - 500K    |
| 11 | 100M - 500M |

## Fundings

| ID | Label       |
|----|-------------|
| 1  | 0 - 500K    |
| 2  | 500K - 1M   |
| 3  | 1M-5M       |
| 4  | 5M-10M      |
| 5  | 10M - 25M   |
| 6  | 25M - 50M   |
| 7  | 50M - 100M  |
| 8  | 100M - 250M |
| 9  | 250+M       |

## Sustainabilities

| ID | Label            |
|----|------------------|
| 1  | Low impact       |
| 2  | Average impact   |
| 3  | High impact      |
| 4  | Very high impact |

## SDGs

| ID | Label                                       |
|----|---------------------------------------------|
| 1  | 1. No poverty                               |
| 2  | 2. Zero hunger                              |
| 3  | 3. Good health and well-being               |
| 4  | 4. Quality education                        |
| 5  | 5. Gender equality                          |
| 6  | 6. Clean water and sanitation               |
| 7  | 7. Affordable and clean energy              |
| 8  | 8. Decent work and economic growth          |
| 9  | 9. Industry, innovation, and infrastructure |
| 10 | 10. Reduced inequalities                    |
| 11 | 11. Sustainable cities and communities      |
| 12 | 12. Responsible consumption and production  |
| 13 | 13. Climate action                          |
| 14 | 14. Life below water                        |
| 15 | 15. Life on land                            |
| 16 | 16. Peace justice and strong institutions   |
| 17 | 17. Partenrships                            |

## Financing Instrument

| Label  |
|--------|
| Debt   |
| Equity | 
| Grant  |

## Equity Stage

| ID | Label             |
|----|-------------------|
| 1  | Other             |
| 2  | Pre-seed and seed |
| 3  | Early stage       |
| 4  | Late stage        |

## Exit Stage

| ID | Label     |
|----|-----------|
| 1  | Venture   |
| 2  | Exit      |
| 3  | Post Exit |

## Deal Type

| ID  | Label                 |
|-----|-----------------------|
| 65  | Accelerator/incubator |
| 66  | Acquisition           |
| 70  | Convertible note      |
| 75  | Debt                  |
| 76  | Early VC              |
| 79  | Grant                 |
| 80  | Growth equity         |
| 81  | ICO                   |
| 82  | IPO                   |
| 83  | Late VC               |
| 84  | Merger                |
| 85  | PIPE                  |
| 88  | SPAC                  |
| 89  | Seed                  |
| 91  | Series A              |
| 92  | Series B              |
| 93  | Series C              |
| 94  | Series D              |
| 95  | Series E              |
| 96  | Series F              |
| 97  | Series G              |
| 98  | Series H              |
| 99  | Spinoff/spinout       |
| 102 | Pre-Seed              |
| 103 | Secondary transaction |
| 104 | Bridge                |
| 105 | In-kind services      |
| 107 | Award/Prize           |
| 108 | Private placement     |
| 109 | Product crowdfunding  |
| 110 | Equity crowdfunding   |
| 111 | Debt crowdfunding     |
| 112 | Revenue financing     |

## Role

| ID | Label          |
|----|----------------|
| 1  | Founder        |
| 2  | HR             |
| 3  | Sales          |
| 4  | Marketing / PR |
| 5  | Tech           |
| 6  | C-Suite        |

## Investor Types

| ID | Label                          |
|----|--------------------------------|
| 1  | Investment Bank                |
| 10 | Venture Capital                |
| 11 | Fund Of Funds                  |
| 14 | Private Equity                 |
| 17 | Hedge Fund                     |
| 23 | Corporate Venture Capital      |
| 24 | Angel Group                    |
| 34 | Asset Manager                  |
| 35 | Family Office                  |
| 41 | Government                     |
| 44 | Angel                          |
| 46 | Accelerator/Incubator          |
| 53 | University                     |
| 57 | Real Estate                    |
| 59 | Lender/Debt Provider           |
| 60 | Holding Company                |
| 61 | Limited Partner                |
| 62 | Infrastructure                 |
| 63 | Other                          |
| 64 | Corporation                    |
| 68 | Commercial Banks               |
| 69 | Non-Profit Organisation        |
| 70 | Advisory Firm                  |
| 71 | Wealth Management Firm         |
| 72 | Investment Company             |
| 73 | Insurance Company              |
| 74 | Sovereign Wealth Fund          |
| 75 | Academic/Research Institutions |
| 77 | Competition/Challenges         |
| 78 | Pension Fund                   |
| 79 | Private Capital Firms          |
| 80 | Foundation                     |
| 81 | Bank                           |

## Investor Regions

| ID | Label                   |
|----|-------------------------|
| 1  | Alpine countries        |
| 2  | Balkan peninsula        |
| 3  | Baltics                 |
| 4  | Benelux                 |
| 5  | Central Europe          |
| 6  | Danubian countries      |
| 7  | Eastern Europe          |
| 8  | European Union          |
| 9  | Eurozone                |
| 10 | Iberian Peninsula       |
| 11 | Mediterranean countries |
| 12 | Nordics                 |
| 13 | Northern Europe         |
| 14 | Scandinavian peninsula  |
| 15 | Southern Europe         |
| 16 | Western Europe          |
| 17 | Europe                  |
| 19 | US Midwest              |
| 20 | US Northeast            |
| 21 | US Southeast            |
| 22 | US West                 |
| 23 | US East Coast           |
| 24 | US West Coast           |
| 25 | US Southwest            |

## Tags

> To get the list of the currently available tags, use this code:

```shell
curl -v -X POST 'https://api-new.netzeroinsights.com/taxonomy/tags' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN' \
-d '{"name": "bio", "offset": 0, "limit": 5}'
```

> In case of a 200 response, the response body will contain all the available tags, with the JSON structured like the following:
     
```json
{
  "count": 75,
  "results": [
    {
      "id": 20,
      "tagTypeID": 3,
      "label": "biofuel",
      "tagFamilyLabel": "Solutions",
      "tagTypeLabel": "technology"
    },
    {
      "id": 22,
      "tagTypeID": 1,
      "label": "biomimicry",
      "tagFamilyLabel": "Buzzwords",
      "tagTypeLabel": "Undefined"
    },
    {
      "id": 24,
      "tagTypeID": 5,
      "label": "bioplastic",
      "tagFamilyLabel": "Buzzwords",
      "tagTypeLabel": "buzzword"
    },
    {
      "id": 25,
      "tagTypeID": 3,
      "label": "biotechnology",
      "tagFamilyLabel": "Solutions",
      "tagTypeLabel": "technology"
    },
    {
      "id": 194,
      "tagTypeID": 46,
      "label": "biochar (BC)",
      "tagFamilyLabel": "Solutions",
      "tagTypeLabel": "solution"
    }
  ]
}
```

To get the list of the currently available tags, you should use the following endpoint:

`POST /taxonomy/tags`

With a JSON request body in the format specified at the section [Tag Filter](#tag-filter).

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Investors

> To get the list of the currently available investors, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/getInvestorsForFilter' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN'
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

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Funding Type

> To get the list of the currently available funding types, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/getFundingTypes' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN'
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

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Searchable Locations

> To get the list of the searchable locations, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/searchLocation/london' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN'
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

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Commercial Deal Types

| ID | Label                                    |
|----|------------------------------------------|
| 1  | Strategic Partnership                    |
| 2  | Joint Venture                            |
| 3  | Memorandum of Understanding (MoU)        |
| 4  | Public-Private Partnership (PPP)         |
| 5  | Research and Development Agreement (R&D) |
| 6  | Offtake Agreement                        |
| 7  | Supply Agreement                         |
| 8  | Manufacturing Partnership                |
| 9  | Licensing Agreement                      |
| 10 | Letter of Intent (LOI)                   |
| 11 | Service Agreement                        |
| 12 | Distribution Agreement                   |
| 13 | Sustainability Partnership               |

## Commercial Deal Roles

| ID | Label   |
|----|---------|
| 1  | Buyer   |
| 2  | Seller  |
| 3  | Partner |
| 4  | Advisor |

## Commercial Deal Participants

> To get the list of companies and/or investors as participants, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/commercial-deals/search/company-investor?searchText=energy' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN' \
-H 'Content-Type: application/json' \       
```

> In case of a 200 response, the response body will contain all the matching participants, with the JSON structured like the following:

```json
[
  {
    "name": "EnergyLab",
    "type": "INVESTOR",
    "logoUrl": "https://d1gpx4pnpaaoyd.cloudfront.net/Startups/New_Empty_Logo_xqsrak.png",
    "website": "https://energylab.es/",
    "investorID": 64348,
    "id": 64348
  },
  {
    "name": "Energy Leap",
    "type": "INVESTOR",
    "logoUrl": "https://d1gpx4pnpaaoyd.cloudfront.net/Startups/New_Empty_Logo_xqsrak.png",
    "investorID": 37952,
    "id": 37952
  },
  {
    "name": "Energy&+",
    "type": "COMPANY",
    "logoUrl": "https://d1gpx4pnpaaoyd.cloudfront.net/Startups/client_1936205.jpg",
    "website": "https://energy.bzh",
    "companyID": 208261,
    "id": 208261
  }
]
```

To get the list of the participants, you should use the following endpoint:

`GET /commercial-deals/search/company-investor?searchText={textParam}`

It takes a single query parameter, indicated as “searchText” in the example, which is a string used to filter the companies and investors and has the following response codes:

| Response code | Meaning                              |
|---------------|--------------------------------------|
| 200           | Request successful                   |
| 403           | Forbidden, insufficient access level |

# Response structures

## Startup search

| Name    | Content                                                      |
|---------|--------------------------------------------------------------|
| results | List of Section [Startup (small)](#startup-(small))          |
| count   | Total number of results, regardless of the ”limit” parameter |

## Startup (small)

| Name                           | Content         |
|--------------------------------|-----------------|
| clientID                       | Startup ID      |
| name                           | Company name    |
| website                        | Company website |

## Startup

| Name                           | Content                                                  |
|--------------------------------|----------------------------------------------------------|
| id                             | Internal ID                                              |
| clientID                       | Startup ID                                               |
| name                           | Name                                                     |
| logo                           | URL to company’s logo                                    |
| website                        | Company website                                          |
| domain                         | Company website domain                                   |
| pitchLine                      | Pitchline                                                |
| description                    | Description fetched from the company website             |
| uniqueSellingProposition       | Unique selling proposition                               |
| impact                         | Company impact on climate                                |
| fundingAmount                  | Company total funding in EUR                             |
| fundingString                  | Company total funding in EUR, formatted                  |
| fundingAmountUSD               | Company total funding in USD                             |
| fundingStringUSD               | Company total funding in USD, formatted                  |
| fundingRange                   | Company total funding range                              |
| fundingRangeID                 | Company total funding range ID                           |
| fundingRangeUSD                | Company total funding range in USD                       |
| fundingRangeIDUSD              | Company total funding range ID in USD                    |
| lastRoundDate                  | Date of the last round                                   |
| acquisitionDate                | Date of insertion into our database                      |
| foundedDate                    | Founded date                                             |
| georowID                       | ID of the searchable location of the company HQ          |
| country                        | Country name                                             |
| countryID                      | Country ID                                               |
| city                           | City name                                                |
| cityID                         | City ID                                                  |
| continent                      | Continent name                                           |
| continentID                    | Continent ID                                             |
| address                        | Address of the company                                   |
| admin1                         | Administrative region level 1 name                       |
| admin2                         | Administrative region level 2 name                       |
| admin3                         | Administrative region level 3 name                       |
| admin4                         | Administrative region level 4 name                       |
| admin1ID                       | Administrative region level 1 ID                         |
| admin2ID                       | Administrative region level 2 ID                         |
| admin3ID                       | Administrative region level 3 ID                         |
| admin4ID                       | Administrative region level 4 ID                         |
| email                          | Company main email                                       |
| phone                          | Company main phone                                       |
| size                           | Company number of employees range                        |
| sizeID                         | Company number of employees range ID                     |
| stage                          | Company growth stage                                     |
| stageID                        | Company growth stage ID                                  |
| employeesRange                 | Employees range                                          |
| linkedinURL                    | URL to company LinkedIn                                  |
| twitterURL                     | URL to company Twitter                                   |
| facebookURL                    | URL to company Facebook                                  |
| directURL                      | URL to our company page                                  |
| sustainabilityMetric           | Company climate impact metric score                      |
| sustainabilityMetricID         | Company climate impact metric range ID                   |
| sustainabilityMetricLabel      | Company climate impact metric label                      |
| lastRoundAmount                | Last round amount in EUR                                 |
| lastRoundAmountUSD             | Last round amount in USD                                 |
| lastRoundAmountString          | Last round amount in EUR, formatted                      |
| lastRoundAmountStringUSD       | Last round amount in USD, formatted                      |
| lastRoundType                  | Last round type                                          |
| revenueEuro                    | Total company revenue                                    |
| revenueYear                    | Year related to the ”revenueEuro” field                  |
| revenuesRange                  | Revenue range                                            |
| tags                           | Company tags                                             |
| trl                            | Company TRL                                              |
| trlID                          | Company TRL ID                                           |
| trlAcquisitionDate             | Last updated date of the company TRL                     |
| fundingTypes                   | Funding types of any round                               |
| sdgs                           | Sustainable Development Goals                            |
| piFrameworks                   | PI Frameworks                                            |
| investorPartnerSet             | Set of investorIDs                                       |
| companyContactSet              | Set of contact IDs                                       |
| isFundRaising                  | Company likelihood to fundraise                          |
| currentlyFundraising           | Estimation about the company being currently fundraising |
| currentlyFundraisingDate       | Date of estimation                                       |
| roundCount                     | Number of rounds                                         |
| roundWithDateCount             | Number of rounds with a date available                   |
| reviewDate                     | Date of latest company review by our analysts            |
| alternativeNames               | Alternative company names                                |
| legalNames                     | Legal company names                                      |
| intellectualProperty           | If true, the company has some registered IP              |
| pitchdeckURL                   | URL to the company pitch deck                            |
| lastPostMoneyValuation         | Latest post money valuation                              |
| lastPostMoneyValuationCurrency | Latest post money valuation currency                     |
| numberOfEquityRounds           | Number of company deals of type Equity                   |
| numberOfDebtRounds             | Number of company deals of type Debt                     |
| numberOfGrants                 | Number of company deals of type Grant                    |
| employeesGrowthJSON            | Historical aggregation of the employees fluctuation      |
| currentEmployeesCount          | Number of current employees                              |
| active                         | Active status of the company                             |
| note                           | Note on the company                                      |

## Deal (small)

| Name       | Content                                                    |
|------------|------------------------------------------------------------|
| dealID     | Internal funding round ID                                  |
| clientID   | Startup ID                                                 |
| clientName | Startup name                                               |

## Deal
        
| Name                   | Content                                                    |
|------------------------|------------------------------------------------------------|
| id                     | Internal funding round ID                                  |
| clientId               | Startup ID                                                 |
| clientName             | Startup name                                               |
| clientLogoURL          | URL to startup's logo                                      |
| clientPitchLine        | Startup pitchLine                                          |
| clientHQ               | Startup headquarters                                       |
| clientCityHQ           | Startup city's headquarters                                |
| clientCountryCode      | Startup country code                                       |
| clientCountryID        | Startup country ID                                         |
| clientContinentID      | Startup continent ID                                       |
| clientFoundedDate      | Startup founded date                                       |
| roundDate              | Date of the round                                          |
| acquisitionDate        | Date of startup insertion into our database                |
| roundType              | Type of the round                                          |
| roundAmount            | Amount of the round (EUR)                                  |
| roundAmountUSD         | Amount of the round (USD)                                  |
| roundAmountString      | Formatted amount of the round (EUR)                        |
| roundAmountStringUSD   | Formatted amount of the round (USD)                        |
| roundAmountRangeID     | Round amount range ID (EUR)                                |
| roundAmountRangeIDUSD  | Round amount range ID (USD)                                |
| roundInvestorsIDs      | List of IDs of all the investors of the round              |
| roundInvestors         | List of all the investor DTOs of the round                 |
| roundNewsIDs           | List of IDs of all the sources of the round                |
| roundNews              | List of all the source DTOs of the round                   |
| roundCurrency          | Original currency of the round                             |
| originalRoundAmount    | Round amount in original currency                          |
| numberOfRounds         | Number of rounds of the company                            |        
| totalFundingRangeID    | Company total funding ID (EUR)                             |        
| totalFundingRangeIDUSD | Company total funding ID (USD)                             |        
| totalFunding           | Company total funding (EUR)                                |        
| totalFundingUSD        | Company total funding (USD)                                |        
| totalFundingString     | Formatted company total funding (EUR)                      |
| totalFundingStringUSD  | Formatted company total funding (USD)                      |
| roundNumber            | Number of the round for the company                        |
| financingInstrument    | Financing instrument                                       |
| lastRound              | If true, this is the latest round for the company          |
| source                 | Name of the analyst who inserted the round                 |
| valuationAmount        | Valuation amount                                           |
| valuationCurrency      | Valuation currency                                         |
| valuationType          | Valuation type                                             |
| equityStageID          | Equity stage ID, see Section [Equity Stage](#equity-stage) |
| exitStageID            | Exit stage ID, see Section [Exit Stage](#exit-stage)       |  
| insertionDate          | Date of insertion into our database                        |

## Deal search

| Name               | Content                                                      |
|--------------------|--------------------------------------------------------------|
| results            | List of Section [Deal (small)](#deal-(small))                |
| count              | Total number of results, regardless of the ”limit” parameter |
| roundsTotalFunding | Total amount of results, regardless of the ”limit” parameter |
| selectedCurrency   | Selected currency of the user                                |

## Funding round

| Name                | Content                                                    |
|---------------------|------------------------------------------------------------|
| id                  | Internal funding round ID                                  |
| clientID            | Startup ID                                                 |
| roundDate           | Date of the round                                          |
| roundType           | Type of the round                                          |
| roundAmount         | Amount of the round (EUR)                                  |
| roundAmountUSD      | Amount of the round (USD)                                  |
| roundAmountId       | ID of the amount range                                     |
| coFundingRoundId    | Additional internal funding round ID                       |
| fundingRange        | Amount range                                               |
| roundInvestors      | List of IDs of all the investors of the round              |
| roundNews           | List of IDs of all the sources of the round                |
| roundCurrency       | Original currency of the round                             |
| originalAmount      | Round amount in original currency                          |
| source              | Name of the analyst who inserted the round                 |
| financingInstrument | Financing instrument                                       |
| equityStageID       | Equity stage ID, see Section [Equity Stage](#equity-stage) |
| exitStageID         | Exit stage ID, see Section [Exit Stage](#exit-stage)       |

## Funding round investor

| Name           | Content              |
|----------------|----------------------|
| id             | Internal investor ID |
| name           | Investor name        |
| website        | Investor website     |
| fundingRoundId | Funding round ID     |

## Funding round source

| Name           | Content            |
|----------------|--------------------|
| id             | Internal source ID |
| url            | Source url         |
| fundingRoundId | Funding round ID   |

## Patent

| Name              | Content                                                    |
|-------------------|------------------------------------------------------------|
| id                | Internal patent ID                                         |
| googlePatentsUrl  | Patent url                                                 |
| filingDate        | Filing date                                                |
| publicationDate   | Pubblication date                                          |
| patentAbstract    | Patent abstract                                            |
| title             | Patent title                                               |
| jurisdiction      | Country ID where the patent has been filed                 |
| jurisdictionName  | Name of the country where the patent has been filed        |
| publicationNumber | External patent ID                                         |
| familyId          | Internal patent family ID                                  |
| clientId          | Client ID of the startup                                   |
| status            | Patent status, see Section [Patent Status](#patent-status) |

## Investor Core

| Name           | Content                                                                         |
|----------------|---------------------------------------------------------------------------------|
| id             | Internal investor ID                                                            |
| name           | Investor name                                                                   |
| firstRoundDate | Date of the first round of the company in which the investor made an appearance |
| roundTypes     | Types of round in which the investor appeared                                   |

## Contact

| Name          | Content                                             |
|---------------|-----------------------------------------------------|
| name          | Person name                                         |
| role          | Person role                                         |
| department    | Person department                                   |
| email         | Person email                                        |
| linkedinURL   | Person LinkedIn URL                                 |
| decisionMaker | True if the person has decision making capabilities |
| id            | Internal person ID                                  |

## Investor search

| Name         | Content                                                               |
|--------------|-----------------------------------------------------------------------|
| results      | List of Section [Investor (small)](#investor-(small))                 |
| count        | Total number of results, regardless of the ”limit” parameter          |
| totalFunding | Total funding from the investors, regardless of the ”limit” parameter |

## Investor (small)

| Name       | Content          |
|------------|------------------|
| investorID | Investor ID      |
| name       | Investor name    |
| website    | Investor website |

## Investor

| Name                  | Content                                                  |
|-----------------------|----------------------------------------------------------|
| id                    | Internal ID                                              |
| investorID            | Investor ID                                              |
| name                  | Name                                                     |
| description           | Description fetched from the investor website            |
| website               | Investor website                                         |
| city                  | City name                                                |
| country               | Country name                                             |
| continent             | Continent name                                           |
| linkedInURL           | URL to investor LinkedIn                                 |
| twitterURL            | URL to investor Twitter                                  |
| facebookURL           | URL to investor Facebook                                 |
| pitchbookURL          | URL to investor Pitchbook                                |
| email                 | Investor main email                                      |
| phone                 | Investor main phone                                      |
| size                  | Investor number of employees range                       |
| sizeID                | Investor number of employees range ID                    |
| foundedDate           | Founded date                                             |
| numberOfDeals         | Number of deals                                          |
| numberOfDealsFiltered | Number of filtered deals                                 |
| lastDealType          | Type of the last deal                                    |
| lastDealDate          | Date of the last deal                                    |
| lastRoundAmount       | Last round amount in EUR                                 |
| lastRoundAmountUSD    | Last round amount in USD                                 |
| note                  | Note on the investor                                     |
| primaryTypeID         | Primary type ID                                          |
| primaryType           | Primary investor type                                    |
| secondaryTypes        | Secondary investor types                                 |
| investments           | List of companies that have been invested in             |
| coInvestors           | List of investors that have invested in mutual companies |

## Investor Contact

| Name          | Content                                             |
|---------------|-----------------------------------------------------|
| name          | Person name                                         |
| role          | Person role                                         |
| email         | Person email                                        |
| linkedinURL   | Person LinkedIn URL                                 |
| decisionMaker | True if the person has decision making capabilities |
| id            | Internal person ID                                  |

## Commercial Deal

| Name                | Content                                    |
|---------------------|--------------------------------------------|
| id                  | Internal commercial deal ID                |
| title               | Commercial deal title                      |
| description         | Commercial deal description                |
| volume              | Volumetric value of the deal component     |
| currency            | Commercial deal currency                   |
| announcedDate       | Commercial deal announcement date          |
| startYear           | Commercial deal start year                 |
| endYear             | Commercial deal end year                   |
| duration            | Commercial deal duration                   |
| pricing             | Commercial deal pricing in given currency  |
| pricingEUR          | Commercial deal pricing in EUR             |
| pricingUSD          | Commercial deal pricing in USD             |
| tags                | Tags associated with the commercial deal   |
| searchableLocations | Commercial deal locations                  |
| primaryTypes        | Commercial deal primary types              |
| secondaryTypes      | Commercial deal secondary types            |
| connectedCompanies  | Companies connected to the commercial deal |
| connectedInvestors  | Investors connected to the commercial deal |
| news                | News connected to the commercial deal      |

# Taxonomy Page

Our taxonomy is a way to visualise the relation between different topics.

## All Taxonomy Items

> To get all Taxonomy Graph Items, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/taxonomy/itemDtos' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN' \
-H 'Content-Type: application/json' \                 
```

> In case of a 200 response, the response body will contain all the available items, with the JSON structured like the following:

```json
[
  {
    "label": "Alternative Fuel",
    "description": "Alternative fuels are at the forefront of innovation, with notable examples being biofuels and synthetic fuels. Solutions in this domain are dedicated to advancing and applying these alternatives, not only for transportation but also for broader energy applications, including electricity generation and industrial processes.",
    "tagID": 995,
    "tagName": "Alternative Fuel",
    "id": 1
  },
  {
    "label": "Biofuel",
    "description": "Biofuels are produced from renewable resources, primarily plant-based feedstocks such as crops, agricultural residues, or algae. Biofuels offer a way to decarbonize sectors that are challenging to electrify, such as aviation and heavy industry, while promoting agricultural sustainability through responsible feedstock sourcing and land-use practices. Some solutions include innovative processes to convert biomass into biofuels, such as biodiesel and bioethanol, through techniques like fermentation and thermochemical conversion.",
    "tagID": 996,
    "tagName": "Biofuel",
    "id": 2
  }
]
```

To get all the taxonomy items you should use the following endpoint:

`GET /taxonomy/itemDtos`

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Level 0 Taxonomy Graph Items

> To get Taxonomy Graph Item list without any parents (which means they are the top level of our taxonomy), use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/taxonomy/graph' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN' \
-H 'Content-Type: application/json' \                 
```

> In case of a 200 response, the response body will contain all the available taxonomy graph items, with the JSON structured like the following:

```json
[
  {
    "label": "Solutions map",
    "description": "The Solutions Map simplifies your exploration of climate tech solutions. We've categorized over 200 solutions into Challenge Areas like Energy, Industry, Transport, and more. When you choose a solution, you can dive into its sub-solutions if they exist. You can also access insights, active investors, and information about startups and SMEs for each solution.",
    "hasChildren": true,
    "id": 347
  },
  {
    "label": "Deep Dives map",
    "description": "The Deep Dives offers a meticulous mapping of the most innovative and extensively researched fields in the realm of Climate Tech. These curated maps serve as a direct, technologically advanced interface, simplifying navigation through the intricate landscape of climate technology. Users can seamlessly delve into specific areas such as Cement and Concrete, Carbon Offset and Markets, Marine Energy, and Hydrogen, gaining valuable insights into advancements, sub-solutions, and active investors. ",
    "hasChildren": true,
    "id": 359
  },
  {
    "label": "Software map",
    "description": "The Software Map is a comprehensive visual representation that outlines the diverse array of software solutions within the climate tech landscape. This map provides a detailed overview of software applications tailored to address climate challenges across various sectors, including energy, transport, industry, food and agriculture, built environment, natural environment, and more. ",
    "hasChildren": true,
    "id": 660
  }
]
```

To get all the level 0 taxonomy items you should use the following endpoint:

`GET /taxonomy/graph`

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

These are the top-most items of our taxonomy, and all the other items are related to them, either directly or through another item(s)

## Taxonomy Graph children Items

> To get the list of children Taxonomy Graph Items of a parent item, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/taxonomy/graph/Biofuel' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN' \
-H 'Content-Type: application/json' \                 
```
> Or

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/taxonomy/graph/2' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN' \
-H 'Content-Type: application/json' \                 
```

> In case of a 200 response, the response body will contain all the available children items of a parent item by ID or label, with the JSON structured like the following:
 
```json
[
  {
    "label": "Bioethanol",
    "description": "Bioethanol is produced through the fermentation of organic materials, such as crops like corn, and sugarcane, or cellulose-rich feedstocks like switchgrass. This process converts the sugars within these materials into ethanol using microorganisms. Bioethanol is a key player in the quest for sustainable transportation fuels, as it can be blended with gasoline to reduce greenhouse gas emissions and dependence on fossil fuels. When compared to other sustainable fuels like biodiesel or synthetic fuels, bioethanol has specific advantages, such as its compatibility with existing gasoline engines and infrastructure.",
    "hasChildren": false,
    "id": 5
  },
  {
    "label": "Bio-Oil",
    "description": "Bio-oil is produced from biomass sources like wood chips, agricultural residues, or algae. It is typically created through a process called pyrolysis or fast pyrolysis, which involves heating biomass in the absence of oxygen to break it down into a liquid form. Bio-oil can be used as a replacement for traditional fossil fuels in applications such as power generation and heating, and it can also serve as a feedstock for the production of biofuels and other valuable chemicals. Compared to other sustainable fuels like bioethanol or biodiesel, bio-oil offers advantages such as a higher energy density and the potential for versatile applications.",
    "hasChildren": false,
    "id": 6
  }
]
```

To get all the children taxonomy items of a parent item, you should use the following endpoint:

`GET /taxonomy/graph/{parentID}`

Where the parameter `parentID` can either be the parent item ID or the parent item label.

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Top Companies

> To get Top Companies of a Taxonomy Graph Item, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/taxonomy/graph/topCompanies/1783' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN' \
-H 'Content-Type: application/json' \                 
```

> In case of a 200 response, the response body will contain at most 3 available companies of the specified item by ID, with the JSON structured like the following:

```json
[
    {
        "clientID": 112504,
        "name": "R3Energise",
        "logo": "https://res.cloudinary.com/eutop-1/image/upload/b_white/v1690205436/Startups/owsivo12opurbi23pgr7.jpg",
        "website": "https://www.r3energise.com/",
        "domain": "r3energise.com",
        "pitchLine": "R3Energise aims to support vessel operators in their transition to cleaner operations for their existing fleet. The ideal client grants R3Energise the opportunity to perform a feasibility study to assess the most suitable arrangement for their vessel, minimising the impact on their operations, CAPEX/OPEX and the environment. With our expertise ranging from CTV’s to ferries, survey vessels to SOV’s, R3Energise is a reliable partner in taking on these challenges and advising its clients.",
        "description": "",
        "fundingAmount": 124343.0,
        "fundingString": "124K",
        "fundingAmountUSD": 134097.0,
        "fundingStringUSD": "134K",
        "fundingRangeID": 1,
        "fundingRange": "0 - 500K",
        "lastRoundDate": "2023-01-01T13:31:00.000+00:00",
        "sustainabilityMetric": 0.2769792,
        "foundedDate": 2023,
        "georowID": 928883,
        "countryID": 225,
        "country": "United Kingdom",
        "city": "Colchester",
        "continent": "Europe",
        "email": "info@r3energise.com",
        "phone": "+44 7794 369903",
        "stageID": 1,
        "stage": "Ideation",
        "linkedinURL": "https://www.linkedin.com/company/r3energise-ltd/",
        "directURL": "r3energise-112504",
        "sustainabilityMetricID": 2,
        "lastRoundAmount": 124343,
        "lastRoundAmountUSD": 134097,
        "lastRoundAmountString": "124K",
        "lastRoundAmountStringUSD": "134K",
        "lastRoundType": "Grant",
        "tags": [
            {
                "tagTypeId": 4,
                "tagType": {
                    "tagType": "business model",
                    "platformOrder": 4,
                    "tagFamily": {
                        "tagFamily": "Business models",
                        "platformOrder": 4,
                        "id": 4
                    },
                    "id": 4
                },
                "filterable": true,
                "id": 303,
                "label": "service"
            }
        ],
        "fundingTypes": [],
        "sdgs": [
            {
                "id": 13,
                "label": "13. Climate action"
            }
        ],
        "note": "",
        "roundCount": 1,
        "fundingRangeUSD": "0 - 500K",
        "fundingRangeIDUSD": 1,
        "intellectualProperty": true,
        "numberOfGrants": 1,
        "sustainabilityMetricLabel": "Average impact",
        "id": 85443,
        "eutopiaScore": 27
    }
]
```

To get the top companies of a taxonomy item you should use the following endpoint:

`GET /taxonomy/graph/topCompanies/{itemID}`

Where the parameter `itemID` is the taxonomy item ID.

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Top Investors

> To get Top Investors of a Taxonomy Graph Item, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/taxonomy/graph/topInvestors/2' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN' \
-H 'Content-Type: application/json' \                 
```

> In case of a 200 response, the response body will contain at most 3 available investors of the specified item by ID, with the JSON structured like the following:

```json
[
    {
        "investorID": 72,
        "name": "UK Research and Innovation",
        "logoURL": "https://res.cloudinary.com/eutop-1/image/upload/b_white/v1691668219/Investors/ocsr6c10pv9t7xumavd1.jpg",
        "numberOfDeals": 977,
        "numberOfDealsFiltered": 31,
        "id": 34
    },
    {
        "investorID": 670,
        "name": "Eit Innoenergy",
        "logoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1687594145/Investors/epm6ozsmb0awp9ljhvg3.jpg",
        "foundedDate": 2010,
        "numberOfDeals": 195,
        "numberOfDealsFiltered": 9,
        "primaryTypeID": 10,
        "primaryType": "Venture Capital",
        "id": 138
    },
    {
        "investorID": 18606,
        "name": "Sosv",
        "logoURL": "https://res.cloudinary.com/eutopia-3/image/upload/b_white/v1692150659/Investors/y4mrqtqfyeexi7yyo12r.jpg",
        "foundedDate": 1994,
        "numberOfDeals": 178,
        "numberOfDealsFiltered": 3,
        "primaryTypeID": 10,
        "primaryType": "Venture Capital",
        "id": 20830
    }
]
```

To get the top investors of a taxonomy item you should use the following endpoint:

`GET /taxonomy/graph/topInvestors/{itemID}`

Where the parameter `itemID` is the taxonomy item ID.

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Taxonomy Item

> To get a Taxonomy Graph Item by parameter, ID, or label, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/taxonomy/item/2' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN' \
-H 'Content-Type: application/json' \                 
```

> Or

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/taxonomy/item/Biofuel' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN' \
-H 'Content-Type: application/json' \                 
```

> In case of a 200 response, the response body will contain a taxonomy graph item, with the JSON structured like the following:

```json
{
    "label": "Biofuel",
    "description": "Biofuels are produced from renewable resources, primarily plant-based feedstocks such as crops, agricultural residues, or algae. Biofuels offer a way to decarbonize sectors that are challenging to electrify, such as aviation and heavy industry, while promoting agricultural sustainability through responsible feedstock sourcing and land-use practices. Some solutions include innovative processes to convert biomass into biofuels, such as biodiesel and bioethanol, through techniques like fermentation and thermochemical conversion.",
    "hasChildren": true,
    "id": 2
}
```

To get a single taxonomy item you should use the following endpoint:

`GET /taxonomy/item/{itemID}`

Where the parameter `itemID` can either be the item ID or the item label.

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Taxonomy Items by Company

> To get the Taxonomy Graph Items by company, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/taxonomy/items/company/10' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN' \
-H 'Content-Type: application/json' \                 
```

> In case of a 200 response, the response body will contain all the available taxonomy graph items of the company, with the JSON structured like the following:

```json
[
  {
    "id": 154,
    "label": "Construction Materials",
    "description": "Construction material solutions refer to innovative and sustainable materials, techniques, and technologies aimed at reducing the environmental impact of the construction industry. These solutions encompass the development and utilization of eco-friendly materials like recycled composites, low-carbon concrete, and bio-based polymers, as well as circular economy applications such as construction materials marketplaces."
  },
  {
    "id": 160,
    "label": "Alternative Cement and Concrete",
    "description": "Alternative cement and concrete refer to innovative materials and construction methods designed to significantly reduce the environmental impact of traditional cement and concrete production. These solutions aim to lower carbon emissions, energy consumption, and resource depletion associated with the construction industry. They often incorporate complete or partial cement substitutes, production process improvement, and others."
  },
  {
    "id": 270,
    "label": "Built Environment",
    "description": "The term ‘built environment’ broadly refers to the human-made environment that provides the setting for human activity.\n\nWithin the scope of this climate change challenge are targeted emissions produced by the construction and operation of homes, buildings, streets, urban infrastructure and spaces. \n\nSolutions to mitigate climate change and to adapt to its effects in this challenge include construction materials, ecodesign, smart city technologies, building management systems, air quality management and others.\n"
  },
  {
    "id": 275,
    "label": "Industry",
    "description": "Industry includes sectors of the economy that mainly produce capital goods to be used in manufacturing.\n\nThe scope of this challenge includes the manufacturing of petrochemicals and plastics, electrical and electronics, textile & fashion, chemicals, heavy machinery and equipment, pharmaceuticals among other sectors of the economy.\n\nSolutions to mitigate climate change and to adapt to its effects in this challenge include electrical equipment manufacturing, industrial efficiency software, automated manufacturing processes, 3D printing and others.\n"
  },
  {
    "id": 347,
    "label": "Solutions map",
    "description": "The Solutions Map simplifies your exploration of climate tech solutions. We've categorized over 200 solutions into Challenge Areas like Energy, Industry, Transport, and more. When you choose a solution, you can dive into its sub-solutions if they exist. You can also access insights, active investors, and information about startups and SMEs for each solution."
  },
  {
    "id": 348,
    "label": "Cement and Concrete",
    "description": "This solution map is focused on climate technologies in Cement and Concrete. From alternative cementitious materials like fly ash and slag to cutting-edge production enhancements such as carbon capture technologies, the page covers a wide spectrum of solutions. Delve into information about the entire value chain, gaining insights into sustainable practices from raw material extraction to final disposal."
  },
  {
    "id": 359,
    "label": "Deep Dives map",
    "description": "The Deep Dives offers a meticulous mapping of the most innovative and extensively researched fields in the realm of Climate Tech. These curated maps serve as a direct, technologically advanced interface, simplifying navigation through the intricate landscape of climate technology. Users can seamlessly delve into specific areas such as Cement and Concrete, Carbon Offset and Markets, Marine Energy, and Hydrogen, gaining valuable insights into advancements, sub-solutions, and active investors. "
  },
  {
    "id": 360,
    "label": "Cement Value Chain",
    "description": "The Cement Value Chain includes the following steps Clinker Production, Cement Grinding, Concrete Production, and Concrete Recycling. Each step comprises innovation to decrease the GHG emissions for the Cement and Concrete industry."
  },
  {
    "id": 363,
    "label": "Concrete Production",
    "description": "Concrete production is witnessing transformative innovations in the field of carbon capture and utilization (CCU) technologies, involving CO2 injection and carbon curing. Advanced concrete formulations incorporate supplementary cementitious materials (SCMs) such as fly ash and slag, lowering the carbon intensity of concrete. Moreover, the integration of recycled aggregates, sourced from demolished structures, significantly diminishes the environmental impact of concrete production. "
  },
  {
    "id": 462,
    "label": "Carbon Capture, Utilization and Storage (CCUS)",
    "description": "Carbon Capture, Utilization, and Storage (CCUS) is the process of capturing carbon dioxide (CO2) emissions from fossil power generation and industrial processes for storage deep underground or re-use. The scope of this sector includes companies and activities related to carbon capture from industrial emissions or flue gas, usage (CCU), and storage (CCS). Some innovations within this technology include energy-efficient capture units, mineralization technologies, carbon storage in materials such as cement, etc. "
  },
  {
    "id": 660,
    "label": "Software map",
    "description": "The Software Map is a comprehensive visual representation that outlines the diverse array of software solutions within the climate tech landscape. This map provides a detailed overview of software applications tailored to address climate challenges across various sectors, including energy, transport, industry, food and agriculture, built environment, natural environment, and more. "
  }
]
```

To get the taxonomy items of the company you should use the following endpoint:

`GET /taxonomy/items/company/{clientID}`

Where the parameter `clientID` is the ID of the company.

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Taxonomy Item Relations by ParentID

> To get Taxonomy Graph Item Relation list by parentID, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/taxonomy/relations/parent/1' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN' \
-H 'Content-Type: application/json' \                 
```

> In case of a 200 response, the response body will contain all the available taxonomy graph item relations, with the JSON structured like the following:

```json
[
  {
    "id": 0,
    "parentID": 1,
    "childID": 3,
    "parentLabel": "Alternative Fuell",
    "childLabel": "Electrofuels"
  },
  {
    "id": 1,
    "parentID": 1,
    "childID": 4,
    "parentLabel": "Alternative Fuell",
    "childLabel": "Synthetic Fuel"
  }
]
```

To get all the parent-children relations of a taxonomy item you should use the following endpoint:

`GET /relations/parent/{itemID}`

Where the parameter `itemID` is the taxonomy item ID.

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |

## Taxonomy Item Relations by ChildID

> To get Taxonomy Graph Item Relation list by childID, use this code:

```shell
curl -v -X GET 'https://api-new.netzeroinsights.com/taxonomy/relations/child/24' \
-H 'Authorization: Bearer EXAMPLE_ACCESS_TOKEN' \
-H 'Content-Type: application/json' \                 
```

> In case of a 200 response, the response body will contain all the available taxonomy graph item relations, with the JSON structured like the following:

```json
[
  {
    "id": 0,
    "parentID": 22,
    "childID": 24,
    "parentLabel": "Solar Energy",
    "childLabel": "Photovoltaic"
  }
]
```

To get all the child-parents relations of a taxonomy item you should use the following endpoint:

`GET /relations/child/{itemID}`

Where the parameter `itemID` is the taxonomy item ID.

The possible response codes are:

| Response code | Meaning            |
|---------------|--------------------|
| 200           | Request successful |
