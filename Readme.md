CTA `ctools` installation instructions
==============================

Installing gammaLib, ctools and CTAtools (and ctamacropy)

Tested in:
- Linux: Ubuntu 16.10
- MacOS: 10.12.5

# 1. gammaLib & ctools

Page: http://cta.irap.omp.eu/ctools/

Download: http://cta.irap.omp.eu/ctools/download.html#download
 *There is a .dmg for Mac and works. 

Instructions can be found in
http://cta.irap.omp.eu/ctools/users/user_manual/getting.html

In Mac, just open the .dmg file and go to 1.3

(the $ symbol indicates the console prompt and is not part of the command that you should type in).

## 1.1 gammalib

### 1.1.1 Install in Linux:

```shell
tar xvfz gammalib-1.2.0.tar.gz 
cd gammalib-1.2.0 
./configure
make
make check
make install 
```

The last step may require system administrator privileges. In this case, use

```
sudo make install
```

### 1.1.2 Set environment

Type
$ export GAMMALIB="/usr/local/gamma"  #default path, but put yours 
$ source $GAMMALIB/bin/gammalib-init.sh  #default path, but put yours

Then you can check 
$python
>>>import gammalib
>>>
And it should be no complains. 

You can also check where the gammalib is, with:
$python
>>>import gammalib, os
>>>path = os.path.dirname(gammalib.__file__)
>>>print path
/usr/local/gamma/lib/python2.7/site-packages/gammalib 
>>>

### 1.1.3 Things can go wrong
 
In Ubuntu 16.10 some libraries were needed: libcifitsio-dev, libncurses5-dev, lib redline-dev
You can easily solve it by:
$ sudo apt-get install libcifitsio-dev libncurses5-dev libredline-dev


## 1.2 ctools

In Linux
$ tar xvfz ctools-1.2.0.tar.gz
$ cd ctools-1.2.0
$ ./configure
$ make
$ make install 

The last step may require system administrator privileges. In this case, use
$ sudo make install

$ export CTOOLS=/usr/local/gamma
$ source $CTOOLS/bin/ctools-init.sh


## 1.3 Permanent environment

Open

in Mac: .bash_profile

in Linux: .bashrc 

you can access with 
$ nano <file>

Then add:

```bash
## CTA var ##
export CTOOLS="/usr/local/gamma"   #default path, but put yours 
export GAMMALIB="/usr/local/gamma"  #default path, but put yours 
. /usr/local/gamma/bin/gammalib-init.sh  #default path, but put yours
```

And make sure that you already have $PYTHONPATH:
$ echo $PYTHONPATH

If not, you can try in your bash file:

export PYTHONPATH=“..your path to your Py.Libs:$PYTHONPATH"

If you use Anaconda:
export PYTHONPATH=“..your path/anaconda/lib:$PYTHONPATH"

### 1.3.1 Things can go wrong

Missing python packages can be install with  

With Anaconda: `$ conda install <package>` or 
`$ pip install <package>`.

You need to use Python 2.x to get it working. If you have multiple Anaconda environments installed, try `source activate <name-of-your-python2-env>`.



# 2. CTAtools

## 2.1 Links

Documentation: 
http://ctatools.readthedocs.io/en/latest/index.html

Download.
In your terminal:
$ git clone https://github.com/davidsanchez/CTAtools.git

If you doesn’t have git
$ sudo apt-get install git

### 2.1.1 Environment

Edit in CTAtools/Init_tools.sh for your Dirs. 

A new ebltable version is in:

https://github.com/me-manu/ebltable 

just substitute the new version in the CTA folder (it has the LIV functions)

Then type

$ python install_CTAtools.py
$ python test_setup.py


Everything can be set in the  bash by:

function var-cta() {
	. /…your path to CTA-Software/CTAtools/Init_tools.sh
	##ctools
	export CTOOLS="/usr/local/gamma"
	export GAMMALIB="/usr/local/gamma"
	./usr/local/gamma/bin/gammalib-init.sh
}

### 2.1.2 Things can go wrong 

If ebltable stills missing, try 
$ conda install ebltable
in CTAtools/ebltable

If doesn’t work, try brute force andcopy the 
ebltable/ebltable/
 
in yours

…/anaconda/lib/python2.7/site-packages/ebltable/


If there are missing pythons libs, try to change the init_tools.sh:

```bash
#manage Python
#unset PYTHONPATH. # <— add #
export PYTHONPATH="$CTATOOLS_DIR:$PYTHONPATH"  # <— add :$PYTHONPATH
```

Then  add to your bash file 

. /your path to CTA-Software/CTAtools/Init_tools.sh

If there are missing commands in Linux, try

$ sudo apt-get install 

Missing python libs in Linux, try

$ conda install …
or 
$ pip install …

The last step may require system administrator privileges. In this case, use
$ sudo pip install… 

# pyRoot

Could be issues with Python 2.7.10/2.7.13

Solution:
Mac:
Last version 6.08/04 works after updating: 
-MacPorts, (for make-version issues)
-brew,  (for make -version issues, brew install cmake)
-Xcode 



# ctamacropy

Download:
$ git clone https://github.com/cta-observatory/ctamacros.git


Only Root is needed
Test 
$cd ctamacros
$root testCTA_v6simple.C

To enable python
$ export PYTHONPATH=“…path/to/ctamacros:$PYTHONPATH"

And add it to your bash file.

<> in makeCTAmaps_v6.C
makeCTAmaps() -> makeCTAmaps_v6.C
spectra.py
line 29, in set_root_spec
    spec		= "{0[norm]}*pow(x / {0[scale]},{0[index])*exp(x * {0[cut]})".format(params)  <- '}' missing extra ')'


# Some Links

https://github.com/davidsanchez/CTAtools
http://ctatools.readthedocs.io/en/latest/index.html
http://cta.irap.omp.eu/ctools/
http://ctatools.readthedocs.io/en/latest/EBL.html​
https://portal.cta-observatory.org/WG/PHYS/SitePages/Consortium%20Publication%20EBL,%20ALP,%20LIV,%20IGMF.aspx
