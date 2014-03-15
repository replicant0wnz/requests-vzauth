requests-vzauth
==============
This package allows for authentication to the Verizon Cloud API using the requests library.

Examples
^^^^^^^^

Basic GET to list all VMs
-------------------------

.. code-block:: python

    import os
    import requests

    from requests_vzauth import vzAuth

    baseurl = 'https://api.cloud.verizon.com'
    secret  = 'YOUR-SECRET'
    access  = 'YOUR-ACCESS'

    request_path = "/api/cloud/vm"
    r = requests.get(baseurl + request_path, auth=vzAuth(secret, access, request_path))

    items = r.json()

    for i in items['items']:
        print i['name'] + ": " + i['status']

Basic POST to power off all VMs
-------------------------------

.. code-block:: python

    import os
    import requests

    from requests_vzauth import vzAuth

    baseurl = 'https://api.cloud.verizon.com'
    secret  = 'YOUR-SECRET'
    access  = 'YOUR-ACCESS'

    request_path = "/api/cloud/vm"
    r = requests.get(baseurl + request_path, auth=vzAuth(secret, access, request_path))

    items = r.json()

    for i in items['items']:
        power_off = "%s/%s/power-off/" %(request_path, i['id'])
        content_type = 'application/vnd.terremark.ecloud.controller.v1+json'
        print "Powering off %s" % i['name']
        r = requests.post(baseurl + power_off, auth=vzAuth(secret, access, power_off, content_type))

Installation
------------
Via PyPI

.. code-block:: bash

    $ pip install requests_vzauth 

Via git

.. code-block:: bash

    $ git clone https://github.com/replicant0wnz/requests-vzauth
    $ cd requests-vzauth; python ./setup.py install

Requirements
------------
- requests_

.. _requests: https://github.com/kennethreitz/requests/
