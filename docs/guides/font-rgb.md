# $font & $rgb

!!! note
	`gr.WriteTextSimple` does not support text containing `$rgb` / `$font` code. It will still strip the code so text is displayed properly.

### $rgb
You can use these colour methods which are documented [here](https://wiki.hydrogenaud.io/index.php?title=Foobar2000:Title_Formatting_Reference#Historical_and_Columns_UI_color_functions).

```
$rgb(r,g,b) // only the 3 value variant is supported
$rgb()
$hsl(h,s,l) // only the 3 value variant is supported
$hsl()
$blend(colour1,colour2,part,total)
$transition(string,colour1,colour2)
```

!!! example
	```js
	'use strict';
	include('helpers');

	const tfo = fb.TitleFormat('$rgb(255,0,0)%artist% $rgb(0,255,0)%title%');
	const default_font = CreateFont('Segoe UI', 20);
	const default_colour = RGB(0, 0, 0);
	let str = '';

	refresh();

	function refresh() {
		str = fb.GetFocusItem()?.FormatTitle(tfo) || '';
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
		gr.Clear(RGB(255, 255, 255));
		gr.WriteText(str, default_font, default_colour, 0, 0, window.Width, window.Height, 2, 2, 2);
	}
	```

### $font
This is not a common function and is exclusive to `JavaScript Panel`. It takes up to 6 values.

`$font(name,size,weight,style,underline,strikethrough)`

If changing the font, you must the supply the `name` and `size` values. The rest are optional.

|Value||
|---|---|
|size|Supported values are `8` - `144`.
|weight|Default `400`, `700` is bold. Supported values are `100` - `950`.|
|style|Default `0`. Use `1` for `oblique` or `2` for `italic`.|
|underline|Default `0`. Use `1` to enable.|
|strikethrough|Default `0`. Use `1` to enable.|

You can use `$font()` with no values to reset back to default.
