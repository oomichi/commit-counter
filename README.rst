Commit counter of git repos
===========================

This tool is for knowing who contribute to each software development
from git history.

1. Recent 100 commits
2. Each version
3. Whole history

Use stackalytics
----------------

Install stackalytics::

 apt-get update
 apt-get install -y git
 apt-get install -y python
 apt-get install -y python-setuptools
 apt-get install -y python-pip
 apt-get install -y libssl-dev
 apt-get install -y libffi-dev
 apt-get install -y memcached
 git clone https://github.com/openstack/stackalytics/
 cd stackalytics/
 pip install -r requirements.txt
 python setup.py install
 memcached -u memcache -d

Store data into memcached DB::

 $ stackalytics-processor  --config-file commit-counter/stackalytics_etc/stackalytics.conf --default-data-uri file:///home/oomichi/commit-counter/stackalytics_etc/default_data.json

Start http server for stackalytics (http://127.0.0.1:8080/)::

 $ stackalytics-dashboard -d --config-file commit-counter/stackalytics_etc/stackalytics.conf

Challenges
----------

1. http://127.0.0.1:8080/widget seems a proxy to http://stackalytics.com
2. http://127.0.0.1:8080//api/1.0/stats/companies needs to provide companies data
   Now: 200 with empty data like {"stats": []}
   It should contain company names from git history

TODO
----

1. (Done) Enable stackalytics-processor for mesos only
2. Enable REST API service of stackalytics-dashboard::
 * /api/1.0/stats/companies
 * /api/1.0/stats/modules
 * /api/1.0/stats/engineers
 * /api/1.0/activity
 * /api/1.0/contribution
 * /api/1.0/modules
 * /api/1.0/companies/<company_name>
 * /api/1.0/modules/<module_id>
 * /api/1.0/releases
3. Enable Web page of stackalytics-dashboard

Config file - default_data.json
-------------------------------

* users: Relationship between developers and companies
* companies: Relationship between e-mail domains and companies
* releases: Consistent version info for all parsed repos. (Mandatory)
* repos: Target git repo
* mail_lists: Target mailing lists - Better to remove whole of this for local usage

