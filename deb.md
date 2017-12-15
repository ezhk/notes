# Create RPM package

- install depencies:

        # apt-get install dh-make devscripts

- prepate build directory:

        $ mkdir debbuild && cd debbuild

- init default DEB struct:

        $ dh_make -c gpl -s -p test_0.1 --createorig

Create our test package:</br>
-> changelog:

        $ dch -i
        test (0.1) UNRELEASED; urgency=medium
          * test package
         -- Andrey Kiselev <MYMAIL_HERE>  Fri, 15 Dec 2017 15:34:06 +0300

- create file:

        $ echo 'test' >test_file

—> debian/install:

        test_file /test

- remove source directory:

        $ rm -r debian/source

- build our package:

        $ dpkg-buildpackage --force-sign

- enjoy:

        $ find . -type f
        ./test_file
        ./debian/test-docs.docs
        ./debian/copyright
        ./debian/test.debhelper.log
        ./debian/install
        ./debian/README.source
        ./debian/README.Debian
        ./debian/debhelper-build-stamp
        ./debian/rules
        ./debian/files
        ./debian/test.doc-base.EX
        ./debian/test.substvars
        ./debian/changelog
        ./debian/control
        ./debian/test/usr/share/doc/test/copyright
        ./debian/test/usr/share/doc/test/README.Debian
        ./debian/test/usr/share/doc/test/changelog.gz
        ./debian/test/DEBIAN/md5sums
        ./debian/test/DEBIAN/control
        ./debian/test/test/test_file
        ./debian/compat

        $ dpkg -c ../test_0.1_amd64.deb
        drwxr-xr-x root/root         0 2017-12-15 15:36 ./
        drwxr-xr-x root/root         0 2017-12-15 15:36 ./usr/
        drwxr-xr-x root/root         0 2017-12-15 15:36 ./usr/share/
        drwxr-xr-x root/root         0 2017-12-15 15:36 ./usr/share/doc/
        drwxr-xr-x root/root         0 2017-12-15 15:36 ./usr/share/doc/test/
        -rw-r--r-- root/root      1399 2017-12-15 15:32 ./usr/share/doc/test/copyright
        -rw-r--r-- root/root       168 2017-12-15 15:32 ./usr/share/doc/test/README.Debian
        -rw-r--r-- root/root       130 2017-12-15 15:34 ./usr/share/doc/test/changelog.gz
        drwxr-xr-x root/root         0 2017-12-15 15:36 ./test/
        -rw-r--r-- root/root         5 2017-12-15 15:33 ./test/test_file
