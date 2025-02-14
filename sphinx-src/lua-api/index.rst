Lua API
#######

|Vendor| controllers offer a Lua API providing access to system information, playback functions and trigger operations.

.. toctree::
   :hidden:

   adjustment-target
   bps
   content-target
   controller
   date-time
   group
   location
   override
   project
   protocol-interface
   replication
   rio
   scene
   system
   temperature
   time
   timeline
   universe
   variant

Functions
*********

The following functions are available in trigger action scripts and in IO modules. In trigger action scripts they are added directly to the environment; in IO modules they are available in the ``controller`` namespace.

Queries
=======

.. _Lua_get_current_project:

get_current_project
-------------------

Returns a :doc:`project` object.

For example:

.. include:: code-examples/project.rst


.. _Lua_get_current_replication:

get_current_replication
-----------------------

Returns a :doc:`replication` object.

For example:

.. include:: code-examples/replication.rst


.. _Lua_get_location:

get_location
------------

Returns a :doc:`location` object.

For example:

.. include:: code-examples/location.rst


.. _Lua_get_timeline:

get_timeline
------------

``get_timeline(timelineNum)``

Returns a single :doc:`timeline` object for the timeline with user number ``timelineNum``.

For example:

.. include:: code-examples/timeline.rst


.. _Lua_get_scene:

get_scene
---------

``get_scene(sceneNum)``

Returns a single :doc:`scene` object for the scene with user number ``sceneNum``.

For example:

.. include:: code-examples/scene.rst


.. _Lua_get_group:

get_group
---------

``get_group(groupNum)``

Returns a single :doc:`group` object for the group with user number ``groupNum``.

For example:

.. include:: code-examples/group.rst

.. note::

   Passing 0 as ``groupNum`` will return :doc:`group` for the *All Fixtures* group. This can also be used on |VLC| family projects to master the intensity of the entire unit.


.. _Lua_get_fixture_override:

get_fixture_override
--------------------

``get_fixture_override(fixtureNum)``

Returns an :doc:`override` object for the fixture with user number ``fixtureNum``.

For example:

.. include:: code-examples/fixture-override.rst


.. _Lua_get_group_override:

get_group_override
------------------

``get_group_override(groupNum)``

Returns an :doc:`override` object for the group with user number ``groupNum``.

.. note::

   Passing 0 as ``groupNum`` will return an :doc:`override` for the *All Fixtures* group.

For example:

.. include:: code-examples/group-override.rst


.. _Lua_get_current_controller:

get_current_controller
----------------------

Returns the :doc:`controller` that the script is being executed on.

For example:

.. include:: code-examples/current-controller.rst


.. _Lua_get_network_primary:

get_network_primary
-------------------

Returns the :doc:`controller` in the project that is set as the *network primary*.


.. _Lua_is_controller_online:

is_controller_online
--------------------

``is_controller_online(controllerNum)``

Returns true if the controller with user number ``controllerNum`` has been discovered, or false otherwise.

For example:

.. code-block:: lua

   if (is_controller_online(2)) then
     log("Controller 2 is online")
   else
     log("Controller 2 is offline")
   end


.. _Lua_get_temperature:

get_temperature
---------------

Returns a :doc:`temperature` object with measurements from the controller's temperature sensors.

For example:

.. include:: code-examples/temperature.rst


.. _Lua_get_rio:

get_rio
-------

``get_rio(type, num)``

Returns a :doc:`rio` object representing a RIO matching the parameters:

* ``type`` can be one of the constants ``RIO80``, ``RIO44`` or ``RIO80``.
* ``num`` is the remote device number within the Designer project.

For example:

.. include:: code-examples/rio44.rst

.. note::

   The constants for ``type`` are in the ``controller`` namespace within IO modules, e.g. ``controller.RIO44``.


.. _Lua_get_bps:

get_bps
-------

``get_bps(num)``

Returns a :doc:`bps` object with remote device number ``num``.

For example:

.. include:: code-examples/bps-get-state.rst


.. _Lua_get_text_slot:

get_text_slot
-------------

``get_text_slot(slotName)``

Returns the value of the text slot with name ``slotName``. If no such text slot exists in the project then an empty string will be returned.

For example:

.. code-block:: lua

   log(get_text_slot("my text slot"))


.. _Lua_get_dmx_universe:

get_dmx_universe
----------------

``get_dmx_universe(idx)``

Returns a :doc:`universe` object for the DMX universe with number ``idx``.

For example:

.. include:: code-examples/universe.rst


.. _Lua_get_artnet_universe:

get_artnet_universe
-------------------

``get_artnet_universe(idx)``

Returns a :doc:`universe` object for the Art-Net universe with number ``idx``.


.. _Lua_get_pathport_universe:

get_pathport_universe
---------------------

``get_pathport_universe(idx)``

Returns a :doc:`universe` object for the Pathport universe with number ``idx``.


.. _Lua_get_sacn_universe:

get_sacn_universe
-----------------

``get_sacn_universe(idx)``

Returns a :doc:`universe` object for the sACN universe with number ``idx``.


.. _Lua_get_kinet_universe:

get_kinet_universe
------------------

``get_kinet_universe(power_supply_num, port_num)``

Returns a :doc:`universe` object for the KiNET power supply port matching the parameters:

* ``power_supply_num`` is the KiNET power supply number in the project.
* ``port_num`` is the port number of the KiNET power supply.


.. _Lua_get_edn_universe:

get_edn_universe
----------------

``get_edn_universe(remote_device_type, remote_device_num, port_num)``

Returns a :doc:`universe` object for the |EDN| output matching the parameter:

* ``remote_device_type`` is be one of the constants ``EDN10`` or ``EDN 20``.
* ``remote_device_num`` is the remote device number of the |EDN| in the project.
* ``port_num`` is the DMX output port number of the |EDN|.

.. note::

   The constants for ``remote_device_type`` are in the ``controller`` namespace within IO modules, e.g. ``controller.EDN20``.


.. _Lua_get_input:

get_input
---------

``get_input(idx)``

Returns the state of the controller's input numbered ``idx`` as a boolean (for digital inputs) or an integer (for analog inputs).

For example:

.. code-block:: lua

   in1 = get_input(1)

   if in1 == true then
     log("Input 1 is digital and high")
   elseif in1 == false then
     log("Input 1 is digital and low")
   else
     log("Input 1 is analog at " .. in1)
   end


.. _Lua_get_dmx_input:

get_dmx_input
-------------

``get_dmx_input(channel)``

Returns the value of the DMX ``channel`` number as an integer. If no DXM input is detected then ``nil`` will be returned.


.. _Lua_get_trigger_variable:

get_trigger_variable
--------------------

``get_trigger_variable(idx)``

Returns the trigger variable at index ``idx`` as a :doc:`variant`.

For example:

.. code-block:: lua

   -- Use with a Touch Colour Move Trigger 
   red = get_trigger_variable(1).integer
   green = get_trigger_variable(2).integer
   blue = get_trigger_variable(3).integer

   -- Use with Serial Input "<s>\r\n"
   input = get_trigger_variable(1).string


.. _Lua_get_trigger_number:

get_trigger_number
------------------

``get_trigger_number()``

Returns the number of the trigger that ran this script. Will return ``nil`` if called from another context.


.. _Lua_get_resource_path:

get_resource_path
-----------------

``get_resource_path(filename)``

Returns the path to the resource file, where ``filename`` is the name of a file on the controller's internal storage.

For example:

.. code-block:: lua

   dofile(get_resource_path("my_lua_file.lua")) 


.. _Lua_get_content_target:

get_content_target
------------------

.. note::

   Only supported on |VLC| and |VLC+|.

On a |VLC|: ``get_content_target(compositionNum)``

On a |VLC+|: ``get_content_target(compositionNum, type)``

Returns a :doc:`content-target` object representing the Content Target in the project that matches the parameters:

* ``compositionNum`` is the user number of the composition containing the desired Content Target.
* ``type`` describes the Content Target type and can be one of the constants ``PRIMARY``, ``SECONDARY`` or ``TARGET_3`` ... ``TARGET_8``.

.. note::

   The constants for ``type`` are in the ``controller`` namespace within IO modules, e.g. ``controller.TARGET_5``.

Will return ``nil`` if no matching Content Target exists in the project.

For example, on a |VLC|:

.. include:: code-examples/content-target-vlc.rst

And on a |VLC+|:

.. include:: code-examples/content-target-vlcp.rst


.. _Lua_get_adjustment:

get_adjustment
--------------

.. note::

   Only supported on |VLC+|.

``get_adjustment(num)``

Returns an :doc:`adjustment-target` object representing the Adjustment Target in the project with the integer user number ``num``:

Will return ``nil`` if no matching Adjustment Target exists in the project.

For example:

.. code-block:: lua

   target = get_adjustment(1)
   target:transition_x_position(10,1,5) -- Move 10 pixels right in 5 seconds
   target:transition_y_position(10,1,5) -- Move 10 pixels down in 5 seconds
   target:transition_rotation(90,1,5) -- Rotate by 90 degrees in 5 seconds


.. _Lua_get_log_level:

get_log_level
-------------

Returns the current log level of the controller, which can be one of the following constants:

* ``LOG_DEBUG``
* ``LOG_TERSE``
* ``LOG_NORMAL``
* ``LOG_EXTENDED``
* ``LOG_VERBOSE``
* ``LOG_CRITICAL``

.. note::

   These constants are in the ``controller`` namespace within IO modules, e.g. ``controller.LOG_NORMAL``.


.. _Lua_get_syslog_enabled:

get_syslog_enabled
------------------

Returns true if Syslog is enabled, or false otherwise.


.. _Lua_get_syslog_ip_address:

get_syslog_ip_address
---------------------

Returns the IP address of the Syslog server as a string.


.. _Lua_get_ntp_enabled:

get_ntp_enabled
---------------

Returns true if NTP is enabled.


.. _Lua_get_ntp_ip_address:

get_ntp_ip_address
------------------

Returns the IP address of the NTP server as a string.


Actions
=======

.. _Lua_log:

log
---

``log([level, ]message)``

Write a message to the controller's log according to the parameters:

.. list-table::
   :widths: 3 3 7 3
   :header-rows: 1

   * - Parameter
     - Value Type
     - Description
     - Value Example
   * - ``level``
     - Integer value of constants: ``LOG_DEBUG``, ``LOG_TERSE``, ``LOG_NORMAL``, ``LOG_EXTENDED``, ``LOG_VERBOSE``, ``LOG_CRITICAL``; defaults to ``LOG_NORMAL``
     - Optional. The log level to apply to the message.
     - ``LOG_VERBOSE``
   * - ``message``
     - string
     - The message to add to the log.
     - ``"Your log message"``

For example:

.. code-block:: lua

   log(LOG_CRITICAL, "This is a critical message!") -- logs a message at Critical log level
   log("This is a normal message.") -- logs a message at Normal log level.


.. _Lua_set_log_level:

set_log_level
-------------

``set_log_level(log_level)``

Changes the log level of the controller, showing more or less detailed information, where ``log_level`` is an integer value of the constants:

* ``LOG_DEBUG`` (5)
* ``LOG_TERSE`` (4)
* ``LOG_NORMAL`` (3)
* ``LOG_EXTENDED`` (2)
* ``LOG_VERBOSE`` (1)
* ``LOG_CRITICAL`` (0)


.. _Lua_pause_all:

pause_all
---------

Pause all timelines in the project.


.. _Lua_resume_all:

resume_all
----------

Resume all timelines in the project.


.. _Lua_release_all:

release_all
-----------

``release_all([fade,] [group])``

Release all timelines and scenes in the project.

.. include:: snippets/release-fade-group-params.rst


.. _Lua_release_all_timelines:

release_all_timelines
---------------------

``release_all_timelines([fade,] [group])``

Release all timelines in the project.

.. include:: snippets/release-fade-group-params.rst


.. _Lua_release_all_scenes:

release_all_scenes
------------------

``release_all_scenes([fade,] [group])``

Release all scenes in the project.

.. include:: snippets/release-fade-group-params.rst


.. _Lua_clear_all_overrides:

clear_all_overrides
-------------------

``clear_all_overrides([fade])``

Removes all overrides from all fixtures and groups. Optionally specify a ``fade`` time in seconds as a float, e.g. ``2.0``.


.. _Lua_enqueue_trigger:

enqueue_trigger
---------------

``enqueue_trigger(num[,var...])``

Queue trigger number ``num`` to be fired on the next controller playback refresh. The trigger's conditions will be tested. Optional variables ``var`` can be passed in as additional arguments.

For example:

.. code-block:: lua

   -- enqueue trigger 2, passing in three variables: 255, 4.0 and "string"
   enqueue_trigger(2,255,4.0,"string")


.. _Lua_enqueue_local_trigger:

enqueue_local_trigger
---------------------

``enqueue_local_trigger(num[,var...])``

Same behaviour as for :ref:`Lua_enqueue_trigger` but the trigger ``num`` will only be queued on the controller that ran the function - the trigger will not propagate to other controllers in the project.


.. _Lua_force_trigger:

force_trigger
-------------

``force_trigger(num[,var...])``

Queue trigger number ``num`` to be fired on the next controller playback refresh without testing the trigger's conditions - the trigger actions will always run. Optional variables ``var`` can be passed in as additional arguments.

For example:

.. code-block:: lua

   -- force the execution of trigger 2's actions
   -- pass in three variables: 255, 4.0 and "string"
   force_trigger(2,255,4.0,"string")


.. _Lua_force_local_trigger:

force_local_trigger
-------------------

``force_local_trigger(num[,var...])``

Same behaviour as for :ref:`Lua_force_trigger` but the trigger ``num`` will only be queued on the controller that ran the function - the trigger will not propagate to other controllers in the project.


.. _Lua_set_text_slot:

set_text_slot
-------------

``set_text_slot(name, value)``

Set the value of the text slot named ``name`` in the project to ``value``, for example:

.. code-block:: lua

   -- Set "My slot" to value "Hello world!"
   set_text_slot("My slot", "Hello world!")


.. _Lua_set_control_value:

set_control_value
-----------------

``set_control_value(name, [index,] value[, emitChange])``

Set the value on a Touch Slider or Colour Picker according to the parameters:

.. list-table::
   :widths: 3 3 7 3
   :header-rows: 1

   * - Parameter
     - Value Type
     - Description
     - Value Example
   * - ``name``
     - string
     - The Key of the Touch Control.
     - ``slider001``
   * - ``index``
     - integer (1-3)
     - Optional. Axis of movement - a slider has 1; a colour picker has 3. Will default to 1 if this parameter isn't specified.
     - ``1``
   * - ``value``
     - integer (0-255)
     - New value to set.
     - ``128``
   * - ``emitChange``
     - boolean
     - Optional. Whether to fire associated triggers as a result of the control value change. Defaults to ``false``.
     - ``true``

For example:

.. code-block:: lua

   -- Set slider001 to half (and don't fire any associated triggers)
   set_control_value("slider001", 128)
   -- Set the second axis (green) to full on colour020
   set_control_value("colour020", 2, 255)


.. _Lua_set_control_state:

set_control_state
-----------------

``set_control_state(name, state)``

Set the state on a Touch control according to the parameters:

.. list-table::
   :widths: 3 3 7 3
   :header-rows: 1

   * - Parameter
     - Value Type
     - Description
     - Value Example
   * - ``name``
     - string
     - The Key of the Touch Control.
     - ``slider001``
   * - ``state``
     - string
     - The name of the state as defined in the Touch theme.
     - ``Green``

For example:

.. code-block:: lua

   -- Set slider001 to a state called "Green"
   set_control_state("slider001", "Green")


.. _Lua_set_control_caption:

set_control_caption
-------------------

``set_control_caption(name, caption)``

Set the caption on a Touch control according to the parameters:

.. list-table::
   :widths: 3 3 7 3
   :header-rows: 1

   * - Parameter
     - Value Type
     - Description
     - Value Example
   * - ``name``
     - string
     - The Key of the Touch Control.
     - ``button001``
   * - ``caption``
     - string
     - The text to display as the control's caption.
     - ``On``

For example:

.. code-block:: lua

   -- Set button001's caption to "On"
   set_control_caption("button001", "On")


.. _Lua_set_interface_page:

set_interface_page
------------------

``set_interface_page(number[, transition])``

Change the current page on the Touch interface according to the parameters:

.. list-table::
   :widths: 3 3 7 3
   :header-rows: 1

   * - Parameter
     - Value Type
     - Description
     - Value Example
   * - ``number``
     - integer
     - Touch interface page to change to.
     - ``2``
   * - ``transition``
     - integer
     - Optional page transition. Integer value of constants: ``SNAP``, ``PAN_LEFT``, ``PAN_RIGHT``
     - ``PAN_LEFT``

.. note::

   Must be executed on the |TPC| that hosts the interface.

For example:

.. code-block:: lua

   -- Change the touch screen interface to page 4 with a snap transition
   set_interface_page(4, SNAP)


.. _Lua_set_interface_enabled:

set_interface_enabled
---------------------

``set_interface_enabled([enabled])``

Enable/disable the touchscreen, according to the optional boolean parameter ``enabled`` (default: ``true``).

.. note::

   Must be executed on the |TPC| that hosts the interface.

For example:

.. code-block:: lua

   -- Disable the touchscreen
   set_interface_enabled(false)


.. _Lua_set_interface_locked:

set_interface_locked
--------------------

``set_interface_locked([lock])``

Lock/unlock the touchscreen, according to the optional boolean parameter ``lock`` (default: ``true``).

.. note::

   Must be executed on the |TPC| that hosts the interface.

For example:

.. code-block:: lua

   -- Lock the touchscreen
   set_interface_locked()
   -- Unlock the touchscreen
   set_interface_locked(false)


.. _Lua_push_to_web:

push_to_web
-----------

``push_to_web(name, value)``

Sends data as JSON to clients who are subscribed to the relevant websocket channel, e.g. custom web interfaces using :ref:`websocket_subscribe_lua` in the ``query.js`` library. The parameters are as follows:

.. list-table::
   :widths: 3 3 7 3
   :header-rows: 1

   * - Parameter
     - Value Type
     - Description
     - Value Example
   * - ``name``
     - string
     - JSON attribute name
     - ``"myVar"``
   * - ``value``
     - :doc:`variant`
     - Value for the JSON, which will be sent as a string.
     - ``"String value"`` or ``1234``

For example:

.. code-block:: lua

   myData = 1234
   -- Will push JSON object {"my_data":"1234"}
   push_to_web("my_data", myData)


.. _Lua_disable_output:

disable_output
--------------

``disable_output(protocol)``

Disables the output of a single protocol from the controller, where ``protocol`` is the integer value of the constants:

* ``DMX``
* ``PATHPORT``
* ``ARTNET``
* ``KINET``
* ``SACN``
* ``DVI``
* ``RIO_DMX``

For example:

.. code-block:: lua

   -- Disable the DMX output from the controller
   disable_output(DMX)


.. _Lua_enable_output:

enable_output
-------------

``enable_output(protocol)``

Enables the output of a single protocol from the controller, where ``protocol`` is the integer value of the constants defined for :ref:`Lua_disable_output`.

For example:

.. code-block:: lua

   -- Enable the DMX output from the controller
   enable_output(DMX)


.. _Lua_set_timecode_bus_enabled:

set_timecode_bus_enabled
------------------------

``set_timecode_bus_enabled(bus[, enable])``

Enable or disable a timecode bus, where bus is the integer value of the constants ``TCODE_1`` ... ``TCODE_6`` and ``enable`` is a boolean, determining whether the bus is enabled (default ``true``) or not.

