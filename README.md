#🅿️SX
---

↪__Forked from,__ https://github.com/michaeljones/packed.

PSX provides [JSX](https://facebook.github.io/jsx/)-style syntax within
Python files. It provides a system for converting:

😎 **Go from this:**

```py
@PSX
def tag(self):
    share = get_share_link()
    return <a href={share}>Share on internet</a>
```

✅ **To this:**

```py
@PSX
def tag(self):
    share = get_share_link()
    return Elem(
        'a',
        {
            'href': share,
        },
        'Share on internet',
    )
```

⚡ Render the appropriate HTML output when called!


#⌚Status
---

This software is in alpha. There is a series of tests which cover the currently
supported syntax. There are no nice error messages if things go wrong. Please
create issues with any syntax that is not handled properly.

**PSX** makes no effort to escape or make safe any content. I would particularly
welcome advice on this aspect.


#🔌Usage
-----

The module can be called from the command line to find files with the **PSX**
syntax and convert them to pure Python. Files using the **PSX** syntax
should use the `.pyx` file extension. The command searches recursively through
the provided directory:

```bash
python -m psx .
```

Will write pure Python `.py` files for all `.pyx` files under the current
directory.


#⌨️Syntax
---

**PSX** supports basic HTML style syntax as well as creating your own custom tags
or components. The term `component` is taken from [React](https://facebook.github.io/react/).
A `component` should have a `render` method which returns `Elem` instances which are created 
from the **PSX** syntax.

For example:

```py
from psx import Component, psx

class ShareLink(Component):

    def render(self):
        return <a href={self.props['link']}>Share on internet</a>

@PSX
def tag(self):
    share = get_share_link()
    return <ShareLink link={share} />
```

The `Component` base class exposes attributes passed in the HTML syntax as
entries in the `props` dictionary in a similar style to React.


#📜Credits
---

PSX uses the [pypeg2](http://fdik.org/pyPEG/) library for the parsing and output of the Python files.

The idea is, of course, inspired by [JSX](https://facebook.github.io/jsx/) from 
[Facebook](https://github.com/facebook).

