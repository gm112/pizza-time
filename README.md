# Meeting Guide API Analysis

## Purpose

This document is to outline the functionality and response data provided by [Alcoholics Anonymous](https://www.aa.org/meeting-guide-app). Using this data, one can extract all known meeting information at any given time. As of the time of this writing, this document is accurate to the calling API Interface that is used by the MeetingGuide App.

## API Interface

### Public Callable Endpoint

The current endpoint is hosted on `api.meetingguide.org`, with one callable endpoint.

### Meeting Directory Endpoint

#### Requirements

There are no authentication requirements that are enforced from the endpoint. This document would like to point out that there is a field within the query string on the HTTP URL. It is currently stored as the `key` field in the Request (see below).

**PLEASE NOTE:** This value may change over time. Currently this endpoint was tested WITHOUT the presence of the `key` field, and the endpoint did in fact work. It is **RECOMMENDED** to keep the value in as part of the request to conform to the behavior of the MeetingGuide App.

#### HTTP Headers

Currently, the only known header to be unique to this request is to specify a specific User Agent, with the following value.

```HTTP
User-Agent: MeetingGuide/1 CFNetwork/1333.0.4 Darwin/21.5.0
```

**PLEASE NOTE:** This value may change over time.

##### Meeting Directory Endpoint Request

The following fields are **query string parameters**.

```http
https://api.meetingguide.org/app/v2/request?latitude=VALUE_HERE&longitude=VALUE_HERE&search=VALUE_HERE&radius=VALUE_HERE&language=VALUE_HERE&key=VALUE_HERE
```

| Field  | Type  | Description  | Notes  |
| ---    | ---   | ---          | ---    |
| latitude       | number      | GPS latitude value of the origin search point             | Example: `41.428327476644355`       |
| longitude       | number      | GPS longitude value of the origin search point             | Example: `-81.74036180608137`        |
| search       | string      | Unknown             | This value always seemed to be empty, so it is likely unused.       |
| radius       | number      | Search radius from the provided latitude/longitude             | Example: `25`. Seems to default to `64`.       |
| language       | string      | Spoken language of meeting directory             | Hard coded to `en` seemingly from the client. Unable to produce another value here.       |
| key       | string      | The API Key granted to the Meeting Guide App on iOS.             | Hard coded to `gPjHLUKZj?XMdQ2PvDyaUFXXXTD?JAhB`.       |

##### Meeting Directory Endpoint Request Example

```bash
curl -k -i --raw -o 0.dat "https://api.meetingguide.org/app/v2/request?latitude=41.428327476644355&longitude=-81.74036180608137&search=&radius=24&language=en&key=gPjHLUKZj?XMdQ2PvDyaUFXXXTD?JAhB" -H "Host: api.meetingguide.org" -H "Accept: */*" -H "Accept-Language: en-US,en;q=0.9" -H "Connection: keep-alive" -H "Accept-Encoding: gzip, deflate, br" -H "User-Agent: MeetingGuide/1 CFNetwork/1333.0.4 Darwin/21.5.0"
```

##### Meeting Directory Endpoint Response

The response object is made up of the [MeetingGuideApiV2Response](interfaces/MeetingGuideApiV2Response.md) object, which is a JSON Object that contains objects of several other types. 

##### Types

- [MeetingGuideApiV2Response](interfaces/MeetingGuideApiV2Response.md)
- [Meeting](interfaces/Meeting.md)
- [News](interfaces/News.md)
- [Organization](interfaces/Organization.md)

##### Example Response JSON

```JSON
{
  "organizations": [
    {
      "id": 282,
      "name": "Akron Intergroup Council",
      "url": "https://akronaa.org/",
      "phone": "+13302538181",
      "email": "info@akronaa.org",
      "location": "Akron, OH, USA",
      "latitude": "41.10651860",
      "longitude": "-81.51041950",
      "address": "775 N Main St, Akron, OH 44310, USA",
      "image_url": null,
      "image_width": null,
      "image_height": null,
      "country": "US",
      "published_at": "2019-04-08",
      "distance": null
    },
    {
      "id": 604,
      "name": "Lorain Inter-Group Office",
      "url": "https://aalorain.org/",
      "phone": "+14402461800",
      "email": "webmaster@aaloraincounty.org",
      "location": "Lorain County, OH, USA",
      "latitude": null,
      "longitude": null,
      "address": null,
      "image_url": null,
      "image_width": null,
      "image_height": null,
      "country": "US",
      "published_at": "2020-10-14",
      "distance": null
    },
    {
      "id": 287,
      "name": "AA Cleveland",
      "url": "https://www.aacle.org",
      "phone": "+12162417387",
      "email": "webmaster@aacleve.org",
      "location": "Cleveland, OH, USA",
      "latitude": "41.50712070",
      "longitude": "-81.68444970",
      "address": "1557 St Clair Ave NE, Cleveland, OH 44114, USA",
      "image_url": null,
      "image_width": null,
      "image_height": null,
      "country": "US",
      "published_at": null,
      "distance": 9.92
    }
  ],
  "meetings": [
    {
      "id": 631087,
      "name": "Brecksville Wednesday",
      "notes": null,
      "day": 3,
      "time": "19:00:00",
      "end_time": "20:00:00",
      "time_periods": [
        "evening"
      ],
      "url": "https://akronaa.org/meetings/brecksville-wednesday/",
      "types": "Big Book,Open",
      "updated_at": "2021-07-21 21:48:00",
      "group": null,
      "group_notes": null,
      "venmo": null,
      "paypal": null,
      "square": null,
      "conference_provider": null,
      "conference_url": null,
      "conference_url_notes": null,
      "conference_phone": null,
      "conference_phone_notes": null,
      "organization_id": 282,
      "organization": "Akron Intergroup Council",
      "distance": 15.21,
      "location_id": 806498,
      "location": "Brecksville United Methodist Church",
      "location_notes": "Room 301",
      "latitude": "41.32090590",
      "longitude": "-81.62744030",
      "formatted_address": "65 Public Square, Brecksville, OH 44141, USA",
      "address": "65 Public Square",
      "city": "Brecksville",
      "state": "OH",
      "postal_code": "44141",
      "approximate": 0,
      "county": "Cuyahoga County",
      "country": "US",
      "timezone": "America/New_York"
    },
    {
      "id": 1096013,
      "name": "(O) Columbia Station Group",
      "notes": "GSN-000136107 Area 54 District 19A",
      "day": 6,
      "time": "20:30:00",
      "end_time": "21:30:00",
      "time_periods": [
        "evening",
        "night"
      ],
      "url": "https://aalorain.org/meetings/o-columbia-station-group/",
      "types": "Open,Speaker",
      "updated_at": "2022-02-12 17:23:18",
      "group": null,
      "group_notes": null,
      "venmo": null,
      "paypal": null,
      "square": null,
      "conference_provider": null,
      "conference_url": null,
      "conference_url_notes": null,
      "conference_phone": null,
      "conference_phone_notes": null,
      "organization_id": 604,
      "organization": "Lorain Inter-Group Office",
      "distance": 19.72,
      "location_id": 814998,
      "location": "Hosanna Lutheran Church",
      "location_notes": "",
      "latitude": "41.31688950",
      "longitude": "-81.92429620",
      "formatted_address": "13485 W River Rd, Columbia Station, OH 44028, USA",
      "address": "13485 West River Road",
      "city": "Columbia Station",
      "state": "OH",
      "postal_code": "44028",
      "approximate": 0,
      "county": "Lorain County",
      "country": "US",
      "timezone": "America/New_York"
    },
    {
      "id": 643089,
      "name": "Western Reserve 12&12 Discussion",
      "notes": null,
      "day": 1,
      "time": "19:30:00",
      "end_time": "20:30:00",
      "time_periods": [
        "evening"
      ],
      "url": "https://akronaa.org/meetings/western-reserve-1212-discussion/",
      "types": "Closed,Step Meeting",
      "updated_at": "2021-08-18 00:28:00",
      "group": null,
      "group_notes": null,
      "venmo": null,
      "paypal": null,
      "square": null,
      "conference_provider": null,
      "conference_url": null,
      "conference_url_notes": null,
      "conference_phone": null,
      "conference_phone_notes": null,
      "organization_id": 282,
      "organization": "Akron Intergroup Council",
      "distance": 20.29,
      "location_id": 807548,
      "location": "Ferfolia Funeral Home",
      "location_notes": "",
      "latitude": "41.31360370",
      "longitude": "-81.55120110",
      "formatted_address": "356 W Aurora Rd, Northfield, OH 44067, USA",
      "address": "356 West Aurora Road",
      "city": "Northfield",
      "state": "OH",
      "postal_code": "44067",
      "approximate": 0,
      "county": "Summit County",
      "country": "US",
      "timezone": "America/New_York"
    },
    {
      "id": 652641,
      "name": "Sagamore Mixed Discussion",
      "notes": null,
      "day": 4,
      "time": "20:00:00",
      "end_time": "21:00:00",
      "time_periods": [
        "evening",
        "night"
      ],
      "url": "https://akronaa.org/meetings/sagamore-mixed-discussion/",
      "types": "Closed,Discussion",
      "updated_at": "2021-09-10 18:42:00",
      "group": null,
      "group_notes": null,
      "venmo": null,
      "paypal": null,
      "square": null,
      "conference_provider": null,
      "conference_url": null,
      "conference_url_notes": null,
      "conference_phone": null,
      "conference_phone_notes": null,
      "organization_id": 282,
      "organization": "Akron Intergroup Council",
      "distance": 20.54,
      "location_id": 808835,
      "location": "Northfield Presbyterian Church",
      "location_notes": "Basement Fellowship Hall",
      "latitude": "41.31305030",
      "longitude": "-81.54797490",
      "formatted_address": "7755 S Boyden Rd, Northfield, OH 44067, USA",
      "address": "7755 South Boyden Road",
      "city": "Northfield",
      "state": "OH",
      "postal_code": "44067",
      "approximate": 0,
      "county": "Summit County",
      "country": "US",
      "timezone": "America/New_York"
    },
    {
      "id": 617943,
      "name": "Alcoholics Only",
      "notes": null,
      "day": 1,
      "time": "19:00:00",
      "end_time": "20:00:00",
      "time_periods": [
        "evening"
      ],
      "url": "https://akronaa.org/meetings/alcoholics-only/",
      "types": "",
      "updated_at": "2022-05-05 13:32:38",
      "group": null,
      "group_notes": null,
      "venmo": null,
      "paypal": null,
      "square": null,
      "conference_provider": null,
      "conference_url": null,
      "conference_url_notes": null,
      "conference_phone": null,
      "conference_phone_notes": null,
      "organization_id": 282,
      "organization": "Akron Intergroup Council",
      "distance": 21.33,
      "location_id": 805393,
      "location": "St. Barnabas School",
      "location_notes": "Rectory basement. Enter the south side of the rectory.",
      "latitude": "41.31130960",
      "longitude": "-81.53779860",
      "formatted_address": "9457 Brandywine Rd, Northfield, OH 44067, USA",
      "address": "9457 Brandywine Road",
      "city": "Northfield",
      "state": "OH",
      "postal_code": "44067",
      "approximate": 0,
      "county": "Summit County",
      "country": "US",
      "timezone": "America/New_York"
    },
    {
      "id": 618279,
      "name": "Keep the Focus Big Book",
      "notes": null,
      "day": 3,
      "time": "20:00:00",
      "end_time": "21:00:00",
      "time_periods": [
        "evening",
        "night"
      ],
      "url": "https://akronaa.org/meetings/keep-the-focus-big-book/",
      "types": "Big Book,Men,Open",
      "updated_at": "2021-06-30 00:19:00",
      "group": null,
      "group_notes": null,
      "venmo": null,
      "paypal": null,
      "square": null,
      "conference_provider": null,
      "conference_url": null,
      "conference_url_notes": null,
      "conference_phone": null,
      "conference_phone_notes": null,
      "organization_id": 282,
      "organization": "Akron Intergroup Council",
      "distance": 21.36,
      "location_id": 805479,
      "location": "St. Barnabas Rectory",
      "location_notes": "",
      "latitude": "41.31117880",
      "longitude": "-81.53740940",
      "formatted_address": "9451 Brandywine Rd, Northfield, OH 44067, USA",
      "address": "9451 Brandywine Road",
      "city": "Northfield",
      "state": "OH",
      "postal_code": "44067",
      "approximate": 0,
      "county": "Summit County",
      "country": "US",
      "timezone": "America/New_York"
    },
    {
      "id": 527669,
      "name": "(C) North Ridgeville Friday Night Discussion",
      "notes": null,
      "day": 5,
      "time": "20:30:00",
      "end_time": "21:30:00",
      "time_periods": [
        "evening",
        "night"
      ],
      "url": "https://aalorain.org/meetings/c-north-ridgeville-friday-night-discussion/",
      "types": "Closed",
      "updated_at": "2021-03-07 21:49:37",
      "group": null,
      "group_notes": null,
      "venmo": null,
      "paypal": null,
      "square": null,
      "conference_provider": null,
      "conference_url": null,
      "conference_url_notes": null,
      "conference_phone": null,
      "conference_phone_notes": null,
      "organization_id": 604,
      "organization": "Lorain Inter-Group Office",
      "distance": 22.25,
      "location_id": 28198,
      "location": "Starting Point Worship Center",
      "location_notes": "",
      "latitude": "41.39349820",
      "longitude": "-82.00319160",
      "formatted_address": "34881 Center Ridge Rd, North Ridgeville, OH 44039, USA",
      "address": "34881 Center Ridge Road",
      "city": "North Ridgeville",
      "state": "OH",
      "postal_code": "44039",
      "approximate": 0,
      "county": "Lorain County",
      "country": "US",
      "timezone": "America/New_York"
    },
    {
      "id": 599518,
      "name": "(C)North Ridgeville Big Book Discussion",
      "notes": null,
      "day": 4,
      "time": "20:00:00",
      "end_time": "21:00:00",
      "time_periods": [
        "evening",
        "night"
      ],
      "url": "https://aalorain.org/meetings/cnorth-ridgeville-big-book-discussion/",
      "types": "Big Book,Closed,Discussion",
      "updated_at": "2021-05-05 16:03:59",
      "group": null,
      "group_notes": null,
      "venmo": null,
      "paypal": null,
      "square": null,
      "conference_provider": null,
      "conference_url": null,
      "conference_url_notes": null,
      "conference_phone": null,
      "conference_phone_notes": null,
      "organization_id": 604,
      "organization": "Lorain Inter-Group Office",
      "distance": 22.25,
      "location_id": 28198,
      "location": "Starting Point Worship Center",
      "location_notes": "",
      "latitude": "41.39349820",
      "longitude": "-82.00319160",
      "formatted_address": "34881 Center Ridge Rd, North Ridgeville, OH 44039, USA",
      "address": "34881 Center Ridge Road",
      "city": "North Ridgeville",
      "state": "OH",
      "postal_code": "44039",
      "approximate": 0,
      "county": "Lorain County",
      "country": "US",
      "timezone": "America/New_York"
    },
    {
      "id": 605087,
      "name": "(O-W) Women Helping Women",
      "notes": null,
      "day": 5,
      "time": "18:00:00",
      "end_time": "19:00:00",
      "time_periods": [
        "evening"
      ],
      "url": "https://aalorain.org/meetings/o-w-women-helping-women/",
      "types": "Open,Women",
      "updated_at": "2021-05-17 15:08:37",
      "group": null,
      "group_notes": null,
      "venmo": null,
      "paypal": null,
      "square": null,
      "conference_provider": null,
      "conference_url": null,
      "conference_url_notes": null,
      "conference_phone": null,
      "conference_phone_notes": null,
      "organization_id": 604,
      "organization": "Lorain Inter-Group Office",
      "distance": 22.25,
      "location_id": 28198,
      "location": "Starting Point Worship Center",
      "location_notes": "",
      "latitude": "41.39349820",
      "longitude": "-82.00319160",
      "formatted_address": "34881 Center Ridge Rd, North Ridgeville, OH 44039, USA",
      "address": "34881 Center Ridge Road",
      "city": "North Ridgeville",
      "state": "OH",
      "postal_code": "44039",
      "approximate": 0,
      "county": "Lorain County",
      "country": "US",
      "timezone": "America/New_York"
    },
    {
      "id": 1166683,
      "name": "(C-W) Lead The Way",
      "notes": null,
      "day": 6,
      "time": "09:00:00",
      "end_time": "10:00:00",
      "time_periods": [
        "morning"
      ],
      "url": "https://aalorain.org/meetings/c-w-lead-the-way/",
      "types": "Closed,Speaker,Women",
      "updated_at": "2022-03-15 16:10:23",
      "group": null,
      "group_notes": null,
      "venmo": null,
      "paypal": null,
      "square": null,
      "conference_provider": null,
      "conference_url": null,
      "conference_url_notes": null,
      "conference_phone": null,
      "conference_phone_notes": null,
      "organization_id": 604,
      "organization": "Lorain Inter-Group Office",
      "distance": 22.25,
      "location_id": 28198,
      "location": "Starting Point Worship Center",
      "location_notes": "",
      "latitude": "41.39349820",
      "longitude": "-82.00319160",
      "formatted_address": "34881 Center Ridge Rd, North Ridgeville, OH 44039, USA",
      "address": "34881 Center Ridge Road",
      "city": "North Ridgeville",
      "state": "OH",
      "postal_code": "44039",
      "approximate": 0,
      "county": "Lorain County",
      "country": "US",
      "timezone": "America/New_York"
    },
    {
      "id": 525302,
      "name": "Richfield Discussion Group",
      "notes": null,
      "day": 1,
      "time": "20:00:00",
      "end_time": "21:00:00",
      "time_periods": [
        "evening",
        "night"
      ],
      "url": "https://akronaa.org/meetings/richfield-discussion-group/",
      "types": "Closed,Discussion",
      "updated_at": "2020-10-05 17:25:00",
      "group": null,
      "group_notes": null,
      "venmo": null,
      "paypal": null,
      "square": null,
      "conference_provider": null,
      "conference_url": null,
      "conference_url_notes": null,
      "conference_phone": null,
      "conference_phone_notes": null,
      "organization_id": 282,
      "organization": "Akron Intergroup Council",
      "distance": 22.61,
      "location_id": 49014,
      "location": "Richfield United Church of Christ",
      "location_notes": "",
      "latitude": "41.23822300",
      "longitude": "-81.64406200",
      "formatted_address": "4340 W Streetsboro Rd, Richfield, OH 44286, USA",
      "address": "4340 West Streetsboro Road",
      "city": "Richfield",
      "state": "OH",
      "postal_code": "44286",
      "approximate": 0,
      "county": "Summit County",
      "country": "US",
      "timezone": "America/New_York"
    },
    {
      "id": 554152,
      "name": "Richfield Big Book",
      "notes": null,
      "day": 3,
      "time": "19:30:00",
      "end_time": "20:30:00",
      "time_periods": [
        "evening"
      ],
      "url": "https://akronaa.org/meetings/big-book-815-richfield/",
      "types": "Closed,Discussion",
      "updated_at": "2020-12-23 23:26:00",
      "group": null,
      "group_notes": null,
      "venmo": null,
      "paypal": null,
      "square": null,
      "conference_provider": null,
      "conference_url": null,
      "conference_url_notes": null,
      "conference_phone": null,
      "conference_phone_notes": null,
      "organization_id": 282,
      "organization": "Akron Intergroup Council",
      "distance": 22.61,
      "location_id": 49014,
      "location": "Richfield United Church of Christ",
      "location_notes": "",
      "latitude": "41.23822300",
      "longitude": "-81.64406200",
      "formatted_address": "4340 W Streetsboro Rd, Richfield, OH 44286, USA",
      "address": "4340 West Streetsboro Road",
      "city": "Richfield",
      "state": "OH",
      "postal_code": "44286",
      "approximate": 0,
      "county": "Summit County",
      "country": "US",
      "timezone": "America/New_York"
    },
    {
      "id": 621328,
      "name": "West Richfield",
      "notes": null,
      "day": 6,
      "time": "20:00:00",
      "end_time": "21:00:00",
      "time_periods": [
        "evening",
        "night"
      ],
      "url": "https://akronaa.org/meetings/west-richfield/",
      "types": "Open",
      "updated_at": "2021-12-13 20:28:00",
      "group": null,
      "group_notes": null,
      "venmo": null,
      "paypal": null,
      "square": null,
      "conference_provider": null,
      "conference_url": null,
      "conference_url_notes": null,
      "conference_phone": null,
      "conference_phone_notes": null,
      "organization_id": 282,
      "organization": "Akron Intergroup Council",
      "distance": 22.61,
      "location_id": 49014,
      "location": "Richfield United Church of Christ",
      "location_notes": "",
      "latitude": "41.23822300",
      "longitude": "-81.64406200",
      "formatted_address": "4340 W Streetsboro Rd, Richfield, OH 44286, USA",
      "address": "4340 West Streetsboro Road",
      "city": "Richfield",
      "state": "OH",
      "postal_code": "44286",
      "approximate": 0,
      "county": "Summit County",
      "country": "US",
      "timezone": "America/New_York"
    },
    {
      "id": 519598,
      "name": "Brunswick Monday Night Men's",
      "notes": null,
      "day": 1,
      "time": "20:00:00",
      "end_time": "21:00:00",
      "time_periods": [
        "evening",
        "night"
      ],
      "url": "https://akronaa.org/meetings/monday-night-mens/",
      "types": "Closed,Men,Wheelchair-Accessible Bathroom",
      "updated_at": "2021-10-28 00:06:00",
      "group": null,
      "group_notes": null,
      "venmo": null,
      "paypal": null,
      "square": null,
      "conference_provider": null,
      "conference_url": null,
      "conference_url_notes": null,
      "conference_phone": null,
      "conference_phone_notes": null,
      "organization_id": 282,
      "organization": "Akron Intergroup Council",
      "distance": 23.13,
      "location_id": 793414,
      "location": "12 Step Recovery Club",
      "location_notes": "",
      "latitude": "41.23512190",
      "longitude": "-81.84326900",
      "formatted_address": "1480 Pearl Rd, Brunswick, OH 44212, USA",
      "address": "1480 Pearl Road",
      "city": "Brunswick",
      "state": "OH",
      "postal_code": "44212",
      "approximate": 0,
      "county": "Medina County",
      "country": "US",
      "timezone": "America/New_York"
    },
    {
      "id": 519617,
      "name": "Brunswick Ask-It-Basket",
      "notes": null,
      "day": 2,
      "time": "21:00:00",
      "end_time": "22:00:00",
      "time_periods": [
        "night"
      ],
      "url": "https://akronaa.org/meetings/brunswick-ask-it-basket/",
      "types": "Closed,Discussion,Men",
      "updated_at": "2021-07-21 16:53:00",
      "group": null,
      "group_notes": null,
      "venmo": null,
      "paypal": null,
      "square": null,
      "conference_provider": null,
      "conference_url": null,
      "conference_url_notes": null,
      "conference_phone": null,
      "conference_phone_notes": null,
      "organization_id": 282,
      "organization": "Akron Intergroup Council",
      "distance": 23.13,
      "location_id": 793414,
      "location": "12 Step Recovery Club",
      "location_notes": "",
      "latitude": "41.23512190",
      "longitude": "-81.84326900",
      "formatted_address": "1480 Pearl Rd, Brunswick, OH 44212, USA",
      "address": "1480 Pearl Road",
      "city": "Brunswick",
      "state": "OH",
      "postal_code": "44212",
      "approximate": 0,
      "county": "Medina County",
      "country": "US",
      "timezone": "America/New_York"
    },
    {
      "id": 640141,
      "name": "Brunswick Discussion",
      "notes": null,
      "day": 4,
      "time": "10:00:00",
      "end_time": "11:00:00",
      "time_periods": [
        "morning"
      ],
      "url": "https://akronaa.org/meetings/brunswick-discussion/",
      "types": "Discussion,Open",
      "updated_at": "2021-08-12 22:59:00",
      "group": null,
      "group_notes": null,
      "venmo": null,
      "paypal": null,
      "square": null,
      "conference_provider": null,
      "conference_url": null,
      "conference_url_notes": null,
      "conference_phone": null,
      "conference_phone_notes": null,
      "organization_id": 282,
      "organization": "Akron Intergroup Council",
      "distance": 23.13,
      "location_id": 793414,
      "location": "12 Step Recovery Club",
      "location_notes": "",
      "latitude": "41.23512190",
      "longitude": "-81.84326900",
      "formatted_address": "1480 Pearl Rd, Brunswick, OH 44212, USA",
      "address": "1480 Pearl Road",
      "city": "Brunswick",
      "state": "OH",
      "postal_code": "44212",
      "approximate": 0,
      "county": "Medina County",
      "country": "US",
      "timezone": "America/New_York"
    },
    {
      "id": 640192,
      "name": "Brunswick Wednesday",
      "notes": null,
      "day": 3,
      "time": "20:00:00",
      "end_time": "21:00:00",
      "time_periods": [
        "evening",
        "night"
      ],
      "url": "https://akronaa.org/meetings/brunswick-wednesday/",
      "types": "Open",
      "updated_at": "2021-08-12 23:02:00",
      "group": null,
      "group_notes": null,
      "venmo": null,
      "paypal": null,
      "square": null,
      "conference_provider": null,
      "conference_url": null,
      "conference_url_notes": null,
      "conference_phone": null,
      "conference_phone_notes": null,
      "organization_id": 282,
      "organization": "Akron Intergroup Council",
      "distance": 23.13,
      "location_id": 793414,
      "location": "12 Step Recovery Club",
      "location_notes": "",
      "latitude": "41.23512190",
      "longitude": "-81.84326900",
      "formatted_address": "1480 Pearl Rd, Brunswick, OH 44212, USA",
      "address": "1480 Pearl Road",
      "city": "Brunswick",
      "state": "OH",
      "postal_code": "44212",
      "approximate": 0,
      "county": "Medina County",
      "country": "US",
      "timezone": "America/New_York"
    },
    {
      "id": 640193,
      "name": "Saturday AM 12x12 Brunswick",
      "notes": null,
      "day": 6,
      "time": "10:00:00",
      "end_time": "11:00:00",
      "time_periods": [
        "morning"
      ],
      "url": "https://akronaa.org/meetings/saturday-am-12x12-brunswick/",
      "types": "Discussion,Open",
      "updated_at": "2021-08-12 23:04:00",
      "group": null,
      "group_notes": null,
      "venmo": null,
      "paypal": null,
      "square": null,
      "conference_provider": null,
      "conference_url": null,
      "conference_url_notes": null,
      "conference_phone": null,
      "conference_phone_notes": null,
      "organization_id": 282,
      "organization": "Akron Intergroup Council",
      "distance": 23.13,
      "location_id": 793414,
      "location": "12 Step Recovery Club",
      "location_notes": "",
      "latitude": "41.23512190",
      "longitude": "-81.84326900",
      "formatted_address": "1480 Pearl Rd, Brunswick, OH 44212, USA",
      "address": "1480 Pearl Road",
      "city": "Brunswick",
      "state": "OH",
      "postal_code": "44212",
      "approximate": 0,
      "county": "Medina County",
      "country": "US",
      "timezone": "America/New_York"
    },
    {
      "id": 786511,
      "name": "Brunswick Sunday",
      "notes": null,
      "day": 0,
      "time": "20:00:00",
      "end_time": "21:00:00",
      "time_periods": [
        "evening",
        "night"
      ],
      "url": "https://akronaa.org/meetings/brunswick-sunday/",
      "types": "Open",
      "updated_at": "2021-11-02 22:11:00",
      "group": null,
      "group_notes": null,
      "venmo": null,
      "paypal": null,
      "square": null,
      "conference_provider": null,
      "conference_url": null,
      "conference_url_notes": null,
      "conference_phone": null,
      "conference_phone_notes": null,
      "organization_id": 282,
      "organization": "Akron Intergroup Council",
      "distance": 23.13,
      "location_id": 793414,
      "location": "12 Step Recovery Club",
      "location_notes": "",
      "latitude": "41.23512190",
      "longitude": "-81.84326900",
      "formatted_address": "1480 Pearl Rd, Brunswick, OH 44212, USA",
      "address": "1480 Pearl Road",
      "city": "Brunswick",
      "state": "OH",
      "postal_code": "44212",
      "approximate": 0,
      "county": "Medina County",
      "country": "US",
      "timezone": "America/New_York"
    }
  ],
  "news": [
    {
      "id": 211,
      "title": "Monthly Grapevine News - July 2022",
      "datetime": "2022-06-15 13:54:00",
      "content": "Find out What’s New and available at Grapevine.",
      "button_url": "https://www.aagrapevine.org/gvr-resources",
      "button_text": null,
      "language": "en",
      "image_url": null,
      "image_width": null,
      "image_height": null
    },
    {
      "id": 210,
      "title": "2023 Trustee-at-Large/Canada Vacancy",
      "datetime": "2022-05-25 19:04:00",
      "content": "Please click the following link to see an important announcement sent on behalf of the Trustees' Nominating Committee.",
      "button_url": "https://www.aa.org/sites/default/files/literature/En_VacancyforTrusteeatLargeCanada_0.pdf",
      "button_text": null,
      "language": "en",
      "image_url": null,
      "image_width": null,
      "image_height": null
    },
    {
      "id": 205,
      "title": "2023 Class B Vacancies",
      "datetime": "2022-05-25 18:41:00",
      "content": "Please click the following link to see an important announcement sent on behalf of the Trustees' Nominating Committee.",
      "button_url": "https://www.aa.org/sites/default/files/literature/en_2023VacancyforClassBTrustees_0.pdf",
      "button_text": null,
      "language": "en",
      "image_url": null,
      "image_width": null,
      "image_height": null
    },
    {
      "id": 202,
      "title": "2025 International Convention FAQ",
      "datetime": "2022-05-18 18:09:00",
      "content": "Frequently Asked Questions about the 2025 International Convention & Travel to Canada",
      "button_url": "https://www.aa.org/sites/default/files/literature/FAQ%202025%20International%20Convention%20(English).pdf",
      "button_text": null,
      "language": "en",
      "image_url": null,
      "image_width": null,
      "image_height": null
    },
    {
      "id": 201,
      "title": "Monthly Grapevine News - June 2022",
      "datetime": "2022-05-13 13:33:00",
      "content": "Find out What’s New and available at Grapevine.",
      "button_url": "https://www.aagrapevine.org/gvr-resources",
      "button_text": null,
      "language": "en",
      "image_url": null,
      "image_width": null,
      "image_height": null
    },
    {
      "id": 196,
      "title": "North/South Connections Virtual Special Forum — A.A. in Remote Communities call for videos",
      "datetime": "2022-05-12 15:57:00",
      "content": "We need your short videos to show during this virtual special forum focused on how A.A.’s carry the message to remote communities.\r\n\r\nThe deadline for submissions is June 1, 2022",
      "button_url": "https://www.aa.org/sites/default/files/literature/North%20South%20Call%20for%20Videos%20EN.pdf",
      "button_text": null,
      "language": "en",
      "image_url": null,
      "image_width": null,
      "image_height": null
    },
    {
      "id": 195,
      "title": "North/South Connections Virtual Special Forum — A.A. in Remote Communities Video Flyer",
      "datetime": "2022-05-12 15:44:00",
      "content": "Saturday, July 16, 2022\r\n\r\nWe hope you can join us for the upcoming North and South Virtual Special Forum about Remote Communities.",
      "button_url": "https://www.aa.org/North-South-Connections-Forum-AA-in-Remote-Communities",
      "button_text": null,
      "language": "en",
      "image_url": null,
      "image_width": null,
      "image_height": null
    },
    {
      "id": 192,
      "title": "Think you might have a drinking problem? Alcoholics Anonymous can help",
      "datetime": "2022-05-02 20:47:00",
      "content": "To help people come to their own conclusions regarding a problem with alcohol, A.A. offers a self-assessment tool, “Is A.A. for You?” It includes twelve questions to help an individual decide whether to give A.A. a try.",
      "button_url": "https://www.aa.org/sites/default/files/literature/en_pr_0522.pdf",
      "button_text": null,
      "language": "en",
      "image_url": null,
      "image_width": null,
      "image_height": null
    },
    {
      "id": 189,
      "title": "North/South Connections Virtual Special Forum — A.A. in Remote Communities",
      "datetime": "2022-04-22 19:29:00",
      "content": "We hope you can join us for the upcoming North and South Virtual Special Forum.",
      "button_url": "https://www.aa.org/sites/default/files/literature/North_South_Connection_Flyer_EN_4.pdf",
      "button_text": null,
      "language": "en",
      "image_url": null,
      "image_width": null,
      "image_height": null
    },
    {
      "id": 187,
      "title": "Monthly Grapevine News - May 2022",
      "datetime": "2022-04-18 13:56:00",
      "content": "Find out What’s New and available at Grapevine.",
      "button_url": "https://www.aagrapevine.org/gvr-resources",
      "button_text": null,
      "language": "en",
      "image_url": null,
      "image_width": null,
      "image_height": null
    },
    {
      "id": 184,
      "title": "Recovery story solicitation for the Fifth Edition of the Book Alcoholics Anonymous ―Big Book",
      "datetime": "2022-04-13 15:08:00",
      "content": "Please click the following highlighted link to find a memo regarding the recovery story solicitation for the Fifth Edition of the Book Alcoholics Anonymous ―Big Book",
      "button_url": "https://www.aa.org/sites/default/files/literature/5th_EditionBB_EN.pdf",
      "button_text": null,
      "language": "en",
      "image_url": null,
      "image_width": null,
      "image_height": null
    },
    {
      "id": 182,
      "title": "Box 4-5-9 Spring 2022",
      "datetime": "2022-04-13 13:38:00",
      "content": "This issue highlights the recent launch of G.S.O.'s new website -- redesigned and updated for a more modern look and feel. There is also information about the upcoming 75th anniversary of A.A. in the United Kingdom and how the Twelve Concepts are approaching their own 60th birthday. There is also information about openings for G.S.O. staff positions and a Call for Stories for three important new literature projects.",
      "button_url": "https://www.aa.org/sites/default/files/newsletters/F-36_Box_4-5-9_Spring_2022.pdf",
      "button_text": null,
      "language": "en",
      "image_url": null,
      "image_width": null,
      "image_height": null
    },
    {
      "id": 179,
      "title": "About AA Spring 2022",
      "datetime": "2022-04-07 17:49:00",
      "content": "About AA is the newsletter from the General Service Office of the U.S. and Canada for professionals in all fields who deal with alcoholics. This issue takes a look at \"A.A. as a Resource Around the World.\" The issue also focuses on \"Reaching Out to Mental Health Professionals\" and introduces three new Class A (nonalcoholic) trustees of A.A.'s General Service Board.",
      "button_url": "https://www.aa.org/sites/default/files/newsletters/f-13_spring2022.pdf",
      "button_text": null,
      "language": "en",
      "image_url": null,
      "image_width": null,
      "image_height": null
    },
    {
      "id": 177,
      "title": "Recovery story solicitation for the “A.A. for the Black and African-American Alcoholic\" Pamphlet Update",
      "datetime": "2022-04-06 14:42:00",
      "content": "Attached, please find a memo regarding the recovery story solicitation for the “A.A. for the Black and African-American Alcoholic\" Pamphlet Update",
      "button_url": "https://www.aa.org/sites/default/files/literature/Announcement_AA%20Blck_Afrcn_Amrcn_EN_1.pdf",
      "button_text": null,
      "language": "en",
      "image_url": null,
      "image_width": null,
      "image_height": null
    },
    {
      "id": 175,
      "title": "Recovery story solicitation for the Fourth Edition of the Big Book Alcohólicos Anónimos",
      "datetime": "2022-04-06 14:32:00",
      "content": "Attached, please find a memo regarding the recovery story solicitation for the Fourth Edition of the Big Book Alcohólicos Anónimos",
      "button_url": "https://www.aa.org/sites/default/files/literature/Announcement_4th%20Ed%20BB_EN.pdf",
      "button_text": null,
      "language": "en",
      "image_url": null,
      "image_width": null,
      "image_height": null
    },
    {
      "id": 173,
      "title": "Did you know we have two brand new A.A. Public Service Announcements?",
      "datetime": "2022-04-04 19:05:00",
      "content": "To support getting them aired, attached you will find an informational packet to guide your committee in cooperating with media outlets in your local community that received the PSAs.",
      "button_url": "https://www.aa.org/sites/default/files/literature/PI%20Info%20Packet%20EN.pdf",
      "button_text": null,
      "language": "en",
      "image_url": null,
      "image_width": null,
      "image_height": null
    },
    {
      "id": 170,
      "title": "Request for shared experience on “Inside” Sponsorship",
      "datetime": "2022-03-17 20:19:00",
      "content": "Please click the following highlighted link to see a request for shared experience from the Corrections Assignment at G.S.O.",
      "button_url": "https://www.aa.org/sites/default/files/literature/Request%20for%20Shared%20Experience%20Inside%20Sponsorship.pdf",
      "button_text": null,
      "language": "en",
      "image_url": null,
      "image_width": null,
      "image_height": null
    }
  ],
  "counts": {
    "types": {
      "Big Book": 3,
      "Open": 9,
      "Speaker": 2,
      "Closed": 9,
      "Step Meeting": 1,
      "Discussion": 7,
      "Men": 3,
      "Women": 2,
      "Wheelchair-Accessible Bathroom": 1
    },
    "days": {
      "0": 1,
      "1": 4,
      "2": 1,
      "3": 4,
      "4": 3,
      "5": 2,
      "6": 4
    },
    "time_periods": {
      "evening": 15,
      "night": 11,
      "morning": 3
    }
  }
}
```

## Meeting Guide Object

```typescript


interface Organization {
    id: number;
    name: string;
    url: string;
    phone: string;
    email: string;
    location: string;
    latitude: string;
    longitude: string;
    address: string;
    image_url?: any;
    image_width?: any;
    image_height?: any;
    country: string;
    published_at: string;
    distance?: number;
}

interface Meeting {
    id: number;
    name: string;
    notes: string;
    day: number;
    time: string;
    end_time: string;
    time_periods: string[];
    url: string;
    types: string;
    updated_at: string;
    group?: any;
    group_notes?: any;
    venmo?: any;
    paypal?: any;
    square?: any;
    conference_provider?: any;
    conference_url?: any;
    conference_url_notes?: any;
    conference_phone?: any;
    conference_phone_notes?: any;
    organization_id: number;
    organization: string;
    distance: number;
    location_id: number;
    location: string;
    location_notes: string;
    latitude: string;
    longitude: string;
    formatted_address: string;
    address: string;
    city: string;
    state: string;
    postal_code: string;
    approximate: number;
    county: string;
    country: string;
    timezone: string;
}

interface News {
    id: number;
    title: string;
    datetime: string;
    content: string;
    button_url: string;
    button_text?: any;
    language: string;
    image_url?: any;
    image_width?: any;
    image_height?: any;
}

interface MeetingGuideApiV2Response {
    organizations: Organization[];
    meetings: Meeting[];
    news: News[];
    counts: any; //ignore this
}

```
