# Direct Offerlink CPA/Mobile Content API
### Context
 * This documentation is intended to help you integrate Mobrand's "CPA/Mobile Content" offers API Feeds.
 * You will find instructions on how to integrate Mobrand's General API Feed.
 
###### Note: If you are an Account Manager and you are reading this, please do not be scared and pass it to a tech guy as they will for sure understand it.

### Endpoint
 * General API Feed URL: https://api.mobrand.net/{YOURUSERID}/cpa/bulk/liveoffers/{sourceid/appid}
 * This Endpoint will only respond to GET.
 * All responses are in JSON.
 * Single Request. Paging not available.
###### JWT can be sent on the query String:
``https://api.mobrand.net/{YOURUSERID}/cpa/bulk/liveoffers/{sourceid/appid}?jwt={APIKEY}``
###### JWT can also be sent on Authorization request header field:
``Authorization: Bearer {APIKEY}``
### Filters
| Parameters | Type | Description |
|-|-|-|
| incent | Boolean | Show only incent / non-incent traffic |
| adult | Boolean | Show only adult / mainstream |
| wifi | Boolean | Show only wifi campaigns |
| min_payout | Decimal | Minimum value of the payouts to show |
| max_payout | Decimal | Maximum value of the payouts to show |
| platform | String | Show only "android" or "ios" or "desktop" or "windowsphone" |
| geos | String | ISO 3166 two-letter country codes, separated by comma |
| preview | Boolean | Show only campaigns with preview url |
##### Example Request:
``https://api.mobrand.net/{YOURUSERID}/cpa/bulk/liveoffers/{sourceid/appid}?jwt={APIKEY}&incent=false&min_payout=0.8``

To show all the offers (no filter), just omit the arguments.

### Response
#### Example Response:
```
{
    "sourceid": "{sourceid}",
    "campaigns": [
        {
            "id": "HVgTEjQ4HBQxQ2JgZFRr",
            "name": "H3G | rofl-vids.com (iPhone, Android) AT - Non incent",
            "incent": false,
            "previewUrl": "http://staticp.mobrand.net/creative/aHR0cDovL2NwYS50YXBnZXJpbmUuY29tL2NyZWF0aXZlL3BOTE5ZYldZTDRrQXNrSzhTYlpqSFp5M1hNYjVxUEpsTWVUbHlhZUY=",
            "iconUrl": "http://staticp.mobrand.net/creative/aHR0cDovL2NwYS50YXBnZXJpbmUuY29tL2NyZWF0aXZlL3BOTE5ZYldZTDRrQXNrSzhTYlpqSFp5M1hNYjVxUEpsTWVUbHlhZUY=",
            "clickUrl": "https://t.go2offer.link/tracking/superlink/{userid}/{sourceid}?tencadid=HVgTEjQ4HBQxQ2JgZFRr",
            "platforms": [
                "iPhone",
                "Android"
            ],
            "adult": false,
            "countries": [
                {
                    "country": "at",
                    "carriers": [
                        {
                            "mcc": "232",
                            "mnc": "10"
                        },
                        {
                            "mcc": "232",
                            "mnc": "14"
                        },
                        {
                            "mcc": "232",
                            "mnc": "05"
                        },
                        {
                            "mcc": "232",
                            "mnc": "12"
                        },
                        {
                            "mcc": "232",
                            "mnc": "06"
                        }
                    ],
                    "payout": 6.0,
                    "wifi": true
                }
            ]
        },
....
    ]
}
```

### Response description
| Field | Type | Description |
|-|-|-|
| campaigns | Array | Description and Info about an App |
| id | String | Campaign ID |
| name | String | The name of the offer |
| previewUrl | String | URL of the preview |
| iconUrl | String | URL of the icon |
| platforms | String[] | Platforms available |
| incent | Boolean | True allows incent traffic, filter available. |
| adult | Boolean | True allows adult traffic, filter available. |
| countries | Country[] | A list of possible countries |
| blackListedSources | String[] | Sources on this list can't convert on that offer |
| whiteListedSources | String[] | Only sources on this list can convert on that offer |
| caps | Cap[] | A list of possible Caps , can be null |

Cap object

| Field | Type | Description |
|-|-|-|
| type | Array | "Installs" or "$" |
| title | Decimal | Possible values: "Monthly Cap","Daily Cap","Daily Budget","Monthly Budget" |
| amount | Decimal | The amount to reach before the offer is capped. |

Country object

| Field | Type | Description |
|-|-|-|
| country | String | ISO 3166 two-letter country codes |
| clickUrl | String | URL of the click/tracking link |
| payout | Decimal | The payout of the campaign in the country |
| wifi | Boolean | True allows wifi traffic |
| carriers | Carrier[] | A list of possible carriers, if empty it doesn't target carriers, only wifi |

Carrier object

| Field | Type | Description |
|-|-|-|
| mcc | String | Mobile Country Codes |
| mnc | String | Mobile Network Code |

Platforms object

| Platforms |
|-|
| Android |
| iPhone |
| Desktop |
| WindowsPhone |
| Kindle |
| BlackBerry |
| iPod |
| Nitendo |
| Symbian |
| Playstation |


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

```https://t.go2offer.link/tracking/superlink/{YOURUSERID}/{sourceid}?tencadid=HVgTEjQ4HBQxQ2JgZFRraff_sub=947017de-e150-11e5-b86d-9a79f06e9478&source=thebestsource&idfa=AEBE52E7-03EE-455A-B3C4-E57283966239&android_id=android_id_hash&advid=96bd03b6-defc-4203-83d3-dc1c730801f7&source_app=CandyCrush```
