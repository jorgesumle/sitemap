Sitemap
=======

[![Build Status](https://img.shields.io/github/workflow/status/pelican-plugins/sitemap/build)](https://github.com/pelican-plugins/sitemap/actions) [![PyPI Version](https://img.shields.io/pypi/v/pelican-sitemap)](https://pypi.org/project/pelican-sitemap/)

This [Pelican][] plugin generates a site map in plain-text or XML format. You can use the `SITEMAP` variable in your settings file to configure the behavior of the plugin.

Installation
------------

This plugin can be installed via:

    python -m pip install pelican-sitemap

Usage
-----

The `SITEMAP` setting must be a Python dictionary and can contain these keys:

* `format`, which sets the output format of the plugin (`xml` or `txt`)

* `priorities`, which is a dictionary with three keys:

    - `articles`, the priority for the URLs of the articles and their translations

    - `pages`, the priority for the URLs of the static pages

    - `indexes`, the priority for the URLs of the index pages, such as tags, author pages, categories indexes, archives, etc.

    All the values of this dictionary must be decimal numbers between `0` and `1`.

* `changefreqs`, which is a dictionary with three items:

    - `articles`, the update frequency of the articles

    - `pages`, the update frequency of the pages

    - `indexes`, the update frequency of the index pages

    Valid frequency values are `always`, `hourly`, `daily`, `weekly`, `monthly`, `yearly` and `never`.

You can exclude URLs from being included in the site map via regular expressions. For example, to exclude all URLs containing `tag/` or `category/` you can use the following `SITEMAP` setting.

```python
SITEMAP = {
    "exclude": ["tag/", "category/"]
}
```

If a key is missing or a value is incorrect, it will be replaced with the default value.

You can also exclude an individual URL by adding metadata to it, setting `private` to `True`.

The sitemap is saved in: `<output_path>/sitemap.<format>`

> **Note:** `priorities` and `changefreqs` are information for search engines and are only used in the XML site maps. For more information, see: <https://www.sitemaps.org/protocol.html#xmlTagDefinitions>

**Example**

Here is an example configuration (it is also the default settings):

```python
# Where your plug-ins reside
PLUGIN_PATHS = ["/where/you/cloned/it/pelican-plugins/",]
PLUGINS=["sitemap",]

SITEMAP = {
    "format": "xml",
    "priorities": {
        "articles": 0.5,
        "indexes": 0.5,
        "pages": 0.5
    },
    "changefreqs": {
        "articles": "monthly",
        "indexes": "daily",
        "pages": "monthly"
    }
}
```

Contributing
------------

Contributions are welcome and much appreciated. Every little bit helps. You can contribute by improving the documentation, adding missing features, and fixing bugs. You can also help out by reviewing and commenting on [existing issues][].

To start contributing to this plugin, review the [Contributing to Pelican][] documentation, beginning with the **Contributing Code** section.

[Pelican]: https://github.com/getpelican/pelican
[existing issues]: https://github.com/pelican-plugins/sitemap/issues
[Contributing to Pelican]: https://docs.getpelican.com/en/latest/contribute.html
