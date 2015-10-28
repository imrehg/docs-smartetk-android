.. _watchdog:

WatchDog Class
==============

.. java:package:: com.viaembedded.smartetk.WatchDog

.. java:type:: class WatchDog

   Create a new WatchDog object.

   .. code-block:: java

      WatchDog m_watchdog = new WatchDog();

.. java:method:: int setEnable(boolean bEnable)

   Enable or disable watch dog function. SmartETK service will feed the watch
   dog within a period automatically. Once watch dog function is enabled, :java:ref:`keepAlive`
   needs to be called within the timeout period set by :java:ref:`setTimeout`,
   otherwise the system will reboot.

   :param boolean enable:  ``true`` for enable, ``false`` for disable
   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`.

.. java:method:: int getEnable(boolean[] enable);

   Get enable state of the watch dog function.

   :param boolean[] enable: parameter to put the return value of the watchdog status, ``true`` for enabled, ``false`` for disabled
   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`.

.. java:method:: int keepAlive()

   Keep watch dog alive to avoid rebooting the system.

   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`.

.. java:method:: int setTimeout(int iTimeout)

   Set watch dog timeout value

   :param int iTimeout: timeout in seconds, accepted values are between ``1`` and ``128``.
   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`.

.. java:method:: int getTimeout (int[] iTimeout)

   Get watchdog timeout value.

   :param int[] iTimeout: parameter to put the return value of the watchdog timeout in seconds
   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`.

WatchDog Code Examples
----------------------

Enable WatchDog
^^^^^^^^^^^^^^^^

.. code-block:: java

   if(null == m_watchdog) {
     m_watchdog = new WatchDog();
   }
   if(SmartETK.S_OK != m_watchdog.enable(true)) {
     return false;
   }

Get WatchDog status
^^^^^^^^^^^^^^^^^^^

.. code-block:: java

   if(null == m_watchdog) {
     m_watchdog = new WatchDog();
   }

   boolean[] bGetEnable = new boolean[1];

   if(SmartETK.S_OK != m_watchdog.getEnable(bGetEnable)) {
     return false;
   }
   return bGetEnable[0];

Keep WatchDog alive
^^^^^^^^^^^^^^^^^^^

.. code-block:: java

   if(null == m_watchdog) {
     m_watchdog = new WatchDog();
   }
   if(SmartETK.S_OK != m_watchdog. keepAlive()){
     return false;
   }
