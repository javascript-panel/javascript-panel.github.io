# playback

**Properties**

|||||
|---|---|---|---|
|playback.CursorFollowPlayback|`boolean`|read, write|
|playback.CustomVolume|`number`|read|See note below.
|playback.IsPaused|`boolean`|read|
|playback.IsPlaying|`boolean`|read|
|playback.Length|`number`|read|
|playback.Order|[PlaybackOrder](../flags.md#playbackorder)|read,write|
|playback.PlaybackFollowCursor|`boolean`|read, write|
|playback.ReplaygainMode|[ReplaygainMode](../flags.md#replaygainmode)|read, write|
|playback.StopAfterCurrent|`boolean`|read, write|
|playback.Time|`number`|read, write|
|playback.Volume|`number`|read, write|See note below.

!!! note "Custom Volume"
	`playback.CustomVolume` can be used for displaying the volume from `UPnP` devices. It will return
	a value of `-1` when using a normal device and that also indicates that `playback.Volume` is writable.
	When a custom volume control is active, you can not use `playback.Volume` and must use `playback.VolumeUp()` / `playback.VolumeDown()` / `playback.VolumeMute()`.

**Methods**
## `playback.GetActiveDSPs()`
Returns an array.

## `playback.GetDSPPresets()`
Returns a `JSON` array in string form so you need to use `JSON.parse` on the result.

!!! example
	```js
	var str = playback.GetDSPPresets();
	console.log(str);
	```

	``` markdown title="Example output"
	[
		{
			"Active": true,
			"Name": "two"
		},
		{
			"Active": false,
			"Name": "three"
		}
	]
	```

	```js
	var arr = JSON.parse(str);
	console.log(arr.length); // number of presets

	for (var i = 0; i < arr.length; i++) {
		if (arr[i].Active) {
			// this is the active preset, do something with the Name??
		}
	}
	```

## `playback.GetNowPlaying()`
Returns a [JsMetadbHandle](../interfaces/JsMetadbHandle.md) instance.

It will be the now playing item or `null` if [foobar2000](https://www.foobar2000.org) isn't playing.

## `playback.GetOrderNames()`
Returns an array.

This is an array of playback order names which can be iterated
or used with `playback.Order`.

!!! example
	=== "Current"
		```js
		console.log(playback.GetOrderNames()[playback.Order]);
		```

	=== "Loop"
		```js
		var arr = playback.GetOrderNames();
		for (var i = 0; i < arr.length; i++) {
			console.log(arr[i]);
		}
		```

## `playback.GetOutputDevices()`
Returns a `JSON` array in string form so you need to use `JSON.parse` on the result.

!!! example
	```js
	var str = playback.GetOutputDevices();
	console.log(str);
	```

	``` markdown title="Example output"
	[
		{
			"Active": false,
			"DeviceID": "5243F9AD-C84F-4723-8194-0788FC021BCC",
			"Name": "Null Output",
			"OutputID": "EEEB07DE-C2C8-44C2-985C-C85856D96DA1"
		},
		{
			"Active": true,
			"DeviceID": "00000000-0000-0000-0000-000000000000",
			"Name": "Primary Sound Driver",
			"OutputID": "D41D2423-FBB0-4635-B233-7054F79814AB"
		},
		{
			"Active": false,
			"DeviceID": "5F6D1D66-4815-4E05-B779-CE7FD5745FBB",
			"Name": "SPDIF-Out (Sound Blaster Z)",
			"OutputID": "D41D2423-FBB0-4635-B233-7054F79814AB"
		},
		{
			"Active": false,
			"DeviceID": "82CDE792-1C9B-4243-BC8B-D07DA9E37068",
			"Name": "Speakers (Sound Blaster Z)",
			"OutputID": "D41D2423-FBB0-4635-B233-7054F79814AB"
		},
		{
			"Active": false,
			"DeviceID": "B6FC1E61-C2E2-4C45-BCA8-4F9B15D148D3",
			"Name": "4 - LG FHD (AMD High Definition Audio Device)",
			"OutputID": "D41D2423-FBB0-4635-B233-7054F79814AB"
		},
		{
			"Active": false,
			"DeviceID": "00000000-0000-0000-0000-000000000000",
			"Name": "Primary Sound Driver [exclusive]",
			"OutputID": "0DD9B977-765B-4804-BF2D-B28EBF0C510D"
		},
		{
			"Active": false,
			"DeviceID": "5F6D1D66-4815-4E05-B779-CE7FD5745FBB",
			"Name": "SPDIF-Out (Sound Blaster Z) [exclusive]",
			"OutputID": "0DD9B977-765B-4804-BF2D-B28EBF0C510D"
		},
		{
			"Active": false,
			"DeviceID": "82CDE792-1C9B-4243-BC8B-D07DA9E37068",
			"Name": "Speakers (Sound Blaster Z) [exclusive]",
			"OutputID": "0DD9B977-765B-4804-BF2D-B28EBF0C510D"
		},
		{
			"Active": false,
			"DeviceID": "B6FC1E61-C2E2-4C45-BCA8-4F9B15D148D3",
			"Name": "4 - LG FHD (AMD High Definition Audio Device) [exclusive]",
			"OutputID": "0DD9B977-765B-4804-BF2D-B28EBF0C510D"
		}
	]
	```

	```js
	var arr = JSON.parse(str);
	console.log(arr.length); // number of devices
	```

As you can see, only one of the items in the array has `Active`
set to `true` so that is the device you'd want to display the name of
or mark as selected in a menu.

To change device you can use [fb.RunMainMenuCommand](fb.md#fbrunmainmenucommandcommand) with the
device name or use [playback.SetOutputDevice](#playbacksetoutputdeviceoutputid-deviceid) with the
`DeviceID`/`OutputID`.

!!! example
	=== "RunMainMenuCommand"
		```js
		var str = playback.GetOutputDevices();
		var arr = JSON.parse(str);
		// Assuming same list from above, switch output to "Primary Sound Driver [exclusive]".
		fb.RunMainMenuCommand("Playback/Device/" + arr[5].Name);
		```

	=== "SetOutputDevice"
		```js
		var str = playback.GetOutputDevices();
		var arr = JSON.parse(str);
		// Assuming same list from above, switch output to "Primary Sound Driver [exclusive]".
		playback.SetOutputDevice(arr[5].OutputID, arr[5].DeviceID);
		```

## `playback.Next()`
Shortcut to main menu command.

No return value.

## `playback.Pause()`
Shortcut to main menu command.

No return value.

## `playback.Play()`
Shortcut to main menu command.

No return value.

## `playback.PlayOrPause()`
Shortcut to main menu command.

No return value.

## `playback.Previous()`
Shortcut to main menu command.

No return value.

## `playback.Random()`
Shortcut to main menu command.

No return value.

## `playback.SetDSPPreset(idx)`
|Arguments|||
|---|---|---|
|idx|`number`|

No return value. See [playback.GetDSPPresets](#playbackgetdsppresets).

## `playback.SetOutputDevice(OutputID, DeviceID)`
|Arguments|||
|---|---|---|
|OutputID|`string`|
|DeviceID|`string`|

No return value. See [playback.GetOutputDevices](#playbackgetoutputdevices).

## `playback.Stop()`
Shortcut to main menu command.

No return value.

## `playback.VolumeDown()`
Shortcut to main menu command.

No return value.

## `playback.VolumeMute()`
Shortcut to main menu command.

No return value.

## `playback.VolumeUp()`
Shortcut to main menu command.

No return value.
