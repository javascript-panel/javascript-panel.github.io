# Styling Ranges Of Text

!!! note
	If any text you pass to `JsGraphics WriteText` or `utils.CreateTextLayout` contain `$rgb`/`$font` code,
	any colour/font arrays described on this page will be ignored. Title formatting always take precedence.

## Using `JsGraphics WriteText`

This first example uses [JsGraphics WriteText](../api/interfaces/JsGraphics.md#writetexttext-font-colour-x-y-w-h-text_alignment-paragraph_alignment-word_wrapping-trimming_granularity)
where you can apply custom fonts/colours to a single string.

The limitation here is that scrolling text vertically is not supported so if you need that, you'll need to use
the `utils.CreateTextLayout` examples below.

!!! example
	```js
	'use strict';

	include('helpers');

	/*
	This sample splits a string in to whole words and then randomly
	styles each one. Every element of the array which is used for
	styling must have a valid start/length value. You can see
	how the start value is incremented for each word.
	*/

	const installed_fonts = utils.ListFonts();
	const text = 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.';

	let colour_string = '';
	let font_string = '';

	// split text in to whole words for styling
	const words = text.split(' ');

	refresh();

	function refresh() {
		const fonts = [], colours = [];
		let start = 0;

		words.forEach((word, i) => {
			// length of word plus following space
			const len = word.length + 1;

			colours.push({
				// when using an array of colours, Start and Length are mandatory
				Start : start,
				Length : len,
				Colour : RGB(Math.random() * 200, Math.random() * 200, Math.random() * 200),
			});

			fonts.push({
				// when using an array of fonts, Start and Length are mandatory
				Start : start,
				Length : len,
				// the following are all optional and may be omitted. Segoe UI/16px will be used if Name/Size are not specified.
				Name : installed_fonts[Math.floor(Math.random() * installed_fonts.length)],
				Size : 12 + Math.floor(Math.random() * 20),
				Weight : Math.round(Math.random() * 800) + 100, // values between 100-900
				Underline : Math.random() < 0.1,
				Strikethrough : Math.random() < 0.1,
			});

			// increment start position for next word
			start += len;
		});

		colour_string = JSON.stringify(colours);
		font_string = JSON.stringify(fonts);
	}

	function on_paint(gr) {
		gr.WriteText(text, font_string, colour_string, 10, 10, window.Width - 20, window.Height - 20);
	}
	```

## Using `utils.CreateTextLayout`
This example demonstrates scrollable text, a single font and a different colour per word.

!!! example
	```js
	'use strict';

	include('helpers');

	const text = 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.';
	const font_string = CreateFontString('Segoe UI', 20);
	const layout = utils.CreateTextLayout(text, font_string);
	let offset = 0;
	let text_height = 0;

	// split text in to whole words for colouring
	const words = text.split(' ');
	let colour_string = '';

	refresh();

	function refresh() {
		const colours = [];
		let start = 0;

		words.forEach((word, i) => {
			// length of word plus following space
			const len = word.length + 1;

			colours.push({
				// when using an array, Start and Length are mandatory
				Start : start,
				Length : len,
				Colour : RGB(Math.random() * 200, Math.random() * 200, Math.random() * 200),
			});

			// increment start position for next word
			start += len;
		});

		colour_string = JSON.stringify(colours);
	}

	const box = {
		x : 50,
		y : 50,
		w : 0,
		h : 0,
	}

	function on_paint(gr) {
		gr.Clear(RGB(255, 255, 255));
		gr.DrawRectangle(box.x, box.y, box.w, box.h, 1, RGB(255, 0, 0));
		gr.WriteTextLayout(layout, colour_string, box.x, box.y, box.w, box.h, offset);
	}

	function on_mouse_wheel(step) {
		if (text_height < box.h)
			return;

		offset += step * 60;

		if (offset > 0)
			offset = 0;
		else if (offset < box.h - text_height)
			offset = box.h - text_height;

		window.Repaint();
	}

	function on_size() {
		box.w = window.Width / 2;
		box.h = window.Height / 2;
		text_height = layout.CalcTextHeight(box.w);

		if (text_height < box.h)
			offset = 0;
		else if (offset < box.h - text_height)
			offset = box.h - text_height;
	}
	```

This example demonstrates scrollable text, per-word colouring and per-word fonts.

!!! example
	```js
	'use strict';

	include('helpers');

	const installed_fonts = utils.ListFonts();
	const text = 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.';
	let layout = null;
	let offset = 0;
	let text_height = 0;
	let colour_string = '';

	// split text in to whole words for styling
	const words = text.split(' ');

	refresh();

	function refresh() {
		const fonts = [];
		const colours = [];
		let start = 0;

		words.forEach((word, i) => {
			// length of word plus following space
			const len = word.length + 1;

			fonts.push({
				// When using an array of fonts, Start and Length are mandatory
				Start : start,
				Length : len,
				// The following are all optional and may be omitted.
				// Segoe UI/16px will be used if Name/Size are not specified.
				Name : installed_fonts[Math.floor(Math.random() * installed_fonts.length)],
				Size : 12 + Math.floor(Math.random() * 20),
				Weight : Math.round(Math.random() * 800) + 100, // values between 100-900
				Underline : Math.random() < 0.1,
				Strikethrough : Math.random() < 0.1,
			});

			colours.push({
				// When using an array of colours, Start and Length are mandatory
				Start : start,
				Length : len,
				Colour : RGB(Math.random() * 200, Math.random() * 200, Math.random() * 200),
			});

			// increment start position for next word
			start += len;
		});

		// Stringify the fonts and create the text layout
		const font_string = JSON.stringify(fonts);
		layout = utils.CreateTextLayout(text, font_string);

		// Stringify the colours. This is passed to WriteTextLayout inside on_paint
		colour_string = JSON.stringify(colours);
	}

	const box = {
		x : 50,
		y : 50,
		w : 0,
		h : 0,
	}

	function on_paint(gr) {
		gr.Clear(RGB(255, 255, 255));
		gr.DrawRectangle(box.x, box.y, box.w, box.h, 1, RGB(255, 0, 0));

		/*
		The 2nd arg of gr.WriteTextLayout is the colour which can be a
		number if you want the same colour for the whole range of text.

		In this example, we're using the stringified colours array created in the
		refresh method above.
		*/
		gr.WriteTextLayout(layout, colour_string, box.x, box.y, box.w, box.h, offset);
	}

	function on_mouse_wheel(step) {
		if (text_height < box.h)
			return;

		offset += step * 60;

		if (offset > 0)
			offset = 0;
		else if (offset < box.h - text_height)
			offset = box.h - text_height;

		window.Repaint();
	}

	function on_size() {
		box.w = window.Width / 2;
		box.h = window.Height / 2;
		text_height = layout.CalcTextHeight(box.w);

		if (text_height < box.h)
			offset = 0;
		else if (offset < box.h - text_height)
			offset = box.h - text_height;
	}
	```
