**readlog** - cuts apache log into pieces
=========================================

Pipe apache logs into `readlog` to selectively display interesting information.

Example: show the access time as Unix epoch and ip addresses

    cat /var/log/apache2/access.log | ./readlog --columns=time,ips

Install
-------

Python 2.5 or later is required. The `ApacheReader` extension is required and
can be compiled and installed by running:

    python setup.py install


Command line options
--------------------

**readlog** offers 3 command line options: 

* `--columns`   - comma delimited list of column names
* `--params`    - comma delimited list of query parameter names
* `--date`      - date format pattern, default is Unix epoch

The available column names, see http://httpd.apache.org/docs/2.2/logs.html#accesslog 
for details

* `ips`         - IP address of the client (remote host) 
* `username`    - userid by HTTP authentication.
* `ident`       - identity 
* `time`        - time that the request was received
* `tz`          - timezone
* `method`      - method used by the client 
* `url`         - requested url
* `path`        - hierarchical path in the url
* `query`       - query component in the url
* `fragment`    - fragment identifier in the url
* `protocol`    - protocol used by the client
* `status`      - status code that the server sends back to the client
* `size`        - size of the object returned to the client
* `referer`     - the site that the client reports having been referred from
* `user-agent`  - User-Agent HTTP request header

The names in the `--params` option can be used to show the corresponding query 
parameter values.

Example: show the query parameter values with names equal to `page` and `type`

    cat /var/log/apache2/access.log | ./readlog --params=page,type

The options `--params` and `--columns` can be combined.

The `--date` option defines the date format for the `time` column. For format 
patterns see:

http://docs.python.org/library/datetime.html#strftime-and-strptime-behavior


Credits
-------

This package uses the `ApacheReader` extension from http://github.com/idealisms/apache-log-reader
