# r-database-connections
Connecting to different databases from R on Mac OS

#Connect to an MS Access .mdb database

## 1. Install `homebrew` [brew.sh/](http://brew.sh/)

	$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
	$ brew install wget

`homebrew` installs packages to their own directory inside `/usr/local/Cellar` and then symlinks their files into `/usr/local`

## 2. Install `mdb-tools` [github.com/brianb/mdbtools](http://github.com/brianb/mdbtools)

To do this, follow these instructions:

First, make sure you have current installations of:

	libtool
	automake
	autoconf

You can use `homebrew` to install these...

	$ brew install libtool
	$ brew install autoconf
	$ brew install automake

Second, you need a current installation of `glib`.

	$ brew install glib

If you want to build the SQL engine for use in `mdbtools`, you'll also need `bison` or `byacc`, and `flex`.

	$ brew install bison
	$ brew install flex

If you want to build the ODBC driver for use in `mdbtools`, you'll need `unixodbc` (version 2.2.10 or
above).

	$ brew install unixodbc

If you want to build `man` pages, you'll need `txt2man`.

	$ brew install txt2man

You also need to install `pkg-config` and `gnome-doc-utils`.

	$ brew install pkg-config
	$ brew install gnome-doc-utils

Next, download and unzip the latest version of the `mdbtools-master.zip` repo from GitHub [https://github.com/brianb/mdbtools](http://github.com/brianb/mdbtools), then `cd` into that directory and run `autoreconf`. I unzipped the repo in my `Downloads` folder.

	$ cd ~/Downloads/mdbtools-master
	$ autoreconf -i -f
	
Now, run `configure`.

	$ ./configure --with-unixodbc=/usr/local

If that is successful, run `make` to create the `mdbtools` C programs and the needed libraries.

	$ make

Once MDB Tools has been compiled, the generated library folders will be in the `src/libmdb` directory inside of your `mdbtools-master` folder and the utility programs will be in the `src/util` directory inside of `mdbtools-master` folder.

Then run `make install` as to install the libraries and programs to the `/usr/local` directory by default.

	$ make install

This installs a set of lib files into `/usr/local/lib` and the necessary MDB Tools binary files into `/usr/local/bin`.

## 3. In your R installation (e.g., in `RStudio`), install the package `Hmisc` and load it.

	> install.package("Hmisc")
	> library(Hmisc)

You should now be able to connect to an .mdb database using

	> mdb.get(filename)

> d <- mdb.get("~/Desktop/Proyecto_Primates.mdb") # cannot have spaces in name

This method reads newline characters!
