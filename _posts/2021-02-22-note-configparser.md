---
layout: post
title: "Configuration file parser"
subtitle: 
tags: [python note]
comments: true
published: true
---

### [Official document](https://docs.python.org/3/library/configparser.html)

Source code: `python-code/configparser/start_configparser.py`

```python
import configparser
```

### Write a 'example.ini' file:
A `.ini` file consists of sections, each section contains keys with values, for example:

```python
config = configparser.ConfigParser()
configuration = {
    'id' : 3,
    'setup' : True,
    'antenna' : ['b827eb8a8f1f', 'b827eb8f8147'],
    'location': 'Taipei_FiveArea',
    'time_range': {
        "gte": "2020-07-01T00:00:00+08",
        "lte": "2020-07-02T00:00:00+08",
    }
}
```


Create a `Default` section consists of `antenna`, `location`, `time_range`:

```python
config["Default"] = configuration

with open('example.ini', 'w') as configfile:
    config.write(configfile)
```


### Read the 'example.ini' file:
```python
config_read = configparser.ConfigParser()
config_read.read('example.ini')
```

Show all section
```python
config_read.sections()
```

Show all options (keys) under the section
```python
config_read.options('Default')
```

`configparser` objects behave as close to actual dictionaries as possible.
```python
print('Default' in config_read)
print('antenna' in config_read['Default'])

{ key: val for key, val in config_read['Default'].items()}
{ section : list(content.items()) for section, content in config_read.items()}
```

### ConfigParser.get(section, option)
```python
config_read.get('Default', 'antenna')
config_read.get('Default', 'location')
config_read.get('Default', 'time_range')
```

Call .get() then transform it such as `int()`
```python
config_read.getint('Default', 'id')
config_read.getfloat('Default', 'id')

config_read.get('Default', 'setup')
config_read.getboolean('Default', 'setup')
```

`fallback` and `vars` in .get()
```python
config_read.get('Default', 'no_exist_section', fallback='fallback_value')
config_read.get('Default', 'no_exist_section', vars={'no_exist_section' : 'this_is_default_config'})
```