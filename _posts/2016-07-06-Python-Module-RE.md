---
layout:     post
title:      " Python Module RE"
subtitle:   " \" RE for Regular Expression! \""
date:       2016-07-01
author:     "Ethan"
header-img: "img/inPost/PythonModuleRE.jpg"
tags:
    - Python
---

## RE

	>>> str1 = ' ShenZhen University '
	
	>>> str1.find('University')
	10
	>>> str1.find('11')
	-1
	>>> help(str1.find)
	find(...)
    S.find(sub [,start [,end]]) -> int
    
    Return the lowest index in S where substring sub is found,
    such that sub is contained within S[start:end].  Optional
    arguments start and end are interpreted as in slice notation.  
   
   
    >>> str1.startswith('Zhen')
	False
	>>> str1.startswith(' Shen')
	True
	>>> import re
	>>> pa = re.compile(r'University')
	
	
	>>> type(pa)
	<type '_sre.SRE_Pattern'>
	>>> dir(pa)
	['__class__', '__copy__', '__deepcopy__', '__delattr__', '__doc__', '__format__', '__getattribute__', '__hash__', '__init__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'findall', 'finditer', 'flags', 'groupindex', 'groups', 'match', 'pattern', 'scanner', 'search', 'split', 'sub', 'subn']
	
	
	>>> help(pa.match) 
	match(...)
    match(string[, pos[, endpos]]) --> match object or None.
    Matches zero or more characters at the beginning of the string
	(END)
	
	
	>>> pa = re.compile('University')
	>>> pa.match(str1)
	>>> pa = re.compile(' Shen')
	>>> pa.match(str1)
	<_sre.SRE_Match object at 0x107f13f38>
	
	
	>>> ma = pa.match(str1)
	>>> ma.group()
	' Shen'
	>>> dir(ma)
	['__class__', '__copy__', '__deepcopy__', '__delattr__', '__doc__', '__format__', '__getattribute__', '__hash__', '__init__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'end', 'endpos', 'expand', 'group', 'groupdict', 'groups', 'lastgroup', 'lastindex', 'pos', 're', 'regs', 'span', 'start', 'string']
		
	>>> pa = re.compile(' shen', re.I)
	>>> ma = pa.match(str1)
	>>> ma.group()
	' Shen'
	
	
	>>> ma = re.match(r'hello', 'hello SZU, blah blah')
	>>> ma.group()
	'hello'
	>>> ma.groups()
	()
	>>> ma = re.match(r'(hello)', 'hello SZU, blah blah')
	>>> ma.group()
	'hello'
	>>> ma.groups()
	('hello',)		 

	>>> help(re.match)	
	match(pattern, string, flags=0)
	    Try to apply the pattern at the start of the string, returning
	    a match object, or None if no match was found.
	(END)





	# match a Python variable(start with a '_' or letter)
	>>> ma = re.match(r'[_a-zA-Z]+[_\w]*', '_str1')
	>>> ma
	<_sre.SRE_Match object at 0x107e1eb28>
	>>> ma.group()
	'_str1'
	>>> ma = re.match(r'[_a-zA-Z]+[_\w]*', '123_wer')
	>>> ma
	>>>


### re.search an re.findall

	# re.search and re.findall
	>>> str2 = 'SZU University course = 999'
	>>> str2.find('999')
	24
	>>> 
	>>> info = re.search(r'\d+', str2)
	>>> info.group()
	'999'
	>>> str3 = 'c++ = 100, java = 90, python = 78'
	>>> info = re.search(r'\d+', str3)
	>>> info.group()
	'100'
	>>> info = re.findall(r'\d+', str3)
	>>> type(info)
	<type 'list'>
	>>> info
	['100', '90', '78']
	>>> sum([int(x) for x in info])
	268
	>>> 
	

### re.sub and re.split
	
	# re.sub and re.split
	>>> def add1(match):
	...     val = match.group()
	...     num = int(val)+1
	...     return str(num)
	... 
	>>> str3 = 'SZ University course = 999'
	>>> re.sub(r'\d+', add1, str3)
	'SZ University course = 1000'
	
	>>> help(re.sub)
		sub(pattern, repl, string, count=0, flags=0)
	    Return the string obtained by replacing the leftmost
	    non-overlapping occurrences of the pattern in string by the
	    replacement repl.  repl can be either a string or a callable;
	    if a string, backslash escapes in it are processed.  If it is
	    a callable, it's passed the match object and must return
	    a replacement string to be used.
	(END)
	
	>>> str4 = 'progLanguage:C C++ Python Java Php'
	>>> re.split(r':|', str4)
	['progLanguage', 'C C++ Python Java Php']
	>>> re.split(r' :| ', str4)
	['progLanguage:C', 'C++', 'Python', 'Java', 'Php']
	
	>>> help(re.split)
		split(pattern, string, maxsplit=0, flags=0)
	    Split the source string by the occurrences of the pattern,
	    returning a list containing the resulting substrings.
		(END)

