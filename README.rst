Module cffi\_utils.sowrapper
============================

Utility functions to locate and load shared libraries

DESCRIPTION
~~~~~~~~~~~

Recommended usage:

Should only need to use get\_lib\_ffi\_shared() or
get\_lib\_ffi\_resource()

Use get\_lib\_ffi\_shared to load a system-wide shared library with a
known library filename and / or path

Use get\_lib\_ffi\_resource to load a module-specific shared library
where library filename *MAY* be mangled as per PEP3149 and path *MAY*
need to be looked up using pkg\_resources. Internally,
get\_lib\_ffi\_resource() calls get\_lib\_ffi\_shared()

Both return a tuple: (ffi, lib):

::

    ffi-->FFIExt - should behave like cffi.FFI with some additional
        utility methods
    lib-->SharedLibWrapper instance - use methods on this object to
        call methods in the shared library

CLASSES
~~~~~~~

::

        class SharedLibWrapper(__builtin__.object)
         |  Methods defined here:
         |  
         |  __init__(self, libpath, c_hdr, module_name=None)
         |      libpath-->str: library name; can also be full path
         |      c_hdr-->str: C-style header definitions for functions to wrap
         |      ffi-->FFIExt or cffi.FFI

FUNCTIONS
~~~~~~~~~

::

    get_lib_ffi_resource(module_name, libpath, c_hdr)
        module_name-->str: module name to retrieve resource
        libpath-->str: shared library filename with optional path
        c_hdr-->str: C-style header definitions for functions to wrap
        Returns-->(ffi, lib)
        
        Use this method when you are loading a package-specific shared library
        If you want to load a system-wide shared library, use get_lib_ffi_shared
        instead
        
    get_lib_ffi_shared(libpath, c_hdr)
        libpath-->str: shared library filename with optional path
        c_hdr-->str: C-style header definitions for functions to wrap
        Returns-->(ffi, lib)

Module cffi\_utils.ffi
======================

Extension of cffi.FFI adding a few utility methods

CLASSES
~~~~~~~

::

        class FFIExt(cffi.api.FFI)
         |  FFIExt is an extension of cffi.FFI, adding a few utility methods
         |  
         |  get_cdata(), get_buffer() and get_bytes() all operate on a variable
         |  list of arguments as a convenience.
         |  
         |  Otherwise, get_cdata() and get_buffer() are equivalent to
         |  FFI.from_buffer() and FFI.buffer() respectively
         |  
         |  get_bytes() is identical to get_buffer() except that outputs are
         |  converted to bytes
         |  
         |  get_buffer(self, *args)
         |      all args-->_cffi_backend.CDataOwn
         |      Must be a pointer or an array
         |      Returns-->buffer (if a SINGLE argument was provided)
         |                LIST of buffer (if a args was a tuple or list)
         |  
         |  get_bytes(self, *args)
         |      all args-->_cffi_backend.CDataOwn
         |      Must be a pointer or an array
         |      Returns-->bytes (if a SINGLE argument was provided)
         |                LIST of bytes (if a args was a tuple or list)
         |  
         |  get_cdata(self, *args)
         |      all args-->_cffi_backend.buffer
         |      Returns-->cdata (if a SINGLE argument was provided)
         |                LIST of cdata (if a args was a tuple or list)
         |  
         |  get_extension(self)

Module cffi\_utils.py2to3
=========================

Utility functions for Py2/Py3 compatibility

FUNCTIONS
~~~~~~~~~

::

    chr(x)
        x-->int / byte
        Returns-->byte / str of length 1
            Behaves like PY2 chr() in PY2 or PY3
        
    decode(b, encoding='latin-1')
        b-->bytes
        encoding-->str: encoding to use. Recommended to use default
        Returns-->str: b decoded to str using encoding
            Works in PY2, PY3
        
    encode(s, encoding='latin-1')
        s-->str
        encoding-->str: encoding to use. Recommended to use default
        Returns-->bytes: s encoded to bytes using encoding
            Works in PY2, PY3
        
    fromBytes(b)
        s-->bytes (or str)
        Returns-->str (works in PY2, PY3)
        
    inputFromBytes(func, *args, **kwargs)
        Descriptor that converts all arguments to str
        
    inputToBytes(func, *args, **kwargs)
        Descriptor that converts all arguments to bytes
        
    ord(x)
        x-->int / byte
        Returns-->int
            Behaves like PY2 ord() in PY2 or PY3
        
    outputFromBytes(func, *args, **kwargs)
        Descriptor that converts all return values to str
        
    outputToBytes(func, *args, **kwargs)
        Descriptor that converts all return values to bytes
        
    toBytes(s)
        s-->str (or bytes)
        Returns-->bytes (works in PY2, PY3)

