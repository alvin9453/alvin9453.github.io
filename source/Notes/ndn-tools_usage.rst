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


Reference
-----------

NDN-tools : https://github.com/named-data/ndn-tools
