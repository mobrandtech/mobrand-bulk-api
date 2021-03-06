########################
Direct Link Bulk API
########################

| This document describes how to make an API call to the Direct link Bulk resource.
| An Direct Link is a Link that represents one single offer.

You will need:
 * Your publisher ID
 * Your source/app ID (check on your My Sources/Apps dashboards)
 * A valid JWT issued by Mobrand


-----------
 Endpoint
-----------
 * URL: https://api.mobrand.net/{publisherId}/bulk/liveoffers/{sourceid/appid}
 * This Endpoint will only respond to GET.
 * All responses are in JSON.
 * Single Request. Paging not available.

JWT can be sent on the query String:

  .. code-block:: none

    https://api.mobrand.net/{publisherId}/bulk/liveoffers/{sourceid/appid}?jwt={validJWT}

JWT can also be sent on Authorization request header field:

  .. code-block:: none

    Authorization: Bearer {JWT}


---------
 Filters
---------

======================  ============================  ============================================================
 Parameters                      TYPE                            Description
======================  ============================  ============================================================
 incent                         Boolean                   Show only incent / non-incent traffic
 min_payout                     Decimal                   Minimum value of the payouts to show
 max_payout                     Decimal                   Maximum value of the payouts to show
 platform                       String                    Show only "android" or "ios"
 geos                           String                    ISO 3166 two-letter country codes, separated by comma
======================  ============================  ============================================================


 Example Request:

``https://api.mobrand.net/{publisherId}/bulk/liveoffers/{sourceid/appid}?jwt={validJWT}&incent=false&min_payout=0.8``

To show all the offers (no filter), just omit the parameters.

------------
 Response
------------

Example Response:

.. code-block:: javascript

  {
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


^^^^^^^^^^^^^^^^^^^^^^
 Response description
^^^^^^^^^^^^^^^^^^^^^^

======================  ========================  ==============================================================
 FIELD                      TYPE                            Description
======================  ========================  ==============================================================
 campaigns                      Array                      Description and Info about an App
 bundleId                       String                      The Unique identifier of the App
 previewLink                    String                      The Link to the App Store
 list                           Array                     List of offers available for the App
 payout                         Decimal                      Payout value in USD ($)
 incent                         Boolean                   True allows incent traffic, filter available.
 reqDeviceId                    Boolean                   if true, add &idfa= & advid= to the tracking link
 notes                          String                   Campaign notes, including KPIs. Can be null.
 blackListedSources             String[]             Sources on this list can't convert on that offer
 whiteListedSources             String[]             Only sources on this list can convert on that offer
======================  ========================  ==============================================================


------------------
 Offerlink Details
------------------

To get postback details and get better tracking you need to add the following parameters/arguments/macros

======================  ==============================================
 Arguments available:
======================  ==============================================
 **aff_sub**             Typically used for click_id,sent to postback
 **aff_sub2**            free macro to be sent on postback
 **source**              for your subid
 **idfa**                iOS Advertising Identifier
 **android_id**          android device id
 **advid**               android advertising id
======================  ==============================================

^^^^^^^^^^^^^^^^^^^^^^
 Direct Link example:
^^^^^^^^^^^^^^^^^^^^^^

``http:``//t.mobrand.net/tracking/aff/h_rZwbUlTTC1RGeVHTzXQg/_LNeaW6gQYKnKJso90PbJA/GCoQNBYWPBoxbnABa3VUZHA?m=2&\ **aff_sub**\ =947017de-e150-11e5-b86d-9a79f06e9478&\ **source**\ =thebestsource&\ **idfa**\ =AEBE52E7-03EE-455A-B3C4-E57283966239&\ **android_id**\ =android_id_hash&\ **advid**\ =96bd03b6-defc-4203-83d3-dc1c730801f7
