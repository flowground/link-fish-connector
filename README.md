# ![LOGO](logo.png) link.fish **flow**ground Connector

## Description

A generated **flow**ground connector for the link.fish API (version 2018-07-05).

Generated from: https://api.apis.guru/v2/specs/link.fish/2018-07-05/swagger.json<br/>
Generated at: 2019-05-07T17:42:44+03:00

## API Description

API to easily extract data from websites.


# Base URL


All URLs referenced in the documentation have the following base:


```
https://api.link.fish
```


The REST API is only served over HTTPS. To ensure data privacy, unencrypted HTTP is not supported.


# Authentication
HTTP requests to the REST API are protected with [HTTP Basic authentication](https://en.wikipedia.org/wiki/Basic_access_authentication). You will use the email address of your link.fish account as the username and your API access token as the password for HTTP Basic authentication.

If you do not have an account yet, go to [https://link.fish/api](https://link.fish/api) and create one first.

You will receive the API access token automatically via email after you signed up. To generate a new token and invalidate the current one log into your link.fish  account at [https://app.link.fish](https://app.link.fish) and go to: "Plugins" -> "API Dashboard"

There you can also see how many credits you used already.


# Errors
The API uses standard HTTP status codes to indicate the success or failure of the API call. The body of the response will be JSON in the following format:
```
{

  "status": {HTTP STATUS CODE}
  "message": "{ERROR MESSAGE}"
}
```
Like for example when the authorization is not provided or wrong:
```
{

  "status": 401
  "message": "Unauthorized"
}
```

# Request IDs

Each API request has an associated request identifier. You can find it in the response headers, under X-LF-Request-Id. In case you have problems please provide this identifier that we can help you as good and fast as possible.


Example:
```
X-LF-Request-Id: f7f0036f-5277-421a-b143-f7a151571d18
```


# Item format

The data is by default deeply nested. So if it should be checked if there is an offer with a price, the whole tree has to be checked. To make that simpler, it is also possible to return the data "flat". If selected it will flatten the tree by copying all the data to the main level under a property with the name of its type and link the data internally.

Information: We created a node module which allows converting between the two formats. It did not get open sourced yet. If you are in need, simply contact us via api@link.fish.


# Response Content Type
By default, all data gets returned as JSON. If the data should be returned as XML add the following header:

```
Accept: application/xml
```

# Credits

Depending on the request made a different amount of credits get charged. How many which request costs can be found on the [API pricing page](http://link.fish/api/#pricing). Additionally, does a  header named "X-LF-Credits-Charged" get added to each successful response with information about the credits.

Example:
```
X-LF-Credits-Charged: 1 # Credits used for current requests
X-LF-Credits-Subscription-Max: 1000 # Total credits available in subscription
X-LF-Credits-Subscription-Used: 512 # Credits still left in current month
```
You can check anytime how many credits you did use already by logging into your link.fish  account at [https://app.link.fish](https://app.link.fish) and checking under:  "Plugins" -> "API Dashboard"


If you have problems, questions or improvement advice please send us an email to api@link.fish


## Authorization

Supported authorization schemes:
- Basic Authentication

## Actions

### Get mobile apps

> Visits the URL and checks if there are mobile apps on them and returns the found ones.<br/>
> <br/>
> Will by default return the app identifiers and not the full URL to the apps. To return URLs instead set the parameter "return_urls" to true.<br/>
> <br/>
> The URLs can also be created manually like this:<br/>
> <br/>
> | Property | URL                                                |<br/>
> | -------- | -------------------------------------------------- |<br/>
> | android  | https://play.google.com/store/apps/details?id={ID} |<br/>
> | ios      | https://itunes.apple.com/us/app/app-name/id{ID}    |<br/>
> <br/>
> Properties only get set when a value for it has been found. That means that if no app has been found only the property "url" will be set.

*Tags:* `REST-Endpoints`

#### Input Parameters
* `url` - _required_ - The URL of the website to query
* `return_urls` - _optional_ - Returns app URLs instead of the identifiers
* `browser_render` - _optional_ - If the page should be fully rendered with a browser to extract data. The request will then cost 5 credits instead of 1!

### Extract data (browser)

> Visits the URL with a full browser and extracts the data. This request costs 5 credits.

*Tags:* `REST-Endpoints`

#### Input Parameters
* `url` - _required_ - The URL of the website to query
* `item_format` - _optional_ - If the items should be return "normal" with multiple levels or "flat" with just one level and linked instead.
    Possible values: normal, flat.
* `simplify_special_types` - _optional_ - Some types like "PropertyValue" do save key and value in separate properties which makes the data harder to process. If this option gets set it converts them automatically into the regular key -> value format.
* `include_raw_html` - _optional_ - Returns additionally also the raw HTML as property "rawHtml".
* `screenshot` - _optional_ - If and what kind of screenshot should be returned. Do only request screenshot generation when really needed because it will increase the response time significantly.
    Possible values: none, normal, full.
* `screenshot_width` - _optional_ - The widh of the screenshot in pixel.
* `screenshot_file_format` - _optional_ - The file format of the screenshot
    Possible values: png, jpg.

### Generate screenshot (browser)

> Visits the URL with full browser and creates a screenshot. This request costs 5 credits.

*Tags:* `REST-Endpoints`

#### Input Parameters
* `url` - _required_ - The URL of the website to create screenshot of
* `type` - _optional_ - What kind of screenshot should be returned. If it should be a regular 16:9 screenshot or one with the full page height
    Possible values: normal, full.
* `file_format` - _optional_ - The file format of the screenshot
    Possible values: png, jpg.
* `width` - _optional_ - The widh of the screenshot in pixel.

### Extract data

> Visits the URL and extracts the data.

*Tags:* `REST-Endpoints`

#### Input Parameters
* `url` - _required_ - The URL of the website to query
* `item_format` - _optional_ - If the items should be return "normal" with multiple levels or "flat" with just one level and linked instead.
    Possible values: normal, flat.
* `simplify_special_types` - _optional_ - Some types like "PropertyValue" do save key and value in separate properties which makes the data harder to process. If this option gets set it converts them automatically into the regular key -> value format.
* `include_raw_html` - _optional_ - Returns additionally also the raw HTML as property "rawHtml".
* `browser_render` - _optional_ - If the page should be fully rendered with a browser to extract data. The request will then cost 5 credits instead of 1!

### Return data of JSON/XML

> Visits the URL and extracts the data.

*Tags:* `REST-Endpoints`

#### Input Parameters
* `url` - _required_ - The URL to get the data of

### Return tabular data

> Visits the URL and extracts tabular data.

*Tags:* `REST-Endpoints`

#### Input Parameters
* `url` - _required_ - The URL to get the data of
* `selector` - _optional_ - CSS selector to define tabular data which should get returned
* `browser_render` - _optional_ - If the page should be fully rendered with a browser to extract data. The request will then cost 5 credits instead of 1!

### Get geo coordinates

> Visits the URL and checks if there are Geo Coordinates on them and returns the found ones.<br/>
> <br/>
> Properties only get set when a value for both latitude and longitude have been found. That means that if no geo coordinates have been found only the property "url" will be set.

*Tags:* `REST-Endpoints`

#### Input Parameters
* `url` - _required_ - The URL of the website to query
* `browser_render` - _optional_ - If the page should be fully rendered with a browser to extract data. The request will then cost 5 credits instead of 1!

### Get social media accounts

> Visits the URL and checks if there are any social media accounts and returns the found ones.<br/>
> <br/>
> Will by default return the account identifiers and not the full URL to the profiles. To return URLs instead set the parameter "return_urls" to true.<br/>
> <br/>
> The URLs can also be created manually like this:<br/>
> <br/>
> | Property        | URL                                    |<br/>
> | --------------- | -------------------------------------- |<br/>
> | facebookPage    | https://facebook.com/{ID}              |<br/>
> | githubUser      | https://github.com/{ID}                |<br/>
> | googlePlus      | https://plus.google.com/+{ID}          |<br/>
> | instagram       | https://instagram.com/{ID}             |<br/>
> | linkedInCompany | https://linkedin.com/company/{ID}      |<br/>
> | pinterest       | https://pinterest.com/{ID}             |<br/>
> | twitter         | https://twitter.com/{ID}               |<br/>
> | youTubeUser     | https://youtube.com/user/{ID}          |<br/>
> <br/>
> Properties only get set when a value for it has been found. That means that if no social media account has been found only the property "url" will be set.

*Tags:* `REST-Endpoints`

#### Input Parameters
* `url` - _required_ - The URL of the website to query
* `return_urls` - _optional_ - Returns profile URLs instead of the profile names/ids
* `browser_render` - _optional_ - If the page should be fully rendered with a browser to extract data. The request will then cost 5 credits instead of 1!

## License

**flow**ground :- Telekom iPaaS / link-fish-connector<br/>
Copyright © 2019, [Deutsche Telekom AG](https://www.telekom.de)<br/>
contact: flowground@telekom.de

All files of this connector are licensed under the Apache 2.0 License. For details
see the file LICENSE on the toplevel directory.
