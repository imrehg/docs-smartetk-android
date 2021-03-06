.. _smartetk:

SmartETK class
==============

This class contains general parts used by the rest of the package, such as function return values, and some
helper classes.

.. java:package:: com.viaembedded.smartetk

.. java:type:: class SmartETK

   .. _helper:

   Helper classes:

   .. java:type:: class Timeout

      Timeout configuration, used by :java:ref:`Can.getTimeout` and :java:ref:`Uart.getTimeout`.

      .. java:field:: boolean Enable

	 Enable or disable timeout function

      .. java:field:: int Timeout

	 timeout value in multiples of 0.1 seconds, accepted range is 0 – 255 (0 - 25.5 seconds)

.. _return:

Function Return Values
----------------------

.. java:package:: com.viaembedded.smartetk.SmartETK

The return values and error codes used by the methods in Smart ETK.

.. java:field:: static int S_OK

   When a function returns the S_OK value, it indicates that the function has successfully completed.

.. java:field:: static int E_FAIL

   When a function returns the E_FAIL value, it indicates that the function has failed to complete.

.. java:field:: static int E_VERSION_NOT_SUPPORT

   When a function returns the E_VERSION_NOT_SUPPORT value, it indicates
   that the versions of ``SmartETK.jar`` and bsservice are not compatible.

.. java:field:: static int E_INVALID_ARG

   When a function returns the E_INVALID_ARG value, it indicates that the
   arguments are invalid.

.. java:field:: static int E_FUNC_NOT_SUPPORT

   When a function returns the E_FUNC_NOT_SUPPORT value, it indicates that
   the function is not supported by this board.

.. java:field:: static int E_CONNECTION_FAIL

   When a function returns the E_CONNECTION_FAIL value, it indicates that the
   ``bsservice`` doesn't respond the request. Please make sure bsservice is running
   successfully.

.. java:field:: static int E_NOT_RESPOND_YET

   When a function returns the E_NOT_RESPOND_YET value, it indicates that the
   ``bsservice`` function is still running and has not finished yet.

.. java:field:: static int E_TIMEOUT

   When a function returns the E_TIMEOUT value, it indicates that no corresponding
   data has been received within the period.

.. java:field:: static int E_UART_OPENFAIL

   When :java:ref:`Uart.open` returns the E_UART_OPENFAIL value, it indicates that the
   UART device can't be opened successfully. Please make sure the name of the
   tty device exists.

.. java:field:: static int E_UART_NOT_OPEN

   When a function returns the E_UART_NOT_OPEN value, it indicates that uart
   object cannot be operated normally. The reason might be that the application
   doesn't open uart device before calling other operating function; or it was
   reset by other uart object.

.. java:field:: static int E_UART_ALREADY_OPENED

   When :java:ref:`Uart.open` returns the E_UART_ALREADY_OPENED value, it indicates
   that the uart object has been opened. If you need to open other uart device,
   please call close function to close the current device, then open the other
   UART again.

.. java:field:: static int E_UART_TTY_BEEN_USED

   When :java:ref:`Uart.open` returns the E_UART_TTY_BEEN_USED value, it indicates
   that the tty device has been used by other uart object. If you want to use it,
   you can call reset function to release the resource and open it again.

.. java:field:: static int E_UART_BAUDRATE_NOT_SUPPORT

   When :java:ref:`Uart.setConfig` returns the E_UART_BAUDRATE_NOT_SUPPORT value,
   it indicates that baud rate is not supported.

.. java:field:: static int E_CAN_OPENFAIL

   When :java:ref:`Can.open` returns the E_CAN_OPENFAIL value, it indicates that the
   CAN device can't be opened successfully. Please make sure the name of the
   CAN device exists.

.. java:field:: static int E_CAN_NOT_OPEN

   When a function returns the E_CAN_NOT_OPEN value, it indicates that can
   object cannot be operated normally. The reason might be that the application
   doesn't open can device before calling other operating function.

.. java:field:: static int E_CAN_ALREADY_OPENED

   When :java:ref:`Can.open` returns the E_CAN_ALREADY_OPENED value, it indicates
   that the can object has been opened. If you need to open other can device,
   please call close function to close the current device, then open the other can
   again.

.. java:field:: static int E_CAN_BAUDRATE_NOT_SUPPORT

   When :java:ref:`Can.setBitrate` returns the E_CAN_BAUDRATE_NOT_SUPPORT value,
   it indicates that bit rate is not supported.
