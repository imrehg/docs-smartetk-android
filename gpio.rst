.. _gpio:

GPIO Class
==========

.. java:package:: com.viaembedded.smartetk.GPIO

.. java:type:: class GPIO<pinID>

   Create a new GPIO object with specified pin ID. Ex: 1, 2, 4, 5, 7, 8, 9, 16.

   :param pinID: GPIO's pin ID.

   .. code-block:: java

      GPIO gpio5 = new GPIO(5);

.. java:method:: int setEnable(boolean enable)

   .. java:import:: com.viaembedded.smartetk GPIO

   Enable the specific GPIO pin.

   :param boolean enable:  ``true`` for enable, ``false`` for disable
   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`.

.. c:macro:: GM_GPI

   Indicates "input" direction for GPIO pin.

.. c:macro:: GM_GPO

   Indicates "output" direction for GPIO pin.

.. java:method:: int setDirection(int direction)

   Set input/output direction for the specific GPIO pin.

   :param int direction: :c:macro:`GM_GPI` for input direction, :c:macro:`GM_GPO` for output direction.
   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`.

.. java:method:: int getDirection(int[] direction)

   Get direction state of the specific GPIO Pin.

   :param int[] direction: parameter to set to :c:macro:`GM_GPI` for input, or :c:macro:`GM_GPO` for output depending on the pin's direction
   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`.

.. java:method:: int setValue(int value)

   Set output signal for the specific GPIO Pin.

   :param int value: GPIO signal, `0` for logic low, `1` for logic high.
   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`.

.. java:method:: int getValue(int[] value);

   Get input signal of the specific GPIO Pin.

   :param int[] value: GPIO signal, return `0` for logic low, return `1` for logic high.
   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`.

GPIO Examples
-------------

GPIO1, GPIO2, GPIO4, GPIO5, GPIO7, GPIO8, GPIO9 and GPIO203 are the external GPIO pins
for user’s own design. An example of setting GPIO1 as input pin and getting its value is shown here.

.. code-block:: java

   /* Declare variables to get GPIO5 values */
   boolean[] bEnable = new boolean[1];
   int[] nDirection = new int[1];
   int[] nValue = new int[1];

   GPIO gpio5 = new GPIO(1); // Create GPIO1 object

   gpio5.setEnable(true); // Enable GPIO1
   gpio5.setDirection(GPIO.GM_GPI); // Set GPIO1 as input direction
   gpio5.getEnable(bEnable); // Get GPIO1's enable status
   gpio5.getDirection(nDirection); // Get GPIO1's input/outputdirection
   gpio5.getValue(nValue); // Get GPIO1's input value

An example of setting GPIO5 as output pin and changing its value is shown here.

.. code-block:: java

   /* Declare variables to get GPIO6 values */
   boolean[] bEnable = new boolean[1];
   int[] nDirection = new int[1];
   int[] nValue = new int[1];
   GPIO gpio6 = new GPIO(5); // Create GPIO5 object

   gpio6.setEnable(true); // Enable GPIO5
   gpio6.setDirection(GPIO.GM_GPO); // Set GPIO5 as output direction
   gpio6.setValue(1); // Set GPIO5's output to high
   gpio6.getEnable(bEnable); // Get GPIO5's enable status
   gpio6.getDirection(nDirection); // Get GPIO5's input/output direction
   gpio6.getValue(nValue); // Get GPIO5's output value

.. note::

   Create GPIO203 by following method:

   .. code-block:: java

      GPIO gpio203 = new GPIO(16);
