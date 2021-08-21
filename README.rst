FakeFiles
============

Generate fake content to populate a file system and take up disk space.

.. warning:: This is a pre-release version. Use at your own risk.

Usage
----------

First, create or select a configuration file with the desired plan to generate.
You may run multiple configuration files across the same target folder, so long
as there are no conflicting patterns or paths. See documentation on
configuration files for additional details on building a configuration file.

You can install the script by following the below steps:

1. Ensure you have Python 3.6 or later installed
2. Download the code from this respository
3. From within the respository run ``pip install -r requirements.txt`` to
   install the needed libraries.
4. Then run ``python fakefiles.py --help`` and you should see a help message
   if the tool is ready for use, or an error if additional steps are required.

FakeFiles Help Text
+++++++++++++++++++++++++

.. code-block:: text

  $ python fakefiles.py --help
  usage: fakefiles.py [-h] [-n] target config

  positional arguments:
    target         Path to write the generated files and folders.
    config         Configuration file to run

  optional arguments:
    -h, --help     show this help message and exit
    -n, --dry-run  Dry run, do everything but make files and folders.


Example Invocation
++++++++++++++++++++

Generate files using the "configs/finance/finance.yml" configuration within the
``fileshare`` directory:

``python fakefiles.py fileshare configs/finance/finance.yaml``


TODO
------

* Config for sales department with contracts


Configuration files
-------------------------

The real logic lies within the configuration files, which permit the
specification of folder structure and filename patterns for the script to
generate. Additionally, it allows for the specification of template files so
that you can control the file content that is placed in the destination.

Variables are available within the configuration files to permit the dynamic
generation of file names and folder paths. You may not specify more than one
variable

The full list of supported variables are defined below and are case sensitive:

:YEAR: A year value, between and including the ``min_year`` and ``max_year``
  specified within the ``_meta`` key of the configuration file.
:MONTH: A month value between 1 and 12.
:INCREMENT_NUMBER: An incrementing number for each time the file is created.
  The possible range of incrementing numbers is specified within the
  ``how_many_range`` key, and requires 2 values in the array for the minimum
  and maximum number of files to generate.
:RAND_NUM: A pseudo-random 1 digit zero padded number. You can control the range with ``min_int`` and ``max_int``.

Feature Requests
-------------------

If you are looking to contribute, consider adding support for one or more of
these desired features:

* Expand out the supported patterns to support additional attributes, such as
  timestamps, random words, random names, random codenames.
* Allow multiple patterns in a single file or folder name
* Develop functionality to allow for timestomping the files after copy.
  Possibly by incorporating https://github.com/Delgan/win32-setctime


Future patterns to develop
+++++++++++++++++++++++++++


:RAND_WORDS: Multiple pseudo-random word with alpha characters only.
  The minimum and maximum character count must be specified with the
  ``word_size`` key and the ``num_words`` must specify the number of words.
  Further you may use the ``delimiter`` to set the delimiter between words.
:YEARMONTH: The current year and month in the format ``YYYY-mm``
:MONTH_LONG: The full english month name. Ie. January, February, etc.
:MONTH_SHORT: The shortened english month name. Ie. JAN, FEB, etc.
:DAY: A day value between 1 and 28.
:YMD: Generates a valid random year-month-day between and including the entirity of ``min_year`` and ``max_year``
:TIMESTAMP: Generates a valid timestamp string with the format ``YYYY-mm-dd_hh-mm-ss`` to comply with filename allowed characters.