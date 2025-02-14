RIO
###

A ``RIO`` object is returned from :ref:`Lua_get_rio`.

For example:

.. include:: code-examples/rio44.rst

Member functions
****************

The following are member functions of ``RIO`` objects.

.. _Lua_rio_get_input:

get_input
=========

``get_input(inputNum)``

Returns the state of the input with integer number ``inputNum`` as a boolean if the input is set to Digital or Contact Closure, or an integer if the input is set to Analog.

For example:

.. code-block:: lua

   rio = get_rio(RIO44, 3)
   input = rio:get_input(1)


.. _Lua_rio_get_output:

get_output
==========

``get_output(outputNum)``

Returns the state of the output with integer number ``outputNum`` as a boolean.

For example:

.. code-block:: lua

   rio = get_rio(RIO44, 2)
   output_state = rio:get_output(1)


.. _Lua_rio_set_output:

set_output
==========

``set_output(outputNum, state)``

Sets the output of a RIO to on or off according to the parameters:

.. list-table::
   :widths: 3 3 7 3
   :header-rows: 1

   * - Parameter
     - Value Type
     - Description
     - Value Example
   * - ``outputNum``
     - integer (1-8)
     - Number of the RIO output to change the state of. Range depends on type of RIO.
     - ``1``
   * - ``state``
     - boolean or integer
     - State to set the output to. Can be any of: ``0``, ``1``, ``true``, ``false``, ``ON`` or ``OFF``
     - ``OFF``

