---
layout: post
title: 'Python: Convert Tuple List to Dictionary'
permalink: howto-convert-tuplelist-dictionary/
description: How to Convert Tuple List to Dictionary in Python...
category: coding
---

Using [Python Docopt](https://github.com/docopt/docopt) (for beautiful command-line interfaces) I recently had the problem of converting a list of tuples into a dictionary. In this post I'd like to document [the solution](https://gist.github.com/jbspeakr/c7c4fcb9ee143cf7e9eb) I came up with...

<div class="wide">
```
"""
usage:
    mytool [options]

options:
    --foo-bar=PARAM1,PARAM2,... params to do stuff with
        [default: key1.value1,key1.value2,key2.value2]
"""

from docopt import docopt
from collections import defaultdict


def run():
    params = [tuple(param.strip().split('.')) for param in arguments["--foo-bar"].split(",")]
    params = convert_tuple_list_to_dictionary(ignored_resources)

def convert_tuple_list_to_dictionary(list_of_tuple):
    dictionary = defaultdict(list)
    for k, v in list_of_tuple:
        dictionary[k].append(v)

    return dictionary

if __name__ == "__main__":
    run()
```
</div>

This code is able to convert the parameter value string `key1.value1,key1.value2,key2.value2` into the following dictionary:

```
{
	'key1': ['value1', 'value2'],
    'key2': ['value2']
}
```

If you know a leaner solution to solve this problem, please write a comment!
