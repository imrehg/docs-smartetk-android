Smart ETK API General Notes
===========================

.. java:package:: com.viaembedded.smartetk

Smart ETK is programmed with the socket IO as the communication between
JAVA and C language to control the hardware modules, therefore you need to
make sure that you have android.permission.INTERNET in AndroidManifest.xml:

.. code-block:: xml

   <uses-permission android:name="android.permission.INTERNET"/>
