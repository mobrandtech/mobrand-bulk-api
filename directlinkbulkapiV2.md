# Direct Offerlink API
### Context
 * This documentation is intended to help you integrate Mobrand's offers API Feeds.
 * You will find instructions on how to make the integration.
 * If you are unsure which URL path to use please start by integrating the General API Feed.
 
###### Note: If you are an Account Manager and you are reading this, please do not be scared and pass it to a tech guy as they will for sure understand it.

### Endpoint
 * YOUR API Feed URL: https://api.mobrand.net/{YOURUSERID}/bulk/liveoffers/v3/{YOURSOURCEID}?apikey={YOURAPIKEY}
 * This Endpoint will only respond to GET.
 * All responses are in JSON.
 * Single Request. Paging not available.

| Field | Type | value |
|-|-|-|
|   url  | string | https://api.mobrand.net/{userid}/bulk/liveoffers/v3/{sourceid}?apikey={apiKey} |
| userid | String | {YOURUSERID} |
| sourceid | String | {YOURSOURCEID} |
| apiKey | String | {YOURAPIKEY} |

### Response
#### Example Response:
```

    "sourceid": "tSDe58XoQwKDzvg7fSPSSA",
    "campaigns": [
        {
          icon: "http://is3.mzstatic.com/image/thumb/Purple122/v4/83/0d/58/830d584b-ca70-53b8-6689-a89f9fd5122c/source/512x512bb.jpg",
          name: "Stash Invest: Investing & Financial Education",
          platform: "ios",
          category1: "apps",
          category2: "finance",
          list: [
              {
                id: "GyoAMxwDIQluZ3AGZHddYw",
                countries: [
                  "us"
                ],
                payout: 0.44,
                incent: false,
                offerLink: "http://t.mobrand.net/tracking/aff/h_rZwbUlTTC1RGeVHTzXQg/tSDe58XoQwKDzvg7fSPSSA/GyoAMxwDIQluZ3AGZHddYw?m=2",
                caps: [
                  {
                    type: "Installs",
                    title: "Daily Cap",
                    amount: 40
                  }
                ],
                notes: "",
                offerName: "Stash Invest: Investing & Financial Education - iOS - US - CPI-Incent-US-iOS_[API]",
                reqDeviceId: false,
                kpi: "RR 30% first 24hours",
                userFlow: "STORE > DOWNLOAD > OPEN APP",
                blackListedSources: [ ],
                whiteListedSources: [ ]
              },
              {
                id: "HD4CPRIQPAIxbnUHZ3NU",
                countries: [
                  "us"
                ],
                payout: 0.22,
                incent: true,
                offerLink: "http://t.mobrand.net/tracking/aff/h_rZwbUlTTC1RGeVHTzXQg/tSDe58XoQwKDzvg7fSPSSA/HD4CPRIQPAIxbnUHZ3NU?m=2",
                caps: [ ],
                notes: "Soft incent (CR bellow 7%) | Pause immediately",
                offerName: "Stash Invest (API) (iPhone 8.0+) US - Incent",
                reqDeviceId: true ,
                kpi: null,
                userFlow: null,
                blackListedSources: [ "123","BadSource","BlackListedSource" ],
                whiteListedSources: [ "foo","goodSource","WhiteListedSource" ]
              }
          ],
          minOsVer: "8.0",
          bundleId: "1017148055"
          previewLink: "https://itunes.apple.com/app/id1017148055"
        }]
  }
```

### Response description
| Field | Type | Description |
|-|-|-|
| campaigns | Array | Description and Info about an App |
| bundleId | String | The Unique identifier of the App
| previewLink | String | The Link to the App Store
| list | Array | List of offers available for the App |
| payout | Decimal | Payout value in USD ($) |
| incent | Boolean | True allows incent traffic, filter available. |
| reqDeviceId | Boolean | if true, add &idfa= & advid= to the tracking link |
| notes | String | Campaign notes, including KPIs. Can be null. |
| blackListedSources | String[] | Sources on this list can't convert on that offer |
| whiteListedSources | String[] | Only sources on this list can convert on that offer |
| cap | Cap[] | A list of possible Caps , can be null |

Cap object

| Field | Type | Description |
|-|-|-|
| type | Array | "Installs" or "$" |
| title | Decimal | Possible values: "Monthly Cap","Daily Cap","Daily Budget","Monthly Budget" |
| amount | Decimal | The amount to reach before the offer is capped. |


### Offerlink Tracking Parameters
To get postback details and get better tracking you need to add the following parameters/arguments/macros.

|Field| Description|
|-|-|
| aff_sub    | Typically used for clickid, sent to postback |
| aff_sub2   | free macro to be sent on postback            |
| source     | for your subid                               |
| idfa       | iOS Advertising Identifier                   |
| android_id | android device id                            |
| advid      | android advertising id                       |
| source_app | Source App Name                              |

### Direct Link example:
```http://t.mobrand.net/tracking/aff/h_rZwbUlTTC1RGeVHTzXQg/_LNeaW6gQYKnKJso90PbJA/GCoQNBYWPBoxbnABa3VUZHA?m=2&aff_sub=947017de-e150-11e5-b86d-9a79f06e9478&source=thebestsource&idfa=AEBE52E7-03EE-455A-B3C4-E57283966239&android_id=android_id_hash&advid=96bd03b6-defc-4203-83d3-dc1c730801f7&source_app=CandyCrush```
