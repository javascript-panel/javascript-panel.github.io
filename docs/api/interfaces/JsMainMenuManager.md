## `BuildMenu(parentMenu, base_id)`
|Arguments|||
|---|---|---|
|parentMenu|[JsMenuObj](JsMenuObj.md)|
|base_id|`number`|

No return value.

## `ExecuteByID(id)`
|Arguments|||
|---|---|---|
|id|`number`|

Returns a `boolean` value.

!!! example
	```js
	include('helpers');

	// Click anywhere in the panel to open the menu.

	function on_mouse_lbtn_up(x, y) {
		const menu = window.CreatePopupMenu();
		const file_popup = window.CreatePopupMenu();
		const edit_popup = window.CreatePopupMenu();
		const view_popup = window.CreatePopupMenu();
		const playback_popup = window.CreatePopupMenu();
		const library_popup = window.CreatePopupMenu();
		const help_popup = window.CreatePopupMenu();

		const file_menu = fb.CreateMainMenuManager('File');
		const edit_menu = fb.CreateMainMenuManager('Edit');
		const view_menu = fb.CreateMainMenuManager('View');
		const playback_menu = fb.CreateMainMenuManager('Playback');
		const library_menu = fb.CreateMainMenuManager('Library');
		const help_menu = fb.CreateMainMenuManager('Help');

		file_menu.BuildMenu(file_popup, 1000);
		edit_menu.BuildMenu(edit_popup, 2000);
		view_menu.BuildMenu(view_popup, 3000);
		playback_menu.BuildMenu(playback_popup, 4000);
		library_menu.BuildMenu(library_popup, 5000);
		help_menu.BuildMenu(help_popup, 6000);

		file_popup.AppendTo(menu, MF_STRING, 'File');
		edit_popup.AppendTo(menu, MF_STRING, 'Edit');
		view_popup.AppendTo(menu, MF_STRING, 'View');
		playback_popup.AppendTo(menu, MF_STRING, 'Playback');
		library_popup.AppendTo(menu, MF_STRING, 'Library');
		help_popup.AppendTo(menu, MF_STRING, 'Help');

		const idx = menu.TrackPopupMenu(x, y);

		switch (true) {
		case idx == 0:
			break;
		case idx < 2000:
			file.ExecuteByID(idx - 1000);
			break;
		case idx < 3000:
			edit.ExecuteByID(idx - 2000);
			break;
		case idx < 4000:
			view.ExecuteByID(idx - 3000);
			break;
		case idx < 5000:
			playback.ExecuteByID(idx - 4000);
			break;
		case idx < 6000:
			library.ExecuteByID(idx - 5000);
			break;
		case idx < 7000:
			help.ExecuteByID(idx - 6000);
			break;
		}
	}
	```
