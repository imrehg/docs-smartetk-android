.. _rtc:

RTC Class
=========

.. java:package:: com.viaembedded.smartetk.RTC

.. java:type:: class RTC

   Create a new RTC (real-time clock) object.

   .. code-block:: java

      RTC m_rtc = new RTC();

.. java:field:: static byte ARG_RTC_MODE_DAY

   Waking up every day.

.. java:field:: static byte ARG_RTC_MODE_WEEK

   Waking up every week.

.. java:field:: static byte ARG_RTC_MODE_MONTH

   Waking up every month.

.. java:method:: int setWakeUpTime(byte Mode, int Year, byte Month, byte Day, byte Hour, byte Min, byte Sec)

   Set the wake up time and mode in RTC. The behavior of wake up from
   suspend mode will start at the wake up time, and it must loop according to
   the wake up mode.

   :param byte Mode: wake up mode, one of :java:ref:`ARG_RTC_MODE_DAY`, :java:ref:`ARG_RTC_MODE_WEEK`, or :java:ref:`ARG_RTC_MODE_MONTH`. 
   :param int Year: year of wake up time, counted since 1900 for wake up, for example 2015 is `iYear = 115` (???)
   :param byte Month: month of wake up time, between 1 and 12
   :param byte Day: day of the month for wake up time, between 1 and 31
   :param byte Hour: hours for wake up time (24h clock), between 0 and 23
   :param byte Min: minutes for wake up time, between 0 and 59
   :param byte Sec: seconds for wake up time, between 0 and 59
   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`

.. java:type:: class RTCStatus

   RTC wake up time object

   :param byte Mode: wake up mode, one of :java:ref:`ARG_RTC_MODE_DAY`, :java:ref:`ARG_RTC_MODE_WEEK`, or :java:ref:`ARG_RTC_MODE_MONTH`. 
   :param int Year: year of wake up time, counted since 1900 for wake up, for example 2015 is `iYear = 115`
   :param byte Month: month of wake up time, between 1 and 12 accepted
   :param byte Day: day of the month for wake up time, between 1 and 31 are
   :param byte Hour: hours for wake up time (24h clock), between 0 and 23
   :param byte Min: minutes for wake up time, between 0 and 59
   :param byte Sec: seconds for wake up time, between 0 and 59

.. java:method:: int getWakeUpTime(RTCStatus RS)

   Get the wake up time and mode set in RTC.
   
   :param RTCStatus RS: parameter to return the current wake up time and mode
   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`

.. java:method:: int setEnable(boolean bEnable)

   Enable or disable RTC wake up function from suspend mode.

   :param boolean bEnable: ``true`` to enable, ``false`` to disable RTC wake up function from suspend mode
   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`
			  
.. java:method:: int getEnable(boolean[] bEnable)

   Get the status if wake up function from suspend mode is enabled or disabled.
   
   :param boolean[] bEnable: parameter to return ``true`` for enabled, ``false`` for disabled
   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`
			     
RTC Code Examples
-----------------

Set RTC Wake Up From Suspend mode
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: java
		
   boolean bSetEnable = true;

   if(null == m_rtc) {
     m_rtc = new RTC();
   }
   if(SmartETK.S_OK != m_rtc.setEnable(bSetEnable)) {
     return false;
   }

Get RTC Wake Up Status
^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: java

   if(null == m_rtc) {
     m_rtc = new RTC();
   }
   boolean[] bGetEnable = new boolean[1];
   if(SmartETK.S_OK != m_rtc.getEnable(bGetEnable)) {
     return false;
   }
   
Set RTC Wake Up Time
^^^^^^^^^^^^^^^^^^^^

The folloing code sets the wake up behaviour to wake up from suspend starting from 2015/5/1, every day at 12:00.

.. code-block:: java
		
   byte Mode = RTC.ARG_RTC_MODE_DAY;
   int Year = 2015;
   byte Month = IntToByte(5);
   byte Day = IntToByte(1);
   byte Hour = IntToByte(12);
   byte Min = IntToByte(0);
   byte Sec = IntToByte(0);

   if(null == m_rtc) {
     m_rtc = new RTC();
   }

   if(SmartETK.S_OK != m_rtc.setWakeUpTime(Mode, Year, Month, Day, Hour, Min, Sec)) {
     return false;
   } 

Get RTC Wake Up Time
^^^^^^^^^^^^^^^^^^^^

.. code-block:: java

   if(null == m_rtc) {
     m_rtc = new RTC();
   }
   m_RS = new RTCStatus();
   if(SmartETK.S_OK != m_rtc.getWakeUpTime(m_RS)) {
     return false; 
   }
