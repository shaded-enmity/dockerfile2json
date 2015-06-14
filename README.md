# dockerfile2json
Converts your Dockerfile to a nice JSON document

Usage
=====

The -f flag switches to nicely formatted output

```
dockerfile2json [-f] path/to/Dockerfile
json2dockerfile path/to/JSON
```

Example of the filters:

```
$ ./dockerfile2json Dockerfile | ./filter-value RUN | ./pkg-install 
yum -y install autoconf bzip2 gcc-c++ git libpqxx{,-devel} libtool libxml2{,-devel} libxslt{,-devel} make nodejs postgresql ruby{,-devel}
```

Note that the original looked like:

```
RUN yum update -y\
 && yum install -y bzip2 libxml2{,-devel} libxslt{,-devel}\
                   libtool ruby{,-devel} make autoconf postgresql\
                   libpqxx{,-devel} git gcc-c++ nodejs bzip2\
 && yum clean -y all
```

In other words -- the pkg-install tool is capable of handling commands embedded within `&&`, `||` and `;`.
The package list was stripped of any duplicate entries (`bzip2`) as well as sorted for better readability.
Flags (`-y`) are preserved too, one limitation is that the parser doesn't know when the flag expects an 
argument, therefore it is neccessary to to use `--variable=value` instead of `--variable value`.

License
=======

MIT
