# List data from last Scan 

Return data from the last Scan.

### Endpoint Information

- __Method__: GET
- __URL__: `https://public-api.wordpress.com/wpcom/v2/sites/<blog_id>/scan`
- __blog_id__: (number) Site to query.

Authentication: [Access token](/jetpack/jetpack-start-endpoints/authentication.md).

### Request Parameters

None

### Response Format

Object with the following fields encapsulated:

- __state__: (string) State of the scanner, possible states are: `idle`, `provisioning`, `unavailable`, `scanning`.
- __threats__: (array) Array of threat objects. A threat object contain the following keys:
  - __id__: (number) The id of this particular threat.
  - __signature__: (string) The name of the signature that triggered the threat.
  - __title__: (string) A human readable title for the threat.
  - __description__: (string) The more detailed description of what the threat.
  - __vulnerability_description__: (string) tbd
  - __fix_description__: (string) A human readable description for what the fixer will do to fix this threat.
  - __payload_subtitle__: (string) tbd
  - __payload_description__: (string) tbd
  - __first_detected__: (string) The date when this threat was first detected on this site.
  - __severity__: (number) A number representing the severity of this threat. 1 is `suspicious`, 2 is `low`, 3 is `medium`, 4 is `high`, 5 is `critical`.
  - __fixer__: (object) An object with information about the fixer if applicable. The keys for the object are:
	- __fixer__: (string) The name of the fixer that will be used for this threat.
	- __file__: (string) The file that will be affected by the fixer.
	- __extensionStatus__: (string) The activation status for the extension this threat affects if applicable.
  - __status__: (string) Status of the threat, possible values are `current`, `new`, `ignored`, `fixed`.
  - __fixable__: (object) Same as `fixer`.
  - __filename__: (string) The file where this threat was found in.
  - __context__: (object) An object with more information about how the threat was found. It contains the lines with the malicious code if it's a file threat as keys.
  - __extension__: (object) If the threat was caused by a vulnerable version of an extension this node will contain information about that extension. The keys for this object are:
	- __isPremium__: (boolean) A boolean indicating if this is a premium extension or not.
	- __name__: (string) Name of the extension.
	- __slug__: (string) Slug of the extension.
	- __type__: (string) Type of the extension, could be either `plugin` or `theme`.
	- __version__: (string) Version of the extension.
- __has_cloud__: (boolean) Whether a site has Jetpack Cloud access or not.
- __credentials__: (array) Array of objects containing credentials that we have stored. The object has the following keys:
  - __still_valid__: (boolean) A boolean indicating if the credentials are still valid or not.
  - __type__: (string) The type of the credentials.
  - __role__: (string) The role of the credentials.
- __most_recent__: (object) An object containing information about the most recent scan attempt. It contains the following keys:
  - __is_initial__: (boolean) A boolean indicating if this is the first scan attempt.
  - __timestamp__: (date) The timestamp for the scan attempt.
  - __duration__: (number) The duration for the scan attempt in seconds.
  - __progress__: (number) The percentage for the scan attempt.
  - __error__: (boolean) A boolean indicating if the scan attempt failed or not.

### Successful Response

```
{
	"state": "idle",
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
	}],
	"has_cloud": true,
	"credentials": [{
		"still_valid": true,
		"type": "managed",
		"role": "main"
	}],
	"most_recent": {
		"is_initial": false,
		"timestamp": "2022-11-27T20:41:27+00:00",
		"duration": 41,
		"progress": 100,
		"error": false
	}
}
```

### Example

Fetch scan information for site `155308227`:

`https://public-api.wordpress.com/wpcom/v2/sites/155308227/scan`
