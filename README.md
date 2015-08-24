# CommandLineInterface

Writing CLI is **NOT** funny. Especially with all the
argument parsing and shit. This is why this module exists.

## TL;DR

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

from command_line_interface import CommandLineInterface, Argument

cli = CommandLineInterface()
users = ["John Doe", "Dick Head"]

@cli.endpoint(Argument('user', help='username to add'))
def do_user_add(args):
    users.append(args.user)
    print users
    
    @cli.endpoint()
    def do_user_list(args):
        print users
        
        cli.parse()
```

As shown in the example.py file.

You can run it like

```
$ ./exemple.py user add
usage: exemple.py user add [-h] user
exemple.py user add: error: too few arguments
$ ./exemple.py user add "foo bar"
['John Doe', 'Dick Head', 'foo bar']
```

Simple as that :)

## Documentation
Some more documentation is comming, stay tuned.
### Using the module
You have to import the components you need, which for now are :

 * `CommandLineInterface`
 * `Argument`
 * `ExclusiveGroup`

Then instanciate a CommandLineInterface
```python
cli = CommandLineInterface()
```

Then decorate your endpoint function as follows :
```python
@cli.endpoint(
    Argument('argument', help="some help"), # positional arg
    Argument('--user', '-u') # optional argument
)
def do_something(args):
    print args # args is a argparse.Namespace object
```

You can add as many arguments as you wish, the parameters
have to follow the `argparse.add_argument` syntax.

Finally to parse something, just call :
```python
cli.parse()
```
Or, if you don't want to use sys.argv :
```python
cli.parse("some string")
```

Easy, right ?

# Licence
```
Copyright (C) 2015  Thomas Maurice <thomas@maurice.fr>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.
```
