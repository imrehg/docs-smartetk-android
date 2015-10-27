CAN Class
==============

.. java:type:: class Can

   Create a new CAN object.

   .. code-block:: java

      Can m_can = newCan();

.. java:method:: int open(String sName)

   Open the specified CAN device.

   :param String sname: CAN device name, for exammple ``can0``, ``can1``.
   :return: ``S_OK`` if the function succeeded
   :return: ``E_CAN_OPENFAIL`` if opening device has failed
   :return: ``E_CAN_ALREADY_OPENED`` if the object is already open
   :return: ``E_*`` otherwise

.. java:method:: int close()

   Close the CAN device that is currently opened.

   :return: ``S_OK`` if the function succeeded
   :return: ``E_*`` otherwise

.. java:method:: int setBitrate(int iBitrate)

   Set the bitrate of the opened CAN device.

   :param int iBitrate: bit rate, e.g. ``125000``. The default rate is ``500000``
   :return: ``S_OK`` if the function succeeded
   :return: ``E_CAN_BAUDRATE_NOT_SUPPORT`` if the given bitrate is not supported.
   :return: ``E_*`` otherwise

.. java:method:: int getBitrate(int[] iBitrate)

   Get the bitrate of the opened CAN device.

   :param int iBitrate: store the return bit rate
   :return: ``S_OK`` if the function succeeded
   :return: ``E_*`` otherwise

.. java:method:: int setTimeout(boolean bEnable, int iTimeout)

   If ``bEnable`` is set to ``true``, the UART read method depends on the ``iTimeout`` value.
   If timeout is set to ``0`` then polling read is used, if ``1-255`` then the data is read with the corresponding timeout.

   If ``bEnable`` is set to ``false`` then blocking read is performed.

   :param boolean bEnable: ``true`` if enable the timeout function, ``false`` otherwise.
   :param int iTimeout: timeout value in multiples of 0.1 seconds, accepted range is 0 – 255 (0 - 25.5 seconds)
   :return: ``S_OK`` if the function succeeded
   :return: ``E_*`` otherwise

.. java:method:: int getTimeout(Timeout timeout)

   Get the timeout configuration of the opened CAN device and store them in passed Timeout Class.

   :param Timeout T: timeout configuration
   :return: ``S_OK`` if the function succeeded
   :return: ``E_*`` otherwise

   Example:

   .. code-block:: java

      Import com.viaembedded.smartetk.SmartETK.Timeout;

      Can m_can = new Can();
      Timeout timeout = new Timeout();

      if(SmartETK.S_OK != m_can.getTimeout(timeout)) {
        cleanStatus();
        return;
      }

.. java:method:: int setLoopback(boolean bEnable);

   The loopback functionality is enabled by default to reflect standard
   networking behavior for CAN applications. A local loopback functionality is
   similar to the local echo e.g. of tty devices.

   ``bEnable = true`` (if setRecvOwnMsgs() also set to true, it will receive its own msgs after transmit)

   ``bEnable = false`` (no matter setRecvOwnMsgs() set to true or false, it won’t receive its onw msgs after transmit)

   :param boolean bEnable: ``true`` to enable loopback, ``false`` otherwise.
   :return: ``S_OK`` if the function succeeded
   :return: ``E_*`` otherwise


.. java:method:: int getLoopback (boolean[] bEnable);

   Get loopback state.

   :param boolean[] bEnable: to variable to place the loopback state, ``true`` for enabled, ``false`` for disabled
   :return: ``S_OK`` if the function succeeded
   :return: ``E_*`` otherwise

   Example:

   .. code-block:: java

      boolean[] bEnable_getlbk = null;

      if(SmartETK.S_OK != m_uart.getLoopback(bEnable_getlbk)) {
        cleanStatus();
	return;
      }

.. java:method:: int setRecvOwnMsgs (boolean bEnable)

   Set CAN_RAW_RECV_OWN_MSGS flag to decide whether the socket
   receives frames its own sent or not. As the local loopback is enabled, the
   reception of the CAN frames on the same socket that was sending the CAN
   frame is assumed to be unwanted and therefore disabled by default.

   ``bEnable = true`` (if setLoopback() set to false, it won’t receive its own msgs
   after sending Can frame)

   ``bEnable = false`` (default)

   :param boolean bEnable: ``true`` if receiving own frames, ``false`` otherwise
   :return: ``S_OK`` if the function succeeded
   :return: ``E_*`` otherwise

.. java:method:: int getRecvOwnMsgs (Boolean[] bEnable)

   Get the state of receiving its own sent frames or not.

   :param boolean[] bEnable: variable to put results, ``true`` if function is enabled, ``false`` if not.
   :return: ``S_OK`` if the function succeeded
   :return: ``E_*`` otherwise

   Example:

   .. code-block:: java

      boolean[] bEnable_recvOwn = null;

      if(SmartETK.S_OK != m_uart.getRecvOwnMsgs(bEnable_recvOwn)) {
        cleanStatus();
	return;
      }

.. java:type:: class CanFilter

   CAN filter object

   :param static final int PAYLOAD_SIZE: ``8``, payload data size
   :param static final int CAN_INV_FILTER:  ``0x20000000``, the filter can be inverted (``CAN_INV_FILTER`` bit is set in can_id)
   :param int iCanID: CAN ID
   :param int iCanMask: Valid bits in CAN ID for frame formats

.. java:method:: int setFilter(CanFilter[] canFilter, int iLength)

   The reception of CAN frames can be controlled by defining 0 .. n filters with
   the CanFilter object array buffer. A filter matches, when:

   ``[received_can_id] &
   CanFilter.iCanMask == CanFilter.iCanID & CanFilter.iCanMask
   To disable the reception of CAN frames: ``setFilter(null, 0);``

   :param CanFilter[] canFilter: CanFilter object array
   :param iLength: number of CanFilters object to set, ``0`` represents to disable the reception of CAN frames. 
   :return: ``S_OK`` if the function succeeded
   :return: ``E_*`` otherwise

.. java:type:: class CanFrame

   CAN frame object

   :param static final int PAYLOAD_SIZE: ``16``, Payload data size
   :param int iCanID: 32 bit CAN_ID + EFF/RTR flags
   :param final byte[] byData: ``= byte[8]`` frame payload data. The object had been created by byte[8] array buffer. Users can modify data byte array, but cannot modify the object.

.. java:method:: int readFrame (CanFrame canFrame)

   Reading CAN frame from the opened CAN device.

   :param CanFrame canFrame: CAN frame object to read
   :return: ``S_OK`` if the function succeeded
   :return: ``E_*`` otherwise

.. java:method:: int writeFrame (CanFrame canFrame)

   Write a CAN frame to the opened CAN device.
   
   :param CanFrame canFrame: CAN frame object to write
   :return: ``S_OK`` if the function succeeded
   :return: ``E_*`` otherwise

