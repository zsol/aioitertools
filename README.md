aioitertools
============

Implementation of itertools, builtins, and more for AsyncIO and mixed-type iterables.

[![build status](https://github.com/jreese/aioitertools/workflows/Build/badge.svg)](https://github.com/jreese/aioitertools/actions)
[![code coverage](https://img.shields.io/codecov/c/gh/jreese/aioitertools)](https://codecov.io/gh/jreese/aioitertools)
[![version](https://img.shields.io/pypi/v/aioitertools.svg)](https://pypi.org/project/aioitertools)
[![license](https://img.shields.io/pypi/l/aioitertools.svg)](https://github.com/jreese/aioitertools/blob/master/LICENSE)
[![code style](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/ambv/black)


Install
-------

aioitertools requires Python 3.6 or newer.
You can install it from PyPI:

    $ pip install aioitertools


Usage
-----

aioitertools shadows the standard library whenever possible to provide
asynchronous version of the modules and functions you already know.  It's
fully compatible with standard iterators and async iterators alike, giving
you one unified, familiar interface for interacting with iterable objects:

```python
from aioitertools import iter, next, map, zip

something = iter(...)
first_item = await next(something)

async for item in iter(something):
    ...


async def fetch(url):
    response = await aiohttp.request(...)
    return response.json

async for value in map(fetch, MANY_URLS):
    ...


async for a, b in zip(something, something_else):
    ...
```


aioitertools emulates the entire `itertools` module, offering the same
function signatures, but as async generators.  All functions support
standard iterables and async iterables alike, and can take functions or
coroutines:

```python
from aioitertools import chain, islice

async def generator1(...):
    yield ...

async def generator2(...):
    yield ...

async for value in chain(generator1(), generator2()):
    ...

async for value in islice(generator1(), 2, None, 2):
    ...
```


See [builtins.py][] and [itertools.py][] for full documentation
of functions and abilities.


License
-------

aioitertools is copyright [John Reese](https://jreese.sh), and licensed under
the MIT license.  I am providing code in this repository to you under an open
source license.  This is my personal repository; the license you receive to
my code is from me and not from my employer. See the `LICENSE` file for details.


[builtins.py]: https://github.com/jreese/aioitertools/blob/master/aioitertools/builtins.py
[itertools.py]: https://github.com/jreese/aioitertools/blob/master/aioitertools/itertools.py
