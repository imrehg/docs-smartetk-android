.. _dpms:

DPMS Class
===============

.. java:package:: com.viaembedded.smartetk.Dpms

.. java:type:: class Dpms

   Create a new DPMS object.

   .. code-block:: java

      m_dpms = new Dpms();

.. java:method:: int setDpms(boolean bEnable)

   Enable or disable the DPMS mode of the HDMI output

   :param boolean bEnable: ``true`` to enable the DPMS mode, ``false`` to disable
   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`

.. java:method:: int getDpms(boolean[] bEnable)

   Get the status if DPMS function.

   :param boolean[] bEnable: parameter to contain the return value, ``true`` for enabled, ``false`` for disabled
   :return: :java:ref:`S_OK` if function succeeds
   :return: ``E_*`` otherwise, see :ref:`return`
