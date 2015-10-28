Smart ETK API General Notes
===========================

.. java:package:: com.viaembedded.smartetk

VIA Smart ETK SDK supports the hardware controlling API for GPIO, Watch
Dog, and UART (RS-232) modules.

Smart ETK is programmed with the socket IO as the communication between
JAVA and C language to control the hardware modules. We implemented the
board support service such as ``bss_vab820`` to meet the request from Smart ETK
API.

Compatibility
-------------

=============== ====  ==== ==== ==== ==== ==== ==== ==== ==== ==== ==== ====
Model           GPIO  WDT  RTC  WOL  RES  UART SUS  CEC  I2C  CAN  UPC  DPMS
=============== ====  ==== ==== ==== ==== ==== ==== ==== ==== ==== ==== ====
`VAB-820`_      ✓     ✓    ×    ×    ×    ✓    ×    ×    ×    ✓    ×    ×
`VAB-1000`_     ✓     ✓    ✓    ✓    ✓    ✓    ✓    ×    ✓    ✓    ×    ×
`ALTA DS 2`_    ×     ✓    ✓    ✓    ✓    ×    ✓    ×    ×    ×    ×    ×
`AMOS-820`_     ✓     ✓    ×    ×    ×    ✓    ×    ×    ×    ✓    ×    ×
`ARTiGO A900`_  ✓     ✓    ✓    ✓    ✓    ×    ✓    ×    ×    ×    ×    ×
`Viega`_        ×     ✓    ×    ×    ×    ×    ×    ×    ×    ×    ✓    ×
=============== ====  ==== ==== ==== ==== ==== ==== ==== ==== ==== ==== ====

**Legend**: ``GPIO``: :ref:`GPIO <gpio>` support, ``WDT``: :ref:`WatchDog <watchdog>` timer,
``RTC`` is :ref:`Real-Time Clock Wake-up <rtc>`, ``WOL``: Wake-on-LAN, ``RES``: :java:ref:`Restart <reboot>` support,
``UART``: :ref:`UART <uart>` support, ``SUS``: :java:ref:`Suspend <suspend>` support,
``CEC``: HDMI CEC support, ``CAN``: :ref:`CAN <can>` support, ``I2C``: :ref:`I2C <i2c>` support,
``UPC``: x, ``DPMS``: :ref:`DPMS <dpms>` support

.. _VAB-820: http://www.viatech.com/en/boards/pico-itx/vab-820/
.. _VAB-1000: http://www.viatech.com/en/boards/pico-itx/vab-1000/
.. _ALTA DS 2: http://www.viatech.com/en/systems/android-signage-players/alta-ds-2/
.. _AMOS-820: http://www.viatech.com/en/systems/industrial-fanless-pcs/amos-820/
.. _ARTiGO A900: http://www.viatech.com/en/systems/small-form-factor-pcs/artigo-a900/
.. _Viega: http://www.viatech.com/en/systems/ruggedized-tablets/viega/


Installation
------------

Open Eclipse IDE and create an Android project. In project properties, import
SmartETK.jar by pressing the button "Add External JARs...".

.. image:: images/Eclipse01.jpg

Select "Order and Export" tab, move ``SmartETK.jar`` to the top and choose it.

.. image:: images/Eclipse02.jpg

Permissions
-----------
Smart ETK is programmed with the socket IO as the communication between
JAVA and C language to control the hardware modules, therefore you need to
make sure that you have android.permission.INTERNET in AndroidManifest.xml:

.. code-block:: xml

   <uses-permission android:name="android.permission.INTERNET"/>
