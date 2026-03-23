# Overview
This component for [foobar2000](https://www.foobar2000.org) allows the creation of customisable panels that can be written with
`JavaScript` rather than the `C++` required by the [foobar2000 SDK](https://www.foobar2000.org/SDK).

It is based on `JScript Panel 3` and `Spider Monkey Panel`. While the scripting engine is
`Spider Monkey`, nothing else from `Spider Monkey Panel` survives. It's basically
`JScript Panel 3` with modern `JavaScript`. It's 64bit only and it has been updated
to `Spider Monkey` `esr115.33`.

# Features
Here are just some of the features provided by the component...

* Custom drawing of text, external images, lines, rectangles, etc.
* Use fonts/colours from the main preferences of whichever user interface you are using.
* Executing main/context menu commands.
* Ability to create custom buttons/menus.
* Capture keystrokes/mouse movement/clicks.
* [Callbacks](api/callbacks/index.md) can be used to trigger code based on various `foobar2000`, `Windows` and `Component` events.
* Read/[write](api/interfaces/JsMetadbHandleList.md#updatefileinfofromjsonstr) file tags.
* Complete manipulation of playlists.
* Media Library display/sorting/filtering
* [Save settings](api/namespaces/window.md#windowgetpropertyname-default_value) on a per panel basis. These persist between restarts
and are stored inside the layout configuration file for whichever UI your are using. You can also write your own functions to
load/save settings from `JSON` or plain text files.
* [Built in support](api/namespaces/utils.md#utilshttprequestasynctype-url-user_agent_or_headers-body) for
making `GET / POST` requests which return plain text and there is also a method for downloading binary files.
* There are many built in methods for working with the local filesystem, launching external applications etc.
* And much more...
