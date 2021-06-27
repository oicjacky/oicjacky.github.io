---
layout: post
title: "Command-line arguments"
subtitle: 
tags: [python note]
comments: true
published: true
---


### [sys.argv[1] meaning in script](https://stackoverflow.com/questions/4117530/sys-argv1-meaning-in-script)

For every invocation of Python, `sys.argv` is automatically a list of strings representing the arguments (as separated by spaces) on the command-line. 

Source code: `python-code/command_line_arg/sys_argv.py`

```python
import sys

print(f"Number of arguments = {len(sys.argv)}, Argument List = {sys.argv}")
```
when you execute:
```bash
> python sys_argv.py foo bar four
Number of arguments = 4, Argument List = ['sys_argv.py', 'foo', 'bar', 'fourth']
```
-----
### See also: [`argparse`](https://docs.python.org/3/howto/argparse.html)

Source code: `python-code/command_line_arg/start_commandLine_args.py`

```python
import argparse
import os
import datetime
parser = argparse.ArgumentParser()
```

The following use `.add_argument()` to specify which command-line options will be accepted.

First, add "Positional args" in your script. Try add some "Optional args" to see what happens.

#### 1. Positional args

After the `parser` call method as `parser.parse_args()`, the returned object will have `.echo` and `.square` attributes.

Note: add some help information for usage.

```python
parser.add_argument('echo',
                    help = 'echo the string you use here')
parser.add_argument('square',
                    help = "display a sqyare of a given number",
                    type = float)
```

#### 2. Optional args

If add `-pid` with allowed type `bool`, it will print the process id:
```python
parser.add_argument('-pid', '--process_id', 
                    type = bool,
                    help = 'show process id of the program')
```

`action = 'store_true'` gives 'True' value when `-v` is called:
```python
parser.add_argument('-v', '--verbose', 
                    help = 'increase output verbosity of square',
                    action = 'store_true')
```

`choices = [0, 1, 2]` will check the input values as we expect:
```python
parser.add_argument('-d', '--date',
                    help = 'show date of the day minus a number what you type in',
                    type = int,
                    default = 0,  # for if statements in the following code
                    choices = [0, 1, 2])
```

`action = 'count'` will count number of 'e' in the args, and start from `default` value:
```python
parser.add_argument('-e', '--echooo',
                    help = 'give more echo of positional arg "echo"',
                    default = 0,
                    action = 'count')
```

**Conflicting options**
```python
group = parser.add_mutually_exclusive_group()
group.add_argument("-n", "--noise", action="store_true")
group.add_argument("-q", "--quiet", action="store_true")
```

Finally, the `__main__` part of the script as:
```python
if __name__ == "__main__":
    args = parser.parse_args()
    print('Parse command line arguments: ', args, type(args))

    print(f"First positional args: 'echo' is {args.echo}")


    if args.process_id:
        print(f"[PROCESS ID] is {os.getpid()}")


    if args.verbose:
        print(f"[verbosity turned on] Second positional args: the square of {args.square} is {args.square**2}")
    else:
        print(f"Second positional args: 'square' is {args.square**2}")


    if args.date:
        print(f"The date minus a number what you type in: {args.date}, is {datetime.datetime.now() - datetime.timedelta(days=args.date)}")


    if args.echooo > 1:
        print(f"Give you more echo {args.echo*args.echooo}")


    if args.noise:
        print("Make some noise ~~~ "*3)
    elif args.quiet:
        print("\n\nAll done in silent.")
```

----
Type `-h` to see how arguments work in the script:
```bash
> python start_commandLine_args.py -h
usage: start_commandLine_args.py [-h] [-pid PROCESS_ID] [-v] [-d {0,1,2}] [-e]
                                 [-n | -q]
                                 echo square

positional arguments:
  echo                  echo the string you use here
  square                display a sqyare of a given number

optional arguments:
  -h, --help            show this help message and exit
  -pid PROCESS_ID, --process_id PROCESS_ID
                        show process id of the program
  -v, --verbose         increase output verbosity of square
  -d {0,1,2}, --date {0,1,2}
                        show date of the day minus a number what you type in
  -e, --echooo          give more echo of positional arg "echo"
  -n, --noise
  -q, --quiet
```

One simple exmaple is:
```bash
> python command_line_arg\start_commandLine_args.py Hello 3
Parse command line arguments:  Namespace(date=0, echo='Hello', echooo=0, noise=False, process_id=None, quiet=False, square=3.0, verbose=False) <class 'argparse.Namespace'>
First positional args: 'echo' is Hello
Second positional args: 'square' is 9.0
```