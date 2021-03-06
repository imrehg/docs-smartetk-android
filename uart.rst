.. _uart:

UART Class
==============

.. java:package:: com.viaembedded.smartetk

.. java:type:: class Uart

   Create a new UART object.

   .. code-block:: java

      Uart m_uart = new Uart();

   .. java:method:: int open(String sDev)

      Open the specified UART device.

      :param String sDev: UART device name, for example ``ttyUSB0``.
      :return: :java:ref:`S_OK` if function succeeds
      :return: :java:ref:`E_UART_OPENFAIL` if failed to open the device
      :return: :java:ref:`E_UART_ALREADY_OPENED` if the device has already has been opened
      :return: :java:ref:`E_UART_TTY_BEEN_USED` if  the device has been used by other object
      :return: ``E_*`` otherwise, see :ref:`return`.

   .. java:method:: int close()

      Close the UART device that is currently opened.

      :return: :java:ref:`S_OK` if function succeeds
      :return: ``E_*`` otherwise, see :ref:`return`.

   .. java:type:: class UartConfig

      Class to contain the Uart configuration values for ``getConfig``.

      .. java:field:: int BaudRate

	 baud rate, for example ``115200``

      .. java:field:: byte DataBits

	 data bits, ``7`` for 7 data bits, ``8`` for 8 data bits

      .. java:field:: byte StopBits

	 stop bits, ``1`` for 1 stop bit, ``2`` for 2 stop bits

      .. java:field:: byte Parity

	 parity, ``0`` for none, ``1`` for odd, ``2`` even parity

      .. java:field:: byte FlowControl

	 flow control, ``0`` for none, ``1`` for CTS/RTS flow control

   .. java:method:: int setConfig(int iBaudRate, byte byDataBIts, byte byStopBits, byte byParity, byte byFlowCtrl)

      Configure an already opened UART device.

      :param int iBaudRate: baud rate, e.g. ``115200``
      :param byte byDataBits: data bits,  `7` for 7-bit data bits, ``8`` for 8-bit data bits
      :param byte byStopBits: stop bits, ``1`` for 1 stop bit, ``2``: 2 stop bits
      :param byte byParity: parity, ``0`` for none, ``1`` for odd, ``2`` for even parity
      :param byte byFlowControl: flow control, ``0`` for none, ``1`` for CTS/RTS flow control
      :return: :java:ref:`S_OK` if function succeeds
      :return: ``E_*`` otherwise, see :ref:`return`.

   .. java:method:: int getConfig(UartConfig UC)

      Get the configurations of the opened Uart device and store them in passed UartConfig Class.

      :param UartConfig UC: Uart Configuration
      :return: :java:ref:`S_OK` if function succeeds
      :return: ``E_*`` otherwise, see :ref:`return`.

      Example:

      .. code-block:: java

         UartConfig UC = m_uart.new UartConfig();

         if (SmartETK.S_OK != m_uart.getConfig(UC)) {
           cleanStatus();
           return;
         }

   .. java:method:: int setTimeout(boolean bEnable, int iTimeout)

      Set the timeout of the opened UART device.

      If ``bEnable`` is set to ``true``, the UART read method depends on the ``iTimeout`` value.
      If timeout is set to ``0`` then polling read is used, if ``1-255`` then the data is read with the corresponding timeout.

      If ``bEnable`` is set to ``false`` then blocking read is performed.

      :param boolean bEnable: ``true`` if enable the timeout function, ``false`` otherwise.
      :param int iTimeout: timeout value in multiples of 0.1 seconds, accepted range is 0 – 255 (0 - 25.5 seconds)
      :return: :java:ref:`S_OK` if function succeeds
      :return: ``E_*`` otherwise, see :ref:`return`.

   .. java:method:: int getTimeout(Timeout T)

      Get the timeout configuration of the opened Uart device and store them in passed Timeout Class.

      :param Timeout T: timeout configuration
      :return: :java:ref:`S_OK` if function succeeds
      :return: ``E_*`` otherwise, see :ref:`return`.

      Example:

      .. code-block:: java

         Timeout T = m_uart.new Timeout();

         if(SmartETK.S_OK != m_uart.getTimeout(T)) {
           cleanStatus();
           return;
         }

   .. java:type:: class ReturnChar

      Used by :java:ref:`getReturnChar`.

      .. java:field:: boolean enabled

         Whether the terlmination character function is enabled.

      .. java:field:: byte returnChar

         The termination character

   .. java:method:: int setReturnChar(boolean bEnable, byte byReturnChar);

      Set the termination character of the opened UART device.

      If ``bEnable`` is ``true``, then read will block until a character equal to``byReturnChar`` is received,
      or read buffer is full. If ``bEnable`` is ``false`` then read will ignore byReturnChar checking when reading data.

      :param boolean bEnable: enable or disable the termination character function.
      :param byte byReturnChar: the termination character
      :return: :java:ref:`S_OK` if function succeeds
      :return: ``E_*`` otherwise, see :ref:`return`.

   .. java:method:: int getReturnChar(ReturnChar RC);

      Get the termination character configuration of the opened Uart device and store them in passed ReturnChar Class.

      :param ReturnChar RC: termination character configuration
      :return: :java:ref:`S_OK` if function succeeds
      :return: ``E_*`` otherwise, see :ref:`return`.

      Example:

      .. code-block:: java

         ReturnChar RC = new ReturnChar();
         if(SmartETK.S_OK != m_uart.getReturnChar(RC)) {
           cleanStatus();
           return;
         }

   .. java:method:: int readData(int iReadLen, byte[] byRead, int[] iActualLen);

      Receive data from the opened UART device.

      :param int iReadLen: number of bytes to read, maximum 1024 bytes per transfer.
      :param byte[] byRead: pointer to the buffer pointer.
      :param int[] iActualLen: the actual number of bytes received
      :return: :java:ref:`S_OK` if function succeeds
      :return: ``E_*`` otherwise, see :ref:`return`.

   .. java:method:: int writeData(int iWriteLen, byte[] byWrite);

      Send the data to the opened UART device.

      :param int iWriteLen: number of bytes to transmit, maximum 1024 bytes per transfer.
      :param byte[] byWrite: pointer to data buffer.
      :return: :java:ref:`S_OK` if function succeeds
      :return: ``E_*`` otherwise, see :ref:`return`.

   .. java:method:: int reset();

      Reset the opened or failed to open UART device. If the uart device has been used by other object,
      :java:ref:`Uart.open` will return an :java:ref:`E_UART_ALREADY_OPENED`. The object could call this reset function to
      release the UART resource and try to open the device again by calling :java:ref:`Uart.open`.

      :return: :java:ref:`S_OK` if function succeeds
      :return: ``E_*`` otherwise, see :ref:`return`.

UART Code Examples
------------------

UART Initialization
^^^^^^^^^^^^^^^^^^^

.. note::

   In the sample code below, ``mETBaudRate`` refers to an ``EditText`` widget.

.. code-block:: java

   private Uart m_uart = null;
   m_uart = new Uart();
   if(null == m_uart) {
     cleanStatus();
     return;
   }
   if(SmartETK.S_OK != m_uart.open((m_sDev = mETDev.getText().toString()))) {
     cleanStatus();
     return;
   }
   if(SmartETK.S_OK != m_uart.setConfig((m_iBaudRate = Integer.valueOf(mETBaudRate.getText().toString())),
                                        (byte)8,
					(byte)1,
					(byte)0,
					(byte)0)) {
     cleanStatus();
     return;
   }

Write UART Data
^^^^^^^^^^^^^^^

.. note::

   In the sample code below, ``mETWrite`` is an ``EditText`` widget.

.. code-block:: java

   if(SmartETK.S_OK != m_uart.writeData(mETWrite.getText().toString().getBytes().length,
                                        mETWrite.getText().toString().getBytes())) {
     return;
   }

Read UART Data
^^^^^^^^^^^^^^

.. code-block:: java

   int iReadLen = LENGTH;
   byte[] byRead = new byte[LENGTH];
   int[] iActualLen = new int[1];

   while(SmartETK.S_OK == m_mainThreadUart.readData(iReadLen,
                                                    byRead,
						    iActualLen)) {
     if(0 == iActualLen[0]) {
        continue;
     }
    /* Process received byRead byte array ... */
    for(int i = 0; i < byRead.length; i++) {
      byRead[i] = 0;
    }
    iActualLen[0] = 0;
   }
