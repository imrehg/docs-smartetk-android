.. _network:

Network Class
=============

.. java:package:: com.viaembedded.smartetk.Network

.. java:type:: class Network

   Create a new Network object.

   .. code-block:: java

      Network m_network = new Network();

.. java:method:: int setWakeOnLan(boolean bEnable)

   Enable or disable Network Wake-on-LAN function from suspend mode.

   :param boolean bEnable: enable or disable functionality
   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`
			   
.. java:method:: int getWakeOnLan(boolean[] bEnable)

   Get the status if Network Wake-on-LAN function.
   
   :param boolean[] bEnable: variable to update with ``true`` for enabled, ``false`` for disabled
   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`
			     
Network Code Examples
---------------------

Set Wake-on-LAN From Suspend Mode
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: java

   boolean bSetEnable = true;

   if(null == m_network) {
     m_network = new Network();
   }
   if(SmartETK.S_OK != m_network.setWakeOnLan(bSetEnable)) {
     return false;
   } 

Get Wake-on-LAN From Suspend Mode Status
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: java
		
   if(null == m_network) {
     m_network = new Network();
   }
   boolean[] bGetEnable = new boolean[1];
   if(SmartETK.S_OK != m_network.getWakeOnLan(bGetEnable)) {
     return false;
   }
   return bGetEnable[0];
