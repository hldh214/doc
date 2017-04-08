---
title: Avgle API v1 Reference

language_tabs:
  - php
  - python
  - javascript

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Avgle API! You can use our API to access information like videos and categories in our database.

We have language bindings in Javascript, PHP, and Python! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

Avgle API v1 is public and free to use. Neither authentication nor API keys is needed.

# Video categories

## Get all video categories

```php
$AVGLE_CATEGORIES_API_URL = 'https://api.avgle.com/v1/categories';
$response = json_decode(file_get_contents($url), true);
var_dump($response);
if ($response['success']) {
    $categories = $response['response']['categories'];
    doSomethingWith($categories);
}
```

```python
import urllib.request
import json
AVGLE_CATEGORIES_API_URL = 'https://api.avgle.com/v1/categories'
response = json.loads(urllib.request.open(url).read().decode())
print(response)
if response['success']:
    categories = response['response']['categories']
    do_something_with(categories)
```

```javascript
// node.js
const request = require('request');
const AVGLE_CATEGORIES_API_URL = 'https://api.avgle.com/v1/categories';
request(AVGLE_CATEGORIES_API_URL, (error, response, body) => {
    if (err) return console.log(err);
    var response = JSON.parse(body);
    console.log(response);
    if (response.success) {
        var categories = response.response.categories;
        doSomethingWith(categories);
    }
});

// jQuery
var AVGLE_CATEGORIES_API_URL = 'https://api.avgle.com/v1/categories';
$.getJSON(AVGLE_CATEGORIES_API_URL, function (response) {
    console.log(response);
    if (response.success) {
        var categories = response.response.categories;
        doSomethingWith(categories);
    }
})
```

> The above command returns JSON structured like this:

```json
{
    "success":true,
    "response":{
        "categories":[
            {
                "CHID":"1",
                "name":"Pornstar・AV女優",
                "slug":"pornstar",
                "total_videos":350,
                "category_url":"https://avgle.com/videos/pornstar",
                "cover_url":"https://avgle.com/media/categories/video/1.jpg"
            },
            {
                "CHID":"2",
                "name": "JAV・日本AV",
                "slug":"jav",
                "total_videos":2500,
                "category_url":"https://avgle.com/videos/jav",
                "cover_url":"https://avgle.com/media/categories/video/2.jpg"
            },
            {
                "CHID":"3",
                "name": "Uncensored・無修正",
                "slug":"uncensored",
                "total_videos":1000,
                "category_url":"https://avgle.com/videos/uncensored",
                "cover_url":"https://avgle.com/media/categories/video/3.jpg"
            }
        ]
    }
}
```

This endpoint retrieves all the video categories.

### HTTP Request

`GET https://api.avgle.com/v1/categories`

<aside class="success">
You can include CHID as a query parameter in search videos API or list videos API to filter results.
</aside>

# Video collections

A video collection denotes a series of videos. All the videos in a series include the `keyword` specified.

In other words, they are recommended searches.

## Get all video collections

```php
$AVGLE_LIST_COLLECTIONS_API_URL = 'https://api.avgle.com/v1/collections/';
$page = 0;
$limit = '?limit=2';
$response = json_decode(file_get_contents($url . $page . $limit), true);
var_dump($response);
if ($response['success']) {
    $collections = $response['response']['collections'];
    doSomethingWith($collections);
}
```

```python
import urllib.request
import json
AVGLE_LIST_COLLECTIONS_API_URL = 'https://api.avgle.com/v1/collections/{}?limit={}'
page = 0
limit = 2
response = json.loads(urllib.request.open(url.format(page, limit)).read().decode())
print(response)
if response['success']:
    collections = response['response']['collections']
    do_something_with(collections)
```

```javascript
// node.js
const request = require('request');
const AVGLE_LIST_COLLECTIONS_API_URL = 'https://api.avgle.com/v1/collections/';
var page = 0;
var limit = '?limit=2';
request(AVGLE_LIST_COLLECTIONS_API_URL + page + limit, (error, response, body) => {
    if (err) return console.log(err);
    var response = JSON.parse(body);
    console.log(response);
    if (response.success) {
        var collections = response.response.collections;
        doSomethingWith(collections);
    }
});

// jQuery
var AVGLE_LIST_COLLECTIONS_API_URL = 'https://api.avgle.com/v1/collections';
var page = 0;
var limit = '?limit=2';
$.getJSON(AVGLE_LIST_COLLECTIONS_API_URL + page + limit, function (response) {
    console.log(response);
    if (response.success) {
        var collections = response.response.collections;
        doSomethingWith(collections);
    }
})
```

> The above command returns JSON structured like this:

```json
{  
    "success":true,
    "response":{  
        "has_more":true,
        "total_collections":88,
        "current_offset":0,
        "limit":2,
        "collections":[  
            {  
                "id":"1",
                "title":"三上悠亜",
                "keyword":"三上悠亜",
                "collection_url":"https://avgle.com/c/三上悠亜",
                "cover_url":"https://avgle.com/media/videos/tmb/19944/1.jpg",
                "total_views":200000,
                "video_count":17
            },
            {  
                "id":"2",
                "title":"高橋しょう子",
                "keyword":"高橋しょう子",
                "collection_url":"https://avgle.com/c/高橋しょう子",
                "cover_url":"https://avgle.com/media/videos/tmb/3520/1.jpg",
                "total_views":115927,
                "video_count":11
            }
        ]
    }
}
```

This endpoint retrieves all the video collections.

### HTTP Request

`GET https://api.avgle.com/v1/collections/<page>`

### URL Parameters

Parameter | Description | Possible values
--------- | ----------- | ---------------
page | 0 based pagination | [0, +inf)

### Query Parameters

Parameter | Default | Description | Possible values
--------- | ------- | ----------- | ---------------
limit | 50 | The maximum number of video collections in the API response per page. | [1, 250]

### Response

Key | Description
--- | -----------
has_more | `true` means there is next page. `false` otherwise.
total_collections | The number of video collections.
current_offset | The number of video collections skipped by pagination.
limit | The maximum number of video collections the API response per page will include.
collection > keyword | The keyword of the collection which is used as search query.
collection > total_views | The total views of the videos in the video collection.
collection > video_count | The number of videos in the video collection.

<aside class="success">
You can use keyword as the search query in search videos API to retrieve all related videos.
</aside>

# Videos

## List all videos

```php
$AVGLE_LIST_VIDEOS_API_URL = 'https://api.avgle.com/v1/videos/';
$page = 0;
$limit = '?limit=2';
$response = json_decode(file_get_contents($url . $page . $limit), true);
var_dump($response);
if ($response['success']) {
    $videos = $response['response']['videos'];
    doSomethingWith($videos);
}
```

```python
import urllib.request
import json
AVGLE_LIST_VIDEOS_API_URL = 'https://api.avgle.com/v1/videos/{}?limit={}'
page = 0
limit = 2
response = json.loads(urllib.request.open(url.format(page, limit)).read().decode())
print(response)
if response['success']:
    videos = response['response']['videos']
    do_something_with(videos)
```

```javascript
// node.js
const request = require('request');
const AVGLE_LIST_VIDEOS_API_URL = 'https://api.avgle.com/v1/videos/';
var page = 0;
var limit = '?limit=2';
request(AVGLE_LIST_VIDEOS_API_URL + page + limit, (error, response, body) => {
    if (err) return console.log(err);
    var response = JSON.parse(body);
    console.log(response);
    if (response.success) {
        var videos = response.response.videos;
        doSomethingWith(videos);
    }
});

// jQuery
var AVGLE_LIST_VIDEOS_API_URL = 'https://api.avgle.com/v1/videos';
var page = 0;
var limit = '?limit=2';
$.getJSON(AVGLE_LIST_VIDEOS_API_URL + page + limit, function (response) {
    console.log(response);
    if (response.success) {
        var videos = response.response.videos;
        doSomethingWith(videos);
    }
})
```

> The above command returns JSON structured like this:

```json
{  
    "success":true,
    "response":{  
        "has_more":true,
        "total_videos":27352,
        "current_offset":0,
        "limit":2,
        "videos":[  
            {  
                "title":"happy-video",
                "keyword":"happy",
                "channel":"17",
                "duration":112.8,
                "framerate":23.976,
                "hd":false,
                "addtime":1491552611,
                "viewnumber":0,
                "likes":0,
                "dislikes":0,
                "video_url":"https://avgle.com/video/38329/happy-video",
                "embedded_url":"https://avgle.com/embed/754cc72672b40296c76e",
                "preview_url":"https://static.avgle.com/media/videos/tmb/38329/1.jpg",
                "vid":"38329",
                "uid":"1"
            },
            {  
                "title":"cool-video",
                "keyword":"cool",
                "channel":"17",
                "duration":209.58,
                "framerate":23.976,
                "hd":false,
                "addtime":1491552558,
                "viewnumber":0,
                "likes":0,
                "dislikes":0,
                "video_url":"https://avgle.com/video/38328/cool-video",
                "embedded_url":"https://avgle.com/embed/07ce8a9652a76f02df10",
                "preview_url":"https://static.avgle.com/media/videos/tmb/38328/1.jpg",
                "vid":"38328",
                "uid":"1"
            }
        ]
    }
}
```

This endpoint retrieves all the videos in criteria.

### HTTP Request

`GET https://api.avgle.com/v1/videos/<page>`

### URL Parameters

Parameter | Description | Possible values
--------- | ----------- | ---------------
page | 0 based pagination | [0, +inf)


### Query Parameters

Parameter | Default | Description | Possible values
--------- | ------- | ----------- | ---------------
o | mr | Videos ordering method. DESC order. For example, `mr` shows the latest videos in page 0. | bw (Last viewed)<br/>mr (Latest)<br/>mv (Most viewed)<br/>tr (Top rated)<br/>tf (Most favoured)<br/>lg (Longest)
t | a | Time frame. Videos older than the specified age will not be showed. For example, `w` shows only the videos uploaded from 7 days ago to now. | t (1 day)<br/>w (1 week)<br/>m (1 month)<br/>a (Forever)
type | (null) | Show only public or private videos, or show all videos if `type` not specified. | public<br/>private
c | (null) | Show only videos within the specified video category. For example, `c`=1 shows only videos in 'Happy videos' categories. See [above](#video-categories). | CHID of a valid video category (integer)
limit | 50 | The maximum number of videos in the API response per page. | [1, 250]

### Response

Key | Description
--- | -----------
has_more | `true` means there is next page. `false` otherwise.
total_videos | The number of videos in criteria.
current_offset | The number of videos skipped by pagination.
limit | The maximum number of videos the API response per page will include.
video > channel | Video category's ID (CHID).
video > duration | Video duration in seconds.
video > video_url | The viewing URL to the video.
video > embedded_url | The URL showing an embedded player of the video.

## Search videos

```php
$AVGLE_SEARCH_VIDEOS_API_URL = 'https://api.avgle.com/v1/search/';
$query = 'happy';
$page = 0;
$limit = '?limit=2';
$response = json_decode(file_get_contents($url . urlencode($query). '/' . $page . $limit), true);
var_dump($response);
if ($response['success']) {
    $videos = $response['response']['videos'];
    doSomethingWith($videos);
}
```

```python
import urllib.request
import urllib.parse
import json
AVGLE_SEARCH_VIDEOS_API_URL = 'https://api.avgle.com/v1/search/{}/{}?limit={}'
query = 'happy'
page = 0
limit = 2
response = json.loads(urllib.request.open(url.format(urllib.parse.quote_plus(query), page, limit)).read().decode())
print(response)
if response['success']:
    videos = response['response']['videos']
    do_something_with(videos)
```

```javascript
// node.js
const request = require('request');
const AVGLE_SEARCH_VIDEOS_API_URL = 'https://api.avgle.com/v1/search/';
var query = 'happy';
var page = 0;
var limit = '?limit=2';
request(AVGLE_SEARCH_VIDEOS_API_URL + encodeURIComponent(query) + '/' + page + limit, (error, response, body) => {
    if (err) return console.log(err);
    var response = JSON.parse(body);
    console.log(response);
    if (response.success) {
        var videos = response.response.videos;
        doSomethingWith(videos);
    }
});

// jQuery
var AVGLE_SEARCH_VIDEOS_API_URL = 'https://api.avgle.com/v1/search';
var query = 'happy';
var page = 0;
var limit = '?limit=2';
$.getJSON(AVGLE_SEARCH_VIDEOS_API_URL + encodeURIComponent(query) + '/' + page + limit, function (response) {
    console.log(response);
    if (response.success) {
        var videos = response.response.videos;
        doSomethingWith(videos);
    }
})
```

> The above command returns JSON structured like this:

```json
{  
    "success":true,
    "response":{  
        "has_more":true,
        "total_videos":123,
        "current_offset":0,
        "limit":2,
        "videos":[  
            {  
                "title":"happy-video",
                "keyword":"happy",
                "channel":"17",
                "duration":112.8,
                "framerate":23.976,
                "hd":false,
                "addtime":1491552611,
                "viewnumber":0,
                "likes":0,
                "dislikes":0,
                "video_url":"https://avgle.com/video/38329/happy-video",
                "embedded_url":"https://avgle.com/embed/754cc72675b40296c76e",
                "preview_url":"https://static.avgle.com/media/videos/tmb/38329/1.jpg",
                "vid":"38329",
                "uid":"1"
            },
            {  
                "title":"awesome-video",
                "keyword":"awesome happy",
                "channel":"17",
                "duration":209.58,
                "framerate":23.976,
                "hd":false,
                "addtime":1491552554,
                "viewnumber":0,
                "likes":0,
                "dislikes":0,
                "video_url":"https://avgle.com/video/38327/awesome-video",
                "embedded_url":"https://avgle.com/embed/07ce8a4652a76f02df10",
                "preview_url":"https://static.avgle.com/media/videos/tmb/38327/1.jpg",
                "vid":"38327",
                "uid":"1"
            }
        ]
    }
}
```

This endpoint retrieves the videos matches the search query which are in criteria.

### HTTP Request

`GET https://api.avgle.com/v1/search/<query>/<page>`

### URL Parameters

Parameter | Description | Possible values
--------- | ----------- | ---------------
query | Search query | URL escaped non empty string
page | 0 based pagination | [0, +inf)


### Query Parameters

See [above](#list-all-videos).

### Response

See [above](#list-all-videos).

## Search JAVs

```php
$AVGLE_SEARCH_JAV_API_URL = 'https://api.avgle.com/v1/jav/';
$query = 'sdde-480';
$page = 0;
$limit = '?limit=2';
$response = json_decode(file_get_contents($url . urlencode($query). '/' . $page . $limit), true);
var_dump($response);
if ($response['success']) {
    $videos = $response['response']['videos'];
    doSomethingWith($videos);
}
```

```python
import urllib.request
import urllib.parse
import json
AVGLE_SEARCH_JAV_API_URL = 'https://api.avgle.com/v1/jav/{}/{}?limit={}'
query = 'sdde-480'
page = 0
limit = 2
response = json.loads(urllib.request.open(url.format(urllib.parse.quote_plus(query), page, limit)).read().decode())
print(response)
if response['success']:
    videos = response['response']['videos']
    do_something_with(videos)
```

```javascript
// node.js
const request = require('request');
const AVGLE_SEARCH_JAV_API_URL = 'https://api.avgle.com/v1/jav/';
var query = 'sdde-480';
var page = 0;
var limit = '?limit=2';
request(AVGLE_SEARCH_JAV_API_URL + encodeURIComponent(query) + '/' + page + limit, (error, response, body) => {
    if (err) return console.log(err);
    var response = JSON.parse(body);
    console.log(response);
    if (response.success) {
        var videos = response.response.videos;
        doSomethingWith(videos);
    }
});

// jQuery
var AVGLE_SEARCH_JAV_API_URL = 'https://api.avgle.com/v1/jav';
var query = 'sdde-480';
var page = 0;
var limit = '?limit=2';
$.getJSON(AVGLE_SEARCH_JAV_API_URL + encodeURIComponent(query) + '/' + page + limit, function (response) {
    console.log(response);
    if (response.success) {
        var videos = response.response.videos;
        doSomethingWith(videos);
    }
})
```

> The above command returns JSON structured like this:

```json
{  
    "success":true,
    "response":{  
        "has_more":false,
        "total_videos":1,
        "current_offset":0,
        "limit":1,
        "videos":[  
            {  
                "title":"SDDE-480 good-video",
                "keyword":"good",
                "channel":"11",
                "duration":112.8,
                "framerate":23.976,
                "hd":false,
                "addtime":1491552611,
                "viewnumber":0,
                "likes":0,
                "dislikes":0,
                "video_url":"https://avgle.com/video/38322/sdde-480-good-video",
                "embedded_url":"https://avgle.com/embed/754cc72675b40296c76e",
                "preview_url":"https://static.avgle.com/media/videos/tmb/38322/1.jpg",
                "vid":"38322",
                "uid":"1"
            }
        ]
    }
}
```

This endpoint retrieves the videos with category (channel, CHID) <= 12 that matches the search query which are in criteria, similar to video search.

### HTTP Request

`GET https://api.avgle.com/v1/jav/<query>/<page>`

### URL Parameters

Parameter | Description | Possible values
--------- | ----------- | ---------------
query | Search query | URL escaped non empty string
page | 0 based pagination | [0, +inf)


### Query Parameters

See [above](#list-all-videos).

### Response

See [above](#list-all-videos).



## Get video by VID

```php
$AVGLE_GET_VIDEO_API_URL = 'https://api.avgle.com/v1/video/';
$vid = '38329';
$response = json_decode(file_get_contents($url . $vid), true);
var_dump($response);
if ($response['success']) {
    $video = $response['response']['video'];
    doSomethingWith($video);
}
```

```python
import urllib.request
import json
AVGLE_GET_VIDEO_API_URL = 'https://api.avgle.com/v1/video/{}'
vid = '38329'
response = json.loads(urllib.request.open(url.format(vid)).read().decode())
print(response)
if response['success']:
    video = response['response']['video']
    do_something_with(video)
```

```javascript
// node.js
const request = require('request');
const AVGLE_GET_VIDEO_API_URL = 'https://api.avgle.com/v1/video/';
var vid = '38329';
request(AVGLE_GET_VIDEO_API_URL + vid, (error, response, body) => {
    if (err) return console.log(err);
    var response = JSON.parse(body);
    console.log(response);
    if (response.success) {
        var video = response.response.video;
        doSomethingWith(video);
    }
});

// jQuery
var AVGLE_GET_VIDEO_API_URL = 'https://api.avgle.com/v1/video';
var vid = '38329';
$.getJSON(AVGLE_GET_VIDEO_API_URL + vid, function (response) {
    console.log(response);
    if (response.success) {
        var video = response.response.video;
        doSomethingWith(video);
    }
})
```

> The above command returns JSON structured like this:

```json
{  
    "success":true,
    "response":{  
        "video":{  
            "title":"happy-video",
            "keyword":"happy",
            "channel":"17",
            "duration":112.8,
            "framerate":23.976,
            "hd":false,
            "addtime":1491552611,
            "viewnumber":0,
            "likes":0,
            "dislikes":0,
            "video_url":"https://avgle.com/video/38329/happy-video",
            "embedded_url":"https://avgle.com/embed/754cc72675b40296c76e",
            "preview_url":"https://static.avgle.com/media/videos/tmb/38329/1.jpg",
            "vid":"38329",
            "uid":"1"
        }
    }
}
```
> Or if video is not found (404)

```json
{  
    "success":false,
    "response":{  
        "error_message":"Video of VID 38329 not found."
    }
}
```

This endpoint retrieves the video of specified VID.

### HTTP Request

`GET https://api.avgle.com/v1/video/<VID>`

### URL Parameters

Parameter | Description | Possible values
--------- | ----------- | ---------------
VID | ID of the video | Integer


### Response

See [above](#list-all-videos).

# Rate limitation

Avgle API v1 does not currently impose any explicit rate limit. However, it's possible for us to impose rate limit anytime depends on the system load without announcement.

When rate limit exceeded, a `429 Too Many Requests` response will be sent.
