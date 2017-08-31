NDN-Tools Usages
==================

Introduction
---------------

This document would show some ndn-tools' command to communicate with other machine over NDN.


Preparation
-------------

First, create a remote face :

::

   > nfdc face create udp4://<remote_ip_addr>:6363

then use ``nfdc face list`` like below to check this face is created successfully.

::

  > nfdc face list
  ...
  ...
  faceid=280 remote=udp4://<remote_ip_addr>:6363 local=udp4://<my_ip_addr>:6363
  ....
  ....

Next, add the route :

::

  nfdc route add /ndn/tw/edu/ncnu/csie/jarvis udp4://<remote_ip_addr>

And ``NFD`` knows how to send interest to the route now!

ndnping [#]_
------------------

Open the ``ndnpingserver`` first:

::

  ndnpingserver /ndn/tw/edu/ncnu/csie/jarvis

Then open another terminal to use ``ndnping`` :

::

  ndnping /ndn/tw/edu/ncnu/csie/jarvis


ndnputchunk and ndncatchunk
------------------------------

``ndnputchunk`` is put a file content in content store (RAM in the computer), and user could retrieve data by ``ndncatchunk``.

Upload a file :

::

  ndnputchunk /ndn/file/name/myfile < myfile

Retrieve this file :

::

  ndncatchunk /ndn/file/name/myfile > myfile



Reference
-----------

.. [#] ndnping : https://github.com/named-data/ndn-tools/tree/master/tools/ping

NDN-tools : https://github.com/named-data/ndn-tools
