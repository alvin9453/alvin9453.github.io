SSH Login Without Passwrod
=============================

Step 1 . Prepare
---------------------

Make sure you have the ``.ssh`` directory in your home directory.
::

  mkdir -p ~/.ssh
  chmod 700 ~/.ssh

Step 2 . Generate keys
-------------------------

Use ``ssh-keygen`` to generate key.
::

  ssh-keygen

That will ask you some questions, just press enter to skip it. Then you will get a ``id_rsa.pub``(public key) and ``id_rsa``(private key) in ``~/.ssh``.

Step 3 . Put public key to where you want to connect by ssh
-------------------------------------------------------------

::

  ssh-copy-id -p [PORT] -i ~/.ssh/id_rsa.pub USER@HOSTNAME

Done!


Reference
----------

https://blog.gtwang.org/linux/linux-ssh-public-key-authentication/
