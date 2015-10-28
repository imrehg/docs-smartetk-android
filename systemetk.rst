.. _systemetk:

SystemETK Class
===============

.. java:package:: com.viaembedded.smartetk.SystemETK

.. java:type:: class SystemETK

   Create a new SystemETK object.

   .. code-block:: java

      SystemETK m_system = new SystemETK();

.. java:method:: int reboot()

   Reboot the machine.

   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`

.. java:method:: int suspend()

   Suspend the machine.

   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`

SystemETK Code Examples
-----------------------

Reboot the Machine
^^^^^^^^^^^^^^^^^^

.. code-block:: java

   private SystemETK m_system = null;
   if(null == m_system) {
     m_system = new SystemETK();
   }
   if(SmartETK.S_OK != m_system.reboot()) {
     return;
   }

Suspend the Machine
^^^^^^^^^^^^^^^^^^^

.. code-block:: java

   private SystemETK m_system = null;
   if(null == m_system) {
     m_system = new SystemETK();
   }
   if(SmartETK.S_OK != m_system.suspend()) {
     return;
   }
