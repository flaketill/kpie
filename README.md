KPie
----

A simple window manipulation tool, modeled after devil's pie.

The configuration is dynamic and built around lua.


Overview
--------

If the file `~/.kpie.lua` exists then it will be parsed every time a new
window is opened upon your system.  If you start `kpie` with a named
Lua file that will be used instead, for example:

   $ kpie ~/.config/kpie.lua

Regardless of what the filename is the configuration file is pure-lua with
the addition of some window-related primitives.  To give you a flavour this
is the default configuration file:


    --
    -- If Xine is launched it should be "always on top"
    --
    if ( window_class() == "xine" ) then
        above()
    end

    --
    -- The xlogo program is so cool it should be visible on all
    -- workspaces
    --
    if ( window_title() == "xlogo" ) then
        pin()
    end


Helper
------

Included within the repository is a configuration file called `dump.lua`,
this is designed to provide a helpful starting point if you wish to script
the manipulation of your windows.

Simply run:

   $ ./kpie ./dump.lua

This will output chunks of config which you can edit or save:

    -- Screen width : 1920
    -- Screen height: 1080
    if ( ( window_title() == "emacs@shelob.my.flat: README.md ** /home/skx/git/kpie/README.md" ) and
         ( window_class() == "emacs" ) ) then
         xy(595,43 )
         size(658,558 )
         workspace(1)
    end
    if ( ( window_title() == "feeds" ) and
         ( window_class() == "Pidgin" ) ) then
         xy(0,33 )
         size(1920,1023 )
         workspace(2)
    end
    if ( ( window_title() == "Buddy List" ) and
         ( window_class() == "Pidgin" ) ) then
         xy(2,33 )
         size(824,1023 )
         workspace(2)
    end

As you can see this has iterated over all existing windows, and shown
you their current state - this is perfect if you wish to reproduce a
complex layout interactively.



Installation
------------

Firstly install the dependencies:

      sudo apt-get install libwnck-de
      sudo apt-get install liblua5.1-0-dev

Then build via:

    make



Primitives
----------

The following primitives are available:

* Information
  * `window_title` - Get the title of the new window.
  * `window_class` - Get the class of the new window.
  * `window_id` - Get the ID of the new window.
  * `window_pid` - Get the PID of the new window.
  * `screen_height` - Get the size of the screen.
  * `screen_width` - Get the size of the screen.
* Depth
  * `above` - Make the window "always on top".
  * `below` - Remove the "always on top" flag.
* Max/Min
  * `maximize` - Maximize the window.
  * `fullscreen` - Make the window "fullscreen".
  * `is_maximized` - Is the window maximized?
  * `is_fullscreen` - Is the window fullscreen?
* Workspace
  * `pin` - Pin on all workspaces.
  * `unpin` - Don't pin on all workspaces.
* Movement
  * `xy` - Get/Set the X/Y coordinates of a window.
  * `size` - Get/Set the width/height of a window.
* Misc
  * `focus` - Focus the window.
  * `workspace` - Get/set the workspace the window is active on.  (Return value will be -1 if the window is pinned, or invisible).
