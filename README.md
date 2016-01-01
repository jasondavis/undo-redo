undo-redo stack
===============

**undo-redo** is an all-purpose lightweight undo/redo stack which you
can store any kind of custom data to.

**undo-redo** comes with simple methods to undo, redo, get status (for
buttons), do stack dump (for storage) and more.

**undo-redo** will take care of all the logistics for you.


Features
--------

- Lightweight (< 1 kb) and efficient
- Add any kind of data to the stack (text, images, canvas data, objects, arrays etc.).
- Single undo() call, returns object for new state
- Single redo() call, returns object for new state (if possible)
- Can use callback functions on undo/redo
- Set optional limit (with fifo)
- Get undo/redo status, count and pointer
- Get current stack so it can be stored persistently.
- HTML documentation included in addition to source documentation

See the `tests` directory for example usage.


Install
-------

**undo-redo** can be installed in various ways:

- Bower: `bower install undo-redo`
- Git using HTTPS: `git clone https://github.com/epistemex/undo-redo.git`
- Git using SSH: `git clone git@github.com:epistemex/undo-redo.git`
- Download [zip archive](https://github.com/epistemex/undo-redo/archive/master.zip) and extract.
- [undo-redo.js](https://raw.githubusercontent.com/epistemex/undo-redo/master/src/undo-redo.js)
- [undo-redo.min.js](https://raw.githubusercontent.com/epistemex/undo-redo/master/undo-redo.min.js)


Usage
-----

Include the script in your project, then create an instance:

    var stack = new UndoRedo();

At this point we can start adding states to the stack:

    stack.add(myData);               // push data to stack, each add is one undo state

To undo, simply call the undo() method. Data from the previous state is returned.
If at first entry null will be returned as there won't be a previous state.

    var data = stack.undo();         // return previous state data
    if (data) ...set data...         // see tests directory for sample usage

If no `add()` was called since last undo, you can call `redo()`. The data for
new current state is returned, or null if a redo was not possible.

    var data = stack.redo();         // redo and return data for next state if any
    if (data) ...set data...

Or using callbacks:

    var stack = new UndoRedo();
    stack.onundo = function(data) { ... };	// get data or null
    stack.onredo = function(data) { ... };	// get data or null
    ...
    stack.undo();                           // invokes callback

or by options:

    var stack = new UndoRedo({
		limit: 100,                         // defaults to -1 = unlimited
	    onUndo: undoCallback,
	    onRedo: redoCallback
    });

See the `tests` directory for example usage.


License
-------

Released under [MIT license](http://choosealicense.com/licenses/mit/). You may use this class in both commercial and non-commercial projects provided that full header (minified and developer versions) is included.

*&copy; 2015-2016 Epistemex*

![Epistemex](http://i.imgur.com/wZSsyt8.png)