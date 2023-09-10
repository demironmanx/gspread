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


New method ``Worksheet.update()`` signature
-------------------------------------------

The method ``Worksheet.update()`` signature has changed.


You can update your code when the new release v6 is out as follow:

Current code using gspread v5.x.y

.. code:: python

    import gspread

    client = gspread.service_account(client_factory=gspread.client.BackoffClient)

    file = client.open("TestGspread")
    file.sheet1.update("I7", "53")


You can update your code right now by naming the parameters ``range_name`` and ``values``.

This can be done from **gspread-5.11**:


.. code:: python

    import gspread

    client = gspread.service_account(http_client=gspread.http_client.BackOffHTTPClient)

    file = client.open("TestGspread")
    file.sheet1.update(range_name="I7", values=[["54"]])


Use hexadecial values to change tab color
-----------------------------------------

When setting the tab color we use a dict with values from ``0`` to ``1``
using a floating point number with 8 decimals.

Instead after the gspread-6.x.y we will use an hexadecial values
(like everyone on the internet).


You can update your code when the new release v6 is out as follow:

Current code using gspread v5.x.y

.. code:: python

    import gspread

    client = gspread.service_account(client_factory=gspread.client.BackoffClient)

    file = client.open("TestGspread")
    tab_color = {"red": 1, "green": 0, "blue": 0}
    file.sheet1.update_tab_color(tab_color)


When gspread v6.x.y is out can be updated to:

.. code:: python

    import gspread

    client = gspread.service_account(http_client=gspread.http_client.BackOffHTTPClient)

    file = client.open("TestGspread")
    tab_color = {"red": 0, "green": 0, "blue": 1}
    hex_color = gspread.utils.convert_colors_to_hex_value(**tab_color)
    file.sheet1.update_tab_color(hex_color)
