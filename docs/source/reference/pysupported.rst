.. _pysupported:

=========================
Supported Python features
=========================

Apart from the :ref:`pysupported-language` part below, which applies to both
:term:`object mode` and :term:`nopython mode`, this page only lists the
features supported in :term:`nopython mode`.

.. _pysupported-language:

Language
========

Constructs
----------

Numba strives to support as much of the Python language as possible, but
some language features are not available inside Numba-compiled functions:

* Function definition
* Class definition
* Exception handling (``try .. except``, ``try .. finally``)
* Context management (the ``with`` statement)
* Comprehensions (either list, dict, set or generator comprehensions)
* Generator delegation (``yield from``)

The ``raise`` statement is supported in several forms:

* ``raise`` (to re-raise the current exception)
* ``raise SomeException``
* ``raise SomeException(<arguments>)``: in :term:`nopython mode`, constructor
  arguments must be :term:`compile-time constants <compile-time constant>`

Similarly, the ``assert`` statement is supported with or without an error
message.

Function calls
--------------

Numba supports function calls using positional and named arguments, as well
as arguments with default values and ``*args``.  Explicit ``**kwargs`` are
not supported.

Generators
----------

Numba supports generator functions and is able to compile them in
:term:`object mode` and :term:`nopython mode`.  The returned generator
can be used both from Numba-compiled code and from regular Python code.

Coroutine features of generators are not supported (i.e. the
:meth:`generator.send`, :meth:`generator.throw`, :meth:`generator.close`
methods).


Built-in types
==============

int, bool
---------

Arithmetic operations as well as truth values are supported.

The following attributes and methods are supported:

* ``.conjugate()``
* ``.real``
* ``.imag``

float, complex
--------------

Arithmetic operations as well as truth values are supported.

The following attributes and methods are supported:

* ``.conjugate()``
* ``.real``
* ``.imag``

tuple
-----

Tuple construction and unpacking is supported, as well as the following
operations:

* comparison between tuples
* iteration over homogenous tuples

None
----

The None value is supported for identity testing (when using an
:class:`~numba.optional` type).

bytes, bytearray, memoryview
----------------------------

The :class:`bytearray` type and, on Python 3, the :class:`bytes` type
support indexing, iteration and retrieving the len().

The :class:`memoryview` type supports indexing, slicing, iteration,
retrieving the len(), and also the following attributes:

* :attr:`~memoryview.contiguous`
* :attr:`~memoryview.c_contiguous`
* :attr:`~memoryview.f_contiguous`
* :attr:`~memoryview.itemsize`
* :attr:`~memoryview.nbytes`
* :attr:`~memoryview.ndim`
* :attr:`~memoryview.readonly`
* :attr:`~memoryview.shape`
* :attr:`~memoryview.strides`


Built-in functions
==================

The following built-in functions are supported:

* :func:`abs`
* :class:`bool`
* :class:`complex`
* :func:`enumerate`
* :class:`float`
* :class:`int`: only the one-argument form
* :func:`len`
* :func:`min`: only the multiple-argument form
* :func:`max`: only the multiple-argument form
* :func:`print`: only numbers and strings; no ``file`` or ``sep`` argument
* :class:`range`: semantics are similar to those of Python 3 even in Python 2:
  a range object is returned instead of an array of values.
* :func:`round`
* :func:`zip`


Standard library modules
========================

``array``
---------

Limited support for the :class:`array.array` type is provided through
the buffer protocol.  Indexing, iteration and taking the len() is supported.
All type codes are supported except for ``"u"``.

``cmath``
---------

The following functions from the :mod:`cmath` module are supported:

* :func:`cmath.acos`
* :func:`cmath.acosh`
* :func:`cmath.asin`
* :func:`cmath.asinh`
* :func:`cmath.atan`
* :func:`cmath.atanh`
* :func:`cmath.cos`
* :func:`cmath.cosh`
* :func:`cmath.exp`
* :func:`cmath.isfinite`
* :func:`cmath.isinf`
* :func:`cmath.isnan`
* :func:`cmath.log`
* :func:`cmath.log10`
* :func:`cmath.phase`
* :func:`cmath.polar`
* :func:`cmath.rect`
* :func:`cmath.sin`
* :func:`cmath.sinh`
* :func:`cmath.sqrt`
* :func:`cmath.tan`
* :func:`cmath.tanh`

``ctypes``
----------

Numba is able to call ctypes-declared functions with the following argument
and return types:

* :class:`ctypes.c_int8`
* :class:`ctypes.c_int16`
* :class:`ctypes.c_int32`
* :class:`ctypes.c_int64`
* :class:`ctypes.c_uint8`
* :class:`ctypes.c_uint16`
* :class:`ctypes.c_uint32`
* :class:`ctypes.c_uint64`
* :class:`ctypes.c_float`
* :class:`ctypes.c_double`
* :class:`ctypes.c_void_p`

``math``
--------

The following functions from the :mod:`math` module are supported:

* :func:`math.acos`
* :func:`math.acosh`
* :func:`math.asin`
* :func:`math.asinh`
* :func:`math.atan`
* :func:`math.atan2`
* :func:`math.atanh`
* :func:`math.ceil`
* :func:`math.copysign`
* :func:`math.cos`
* :func:`math.cosh`
* :func:`math.degrees`
* :func:`math.erf`
* :func:`math.erfc`
* :func:`math.exp`
* :func:`math.expm1`
* :func:`math.fabs`
* :func:`math.floor`
* :func:`math.frexp`
* :func:`math.gamma`
* :func:`math.hypot`
* :func:`math.isfinite`
* :func:`math.isinf`
* :func:`math.isnan`
* :func:`math.ldexp`
* :func:`math.lgamma`
* :func:`math.log`
* :func:`math.log10`
* :func:`math.log1p`
* :func:`math.pow`
* :func:`math.radians`
* :func:`math.sin`
* :func:`math.sinh`
* :func:`math.sqrt`
* :func:`math.tan`
* :func:`math.tanh`
* :func:`math.trunc`

``operator``
------------

The following functions from the :mod:`operator` module are supported:

* :func:`operator.add`
* :func:`operator.and_`
* :func:`operator.div` (Python 2 only)
* :func:`operator.eq`
* :func:`operator.floordiv`
* :func:`operator.ge`
* :func:`operator.gt`
* :func:`operator.iadd`
* :func:`operator.iand`
* :func:`operator.idiv` (Python 2 only)
* :func:`operator.ifloordiv`
* :func:`operator.ilshift`
* :func:`operator.imod`
* :func:`operator.imul`
* :func:`operator.invert`
* :func:`operator.ior`
* :func:`operator.ipow`
* :func:`operator.irshift`
* :func:`operator.isub`
* :func:`operator.itruediv`
* :func:`operator.ixor`
* :func:`operator.le`
* :func:`operator.lshift`
* :func:`operator.lt`
* :func:`operator.mod`
* :func:`operator.mul`
* :func:`operator.ne`
* :func:`operator.neg`
* :func:`operator.not_`
* :func:`operator.or_`
* :func:`operator.pos`
* :func:`operator.pow`
* :func:`operator.rshift`
* :func:`operator.sub`
* :func:`operator.truediv`
* :func:`operator.xor`

.. _pysupported-random:

``random``
----------

Numba supports top-level functions from the :mod:`random` module, but does
not allow you to create individual Random instances.  A Mersenne-Twister
generator is used, with a dedicated internal state.  It is initialized at
startup with entropy drawn from the operating system.

* :func:`random.betavariate`
* :func:`random.expovariate`
* :func:`random.gammavariate`
* :func:`random.gauss`
* :func:`random.getrandbits`: number of bits must not be greater than 64
* :func:`random.lognormvariate`
* :func:`random.normalvariate`
* :func:`random.paretovariate`
* :func:`random.randint`
* :func:`random.random`
* :func:`random.randrange`
* :func:`random.seed`: with an integer argument only
* :func:`random.shuffle`: the sequence argument must be a one-dimension
  Numpy array or buffer-providing object (such as a :class:`bytearray`
  or :class:`array.array`); the second (optional) argument is not supported
* :func:`random.uniform`
* :func:`random.triangular`
* :func:`random.vonmisesvariate`
* :func:`random.weibullvariate`

.. note::
   Calling :func:`random.seed` from non-Numba code (or from :term:`object mode`
   code) will seed the Python random generator, not the Numba random generator.

.. note::
   The generator is not thread-safe when :ref:`releasing the GIL <jit-nogil>`.

   Also, under Unix, if creating a child process using :func:`os.fork` or the
   :mod:`multiprocessing` module, the child's random generator will inherit
   the parent's state and will therefore produce the same sequence of
   numbers (except when using the "forkserver" start method under Python 3.4
   and later).

.. seealso::
   Numba also supports most additional distributions from the :ref:`Numpy
   random module <numpy-random>`.


Third-party modules
===================

.. I put this here as there's only one module (apart from Numpy), otherwise
   it should be a separate page.

``cffi``
--------

Similarly to ctypes, Numba is able to call into `cffi`_-declared external
functions, using the following C types:

* :c:type:`char`
* :c:type:`short`
* :c:type:`int`
* :c:type:`long`
* :c:type:`long long`
* :c:type:`unsigned char`
* :c:type:`unsigned short`
* :c:type:`unsigned int`
* :c:type:`unsigned long`
* :c:type:`unsigned long long`
* :c:type:`int8_t`
* :c:type:`uint8_t`
* :c:type:`int16_t`
* :c:type:`uint16_t`
* :c:type:`int32_t`
* :c:type:`uint32_t`
* :c:type:`int64_t`
* :c:type:`uint64_t`
* :c:type:`float`
* :c:type:`double`
* :c:type:`char *`
* :c:type:`void *`
* :c:type:`uint8_t *`
* :c:type:`ssize_t`
* :c:type:`size_t`
* :c:type:`void`

.. _cffi: https://cffi.readthedocs.org/
