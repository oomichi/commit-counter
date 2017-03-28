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

 /usr/local/bin/stackalytics-processor  --config-file commit-counter/stackalytics_etc/stackalytics.conf --default-data-uri file:///home/oomichi/commit-counter/stackalytics_etc/default_data.json

Start http server for stackalytics (http://127.0.0.1:8080/)::

 /usr/local/bin/stackalytics-dashboard

We can access a web site with http://127.0.0.1:8080/widget


Config file - default_data.json
-------------------------------

* users: Relationship between developers and companies
* companies: Relationship between e-mail domains and companies
* releases: Consistent version info for all parsed repos. (Mandatory)
* repos: Target git repo
* mail_lists: Target mailing lists - Better to remove whole of this for local usage

