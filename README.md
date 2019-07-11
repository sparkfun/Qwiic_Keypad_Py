Qwiic_Keypad_Py
==============

<p align="center">
   <img src="https://cdn.sparkfun.com/assets/custom_pages/2/7/2/qwiic-logo-registered.jpg"  width=200>  
   <img src="https://www.python.org/static/community_logos/python-logo-master-v3-TM.png"  width=240>   
</p>
<p align="center">
	<a href="https://pypi.org/project/sparkfun-qwiic-keypad/" alt="Package">
		<img src="https://img.shields.io/pypi/pyversions/sparkfun_qwiic_keypad.svg" /></a>
	<a href="https://github.com/sparkfun/Qwiic_Keypad_Py/issues" alt="Issues">
		<img src="https://img.shields.io/github/issues/sparkfun/Qwiic_Keypad_Py.svg" /></a>
	<a href="https://qwiic-keypad-py.readthedocs.io/en/latest/?" alt="Documentation">
		<img src="https://readthedocs.org/projects/qwiic-keypad-py/badge/?version=latest&style=flat" /></a>
	<a href="https://github.com/sparkfun/Qwiic_Keypad_Py/blob/master/LICENSE" alt="License">
		<img src="https://img.shields.io/badge/license-MIT-blue.svg" /></a>
	<a href="https://twitter.com/intent/follow?screen_name=sparkfun">
        	<img src="https://img.shields.io/twitter/follow/sparkfun.svg?style=social&logo=twitter"
           	 alt="follow on Twitter"></a>
	
</p>

<img src="https://cdn.sparkfun.com//assets/parts/1/3/7/7/7/15290-SparkFun_Qwiic_Keypad_-_12_Button-01.jpg"  align="right" width=300 alt="SparkFun Qwiic Keypad Breakout">

Python module for the qwiic keypad, which is part of the [SparkFun Qwiic Keypad - 12 Button](https://www.sparkfun.com/products/15290)

This python package is a port of the existing [SparkFun Qwiic Keypad Arduino Library](https://github.com/sparkfun/SparkFun_Qwiic_Keypad_Arduino_Library)

This package can be used in conjunction with the overall [SparkFun qwiic Python Package](https://github.com/sparkfun/Qwiic_Py)

New to qwiic? Take a look at the entire [SparkFun qwiic ecosystem](https://www.sparkfun.com/qwiic).

## Contents

* [Dependencies](#dependencies)
* [Installation](#installation)
* [Documentation](#documentation)
* [Example Use](#example-use)

Dependencies 
---------------
This driver package depends on the qwiic I2C driver: 
[Qwiic_I2C_Py](https://github.com/sparkfun/Qwiic_I2C_Py)

Documentation
-------------
The SparkFun qwiic Keypad module documentation is hosted at [ReadTheDocs](https://qwiic-keypad-py.readthedocs.io/en/latest/?)

Installation
-------------

### PyPi Installation
This repository is hosted on PyPi as the [sparkfun-qwiic-keypad](https://pypi.org/project/sparkfun-qwiic-keypad/) package. On systems that support PyPi installation via pip, this library is installed using the following commands

For all users (note: the user must have sudo privileges):
```sh
sudo pip install sparkfun-qwiic-keypad
```
For the current user:

```sh
pip install sparkfun-qwiic-keypad
```

### Local Installation
To install, make sure the setuptools package is installed on the system.

Direct installation at the command line:
```sh
python setup.py install
```

To build a package for use with pip:
```sh
python setup.py sdist
 ```
A package file is built and placed in a subdirectory called dist. This package file can be installed using pip.
```sh
cd dist
pip install sparkfun_qwiic_keypad-<version>.tar.gz
  
```
Example Use
 ---------------
See the examples directory for more detailed use examples.

```python
import qwiic_keypad
import time
import sys

def runExample():

	print("\nSparkFun qwiic Keypad   Example 1\n")
	myKeypad = qwiic_keypad.QwiicKeypad()

	if myKeypad.isConnected() == False:
		print("The Qwiic Keypad device isn't connected to the system. Please check your connection", \
			file=sys.stderr)
		return

	myKeypad.begin()

	button = 0
	while True:

		# necessary for keypad to pull button from stack to readable register
		myKeypad.updateFIFO()  
		button = myKeypad.getButton()

		if button == -1:
			print("No keypad detected")
			time.sleep(1)

		elif button != 0:

			# Get the character version of this char
			charButton = chr(button)
			if charButton == '#':
				print()
			elif charButton == '*':
				print(" ", end="")
			else: 
				print(charButton, end="")

			# Flush the stdout buffer to give immediate user feedback
			sys.stdout.flush()

		time.sleep(.25)
		# Development in progress
```
<p align="center">
<a href="https://www.sparkfun.com" alt="SparkFun">
<img src="https://cdn.sparkfun.com/assets/custom_pages/3/3/4/dark-logo-red-flame.png" alt="SparkFun - Start Something"></a>
</p>
