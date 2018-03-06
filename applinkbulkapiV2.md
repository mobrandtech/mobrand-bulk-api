# App Link Bulk API
### Endpoint
#### Method 1
``https://api.mobrand.net/{publisherId}/bulk/smartoffers/{sourceid/appid}?jwt={validJWT}``
#### Method 2
``https://api.mobrand.net/{publisherId}/bulk/smartoffers/{sourceid/appid}``
##### Http Headers:
**Authorization**: Bearer {JWT}
#### Example Response:
```
{
  "sourceid": "tSDe58XoQwKDzvg7fSPSSA",
  "campaigns": [{
      "name": "DragonVale",
      "bundleId": "440045374",
      "payoutRange": {
          "min": 0.71,
          "max": 1.68
      },
      "category1": "Games",
      "category2": "Simulation",
      "appLink": "http://t.mobrand.net/tracking/smartaff/h_rZwbUlTTC1RGeVHTzXQg/tSDe58XoQwKDzvg7fSPSSA/XGtCakNXZltg",
      "appstoreLink": "https://itunes.apple.com/app/id440045374",
      "platform": "ios",
      "icon": "http://is4.mzstatic.com/image/thumb/Purple69/v4/af/6e/8c/af6e8c14-38b4-94f1-ad2d-086a1d41a10f/source/512x512bb.jpg",
      "notes": "USER FLOW: \n1) User clicks on creative and is forwarded to Apple / Google Play Store \n2) User downloads the App on the phone \n3) User opens the App after download",
      "countries": ["jp", "gb", "us"],
      "payoutRanges": {
          "jp": {
              "min": 1.15,
              "max": 1.55
          },
          "gb": {
              "min": 0.71,
              "max": 0.71
          },
          "us": {
              "min": 1.68,
              "max": 1.68
          }
      }
  }]
}
```
### Filters
#### Incent offers
``https://api.mobrand.net/{publisherId}/bulk/smartoffers/{sourceid/appid}?incent=true/false``
*  To show only incent offers, the argument should be incent=true.
*  To not show incent offers, the argument should be incent=false.

To show all the offers (no filter), just omit the argument.
###  App Link Details
To get postback details and get better tracking you need to add the following arguments
| Arguments available: | |
|-|-|
| aff_sub | Typically used for click_id,sent to postback |
| aff_sub2 | free macro to be sent on postback |
| source | for your subid |
| idfa | iOS Advertising Identifier |
| android_id | android device id |
| advid | android advertising id |

### App Link example:
```http://t.mobrand.net/tracking/smartaff/h_rZwbUlTTC1RGeVHTzXQg/_LNeaW6gQYKnKJso90PbJA/GCoQNBYWPBoxbnABa3VUZHA?aff_sub=947017de-e150-11e5-b86d-9a79f06e9478&source=thebestsource&idfa=AEBE52E7-03EE-455A-B3C4-E57283966239&android_id=android_id_hash&advid=96bd03b6-defc-4203-83d3-dc1c730801f7[&incent=true|false]```
