# SkyAlmanac-Py2

SkyAlmanac-Py2 is a Python 2.7 script that creates the daily pages of the Nautical Almanac. These are tables that are needed for celestial navigation with a sextant. Although you are strongly advised to purchase the official Nautical Almanac, this program will reproduce the tables with no warranty or guarantee of accuracy.

SkyAlmanac-Py2 was developed with the intention of having identical output format as SFalmanac-Py2. It is a hybrid version based on two astronomical libraries:  

* the older PyEphem library:  https://rhodesmill.org/pyephem/
* the newer Skyfield library: https://rhodesmill.org/skyfield/

It uses the star database in Skyfield, which is based on data from the Hipparcos Catalogue. PyEphem is used for calculating twilight (actual, civil and nautical sunrise/sunset) and moonrise/moonset. As a consequence, it is **four times faster** than SFalmanac (which uses Skyfield for almost everything).

NOTE: two scripts are included (both can be run): 'skyalmanac.py' and 'increments.py'  
NOTE: a Python 3 script with identical functionality can be found at:  https://github.com/aendie/SkyAlmanac-Py3  
NOTE: a 100% [PyEphem](https://rhodesmill.org/pyephem/) version of SkyAlmanac is available here: https://github.com/aendie/Pyalmanac-Py2

An aim of this development was to maintain:

* **identical PDF output formatting with a similar control program**  
	 It is then possible to display both generated tables (from PyEphem, Skyfield and SkyAlmanac) and compare what has changed by flipping between the two tabs in Adobe Acrobat Reader DC.
	 Anything that has changed flashes, thereby drawing your attention to
	 it. This crude and simple method is quite effective in highlihgting data that might need further attention.

The results have been crosschecked with USNO data to some extent.  
(However, constructive feedback is always appreciated.)

**UPDATE: Nov 2019**

Declination formatting has been changed to the standard used in Nautical Almanacs. In each 6-hour block of declinations, the degrees value is only printed on the first line if it doesn't change. It is printed whenever the degrees value changes. The fourth line has two dots indicating "ditto". This applies to all planet declinations and for the sun's declination, but not to the moon's declination as this is continuously changing.

This also includes some very minor changes and an improved title page for the full almanac with two star charts that indicate the equatorial navigational stars.

**UPDATE: Jan 2020**

The Nautical Almanac tables now indicate if the sun never sets or never rises; similarly if the moon never sets or never rises. For better performance, the *SunNeverSets* or *SunNeverRises* state is determined only by the month of year and hemisphere. (This is reliable for the set of latitudes printed in the Nautical Almanac tables.) The code also has cosmetic improvements.  
P.S. The *Overfull \hbox in paragraph...* messages can be ignored - the PDF is correctly generated.

**UPDATE: Feb 2020**

The main focus was on cleaning up the TeX code and eliminating the *Overfull/Underfull hbox/vbox* messages. Other minor improvements were included.

**UPDATE: Mar 2020**

A new parameter in *config.py* enables one to choose between A4 and Letter-sized pages. A [new approach](https://docs.python.org/3/whatsnew/3.0.html#pep-3101-a-new-approach-to-string-formatting) to string formatting has been implemented:
the [old](https://docs.python.org/2/library/stdtypes.html#string-formatting) style Python string formatting syntax has been replaced by the [new](https://docs.python.org/3/library/string.html#format-string-syntax) style string formatting syntax. 

**UPDATE: Jun 2020**

The Equation Of Time is shaded whenever EoT is negative indicating that apparent solar time is slow compared to mean solar time (mean solar time > apparent solar time).
It is possible to extend the maximum year beyond 2050 by choosing a different ephemeris in config.py.
Bugfix applied to correct the Meridian Passage times.

**UPDATE: Jul 2020**

A new option has been added into config.py: *moonimg = True* will display a graphic image of the moon phase (making the resulting PDF slightly larger). Use *moonimg = False* to revert to the previous format without the graphic moon image.

## Requirements

&nbsp;&nbsp;&nbsp;&nbsp;Computation is done by the free PyEphem and Skyfield libraries.  
&nbsp;&nbsp;&nbsp;&nbsp;Typesetting is done by MiKTeX or TeX Live so you first need to install:

* Python v2.x (2.6 or later)
* Skyfield 1.31 (for best accuracy use 1.31 or higher - see the Skyfield Changelog)
* Pandas (to load the Hipparcos catalog; tested: 0.24.2, 0.25.3)
* Ephem 3.7.6 or 3.7.7
* TeX/LaTeX&nbsp;&nbsp;or&nbsp;&nbsp;MiKTeX&nbsp;&nbsp;or&nbsp;&nbsp;TeX Live

&nbsp;&nbsp;&nbsp;&nbsp;**DEPRECATION:** Python 2.7 will reach the end of its life on January 1st, 2020.  
&nbsp;&nbsp;&nbsp;&nbsp;Please upgrade your Python as Python 2.7 won't be maintained after that date.  
&nbsp;&nbsp;&nbsp;&nbsp;A future version of pip will drop support for Python 2.7.

## Files required in the execution folder:

* &ast;.py
* Ra.jpg
* croppedmoon.png
* A4chart0-180_P.pdf
* A4chart180-360_P.pdf

&nbsp;&nbsp;&nbsp;&nbsp;If upgrading from an older version of Skyfield to 1.31 or higher, these files may be deleted:  
&nbsp;&nbsp;&nbsp;&nbsp;**deltat.data** and **deltat.preds**

### INSTALLATION GUIDELINES on Windows 10:

&nbsp;&nbsp;&nbsp;&nbsp;Tested on Windows 10 Pro, Version 20H2 with an AMD Ryzen 7 3700X 8-Core Processor  

&nbsp;&nbsp;&nbsp;&nbsp;Install Python 2.7 (do not add python.exe to path)  
&nbsp;&nbsp;&nbsp;&nbsp;Install MiKTeX 20.11 from https://miktex.org/  
&nbsp;&nbsp;&nbsp;&nbsp;When MiKTeX first runs it will require installation of additional packages.  
&nbsp;&nbsp;&nbsp;&nbsp;Run Command Prompt as Administrator; go to your Python Scripts folder and execute, e.g.:

&nbsp;&nbsp;&nbsp;&nbsp;**cd C:\\Python27\\Scripts**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install wheel**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip uninstall pyephem**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install ephem**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install skyfield**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install pandas**  

&nbsp;&nbsp;&nbsp;&nbsp;NOTE: if Python 3 is already installed, you need to be in the Scripts folder - otherwise the Py3 version of pip will execute.  
&nbsp;&nbsp;&nbsp;&nbsp;NOTE: you may get the following error:  
&nbsp;&nbsp;&nbsp;&nbsp;**error: Microsoft Visual C++ 9.0 is required. Get it from http://aka.ms/vcpython27**

&nbsp;&nbsp;&nbsp;&nbsp;On Windows 10 Version 2004 and 20H2 there is currently a bug that may cause the following error:  
&nbsp;&nbsp;&nbsp;&nbsp;**RuntimeError: The current Numpy installation fails to pass a sanity check due to a bug in the windows runtime.**  
&nbsp;&nbsp;&nbsp;&nbsp;The final resolution is expected end of January 2021, however the following workaround will bypass the problem:  
&nbsp;&nbsp;&nbsp;&nbsp;**pip uninstall numpy**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install numpy==1.19.3**  

&nbsp;&nbsp;&nbsp;&nbsp;NOTE: if Python 3 is already installed, you need to be in the Scripts folder - otherwise the Py3 version of pip will execute.

&nbsp;&nbsp;&nbsp;&nbsp;Put the SkyAalmanac files in a new folder, run Command Prompt in that folder and start with:  
&nbsp;&nbsp;&nbsp;&nbsp;**python.exe skyalmanac.py**  

&nbsp;&nbsp;&nbsp;&nbsp;However, if Python 3 is also installed, start with:  
&nbsp;&nbsp;&nbsp;&nbsp;**py -2 skyalmanac.py**  


### INSTALLATION GUIDELINES on Ubuntu 18.04:

&nbsp;&nbsp;&nbsp;&nbsp;Ubuntu 18 and earlier come with Python 2 preinstalled,  
&nbsp;&nbsp;&nbsp;&nbsp;however pip may need to be installed:  
&nbsp;&nbsp;&nbsp;&nbsp;**sudo apt install python-pip**  
&nbsp;&nbsp;&nbsp;&nbsp;Note: Ubuntu 20.04 comes with Python 3 preinstalled, which is preferable to Python 2.

&nbsp;&nbsp;&nbsp;&nbsp;Install the following TeX Live package:  
&nbsp;&nbsp;&nbsp;&nbsp;**sudo apt install texlive-latex-extra**

&nbsp;&nbsp;&nbsp;&nbsp;Install the required astronomical libraries etc.:  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install wheel**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip uninstall pyephem**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install ephem**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install skyfield**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install pandas**  

&nbsp;&nbsp;&nbsp;&nbsp;Put the SkyAlmanac files in a folder and start with:  
&nbsp;&nbsp;&nbsp;&nbsp;**python skyalmanac.py**  


### INSTALLATION GUIDELINES on MAC:

&nbsp;&nbsp;&nbsp;&nbsp;Every Mac comes with python preinstalled.  
&nbsp;&nbsp;&nbsp;&nbsp;(Please choose the Python 3.7 version of SkyAlmanac if Python 3.* is installed.)  
&nbsp;&nbsp;&nbsp;&nbsp;You need to install the PyEphem and Skyfield libraries to use SkyAlmanac.  
&nbsp;&nbsp;&nbsp;&nbsp;Type the following commands at the commandline (terminal app):

&nbsp;&nbsp;&nbsp;&nbsp;**sudo easy_install pip**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip uninstall pyephem**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install ephem**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install skyfield**  
&nbsp;&nbsp;&nbsp;&nbsp;**pip install pandas**  

&nbsp;&nbsp;&nbsp;&nbsp;If this command fails, your Mac asks you if you would like to install the header files.  
&nbsp;&nbsp;&nbsp;&nbsp;Do so - you do not need to install the full IDE - and try again.

&nbsp;&nbsp;&nbsp;&nbsp;Install TeX/LaTeX from http://www.tug.org/mactex/

&nbsp;&nbsp;&nbsp;&nbsp;Now you are almost ready. Put the SkyAlmanac files in any directory and start with:  
&nbsp;&nbsp;&nbsp;&nbsp;**python skyalmanac**  
&nbsp;&nbsp;&nbsp;&nbsp;or  
&nbsp;&nbsp;&nbsp;&nbsp;**./skyalmanac**
