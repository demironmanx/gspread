V6 migration guide
==================

Below is a migration guide to help you migrate
you code to the new v6.x.y version of gspread.


HTTP Client migration
---------------------

The HTTP clients have been moved to a dedicated file.

The methods to invoke them have been slightly renamed too.

By default gspread uses the regular HTTP `Client`.
If you wish to change that and use the HTTP `BackoffClient`.

You can update your code when the new release v6 is out as follow:

Current code using gspread v5.x.y

.. code:: python

    import gspread

    client = gspread.service_account(client_factory=gspread.client.BackoffClient)


When gspread v6.x.y is out can be updated to:


.. code:: python

    import gspread

    client = gspread.service_account(http_client=gspread.http_client.BackOffHTTPClient)


Python-3.7 end of life
----------------------

From release v6.x.y we do not support python-3.7 anymore.

This python version has been deprecated since.

In order to keep your code compatible please upgrade your python version.

