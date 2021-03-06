.. _tutorials__getting_started__connect_to_data:

Connect to data
===============

Once you have a DataContext, you'll want to connect to data.  In Great Expectations, :ref:`Datasources` simplify connections, by managing configuration and providing a consistent, cross-platform API for referencing data.

Let's configure your first Datasource, a connection to the local Postgres database we've provided. Follow the next steps in the CLI init flow (**note** the non-standard port for the Postgres connection!):
    
.. code-block:: bash
    
    Would you like to configure a Datasource? [Y/n]: 
    
    What data would you like Great Expectations to connect to?
        1. Files on a filesystem (for processing with Pandas or Spark)
        2. Relational database (SQL)
    : 2
    
    Which database backend are you using?
        1. MySQL
        2. Postgres
        3. Redshift
        4. Snowflake
        5. BigQuery
        6. other - Do you have a working SQLAlchemy connection string?
    : 2
    
    Give your new Datasource a short name.
     [my_postgres_db]:
    
    Next, we will configure database credentials and store them in the `my_postgres_db`
    section of this config file: great_expectations/uncommitted/config_variables.yml:

    Would you like to proceed? [Y/n]:

    What is the host for the postgres connection? [localhost]: <enter>
    What is the port for the postgres connection? [5432]: 65432
    What is the username for the postgres connection? [postgres]: ge_tutorials
    What is the password for the postgres connection?: ge_tutorials
    What is the username for the postgres connection? [postgres]: ge_tutorials

    ...

    Would you like to profile new Expectations for a single data asset
    within your new Datasource? [Y/n]: n

That's it! You just configured your first Datasource! Make sure to choose ``n`` at this prompt to exit the ``init`` flow for now.

**Before continuing, let's stop and unpack what just happened.**


Configuring Datasources
-----------------------

When you completed those last few steps in ``great_expectations init``, you told Great Expectations that:

1. You want to create a new Datasource called ``my_postgres_db``.
2. You want to use SqlAlchemy to evaluate your Expectations, hence ``data_asset_type.class_name = SqlAlchemyDataset``. Your database configuration tells the SqlAlchemyDataset to use a Postgresql-specific driver.

Based on that information, the CLI added the following entry into your ``great_expectations.yml`` file, under the ``datasources`` header:

.. code-block:: yaml

    my_postgres_db:
    credentials: ${my_postgres_db}
    data_asset_type:
      class_name: SqlAlchemyDataset
      module_name: great_expectations.dataset
    class_name: SqlAlchemyDatasource
    module_name: great_expectations.datasource

In addition, you will find the credentials for the database in ``great_expectations/uncommitted/config_variables.yml``:

.. code-block:: yaml

    my_postgres_db:
      drivername: postgresql
      host: localhost
      port: '65432'
      username: ge_tutorials
      password: ge_tutorials
      database: ge_tutorials

In the future, you can modify or delete your configuration by editing your ``great_expectations.yml`` and ``config_variables.yml`` file directly. For instructions on how to configure various Datasources, check out :ref:`How-to guides for configuring Datasources <how_to_guides__configuring_datasources>`.

For now, let's continue to create your first Expectations.