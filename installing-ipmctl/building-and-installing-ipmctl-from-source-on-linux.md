# Building and Installing IPMCTL from Source on Linux

Building ipmctl from source code if your Linux package repository does not provide package or it contains a old version.

{% tabs %}
{% tab title="Fedora" %}
This procedure provides the steps for building and installing ipmctl on Fedora.

### Prerequisites

ipmctl has a dependency on libsafec-devel, libndctl-devel and rubygem-asciidoctor. Steps to install these packages is provided below.

#### Install the required utilities

This procedure requires the following utilities

* wget
* git
* cmake
* gcc
* gcc-c++
* glibc 
* glibc-static

```text
sudo dnf install wget git cmake gcc gcc-c++ glibc glibc-static 
```

#### libsafec

libsafec is available as a package in the EPEL repository \(Extra Packages for Enterprise Linux\).

Alternately, when compiling ipmctl from source code, use the `-DSAFECLIB_SRC_DOWNLOAD_AND_STATIC_LINK=ON` option to download safelibc source and build it as a static library with ipmctl. See the Build section below for more information.

Verify the `libsafec` package can be found

```text
dnf info libsafec libsafec-devel
```

Example:

```text
$ dnf info libsafec libsafec-devel

Available Packages
Name         : libsafec
Version      : 3.3
Release      : 5.fc31
Architecture : i686
Size         : 82 k
Source       : libsafec-3.3-5.fc31.src.rpm
Repository   : fedora
Summary      : Safec fork with all C11 Annex K functions
URL          : https://github.com/rurban/safeclib
License      : MIT
Description  : Safec fork with all C11 Annex K functions

Name         : libsafec-devel
Version      : 3.3
Release      : 5.fc31
Architecture : i686
Size         : 19 k
Source       : libsafec-3.3-5.fc31.src.rpm
Repository   : fedora
Summary      : Development packages for libsafec
URL          : https://github.com/rurban/safeclib
License      : MIT
Description  : Development files for libsafec
```

Install the libsafec and libsafec-devel packages

```text
sudo dnf install libsafec libsafec-devel
```

#### libndctl-devel

The development files can be installed from source code or packages. See '[Installing NDCTL & DAXCTL](https://docs.pmem.io/ndctl-user-guide/installing-ndctl)' in the ndctl user guide for detailed instructions. 

To install the package:

```text
sudo dnf install ndctl-devel
```

#### Asciidoctor

The `rubygem-asciidoctor` package can be found in the EPEL \(Extra Package for Enterprise Linux\) repository. 

Install the rubygem-asciidoctor and optional rubygem-asciidoctor-pdf packages

```text
sudo dnf install rubygem-asciidoctor rubygem-asciidoctor-pdf
```

### 

### Build

Create a temporary build area

```text
mkdir ~/downloads
cd ~/downloads
```

Clone the ipmctl GitHub repository

```text
git clone https://github.com/intel/ipmctl
cd ipmctl
```

If you installed the safelibc package, use:

```text
mkdir output && cd output
cmake -DRELEASE=ON -DCMAKE_INSTALL_PREFIX=/ ..
make -j all
```

To have ipmctl cmake download and statically build safelibc, use:

```text
mkdir output && cd output
cmake -DRELEASE=ON -DSAFECLIB_SRC_DOWNLOAD_AND_STATIC_LINK=ON -DCMAKE_INSTALL_PREFIX=/ ..
make -j all
```

### 

### Install

Install ipmctl using:

```text
sudo make install
```
{% endtab %}

{% tab title="RHEL & CENTOS" %}
This procedure provides the steps for building and installing ipmctl on RHEL, CENTOS, and RHEL for SAP HANA 7.5 and later.

### Prerequisites

ipmctl has a dependency on libsafec-devel, libndctl-devel and rubygem-asciidoctor. Steps to install these packages is provided below.

#### EPEL Package Repository

Several packages required by ipmctl are available in the EPEL \(Extra Packages for Enterprise Linux\). The epel repository must be installed and enabled.

Verify the EPEL repository is available and enabled:

```text
yum repolist
```

Example:

```text
$ yum repolist
repo id                                   repo name                                                          status
epel/x86_64                               Extra Packages for Enterprise Linux 7 - x86_64                     13,220
```

If the EPEL repository is not listed, install and enable it using:

```text
sudo yum install epel-release
```

#### Enable the PowerTools repository

```text
sudo yum config-manager --set-enabled PowerTools
```

#### Install the required utilities

This procedure requires the following utilities

* wget
* git
* cmake
* gcc
* gcc-c++
* glibc 
* glibc-static

```text
sudo yum install wget git cmake gcc gcc-c++ glibc glibc-static 
```

#### libsafec

libsafec is available as a package in the EPEL repository \(Extra Packages for Enterprise Linux\).

Alternately, when compiling ipmctl from source code, use the `-DSAFECLIB_SRC_DOWNLOAD_AND_STATIC_LINK=ON` option to download safelibc source and build it as a static library with ipmctl. See the Build section below for more information.

Verify the `libsafec` package can be found

```text
yum info libsafec libsafec-devel
```

Example:

```text
$ yum info safelibc

Available Packages
Name        : libsafec
Arch        : x86_64
Version     : 3.3
Release     : 5.el7
Size        : 69 k
Repo        : epel/x86_64
Summary     : Safec fork with all C11 Annex K functions
URL         : https://github.com/rurban/safeclib
License     : MIT
Description : Safec fork with all C11 Annex K functions

Name        : libsafec-devel
Arch        : x86_64
Version     : 3.3
Release     : 5.el7
Size        : 74 k
Repo        : installed
From repo   : epel
Summary     : Development packages for libsafec
URL         : https://github.com/rurban/safeclib
License     : MIT
Description : Development files for libsafec
```

Install the libsafec and libsafec-devel packages

```text
sudo yum install libsafec libsafec-devel
```

#### libndctl-devel

The development files can be installed from source code or packages. See '[Installing NDCTL & DAXCTL](https://docs.pmem.io/ndctl-user-guide/installing-ndctl)' in the ndctl user guide for detailed instructions. 

To install the package:

```text
sudo yum install ndctl-devel
```

#### Asciidoctor

The `rubygem-asciidoctor` package can be found in the EPEL \(Extra Package for Enterprise Linux\) repository. 

Install the rubygem-asciidoctor package

```text
sudo yum install rubygem-asciidoctor
```

**\[Optional\]** PDF documents can be built if `asciidoctor-pdf` is installed. This is completely optional. Warnings during the cmake make occur but can be ignored. Asciidoctor-pdf is installed using the `gem` utility. Asciidoctor-pdf requires Ruby 2.1 or later. CentOS 7 provides Ruby 2.0. See [How to Install Ruby on CentOS/RHEL 7/6](https://tecadmin.net/install-ruby-latest-stable-centos/) for instructions to install a current Ruby version.

With Ruby &gt;2.1 installed, install asciidoctor-pdf

```text
sudo gem install asciidoctor-pdf
```

### 

### Build

Create a temporary build area

```text
mkdir ~/downloads
cd ~/downloads
```

Clone the ipmctl GitHub repository

```text
git clone https://github.com/intel/ipmctl
```

If you installed the safelibc package, use:

```text
mkdir output && cd output
cmake -DRELEASE=ON -DCMAKE_INSTALL_PREFIX=/ ..
make -j all
```

To have ipmctl cmake download and statically build safelibc, use:

```text
mkdir output && cd output
cmake -DRELEASE=ON -DSAFECLIB_SRC_DOWNLOAD_AND_STATIC_LINK=ON -DCMAKE_INSTALL_PREFIX=/ ..
make -j all
```

### 

### Install

Install ipmctl using:

```text
sudo make install
```
{% endtab %}

{% tab title="Ubuntu" %}
This procedure provides the steps for building and installing ipmctl on Ubuntu.

### Prerequisites

ipmctl has a dependency on libsafec-devel, libndctl-devel and ruby-asciidoctor. Steps to install these packages is provided below.

#### Install the required utilities

This procedure requires the following utilities

* wget
* git
* cmake
* pkg-config
* autoconf
* doxygen
* libtool
* gcc 
* gcc-c++
* glibc

```text
sudo apt update
sudo apt install wget git cmake pkg-config autoconf doxygen libtool build-essential
```

#### libsafec

libsafec is available as a package in the default package repository for Ubuntu 19.10 \(Eoan\) or later. For earlier releases, use the `-DSAFECLIB_SRC_DOWNLOAD_AND_STATIC_LINK=ON` option to download safelibc source and build it as a static library with ipmctl. See the Build section below for more information.

Verify the `libsafec` package can be found

```text
sudo apt info libsafec* libsafec-dev*
```

Install the libsafec and libsafec-devel packages

```text
sudo apt install libsafec-3.5.3 libsafec-dev
```



#### libndctl-devel

The development files can be installed from source code or packages. See '[Installing NDCTL & DAXCTL](https://docs.pmem.io/ndctl-user-guide/installing-ndctl)' in the ndctl user guide for detailed instructions. 

To install the package:

```text
sudo apt install libndctl-dev
```



#### Asciidoctor

**Ubuntu 16.04 & 18.04**

Install asciidoctor using the ruby gems

```text
sudo apt install ruby
sudo gem install asciidoctor asciidoctor-pdf --pre
```

**Ubuntu 19.04 or later**

The `ruby-asciidoctor` package can be found in the default package repository. 

Install the ruby-asciidoctor and optional ruby-asciidoctor-pdf packages

```text
sudo apt install ruby-asciidoctor ruby-asciidoctor-pdf
```



### Build

Create a temporary build area

```text
mkdir ~/downloads
cd ~/downloads
```

Clone the ipmctl GitHub repository

```text
git clone https://github.com/intel/ipmctl
```

If you installed the safelibc package, use:

```text
mkdir output && cd output
cmake -DRELEASE=ON -DCMAKE_INSTALL_PREFIX=/ ..
make -j all
```

To have ipmctl cmake download and statically build safelibc, use:

```text
mkdir output && cd output
cmake -DRELEASE=ON -DSAFECLIB_SRC_DOWNLOAD_AND_STATIC_LINK=ON -DCMAKE_INSTALL_PREFIX=/ ..
make -j all
```



### Install

Install ipmctl using:

```text
sudo make install
```
{% endtab %}
{% endtabs %}



Go to the [Basic Usage](../basic-usage.md) section of this user guide for more information.



### Troubleshooting

The following lists common issues and errors encountered during the cmake process and how to resolve them

#### Issue: -- Could NOT find asciidoctor-pdf \(missing: ASCIIDOCTOR\_PDF\_BINARY\)

You may see a warning during the cmake process referencing a missing asciidoctor-pdf binary.

```text
-- Could NOT find asciidoctor-pdf (missing:  ASCIIDOCTOR_PDF_BINARY) 
asciidoctor-pdf not found
```

#### **Solution:**

PDF documents can be built if asciidoctor-pdf is installed. This is completely optional. Warnings during the cmake make occur but can be ignored. Asciidoctor-pdf is installed using the gem utility. Asciidoctor-pdf requires Ruby 2.1 or later. CentOS 7 provides Ruby 2.0. See How to Install Ruby on CentOS/RHEL 7/6 for instructions to install a later version of Ruby. With Ruby &gt;2.1 installed, install asciidoctor-pdf:

```text
sudo gem install asciidoctor-pdf
```

#### 

#### Issue: -- Could NOT find asciidoc \(missing: ASCIIDOC\_BINARY\)

#### Solution: 

If asciidoctor is installed, ascidoc is not required. This message can be safely ignored.---



#### Issue: -- Could NOT find a2x \(missing: A2X\_BINARY\)

#### Solution:

The `a2x` binary is delivered with the asciidoc package. a2x converts Asciidoc text file to PDF, XHTML, HTML Help, manpage or plain text. If the asciidoc package is not installed, this message can be safely ignored. Asciidoctor will be used instead to build the documentation.

#### Issue: -- package 'safec-3.3&gt;=03032018.0-g570fa5' not found

Example:

```text
--   package 'safec-3.3>=03032018.0-g570fa5' not found
CMake Error at /usr/share/cmake/Modules/FindPkgConfig.cmake:279 (message):
  A required package was not found
Call Stack (most recent call first):
  /usr/share/cmake/Modules/FindPkgConfig.cmake:333 (_pkg_check_modules_internal)
  CMakeLists.txt:87 (pkg_check_modules)
```

You should not encounter this message when using the `-DSAFECLIB_SRC_DOWNLOAD_AND_STATIC_LINK=ON` cmake option.

#### Solution:

The issue can occur if the libsafec and libsafec-devel packages are not installed. See the 'Prerequisites' section at the top of this page.

If you installed the libsafec package from a repository other than EPEL, remove and re-install the libsafec package using the epel repository. Follow the instructions in the 'libsafec' section above. 

If you built and installed libsafec from source code, the error is caused by a missing pkgconfig \(pc\) file. Update your LD\_LIBRARY\_PATH and PKG\_CONFIG\_PATH to include the path you installed libsafec to. For example, the following adds the common install locaitons to your shell environment. You will need to add these to your shell environment file \(eg: ~/.bashrc\) for them to become permanent. 

```text
export LD_LIBRARY_PATH=/usr/lib:/usr/lib64:/usr/local/lib:/usr/local/lib64:${LD_LIBRARY_PATH}
export PKG_CONFIG_PATH=/usr/lib64/pkgconfig:/usr/lib/pkgconfig:usr/local/lib64/pkgconfig:/usr/local/lib/pkgconfig:/usr/share/pkgconfig:${PKG_CONFIG_PATH}
```

Alternatively, add `-DSAFECLIB_SRC_DOWNLOAD_AND_STATIC_LINK=ON`to the cmake file to download and build the static version of libsafec.



