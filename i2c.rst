.. _i2c:

I2C Class
=========

.. java:package:: com.viaembedded.smartetk.I2C

.. java:type:: class I2C

   Create a new I2C object with specified bus number, slave address and the
   length of the offset address.

   :param int I2CBusNum: I2C bus number, for example: ``0`` is for ``i2c-0`` bus
   :param byte I2CAddress: I2C slave address, support 7 bits slave addresses
   :param int OffsetLen: the length of the registers' offset in number of bytes, accepted values are 0 to 4, ``0``: no registers, ``1``: 1 byte = 8 bit registers, ``2``: 2 bytes = 16 bit registers, ``3``: 3 bytes = 24 bit registers, ``4``: 4 bytes = 32 bit registers

   For example, create an I2C object in I2C bus 1 and I2C slave address 10, and the offset length is 0

   .. code-block:: java

      I2C m_i2c = new I2C(1,10,0);

   Another example, create an I2C object in I2C bus 1 and I2C slave address 52, and the offset length is 2 (16 bit registers).

   .. code-block:: java

      I2C m_i2c = new I2C(1,52,2);

.. java:method:: int read(byte[] Buf, int Offset, int ReadLen)

   Read data from specified offset with a given length, and store the data in buffer.

   :param byte[] Buf: buffer to store the read data
   :param int Offset: the registers' offset to read from a specified I2C bus number and slave address, accepted values are from 0 to 0x7FFFFFFF
   :param int ReadLen: number of bytes to read, maximum 255 bytes per transfer. 
   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`

.. java:method:: int write(byte[] byBuf, int iOffset, int iWriteLen)

   Write data to a specified offset with a given length.

   :param byte Buf: the write buffer
   :param int Offset: the registers' offset of writing to a specified I2C bus number and slave address, accepted values are from 0 to 7FFFFFFF
   :param int WriteLen: the written data length, maximum 255 bytes per transfer
   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`

I2C Code Examples
-----------------

Initializate I2C
^^^^^^^^^^^^^^^^

Create an I2C object in I2C bus 1 and I2C slave address 52, and the offset length is 2.

.. code-block:: java

   int iBusNum = 1;
   byte byAddress = IntToByte(52);
   int iOffsetLen = 2;

   if(iBusNum < 0 || byAddress < 0 || iOffsetLen < 0) {
     return false;
   }
   m_i2c = new I2C(iBusNum, byAddress, iOffsetLen);

Read I2C Data
^^^^^^^^^^^^^

Read data from offset “0” with length “2” bytes, and store data in byRead byte array buffer.

.. code-block:: java

   byte[] byRead = new byte[255]
   int iOffset = 0;
   int iReadLen = 2; 
   Arrays.fill(byRead, 0);
   if(SmartETK.S_OK != m_i2c.read(byRead, iOffset, iReadLen) || null == byRead) {
     return false;
   }

Write I2C Data
^^^^^^^^^^^^^^

Write data to offset 0 with length 2 bytes and data value 0x0101. The written data is stored in byWrite byte array buffer.

.. code-block:: java

   byte[] byWrite = new byte[2]
   byWrite[0] = 0x01;
   byWrite[1] = 0x01;
   int iOffset = 0;
   int iWriteLen = 2;

   if(SmartETK.S_OK != m_i2c.write(byWrite, iOffset, iWriteLen)) {
     return false;
   }
