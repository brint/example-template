Description
===========

This is a template for deploying a given shared image ID. This template is
purely an example.

First, [create an Image](http://www.rackspace.com/knowledge_center/article/cloud-essentials-creating-an-image-backup-cloning-and-restoring-a-server-from-a-saved-image).

You will need the Image ID.  There are two ways to get the UUID of the image:

1. In [mycloud.rackspace.com](https://mycloud.rackspace.com/), click 'Saved
  Images', click the gear cog next to your image and click 'Create Server with
  Image'. You will see the imageId listed at the end of the url.
2. Using
  [python-novaclient](http://www.rackspace.com/knowledge_center/article/installing-python-novaclient-on-linux-and-mac-os),
  run `nova image-list` with your cloud credentials.

Requirements
============
* An OpenStack username, password, and tenant id.
* [python-heatclient](https://github.com/openstack/python-heatclient)
`>= v0.2.8`:

```bash
pip install python-heatclient
```

We recommend installing the client within a [Python virtual
environment](http://www.virtualenv.org/).

Example Usage
=============
Here is an example of how to deploy this template using the
[python-heatclient](https://github.com/openstack/python-heatclient):

```
heat --os-username <OS-USERNAME> --os-password <OS-PASSWORD> --os-tenant-id \
  <TENANT-ID> --os-auth-url https://identity.api.rackspacecloud.com/v2.0/ \
  stack-create Example-Stack -f example.yaml \
  -P flavor="1 GB Performance"
```

* For UK customers, use `https://lon.identity.api.rackspacecloud.com/v2.0/` as
the `--os-auth-url`.

Optionally, set environmental variables to avoid needing to provide these
values every time a call is made:

```
export OS_USERNAME=<USERNAME>
export OS_PASSWORD=<PASSWORD>
export OS_TENANT_ID=<TENANT-ID>
export OS_AUTH_URL=<AUTH-URL>
```

Parameters
==========
Parameters can be replaced with your own values when standing up a stack. Use
the `-P` flag to specify a custom parameter.

* `db_image`: Image to use for the Database server (Default:
  5cc098a5-7286-4b96-b3a2-49f4c4f82537 - Ubuntu 14.04)
* `web_image`: Image to use for the Web server (Default:
  5cc098a5-7286-4b96-b3a2-49f4c4f82537 - Ubuntu 14.04)
* `flavor`: Size of the server to provision (Default: 1 GB Performance)

Outputs
=======
Once a stack comes online, use `heat output-list` to see all available outputs.
Use `heat output-show <OUTPUT NAME>` to get the value fo a specific output.

* `private_key`: SSH private that can be used to login as root to the server.
* `web_server_ip`: Public IP address of the web server
* `db_server_ip`: Public IP address of the db server
* `database_password`: Password for the database user
* `site_url`: URL to access the site

For multi-line values, the response will come in an escaped form. To get rid of
the escapes, use `echo -e '<STRING>' > file.txt`. For vim users, a substitution
can be done within a file using `%s/\\n/\r/g`.

License
=======
```
Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
