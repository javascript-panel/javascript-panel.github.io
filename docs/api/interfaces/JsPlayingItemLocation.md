**Properties**

||||
|---|---|---|
IsValid|`boolean`|read|
PlaylistIndex|`number`|read|
PlaylistItemIndex|`number`|read|

`IsValid` will be `false` if [foobar2000](https://www.foobar2000.org) isn't playing
or the playing track does does not belong to belong to a playlist.

!!! example
	```js
	var playing_item_location = plman.GetPlayingItemLocation();
	if (playing_item_location.IsValid) {
		console.log(playing_item_location.PlaylistIndex);
		console.log(playing_item_location.PlaylistItemIndex);
	}
	```
