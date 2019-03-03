# qcad-debian

Debianization of QCAD community version. This is a work in progress; currently it does not conform to debian policy neither do it pass lintian check. However, the resulting package does not clutter the system and it works.

## Downloading

Go to http:://www.qcad.org/download scroll down to 'QCad Community Edition Source Code' and download the most recent version. Alternatively, go to http://github.com/qcad/qcad and download one of the supported releases (more on this below).

Unpack the downloaded archive and cd to the resulting directory
```shell
tar -zxv qcad-3.xx.yy.zz.tar.gz
cd qcad-3.xx.yy.zz/
```
Substitute xx.yy.zz in the command above with the actual version of your downloaded archive.

In the unpacked directory do a clone of this repository and check out the tag that matches the version of the downloaded archive.
```shell
git clone -b v3.xx.yy.zz http://github.com/pixeldexter/qcad-debian/ debian/
```
Again, in the command above you should substitute xx.yy.zz with the actual version of the downloaded archive.

## Supported Versions

In this repository there exists a tag for each of the supported version of the parent QCAD project. The name of the tag matches
the release name of the parent project.

E.g., QCAD release 3.22.0.0 is tagged as 'v3.22.0.0'. To build a debian package of this release you should also check out v3.22.0.0 in clone of this repository as well.

## Prerequisites

Install everything that is required for building a package. Devscripts is also highly recommended.
```shell
sudo apt-get install build-essential dpkg-dev devscripts
```

## Building

Normal methods of building debian packages apply. For instance, you can use either dpkg-buildpackage or sbuild.

Using dpkg-buildpackage you should first install build dependencies. In the directory from where you unpacked the archive do:
```shell
mk-build-deps qcad-3.xx.yy.zz/debian/control
sudo dpkg -i qcad-build-deps_3.xx.yy.zz-1_all.deb
sudo apt-get install --fix-broken
```

Make sure that all dependencies are installed, then:
```
dpkg-buildpackage qcad-3.xx.yy.zz
```
It should produce a deb package. Install it directly with 'dpkg -i' or put into an archive (local-apt-repository is recommended) and install from there by normal means.

Do not forget to remove qcad-build-deps
```shell
sudo apt-get remove qcad-build-deps
```

## Changelog

See here: [changelog](changelog)

## TODO

* Split into multiple packages (-docs, -data, etc).
* Write README's
* Write proper copyright file
* Fix lintian issues
* Submit to debian?
