boostinator
===========

Make Boost C++ libraries available for building Python C/C++ extensions.

NOTE: currently header only supported; shared libraries may be availble in the future.

Installation
============

Easy pip install:

.. code-block::

   pip install boostinator

This should install all platform-independent boost headers (currently from boost 1.74.0).

Usage
=====

Exposes a single function to get the include directory:

.. code-block:: python

   from boostinator import get_include_dir

   # returns a pathlib.Path object
   import pathlib
   assert isinstance(get_include_dir(), pathlib.Path)

We can now use the libraries when compiling extensions, e.g.:

.. code-block::

   from boostinator import get_include_dir

   setup(
   ...
       ext_modules=[
           Extension(
               'my.CoolExtension',
               sources=['myCythonFile.pyx', 'myCppFile.cpp'],
               include_dirs=[str(get_include_dir())], # include boost headers
               language='c++',
           ),
       ],
   )
