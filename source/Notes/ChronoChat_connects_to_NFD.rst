ChronoChat connects to NFD
================================

Introduction
---------------

When I download `Web ChronoChat <https://github.com/named-data/ChronoChat-js>`_ , I notice that there is a wshub option. User could chat with each other via connect to ucla NFD, but why not just use my own NFD?

Configure nfd.conf file
-------------------------

ChronoChat needs to connect with NFD to receive interests. For testing with my own NFD, I have to update ``/usr/local/etc/ndn/nfd.conf`` to accept remote connections.(Even though I am connecting to my localhost, a WebSocket connection is always considered remote.).
::

    ; The following localhop_security should be enabled when NFD runs on a hub,
    ; which accepts all remote registrations and is a short-term solution.
    localhop_security
    {
        trust-anchor
        {
            type any
        }
    }

Replace wshub with my NFD IP address or domain name, and users could chat based on my NFD now!