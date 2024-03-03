.. include:: new_major_version.rst

****************
Overview
****************

1. Support for model-to-model conversion.
2. Support for attrs and sqlalchemy (integration with many other libraries is coming).
3. Fully redesigned API helping to follow DRY.
4. Performance improvements of `up to two times <https://adaptix.readthedocs.io/en/latest/benchmarks.html>`_.


Requirements
==================

* python >= 3.6

You can use ``dataclass_factory`` with python 3.6 and ``dataclass`` library installed from pip.

From python 3.7 it has no external dependencies outside of the Python standard library.


Advantages
=============

* No schemas or configuration needed for simple cases. Just create ``Factory`` and call ``load``/``dump`` methods
* Speed. It is up to 10 times faster than ``marshmallow`` and ``dataclasses.asdict``
* Automatic name style conversion (e.g. ``snake_case`` to ``CamelCase``)
* Automatic skipping of "internal use" fields (with leading underscore)
* Enums, typed dicts, tuples and lists are supported from the box
* Unions and Optionals are supported without need to define them in schema
* Generic dataclasses can be automatically parsed as well
* Cyclic-referenced structures (such as linked-lists or trees) also can be converted
* Per-field validators

Example
=============

.. literalinclude:: examples/tldr.py


Supported types
=====================

* numeric types (``int``, ``float``, ``Decimal``, ``complex``, ``Fraction``)
* ``bool``
* ``str``, ``bytearray``, ``bytes``
* ``List`` and common protocols like ``Iterable`` are parsed as ``list``
* ``Tuple``, including something like ``Tuple[int, ...]`` or ``Tuple[int, str, int]``
* ``Dict``
* ``Enum`` is converted using its value
* ``Optional``
* ``Any``, using this type no conversion is done during parsing. But serialization is based on real data type
* ``Union``
* ``Literal`` types, including variant from ``typing_extensions``
* ``TypedDict`` types with checking of ``total``, including variant from ``typing_extensions``
* ``dataclass`` and ``NamedTuple``
* ``Generic`` dataclasses
* Other standard types like ``datetime``, ``Path``, ``UUID`` and ``IPV4Address``
* Custom classes can be parsed automatically using info from their ``__init__`` method. Serialization is done by calling `vars()` function and then processing real data types
* Or you can provide custom parser/serializer
