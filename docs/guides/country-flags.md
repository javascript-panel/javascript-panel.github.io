# Country Flags

!!! note
	This requires that you have a supported font like [Twemoji Mozilla](https://github.com/mozilla/twemoji-colr/releases/latest)
	or [Noto Color Emoji](https://fonts.google.com/noto/specimen/Noto+Color+Emoji) installed.

While it has always been possible to display flags with images or writing your own scripts
to make use of emoji, this details some helper methods which have been added to make it
easier.

## Title formatting

!!! note
	These examples assume you have a [supported value](#supported-values) inside a `%country%` tag. Adjust as
	necessary.

A `$country_flag` function has been added and you can use it like this:

```
$font(Twemoji Mozilla,16)$country_flag(%country%)
```

!!! note
	The use of `$font` is detailed [here](font-rgb.md).

!!! example
	```js
	include('helpers');

	// $font() with no args resets back to the default_font supplied to
	// DrawStyledText in on_paint
	// also includes $rgb example
	var tfo = fb.TitleFormat(
		"[$font(Twemoji Mozilla,18)$country_flag(%country%)$font() ]$rgb(255,0,0)%artist%"
	);
	var str = "";

	refresh();

	function refresh() {
		var item = fb.GetFocusItem();
		if (item) {
			str = item.FormatTitle(tfo);
		} else {
			str = "";
		}
	}

	function on_item_focus_change() {
		refresh();
		window.Repaint();
	}

	function on_playlist_switch() {
		refresh();
		window.Repaint();
	}

	function on_paint(gr) {
		// default_font is an empty string, defaulting to Segoe UI, 16px
		gr.WriteText(str, "", 0, 0, 0, window.Width, window.Height, 2, 2);
	}
	```

## JavaScript

If you prefer not to use title formatting, you can use `utils.GetCountryFlag` method
which accepts a 2 letter country code or the full country name. See
[supported values](#supported-values). An empty string will be returned on failure.

!!! example
	```js
	include('helpers');

	var font = CreateFontString("Twemoji Mozilla", 24);
	var flag = utils.GetCountryFlag("GB");

	function on_paint(gr) {
		gr.WriteText(flag, font, 0, 0, 0, window.Width, window.Height, 2, 2);
	}
	```

## Supported values
Case is not important. You can supply the code or full name.

|Flag|Code|Country|
|---|---|---|
|🇦🇫|AF|Afghanistan|
|🇦🇽|AX|Aland Islands|
|🇦🇱|AL|Albania|
|🇩🇿|DZ|Algeria|
|🇦🇸|AS|American Samoa|
|🇦🇩|AD|Andorra|
|🇦🇴|AO|Angola|
|🇦🇮|AI|Anguilla|
|🇦🇶|AQ|Antarctica|
|🇦🇬|AG|Antigua and Barbuda|
|🇦🇷|AR|Argentina|
|🇦🇲|AM|Armenia|
|🇦🇼|AW|Aruba|
|🇦🇺|AU|Australia|
|🇦🇹|AT|Austria|
|🇦🇿|AZ|Azerbaijan|
|🇧🇸|BS|Bahamas|
|🇧🇭|BH|Bahrain|
|🇧🇩|BD|Bangladesh|
|🇧🇧|BB|Barbados|
|🇧🇾|BY|Belarus|
|🇧🇪|BE|Belgium|
|🇧🇿|BZ|Belize|
|🇧🇯|BJ|Benin|
|🇧🇲|BM|Bermuda|
|🇧🇹|BT|Bhutan|
|🇧🇴|BO|Bolivia|
|🇧🇦|BA|Bosnia and Herzegovina|
|🇧🇼|BW|Botswana|
|🇧🇷|BR|Brazil|
|🇮🇴|IO|British Indian Ocean Territory|
|🇻🇬|VG|British Virgin Islands|
|🇧🇳|BN|Brunei Darussalam|
|🇧🇬|BG|Bulgaria|
|🇧🇫|BF|Burkina Faso|
|🇧🇮|BI|Burundi|
|🇨🇻|CV|Cabo Verde|
|🇰🇭|KH|Cambodia|
|🇨🇲|CM|Cameroon|
|🇨🇦|CA|Canada|
|🇧🇶|BQ|Caribbean Netherlands|
|🇰🇾|KY|Cayman Islands|
|🇨🇫|CF|Central African Republic|
|🇹🇩|TD|Chad|
|🇨🇱|CL|Chile|
|🇨🇳|CN|China|
|🇨🇽|CX|Christmas Island|
|🇨🇨|CC|Cocos (Keeling) Islands|
|🇨🇴|CO|Colombia|
|🇰🇲|KM|Comoros|
|🇨🇬|CG|Congo|
|🇨🇰|CK|Cook Islands|
|🇨🇷|CR|Costa Rica|
|🇨🇮|CI|Cote d'Ivoire|
|🇭🇷|HR|Croatia|
|🇨🇺|CU|Cuba|
|🇨🇼|CW|Curaçao|
|🇨🇾|CY|Cyprus|
|🇨🇿|CZ|Czechia|
|🇰🇵|KP|Democratic People's Republic of Korea|
|🇨🇩|CD|Democratic Republic of the Congo|
|🇩🇰|DK|Denmark|
|🇩🇯|DJ|Djibouti|
|🇩🇲|DM|Dominica|
|🇩🇴|DO|Dominican Republic|
|🇪🇨|EC|Ecuador|
|🇪🇬|EG|Egypt|
|🇸🇻|SV|El Salvador|
|🇬🇶|GQ|Equatorial Guinea|
|🇪🇷|ER|Eritrea|
|🇪🇪|EE|Estonia|
|🇸🇿|SZ|Eswatini|
|🇪🇹|ET|Ethiopia|
|🇫🇰|FK|Falkland Islands|
|🇫🇴|FO|Faroe Islands|
|🇫🇯|FJ|Fiji|
|🇫🇮|FI|Finland|
|🇫🇷|FR|France|
|🇬🇫|GF|French Guiana|
|🇵🇫|PF|French Polynesia|
|🇬🇦|GA|Gabon|
|🇬🇲|GM|Gambia|
|🇬🇪|GE|Georgia|
|🇩🇪|DE|Germany|
|🇬🇭|GH|Ghana|
|🇬🇮|GI|Gibraltar|
|🇬🇷|GR|Greece|
|🇬🇱|GL|Greenland|
|🇬🇩|GD|Grenada|
|🇬🇵|GP|Guadeloupe|
|🇬🇺|GU|Guam|
|🇬🇹|GT|Guatemala|
|🇬🇬|GG|Guernsey|
|🇬🇳|GN|Guinea|
|🇬🇼|GW|Guinea-Bissau|
|🇬🇾|GY|Guyana|
|🇭🇹|HT|Haiti|
|🇭🇳|HN|Honduras|
|🇭🇰|HK|Hong Kong|
|🇭🇺|HU|Hungary|
|🇮🇸|IS|Iceland|
|🇮🇳|IN|India|
|🇮🇩|ID|Indonesia|
|🇮🇷|IR|Iran|
|🇮🇶|IQ|Iraq|
|🇮🇪|IE|Ireland|
|🇮🇲|IM|Isle of Man|
|🇮🇱|IL|Israel|
|🇮🇹|IT|Italy|
|🇯🇲|JM|Jamaica|
|🇯🇵|JP|Japan|
|🇯🇪|JE|Jersey|
|🇯🇴|JO|Jordan|
|🇰🇿|KZ|Kazakhstan|
|🇰🇪|KE|Kenya|
|🇰🇮|KI|Kiribati|
|🇽🇰|XK|Kosovo|
|🇰🇼|KW|Kuwait|
|🇰🇬|KG|Kyrgyzstan|
|🇱🇦|LA|Laos|
|🇱🇻|LV|Latvia|
|🇱🇧|LB|Lebanon|
|🇱🇸|LS|Lesotho|
|🇱🇷|LR|Liberia|
|🇱🇾|LY|Libya|
|🇱🇮|LI|Liechtenstein|
|🇱🇹|LT|Lithuania|
|🇱🇺|LU|Luxembourg|
|🇲🇴|MO|Macao|
|🇲🇬|MG|Madagascar|
|🇲🇼|MW|Malawi|
|🇲🇾|MY|Malaysia|
|🇲🇻|MV|Maldives|
|🇲🇱|ML|Mali|
|🇲🇹|MT|Malta|
|🇲🇭|MH|Marshall Islands|
|🇲🇶|MQ|Martinique|
|🇲🇷|MR|Mauritania|
|🇲🇺|MU|Mauritius|
|🇾🇹|YT|Mayotte|
|🇲🇽|MX|Mexico|
|🇫🇲|FM|Micronesia|
|🇲🇩|MD|Moldova|
|🇲🇨|MC|Monaco|
|🇲🇳|MN|Mongolia|
|🇲🇪|ME|Montenegro|
|🇲🇸|MS|Montserrat|
|🇲🇦|MA|Morocco|
|🇲🇿|MZ|Mozambique|
|🇲🇲|MM|Myanmar|
|🇳🇦|NA|Namibia|
|🇳🇷|NR|Nauru|
|🇳🇵|NP|Nepal|
|🇳🇱|NL|Netherlands|
|🇳🇨|NC|New Caledonia|
|🇳🇿|NZ|New Zealand|
|🇳🇮|NI|Nicaragua|
|🇳🇪|NE|Niger|
|🇳🇬|NG|Nigeria|
|🇳🇺|NU|Niue|
|🇳🇫|NF|Norfolk Island|
|🇲🇰|MK|North Macedonia|
|🇲🇵|MP|Northern Mariana Islands|
|🇳🇴|NO|Norway|
|🇴🇲|OM|Oman|
|🇵🇰|PK|Pakistan|
|🇵🇼|PW|Palau|
|🇵🇸|PS|Palestinian Territory|
|🇵🇦|PA|Panama|
|🇵🇬|PG|Papua New Guinea|
|🇵🇾|PY|Paraguay|
|🇵🇪|PE|Peru|
|🇵🇭|PH|Philippines|
|🇵🇳|PN|Pitcairn|
|🇵🇱|PL|Poland|
|🇵🇹|PT|Portugal|
|🇵🇷|PR|Puerto Rico|
|🇶🇦|QA|Qatar|
|🇷🇪|RE|Reunion|
|🇷🇴|RO|Romania|
|🇷🇺|RU|Russia|
|🇷🇼|RW|Rwanda|
|🇧🇱|BL|Saint Barthelemy|
|🇸🇭|SH|Saint Helena, Ascension and Tristan Da Cunha|
|🇰🇳|KN|Saint Kitts and Nevis|
|🇱🇨|LC|Saint Lucia|
|🇲🇫|MF|Saint Martin|
|🇵🇲|PM|Saint Pierre and Miquelon|
|🇻🇨|VC|Saint Vincent and the Grenadines|
|🇼🇸|WS|Samoa|
|🇸🇲|SM|San Marino|
|🇸🇹|ST|Sao Tome and Principe|
|🇸🇦|SA|Saudi Arabia|
|🇸🇳|SN|Senegal|
|🇷🇸|RS|Serbia|
|🇸🇨|SC|Seychelles|
|🇸🇱|SL|Sierra Leone|
|🇸🇬|SG|Singapore|
|🇸🇰|SK|Slovakia|
|🇸🇮|SI|Slovenia|
|🇸🇧|SB|Solomon Islands|
|🇸🇴|SO|Somalia|
|🇿🇦|ZA|South Africa|
|🇬🇸|GS|South Georgia and the South Sandwich Islands|
|🇰🇷|KR|South Korea|
|🇸🇸|SS|South Sudan|
|🇪🇸|ES|Spain|
|🇱🇰|LK|Sri Lanka|
|🇸🇩|SD|Sudan|
|🇸🇷|SR|Suriname|
|🇸🇯|SJ|Svalbard and Jan Mayen|
|🇸🇪|SE|Sweden|
|🇨🇭|CH|Switzerland|
|🇸🇾|SY|Syrian Arab Republic|
|🇹🇼|TW|Taiwan|
|🇹🇯|TJ|Tajikistan|
|🇹🇿|TZ|Tanzania|
|🇹🇭|TH|Thailand|
|🇹🇱|TL|Timor-Leste|
|🇹🇬|TG|Togo|
|🇹🇰|TK|Tokelau|
|🇹🇴|TO|Tonga|
|🇹🇹|TT|Trinidad and Tobago|
|🇹🇳|TN|Tunisia|
|🇹🇲|TM|Turkmenistan|
|🇹🇨|TC|Turks and Caicos Islands|
|🇹🇻|TV|Tuvalu|
|🇹🇷|TR|Türkiye|
|🇻🇮|VI|US Virgin Islands|
|🇺🇬|UG|Uganda|
|🇺🇦|UA|Ukraine|
|🇦🇪|AE|United Arab Emirates|
|🇬🇧|GB|United Kingdom|
|🇺🇸|US|United States|
|🇺🇾|UY|Uruguay|
|🇺🇿|UZ|Uzbekistan|
|🇻🇺|VU|Vanuatu|
|🇻🇦|VA|Vatican City|
|🇻🇪|VE|Venezuela|
|🇻🇳|VN|Vietnam|
|🇼🇫|WF|Wallis and Futuna|
|🇾🇪|YE|Yemen|
|🇿🇲|ZM|Zambia|
|🇿🇼|ZW|Zimbabwe|
