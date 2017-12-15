# Create RPM package
Install depencies:

    $ yum install rpmdevtools rpm-build

Prepare build directory:

    $ mkdir rmpbuild && cd rmpbuild

Init default RPM struct:

    $ rpmdev-setuptree

you might create directories as alternative :

    $ mkdir {BUILD,BUILDROOT,RPMS,SOURCES,SPECS,SRPMS}

Create our test spec file:
- edit SPECS/test.spec:

    Name:           test
    Version:        0.1
    Release:        1%{?dist}
    Summary:        test package

    Group:          Development/Tools
    License:        GPL
    URL:            None
    Source:         %{name}.tar.gz

    %description

    %prep
    %setup -q

    %install
    mkdir -p $RPM_BUILD_ROOT/test
    cp * $RPM_BUILD_ROOT/test/

    %files
    /test
    %doc

    %changelog
    * Fri Dec 15 2017 Andrey Kiselev <MYMAIL_HERE> 0.1
    - test build

Create source tarball with files:

    $ mkdir test-0.1 && echo 'test' >test-0.1/test_file
    $ tar zcvf SOURCES/test.tar.gz test-0.1/

Build our package:

    $ rpmbuild -v -ba SPECS/test.spec

Enjoy:

    $ find . -type f
    ./RPMS/x86_64/test-0.1-1.el7.centos.x86_64.rpm
    ./SOURCES/test.tar.gz
    ./SPECS/test.spec
    ./SRPMS/test-0.1-1.el7.centos.src.rpm
    ./BUILD/test-0.1/test_file
    ./test-0.1/test_file

    $ rpm -qlp RPMS/x86_64/test-0.1-1.el7.centos.x86_64.rpm
    /test
    /test/test_file
