---
layout:     post
title:      "Convert the Picture to Ascii"
subtitle:   " \"Just for fun.\""
date:       2016-07-10
author:     "Ethan"
header-img: "img/Hello-Blog.jpg"
tags:
    - Python

---

## Python code

convert a picture to text.

	from PIL import Image
	import argparse
	
	# turn all of the ascii_char to list ['$', '@', ...., '.']
	ascii_char = list("$@B%8&WM#*oahkbdpqwmZO0QLCJUYXzcvunxrjft/\|()1{}[]?-_+~<>i!lI;:,\"^`'. ")
	
	# generate an instance of argument parser 
	parser = argparse.ArgumentParser()
	
	parser.add_argument('file')		# input file
	parser.add_argument('-o', '--output')	# output file
	parser.add_argument('--width', type = int, default = 80) 
	parser.add_argument('--height', type = int, default = 80)
	
	# acquire arguments
	args = parser.parse_args()
	
	
	IMG = args.file
	WIDTH = args.width
	HEIGHT = args.height
	OUTPUT = args.output
	
	
	def get_char(r, b, g, alpha = 256):
		if alpha == 0:
			return ' '
		length = len(ascii_char)
		gray = int(0.2126 * r + 0.7152 * g + 0.0722 * b)
		unit = (256.0 + 1) / length
		return ascii_char[int(gray/unit)]
		
	
	if __name__ == '__main__':
		
		im = Image.open(IMG)
		im = im.resize((WIDTH, HEIGHT), Image.NEAREST)
		txt = ""
		
		for i in range(HEIGHT):
			for j in range(WIDTH):
				txt += get_char(*im.getpixel((j, i)))
			txt += '\n'
			
		print txt
	
	if OUTPUT:
		with open(OUTPUT, 'w') as f:
			f.write(txt)
	else:
		with open("output.txt", 'w') as f:
			f.write(txt)
	
	# python it in Terminal		
	MBP-Ethan:shiyanlou xing$ python ascii.py ascii_dora.png 

Here's the Output.txt

<img class="shadow" src="/img/inPost/PicturetoAscii.png" width="520">

## Parse

The key point of this script is: 

	txt += get_char(*im.getpixel((j, i)))
	
Using the **im.getpixel()** method to get the pixel of the Picture.

	>>> import Image
	>>> import os
	>>> os.listdir('.')
	['.DS_Store', 'ascii.py', 'ascii_dora.png', 'output.txt', 'test.png', 'utput.txt']
	>>> im = Image.open(os.listdir('.')[2])
	>>> h, w = im.size
	>>> im.getpixel((h/2, w/2))
	(255, 255, 255, 255)
	>>> im.getpixel((h/4, w/4))
	(0, 160, 233, 255)


Then called the **get_char()** function convert it to character.

	def get_char(r, b, g, alpha = 256):
		if alpha == 0:
			return ' '
		length = len(ascii_char)
		gray = int(0.2126 * r + 0.7152 * g + 0.0722 * b)
		unit = (256.0 + 1) / length
		return ascii_char[int(gray/unit)]
		
Mapping pixel to sequence ascii characters.  step by step: 

	>>> ac = list("$@B%8&WM#*oahkbdpqwmZO0QLCJUYXzcvunxrjft/\|()1{}[]?-_+~<>i!lI;:,\"^`'. ")
	>>> ac
	['$', '@', 'B', '%', '8', '&', 'W', 'M', '#', '*', 'o', 'a', 'h', 'k', 'b', 'd', 'p', 'q', 'w', 'm', 'Z', 'O', '0', 'Q', 'L', 'C', 'J', 'U', 'Y', 'X', 'z', 'c', 'v', 'u', 'n', 'x', 'r', 'j', 'f', 't', '/', '\\', '|', '(', ')', '1', '{', '}', '[', ']', '?', '-', '_', '+', '~', '<', '>', 'i', '!', 'l', 'I', ';', ':', ',', '"', '^', '`', "'", '.', ' ']
	>>> import Image
	>>> picPath = '/Users/xing/Documents/shiyanlou/ascii_dora.png'
	>>> im = Image.open(picPath)
	>>> h, w = im.size
	>>> pix = im.getpixel((h/3, w/3))
	>>> pix
	(45, 31, 34, 255)
	>>> length = len(ac)
	>>> r, b, g, alpha = pix
	>>> gray = int(0.2126 * r + 0.7152 * g + 0.0722 * b)
	>>> gray
	36
	>>> unit = (256.0 + 1) / length
	>>> unit
	3.6714285714285713
	>>> int(gray / unit)
	9
	>>> ac[9]
	'*'
	>>>

#### Argparse module

[Argparse](http://songpengfei.iteye.com/blog/1320877)

[introduction to Argparse](http://www.cnblogs.com/jianboqi/archive/2013/01/10/2854726.html)










