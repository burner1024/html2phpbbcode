[![Build Status](https://travis-ci.org/tdiam/html2phpbbcode.svg?branch=master)](https://travis-ci.org/tdiam/html2phpbbcode)
[![PyPI version](https://badge.fury.io/py/html2phpbbcode.svg)](https://badge.fury.io/py/html2phpbbcode)
[![License](https://img.shields.io/badge/License-BSD%203--Clause-orange.svg)](https://opensource.org/licenses/BSD-3-Clause)

# HTML2PHPBBCode

HTML2PHPBBCode is a Python 3 package that can be used to parse HTML code and convert it to phpBB-compatible BBCode.

### Usage

```python
>>> from html2phpbbcode.parser import HTML2PHPBBCode
>>> parser = HTML2PHPBBCode()
>>> parser.feed('<ul><li>Hello</li><li>World</li></ul>')
'[list][*]Hello[*]World[/list]'
>>> parser.feed('<ol><li>one<li>two</ol>')
'[list=1][*]one[*]two[/list]'
>>> parser.feed('<a href="https://water.org">Water.org</a>')
'[url=https://water.org]Water.org[/url]'
>>> parser.feed('<a href="mailto:info@water.org">Mail Water.org</a>')
'[email=info@water.org]Mail Water.org[/email]'
>>> parser.feed('<strong>Hello <i>World</i>. It&#39;s a wonderful world</strong>')
"[b]Hello [i]World[/i]. It's a wonderful world[/b]"
```

### Acknowledgements

HTML2PHPBBCode is based on the [html2bbcode](https://bitbucket.org/amigo/html2bbcode) package of [Vladimir Korsun](mailto:korsun.vladimir@gmail.com) which is available under the BSD License.

The [regex](https://pypi.org/project/regex/) package by [Matthew Barnett](mailto:regex@mrabarnett.plus.com) is also used, available under the Python Software Foundation License.

The code includes some regular expressions from the [phpBB](https://github.com/phpbb/area51-phpbb3) bulletin board software as well. Minor changes have been made for Python compatibility. phpBB code is available under [GNU GPL v2.0](https://opensource.org/licenses/gpl-2.0.php).

### Differences from html2bbcode

This package differs from html2bbcode in the following:
* The generated BBCode follows the syntax described in phpBB's [BBCode guide](https://www.phpbb.com/community/help/bbcode).
* `<b>`, `<i>`, `<u>`, `<s>`, `<ol>` HTML tags are also supported.
* `<font>`'s `size` attribute handling has been changed so that it maps to reasonable BBCode size values.
* If the `href` attribute of an `<a>` link uses the `mailto:` protocol, then the `[email]` BBCode tag is used.
* If the `href` attribute of an `<a>` link is neither an email nor a valid http/https URL, the link is converted to plain-text in BBCode.
* The parser removes excessive whitespace such as newlines between tags: `<p>Hello</p>\n<p>World</p>` *(TODO: Use the [W3C spec](https://www.w3.org/TR/css-text-3/) rules)*

### Installing

The package is available at [PyPI](https://pypi.org/project/html2phpbbcode/) and can be installed with the following command:

```bash
pip install html2phpbbcode
```

Installing from source is also an option:

```bash
python3 setup.py install
```

### Testing

[pytest](https://pytest.org) is used for testing. Just run `pytest` in the project directory to execute the tests.