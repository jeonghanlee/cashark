Wireshark disector plugin for Channel Access protocol
=====================================================

Tested with wireshark 1.2.11, 1.8.2, and 1.10.8.

Using
-----

Only the file ca.lua is needed.  Then start wireshark with

    wireshark -X lua_script:/path/to/ca.lua

Status
------

This plugin does general decoding of CA UDP and TCP traffic on the standard
ports (5064 and 5065).  It does TCP segment reassembly for large messages.

The CA protocol provides no easy way to distinguish client and server
messages without observing the start of the connection.  Thus this plugin
can not fully decode all messages.  Currently only some messages are fully decoded.
Others decode with only generic field names.

DBR data in get, put, and monitor operations is not decoded.

Reporting bugs
--------------

Bug reports are welcome (and patches more so).

Send to "Michael Davidsaver" <mdavidsaver@bnl.gov>
or open a [github] [gh] issue.

If possible, please include a packet capture file which will trigger the error.

[gh]: https://github.com/mdavidsaver/cashark/issues

Setup
-----

To automatically load the CA disector *instead* of using the -X argument.

Edit /etc/wireshark/init.lua and remove or comment out the line about
disabling LUA support ("`disable_lua = true`").  You may also need
to change the line "`run_user_scripts_when_superuser = false`"
depending on how you run wireshark.

Next copy the file ca.lua from this repository to /etc/wireshark/.

Then add a line to the end of init.lua.

    dofile("ca.lua")

If all goes well the string "Load CA" will be printed to the console
when wireshark starts.

To install this for a single user create `$HOME/.wireshark/init.lua` with
a single line "`dofile("ca.lua")`" and place ca.lua in this directory.