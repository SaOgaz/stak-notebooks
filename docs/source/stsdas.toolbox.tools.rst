:orphan:


stsdas.toolbox.tools
====================

General utilities

Notes
-----

**For questions or comments please see** `our github
page <https://github.com/spacetelescope/stak>`__. **We encourage and
appreciate user feedback.**

**Most of these notebooks rely on basic knowledge of the Astropy FITS
I/O module. If you are unfamiliar with this module please see the**
`Astropy FITS I/O user
documentation <http://docs.astropy.org/en/stable/io/fits/>`__ **before
using this documentation**.

Contents:

-  `base2dec-dec2base <#base2dec-dec2base>`__
-  `ddiff <#ddiff>`__
-  `epoch-tepoch <#epoch-tepoch>`__
-  `fparse <#fparse>`__
-  `newredshift <#newredshift>`__
-  `tprecess <#tprecess>`__





base2dec-dec2base
-----------------

**Please review the** `Notes <#notes>`__ **section above before running
any examples in this notebook**

The base2dec and dec2base tasks transform strings to decimal integers,
and decimal integers to other base strings. Python has various built ins
for these conversion. The ``int()`` function can transform any base to
integer, which can then be printed in decimal. For the reverse direction
Python contains built in functionality to transform integers to octal,
hexidecimal, and binary.

-  `oct
   function <https://docs.python.org/3.6/library/functions.html#oct>`__
-  `hex
   function <https://docs.python.org/3.6/library/functions.html#hex>`__

.. code:: ipython3

    # base 16 to integer
    a = int("b1", base=16)
    print(a)
    
    # integer to base 16
    b = hex(177)
    print(b)
    
    # integer to binary
    c = "{0:b}".format(177)
    print(c)


.. parsed-literal::

    177
    0xb1
    10110001




ddiff
-----

**Please review the** `Notes <#notes>`__ **section above before running
any examples in this notebook**

Ddiff is used to print differences between two directory trees. This can
be replicated using
`os.walk <https://docs.python.org/3.6/library/os.html#walk>`__ and a
little bit of `set
maniputaion <https://docs.python.org/3/tutorial/datastructures.html#sets>`__.

.. code:: ipython3

    # Standard Imports
    import os

.. code:: ipython3

    full_filepaths1 = []
    full_filepaths2 = []
    
    # loop through walk iterator, using current directory
    # for this example with the sting "."
    for root, dirs, files in os.walk("."):
        for filestring in files:
            full_filepaths1.append(os.path.join(root,filestring))      
            
    # We will use the same directory for this example, so the set difference should be empty
    for root, dirs, files in os.walk("."):
        for filestring in files:
            full_filepaths2.append(os.path.join(root,filestring))
            
    # Now we turn both filepath lists into sets, and take the difference
    set1 = set(full_filepaths1)
    set2 = set(full_filepaths2)
    print(set1 - set2)


.. parsed-literal::

    set()




epoch-tepoch
------------

**Please review the** `Notes <#notes>`__ **section above before running
any examples in this notebook**

Epoch and tepoch are used to convert time formats. This functionality is
heavily covered by the `Astropy Time
module <http://docs.astropy.org/en/stable/time/>`__ and the
documentation is well developed. Alternatively, there is a native Python
`datetime module <https://docs.python.org/3/library/datetime.html>`__.
Please see the linked documentation for more thorough details.

Below we will show an example of how to combine the Astropy ``Time``
module with the ``Table`` module. This example uses ``Table`` mixin
columns. Before expanding on this example for your own use, please read
over the `mixin column
documentation <http://docs.astropy.org/en/stable/table/mixin_columns.html>`__.

.. code:: ipython3

    # Astronomy Specific Imports
    from astropy.time import Time
    from astropy.table import Table

.. code:: ipython3

    # Here we setup a simple Astropy Table, and attach some dates
    # The Time wrapper around the epoch variable is for the Astropy
    # Time object.
    objname = ['obj1', 'obj2']
    epoch = Time(['2010-1-2', '2010-1-3'])
    tab = Table([objname, epoch], names=['name', 'epoch'])
    
    # And here in a single line we can display this object in mjd
    mjd = tab['epoch'].mjd
    print("mjd: {}\n".format(mjd))
    
    # To make this change permanent we can re-assign the whole column
    tab['epoch'] = mjd
    
    # Print updated Table column
    print(tab['epoch'])


.. parsed-literal::

    mjd: [ 55198.  55199.]
    
     epoch 
    -------
    55198.0
    55199.0




fparse
------

**Please review the** `Notes <#notes>`__ **section above before running
any examples in this notebook**

Fparse is used to parse file specifications and leave results in
parameters. This can be done using the ``os`` `path.split
function <https://docs.python.org/3.6/library/os.path.html#os.path.split>`__
and the built in `String split
method <https://docs.python.org/3.6/library/stdtypes.html#str.split>`__.

.. code:: ipython3

    # Standard Imports
    import os

.. code:: ipython3

    # code goes here
    my_filepath = "/home/user/snowball/stars.txt"
    directory, filename = os.path.split(my_filepath)
    print(directory)
    print(filename)
    print(filename.split("."))


.. parsed-literal::

    /home/user/snowball
    stars.txt
    ['stars', 'txt']




newredshift
-----------

**Please review the** `Notes <#notes>`__ **section above before running
any examples in this notebook**

.. figure:: static/150pxblueconstuc.png
   :alt: Work in progress



tprecess
--------

**Please review the** `Notes <#notes>`__ **section above before running
any examples in this notebook**

Tprecess is used to precess images, tables, or lists of coordinates.
This capability is part of the `Astropy coordinates
package <http://docs.astropy.org/en/stable/coordinates/#transformation>`__.
Please explore the doumentation for more instruction. In particular, see
the second example in this section for a transformation example. For a
larger overview of how coordinates are handeled in Astropy please start
at the `top of this documentation
page <http://docs.astropy.org/en/stable/coordinates/#>`__.





Not Replacing
-------------

-  mkapropos - Make the apropos database. Deprecated.
-  uniqfile - Give a file a unique name prior to archiving. Deprecated.
-  uniqid - Create a unique character string identifier. Deprecated.
-  uniqname - Create a unique file name for archiving. Deprecated.
-  uniqtab - Give all the files in an STSDAS table unique names.
   Deprecated.
