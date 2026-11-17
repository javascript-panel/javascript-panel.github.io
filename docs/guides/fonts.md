# Fonts
This page is for working with fonts that are passed to
[JsGraphics WriteText](../api/interfaces/JsGraphics.md#writetexttext-font-colour-x-y-w-h-text_alignment-paragraph_alignment-word_wrapping-trimming_granularity),
[JsGraphics WriteTextSimple](../api/interfaces/JsGraphics.md#writetextsimpletext-font-colour-x-y-w-h-text_alignment-paragraph_alignment-word_wrapping-trimming_granularity) and
[utils.CreateTextLayout](../api/namespaces/utils.md#utilscreatetextlayouttext-font_str-text_alignment-paragraph_alignment-word_wrapping-trimming_granularity).

In this component, fonts are standard `JavaScript` objects.

These are all of the supported properties but none are mandatory.

```js
const font = {
	Name : name, // string
	Size : size, // number
	Weight : weight, // number
	Style : style, // number
	Stretch : stretch, // number
	Underline : underline, // boolean
	Strikethrough : strikethrough, // boolean
};
```

!!! note
	`JsGraphics WriteTextSimple` does not support `Underline` or `Strikethrough`.

See [Flags](../api/flags.md) for supported `Weight`, `Style` and `Stretch` values.

You can even supply an undefined font argument
and `Segoe UI` and `16px` will be used.

!!! example
	```js
	include('helpers');

	let undefined_font;
	const colour = RGB(0, 0, 0);

	function on_paint(gr) {
		gr.WriteText("some text", undefined_font, colour, 0, 0, window.Width, window.Height);
	}
	```

## Using `window.GetUIFont`.
!!! example
	```js
	const font = window.GetUIFont(0);
	console.log(JSON.stringify(font, null, 4));
	```

	``` markdown title="Example output"
	{
		"Name": "Segoe UI",
		"Size": 12,
		"Stretch": 5,
		"Style": 0,
		"Weight": 400
	}
	```

The returned `font` can be passed directly without modification.

!!! example
	```js
	include('helpers');

	const font = window.GetUIFont(0);
	const colour = RGB(0, 0, 0);

	function on_paint(gr) {
		gr.WriteText("some text", font, colour, 0, 0, window.Width, window.Height);
	}
	```

!!! note
	Not all fonts supported by `Default UI` can be used by this component. This
	is because it uses older `GDI` graphics whereas this component uses `DirectWrite`. If
	an unsupported font is detected, the method will fallback to returning `Segoe UI`. The most
	likely cause of this happening would be using `Raster` fonts like `System` or `Small Fonts`.

All properties of the font are writable to you can make any changes you like.

!!! example
	```js
	let font = window.GetUIFont(0);

	// double the size, leave other properties untouched.
	font.Size = font.Size * 2;
	```

## Creating your own from scratch
Writing your own object for every font you create would be a bit cumbersome
so `helpers.js` contains a simplified method to use anywhere.

```js
function CreateFont(name, size, bold) {
	return {
		Name : name,
		Size : Math.round(size * DPI / 72), // DPI comes from window.DPI
		Weight : bold ? DWRITE_FONT_WEIGHT_BOLD : DWRITE_FONT_WEIGHT_NORMAL
	};
}
```

Now it's easier to write...

```js
const font = CreateFont("Verdana", 16);
const large_bold_font = CreateFont("Verdana", 24, true);
```

You can of course write your own if you need more customisation.

## Advanced usage
When using [utils.CreateTextLayout](../api/namespaces/utils.md#utilscreatetextlayouttext-font_str-text_alignment-paragraph_alignment-word_wrapping-trimming_granularity),
you can also supply an array of fonts and apply them to a single string. You can style each word or even character
independently. See [Styling Ranges Of Text](styling-ranges-text.md).
