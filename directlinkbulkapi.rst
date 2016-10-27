########################
Directlink Bulk API
########################

This document describes how to make an API call.

You will need:
 * Your publisher ID
 * Your source/app ID (check on your My Sources/Apps dashboards)
 * A valid JWT issued by Mobrand


----------
 Endpoint
----------

^^^^^^^^^^
 Method 1
^^^^^^^^^^
``https://api.mobrand.net/{publisherId}/bulk/offers/{sourceid/appid}?jwt={validJWT}``

^^^^^^^^^^
 Method 2
^^^^^^^^^^
``https://api.mobrand.net/{publisherId}/bulk/offers/{sourceid/appid}``

Http Headers:

**Authorization**: Bearer {JWT}


Example Response:

.. code-block:: javascript

  {
  "sourceid": "tSDe58XoQwKDzvg7fSPSSA",
  "campaigns": [
    {
      "icon": "http://lh3.googleusercontent.com/-MNNMA7VPCuQAL9EEXMISd87GhMO2hJ7dV6K0j6LCE8jGhtnRQ8VdZlITTdziQvWMLw=w300",
      "name": "DomiNations",
      "platform": "android",
      "category1": "games",
      "category2": "strategy",
      "list": [
        {
          "id": "BTYcMxoNN1ZhYiUDZ3NdZ3gyH2kzVg",
          "countries": [
            "kr"
          ],
          "payout": 2.5,
          "incent": false,
          "offerLink": "http://t.mobrand.net/tracking/aff/h_rZwbUlTTC1RGeVHTzXQg/tSDe58XoQwKDzvg7fSPSSA/BTYcMxoNN1ZhYiUDZ3NdZ3gyH2kzVg",
          "caps": [
            {
              "type": "Installs",
              "title": "Daily Cap",
              "amount": 1996
            }
          ],
          "notes": "USER FLOW: \r\n1) User clicks on creative and is forwarded to Apple / Google Play Store \r\n2) User downloads the App on the phone \r\n3) User opens the App after download"
        },
        {
          "id": "ETAHOwcSPFZlZHMAan9cYw",
          "countries": [
            "hk"
          ],
          "payout": 3.38,
          "incent": false,
          "offerLink": "http://t.mobrand.net/tracking/aff/h_rZwbUlTTC1RGeVHTzXQg/tSDe58XoQwKDzvg7fSPSSA/ETAHOwcSPFZlZHMAan9cYw",
          "caps": [
            {
              "type": "Installs",
              "title": "Daily Cap",
              "amount": 50
            }
          ],
          "notes": null
        }
      ],
      "bundleId": "com.nexonm.dominations.adk"
    }]
  }


---------
 Filters
---------
^^^^^^^^^^^^^^^
 Incent offers
^^^^^^^^^^^^^^^

``https://api.mobrand.net/{publisherId}/bulk/offers/{sourceid/appid}?incent=true/false``

To show only incent offers, the argument should be incent=true.
To not show incent offers, the argument should be incent=false.

To show all the offers (no filter), just omit the argument.

------------------
 Offerlink Details
------------------

To get postback details and get better tracking you need to add the following arguments

======================  ============================================
 Arguments available:
======================  ============================================
 **aff_sub**             for click_id that will be then postbacked
 **source**              for your subid
 **idfa**                iOS Advertising Identifier
 **android_id**          android device id
 **advid**               android advertising id
======================  ============================================

^^^^^^^^^^^^^^^^^^^
 App Link example:
^^^^^^^^^^^^^^^^^^^

``http:``//t.mobrand.net/tracking/aff/h_rZwbUlTTC1RGeVHTzXQg/_LNeaW6gQYKnKJso90PbJA/GCoQNBYWPBoxbnABa3VUZHA?\ **aff_sub**\ =947017de-e150-11e5-b86d-9a79f06e9478&\ **source**\ =thebestsource&\ **idfa**\ =AEBE52E7-03EE-455A-B3C4-E57283966239&\ **android_id**\ =android_id_hash&\ **advid**\ =96bd03b6-defc-4203-83d3-dc1c730801f7
