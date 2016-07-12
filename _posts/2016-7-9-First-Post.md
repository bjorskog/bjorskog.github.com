---
layout: post
title: How to make a python namespace package.
---

Some notes on how to make a namespace package.

In setup.py, you need the following lines:

* `namespace_packages=['NAMESPACE']`
* `name=['NAMESPACE.PACKAGENAME']`
* `packages=['NAMESPACE', 'NAMESPACE.PACKAGENAME']`, or `packages=find_packages('src')`

where find_packages comes from setuptools.

Optionally, depending on the place of your source code:

* `package_dir={'': 'src'}`

To include test:

* `test_suite='NAMESPACE.PACKAGENAME.tests.test_suite'`

In the source code itself, you must have the top folder `PACKAGE/` (again, optionally under `src/`), containing `__init__.py` that has the following line:

* `__import__('pkg_resources').declare_namespace(__name__)`

Another possibility is the following if the above is not availible:

* `import pkgutil`
* `__path__ = pkgutil.extend_path(__path__, __name__)`

And finally all your code under the folder `PACKAGE/PACKAGENAME`.
