---
title: Event Discovery API

language_tabs:
  - shell

toc_footers:
  - <a href="mailto:hello@schedjoules.com">Sign Up for a API key</a>

includes:
//  - errors

search: true
---

# Introduction

Welcome to the Event Discovery API! You can use our API to access Event Discovery API endpoints, which can get information on events around the world.

You can view code examples in the dark area to the right.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "'Authorization: Token token="0443a55244bb2b6224fd48e0416f0d9c"'"
```

> Make sure to replace `0443a55244bb2b6224fd48e0416f0d9c` with your API key.

We use API keys to allow access to the API. You can register for a new API key via hello@schedjoules.com.

We expect for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Token token="0443a55244bb2b6224fd48e0416f0d9c"`

<aside class="notice">
You must replace <code>0443a55244bb2b6224fd48e0416f0d9c</code> with your personal API key. <a href="mailto:hello@schedjoules.com">Request one.</a>
</aside>

# Events

## Get All Events

We expect a u parameter appendend to events. The u parameter is unique, consistent, non-traceable user ID. We use this to statistical purposes and recommendations.

```shell
curl "https://api.schedjoules.com/events"
  -H 'Authorization: Token token="0443a55244bb2b6224fd48e0416f0d9c"'
```

> The above command returns JSON structured like this:

```json
[
    {
        "uid": "ff4ef8be88fca4a3",
        "etag": "304a4c141a9237191e884033684a53f1",
        "eventData": {
            "uid": "ff4ef8be88fca4a3",
            "created": "2017-05-07T11:59:30",
            "updated": "2017-05-08T11:51:18",
            "title": "New AS/A Level Science Teacher Network - Birmingham",
            "description": "Would you like to know more about ....",
            "locations": {
                "start": {
                    "name": "Joseph Chamberlain Sixth Form College",
                    "coordinates": "geo:52.4625592,-1.8851711",
                    "address": {
                        "street": "1 Belgrave Road",
                        "region": null,
                        "postcode": "B12 9FF",
                        "locality": "Birmingham",
                        "country": "United Kingdom"
                    }
                }
            },
            "isAllDay": false,
            "start": "2017-05-10T16:30:00",
            "timeZone": "UTC",
            "duration": "PT2H",
            "links": [
                {
                    "rel": "http://schedjoules.com/rel/banner",
                    "type": "image/png",
                    "href": "https://images.schedjoules/ff4ef8be88fca4a3.png",
                    "properties": {
                        "https://schedjoules.com/prop/width": "768",
                        "https://schedjoules.com/prop/height": "512"
                    }
                },
                {
                    "rel": "http://schedjoules.com/rel/thumbnail",
                    "type": "image/png",
                    "href": "https://images.schedjoules/ff4ef8be88fca4a3.png",
                    "properties": {
                        "https://schedjoules.com/prop/width": "128",
                        "https://schedjoules.com/prop/height": "128"
                    }
                }
            ]
        }
    },
    {
	...
    }
]
```

This endpoint retrieves all events.

### HTTP Request

`GET https://api.schedjoules.com/events?u={UID}`

<aside class="notice">
You must replace <code>{UID}</code> with unique, consistent, non-traceable user ID.
</aside>

### Query Parameters

Parameter |Required |Description
--------- | --- |--------
u |Yes | > 19 chars
latlng |No | float
radius |No | meters
start_at_or_after|No | UTC
start_before|No |UTC
results|No |default: 20. max: 100

`GET https://api.schedjoules.com/events?latlng=52.3,4.9&radius=10000&u={UID}`

### Pagination
By default the api returns a maximum of 100 results per request. The <a href='https://tools.ietf.org/html/rfc5988'>link headers</a> let you scroll into the future or past.



## Get a Specific Event

```shell
curl "https://api.schedjoules.com/events/169e687b8d5375fe?u={UID}"
  -H "Authorization: 0443a55244bb2b6224fd48e0416f0d9c"
```

This endpoint retrieves one specific event.

### HTTP Request

`GET https://api.schedjoules.com/events/<ID>?u={UID}`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the event to retrieve

<aside class="notice">
You must replace <code>{UID}</code> with unique, consistent, non-traceable user ID.
</aside>

# Actions

Every event is actionable. We provide links for buying tickets, navigation, share and add-to-calendar.

## Get Event Actions
```shell
curl "https://api.schedjoules.com/events/169e687b8d5375fe/actions?u={UID}"
  -H "Authorization: 0443a55244bb2b6224fd48e0416f0d9c"
```
> The above command returns JSON structured like this:

```json
{

    "links": [
        {
            "rel": "http://schedjoules.com/rel/action/book",
            "href": "https://actions.schedjoules.com/actions/28c6ba5002b71f44",
            "properties": {
                "http://schedjoules.com/props/booking/type": "ticket",
                "http://schedjoules.com/props/booking/sale-start": "2016-12-09T11:00:00Z",
                "http://schedjoules.com/props/booking/sale-end": "2017-06-28T19:00:00Z",
                "http://schedjoules.com/props/booking/sale-status": "unavailable",
                "http://schedjoules.com/props/vendor/icon": "data:image/png;base64,XXXXXXXXX"
            }
        },
        {
            "rel": "http://schedjoules.com/rel/action/add-to-calendar"
        },
        {
            "rel": "http://schedjoules.com/rel/action/share",
            "href": "https://actions.schedjoules.com/actions/d745c18339287eed"
        },
        {
            "rel": "http://schedjoules.com/rel/action/directions",
            "href": "https://actions.schedjoules.com/actions/8e436d28ef9e8864"
        }
    ]

}
```
### HTTP Request
`GET https://api.schedjoules.com/events/{ID}/actions?u={UID}`


### URL Parameters

Parameter |Required |Description
--------- | --- |--------
ID | Yes|The ID of the event to retrieve
u |Yes | > 19 chars

<aside class="notice">
You must replace <code>{UID}</code> with unique, consistent, non-traceable user ID.
</aside>

# Questions
Please tell us how we can make the API better. If you have a specific feature request or if you find a bug, please send us an <a href="mailto:hello@schedjoules.com">email</a>.