# Monitor Downtime Notifications Webhook

This document outlines the system by which a Jetpack partner host may receive notifications of downtime for sites they are hosting, which are using Jetpack. This allows the host to independently examine the downtime event, and verify it from their end.

In addition, there is allowance for the partner host to request we suppress user notifications in the case of scheduled or known downtime.

## Basic Architecture

Jetpack Monitor uses a distributed set of nodes in different data centers to check the response being received from sites running Jetpack. After an initial failure from one node, multiple secondary nodes are used to verify the initial results before triggering a notification (via email) to the user. Requests are executed as HEAD requests, and only currently verify HTTP response codes (not actual page content).

Immediately before sending the notification to users, Monitor may send a webhook-style request to the host of the site in question (host is determined per our records, based primarily on DNS information).

Optionally, a host may respond to this initial notification to indicate that the site in question is known to be down (e.g. scheduled maintenance) and thus we may suppress notifying the user of their downtime at our discretion.

## Endpoint Specification

### Request Payload

Jetpack Monitor will make an HTTP POST request to the URI you specify. The POST will contain a body which is the JSON-encoded details of the last check for a site. It will look approximately like this:

```json
{"ts":1385139152,"url":"http:\/\/example.com","code":403,"host":"example","type":"http"}
```


Fields included are:

* **ts:** Timestamp of the last check, as a UNIX style timestamp.
* **url:** The URL that was checked (with forward slashes escaped)
* **code:** The _highest_ HTTP response code we received during the last check. Note that since multiple nodes are used to verify a URL, it is possible for one node to receive e.g. a 200 response, while another gets a 500. In this case, we will return the 500. Can contain any HTTP status code, including 200 (indicating site is back online). If code is ‘0’, then there was a timeout on our verification check. Any non 2xx code is considered a failure.
* **host:** A string/”slug” representing who we think the host of this site is. Normally based off either DNS or ASN records.
* **type:** Indication of what kind of error was encountered. Currently only supports “http”

### Response

#### Normal Response

When we notify you of an unexpected/normal downtime event, your endpoint should just respond to our request with an HTTP 200 status, with the string `ok` in the body (no quotes, no period).

#### Scheduled downtime/suppress notification

In the case where the specific URL (or entire host) is known to be down, you may optionally respond with a timestamp (full UTC ISO 8601 format; 2017-11-05T13:15:30Z), indicating the expected time after which the site will be online again. An HTTP 200 is still expected in this case. Given this timestamp, we may optionally suppress further webhook notifications/requests to your endpoint until that time for this site/partner, to reduce redundant requests. We may also use this timestamp as an indication to suppress notification to the user.
