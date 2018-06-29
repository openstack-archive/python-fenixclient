2. Edit the ``/etc/fenixclient/fenixclient.conf`` file and complete the following
   actions:

   * In the ``[database]`` section, configure database access:

     .. code-block:: ini

        [database]
        ...
        connection = mysql+pymysql://fenixclient:FENIXCLIENT_DBPASS@controller/fenixclient
