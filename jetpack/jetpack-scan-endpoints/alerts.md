# Ignore or fix a specific threat.

This endpoint is used to act on a specific alert. It can be used to fix or ignore a threat.

Request URL: https://public-api.wordpress.com/wpcom/v2/sites/212734736/alerts/81431083?ignore=true&_envelope=1


### Endpoint Information

- __Method__: POST
- __URL__: `https://public-api.wordpress.com/wpcom/v2/sites/<blog_id>/alerts/<threat_id>`
- __blog_id__: (number) Site to query.

Authentication: [Bearer token](/jetpack/reporting-endpoints/README.md).

### Request Parameters

#### Fixing a threat
Append `?fix=true` in the query string if you want to fix the threat. 

#### Ignoring a threat.
Append `?ignore=true` in the query string if you want to fix the threat. 

### Response Format

Object with the following fields encapsulated:

- __alerts__: (object) An object containing information about the alerts of the site. It contains the following keys:
    - __threats__: (object) Same threat object as in the regular `scan` endpoint.
- __credentials__: (object) Same credentials object as in the regular `scan` endpoint.
- __last_updated__: (date) Timestamp when an alert was last updated.
- __state__: (string) dunno yet. 

### Successful Response

```
{
	"credentials": [{
		"still_valid": true,
		"type": "managed",
		"role": "main"
	}],
	"alerts": {
		"threats": [{
			"id": 81427324,
			"signature": "EICAR_AV_Test",
			"title": "Malicious code found in file: akismet.php",
			"description": "This is the standard EICAR antivirus test code, and not a real infection. If your site contains this code when you don't expect it to, contact Jetpack support for some help.",
			"vulnerability_description": "Threat found EICAR_AV_Test",
			"fix_description": "Jetpack Scan will replace the affected file or directory.",
			"payload_subtitle": null,
			"payload_description": null,
			"first_detected": "2022-11-27T20:06:54.000Z",
			"severity": 4,
			"fixer": {
				"fixer": "replace",
				"file": "\/srv\/htdocs\/wp-content\/plugins\/akismet\/akismet.php",
				"extensionStatus": "active"
			},
			"status": "current",
			"fixable": {
				"fixer": "replace",
				"file": "\/srv\/htdocs\/wp-content\/plugins\/akismet\/akismet.php",
				"extensionStatus": "active"
			},
			"filename": "\/srv\/htdocs\/wp-content\/plugins\/akismet\/akismet.php",
			"context": {
				"2": "\/**",
				"3": " * X5O!P%@AP[4\\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*",
				"4": " * X5O!P%@AP[4\\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*",
				"5": " * X5O!P%@AP[4\\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*",
				"6": " * X5O!P%@AP[4\\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*",
				"7": " * X5O!P%@AP[4\\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*",
				"8": " * X5O!P%@AP[4\\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*",
				"9": " * X5O!P%@AP[4\\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*",
				"10": " * X5O!P%@AP[4\\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*",
				"11": " * X5O!P%@AP[4\\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*",
				"12": " * X5O!P%@AP[4\\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*",
				"13": " * X5O!P%@AP[4\\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*",
				"14": " * X5O!P%@AP[4\\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*",
				"15": " * X5O!P%@AP[4\\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*",
				"16": " * X5O!P%@AP[4\\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*",
				"17": " * X5O!P%@AP[4\\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*X5O!P%@AP[4\\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*",
				"18": " * X5O!P%@AP[4\\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*",
				"19": " * ",
				"20": " * X5O!P%@AP[4\\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*",
				"21": " * @package Akismet",
				"marks": {}
			}
		}]
	},
	"downloads": [],
	"state": "active",
	"last_updated": "2022-11-27T21:36:51.593+00:00"
}
```

### Example

To ignore the threat `81427324` for the site `155308227`:

`https://public-api.wordpress.com/wpcom/v2/sites/155308227/alerts/81427324?ignore=true`

To fix the threat `81427324` for the site `155308227`:

`https://public-api.wordpress.com/wpcom/v2/sites/155308227/alerts/81427324?ignore=true`
