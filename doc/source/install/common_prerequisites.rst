Prerequisites
-------------

Before you install and configure the fenixclient service,
you must create a database, service credentials, and API endpoints.

#. To create the database, complete these steps:

   * Use the database access client to connect to the database
     server as the ``root`` user:

     .. code-block:: console

        $ mysql -u root -p

   * Create the ``fenixclient`` database:

     .. code-block:: none

        CREATE DATABASE fenixclient;

   * Grant proper access to the ``fenixclient`` database:

     .. code-block:: none

        GRANT ALL PRIVILEGES ON fenixclient.* TO 'fenixclient'@'localhost' \
          IDENTIFIED BY 'FENIXCLIENT_DBPASS';
        GRANT ALL PRIVILEGES ON fenixclient.* TO 'fenixclient'@'%' \
          IDENTIFIED BY 'FENIXCLIENT_DBPASS';

     Replace ``FENIXCLIENT_DBPASS`` with a suitable password.

   * Exit the database access client.

     .. code-block:: none

        exit;

#. Source the ``admin`` credentials to gain access to
   admin-only CLI commands:

   .. code-block:: console

      $ . admin-openrc

#. To create the service credentials, complete these steps:

   * Create the ``fenixclient`` user:

     .. code-block:: console

        $ openstack user create --domain default --password-prompt fenixclient

   * Add the ``admin`` role to the ``fenixclient`` user:

     .. code-block:: console

        $ openstack role add --project service --user fenixclient admin

   * Create the fenixclient service entities:

     .. code-block:: console

        $ openstack service create --name fenixclient --description "fenixclient" fenixclient

#. Create the fenixclient service API endpoints:

   .. code-block:: console

      $ openstack endpoint create --region RegionOne \
        fenixclient public http://controller:XXXX/vY/%\(tenant_id\)s
      $ openstack endpoint create --region RegionOne \
        fenixclient internal http://controller:XXXX/vY/%\(tenant_id\)s
      $ openstack endpoint create --region RegionOne \
        fenixclient admin http://controller:XXXX/vY/%\(tenant_id\)s
