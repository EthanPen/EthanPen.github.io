---
layout:     post
title:      "Python Challenge (7 - 10)"
subtitle:   "\" The first programming riddle on the net \" "
date:       2016-06-25
author:     "Ethan"
header-img: "img/inPost/PythonChallenge.png"
tags:
    - PythonChallenge
    
---

> [PythonChallenge](http://www.pythonchallenge.com/)  
> To read the pre-Level of PythonChallenge at this site: [Ethan.Penx Blog in ITeye](http://jnstar.iteye.com/admin/blogs/2214796) 

#### Table of Contents
1. [Level 7](#Level 7)
2. [Level 8](#Level 8)
3. [Level 9](#Level 9)
4. [Level 10](#Level 10)

---

<p id="Level 7"></p>

## Level 7  

**Riddle Page L7:** [http://www.pythonchallenge.com/pc/def/oxygen.html](http://www.pythonchallenge.com/pc/def/oxygen.html) 

The title of the page is "smarty", and there's a picture  with a strip of greyscale squares across the middle which is at the top of the page. At the sight of the clue "smarty", what occurs to me is a **Python Module** named **Smartypants**, but sadly, there's nothing I can get by **smartypants.**

Mabye the clue is in those greyscale squares, with the greyscale level (range from 0-255) encoding something in it, whatever, try it first.

Downloaded the picture(named it '**oxygen.png**').

	>>> import Image
	>>> im = Image.open("/Users/xing/Desktop/oxygen.png")
	>>> width, height = im.size
	>>> im.getpixel((0, h//2))
	(115, 115, 115, 255)
	>>> print chr(115), chr(255)
	s ?

Well, that make sense. Let's guess that each block is 4 pixel wider:

	>>> smarty = [chr(im.getpixel((i, h//2))[0]) for i in range(0, width, 4)]
	>>> ''.join(smarty)
	'ssmaarrtt gguuyy,  yyoou  mmaadee  iit..  tthee  nnexxtt  leevveel  iiss [[11005,,  11100,,  11166,, 110011,  11003,,  11144,,  10055,, 111166,  11221]]rbecbc'
	>>> 

Obviously, I choose the wrong pixel width, try it a few of times.

Turns out, the colour changes every 7 pixels.
	
	>>> print ''.join([chr(im.getpixel((i, h//2))[0]) for i in range(0, width, 7)])
	smart guy, you made it. the next level is [105, 110, 116, 101, 103, 114, 105, 116, 121]pe_
	>>> print ''.join(map(chr, [105, 110, 116, 101, 103, 114, 105, 116, 121]))
	integrity
	>>> 

So, change the **url** (**oxygen --> integrity**) to getting Level 8:
**Riddle Page L8:** [http://www.pythonchallenge.com/pc/def/integrity.html](http://www.pythonchallenge.com/pc/def/integrity.html)

### The Related

There's something to help understand all the Image stuff as following:

* [PIL - Image Module](http://pillow.readthedocs.io/en/3.2.x/reference/Image.html)

* [Display image as grayscale using matplotlib](http://stackoverflow.com/questions/3823752/display-image-as-grayscale-using-matplotlib)

* [Get pixel's RGB using PIL](http://stackoverflow.com/questions/11064786/get-pixels-rgb-using-pil)

##### functions:

* **Image.getpixel(xy):**  
>	Returns the pixel value at a given position.  
Parameters:	xy – The coordinate, given as (x, y).  
Returns:	The pixel value. If the image is a multi-layer image, this method returns a tuple.


* **map(function, sequence[, sequence, ...]) -> list**   
> 	Return a list of the results of applying the function to the items of
    the argument sequence(s).  If more than one sequence is given, the
    function is called with an argument list consisting of the corresponding
    item of each sequence, substituting None for missing values when not all
    sequences have the same length.  If the function is None, return a list of the items of the sequence (or a list of tuples if more than one sequence).

---




<p id="Level 8"></p>

## Level 8



**Riddle Page L8:** [http://www.pythonchallenge.com/pc/def/integrity.html](http://www.pythonchallenge.com/pc/def/integrity.html)

Well, there's a picture with a bee flying up the flower, and the clues "Where is the missing link?" at the bottom of the page, clicked the picture takes us to a **password-protected** page for area "inflate". And the title of this page is "working hard?".  Seriously? working hard? I'm totally confused...

Let's do it the old ways, check the source code of this page, it's showed me a series of messy strings, Unfortunately, I can't figure out what types of coding it used, neither encoding it.

Fine, google the messy strings, turns out, it's brz2 compressed file format. 
	
	>>> un = "BZh91AY&SYA\xaf\x82\r\x00\x00\x01\x01\x80\x02\xc0\x02\x00 \x00!\x9ah3M\x07<]\xc9\x14\xe1BA\x06\xbe\x084"
	>>> pw = 'BZh91AY&SY\x94$|\x0e\x00\x00\x00\x81\x00\x03$ \x00!\x9ah3M\x13<]\xc9\x14\xe1BBP\x91\xf08'
	
	>>> import bz2
	>>> bz2.decompress(un)
	'huge'
	>>> bz2.decompress(pw)
	'file'
	
So, entered the username&password come to the Level 9: [http://www.pythonchallenge.com/pc/return/good.html](http://www.pythonchallenge.com/pc/return/good.html)


BTW, here's the hint comes from official solutions:

> You see a bee in the picture. She sounds busy too. What could that mean?
bee? busy. busy? busy too ? bz2?
The hint in the password box says "inflate" so you consider to try to decompress the strings.


#### THe Related


* [Level8:Main Page
](http://wiki.pythonchallenge.com/index.php?title=Level8:Main_Page)

##### functions: 

* **bz2.compress(data[, compresslevel])**  
Compress data in one shot. If you want to compress data sequentially, use an instance of BZ2Compressor instead. The compresslevel parameter, if given, must be a number between 1 and 9; the default is 9.

* **bz2.decompress(data)**  
Decompress data in one shot. If you want to decompress data sequentially, use an instance of BZ2Decompressor instead.

---



<p id="Level 9"></p>

## Level 9

**Riddle Page Level 9: (Uname: huge, Pwd: file)** [http://www.pythonchallenge.com/pc/return/good.html](http://www.pythonchallenge.com/pc/return/good.html)

The title of this page is "connect the dots", and there are a long lists of numbers for "first"&"second" in the source page. Maybe the numbers are the coordinates of dots which join another picture? Just do it.

	MBP-Ethan:TextWrangler xing$ vim pythonchallenge9.py
	'''
	copy & paste the "first" and "second"
	'''
	MBP-Ethan:TextWrangler xing$ python pythonchallenge9.py 

	# enter python shell
	>>> from pythonchallenge9 import *
	>>> len(list1), min(list1), max(list1)
	(442, 77, 403)
	>>> len(list2), min(list2), max(list2)
	(112, 77, 220)

	>>> import Image
	>>> help(Image.new)
	new(mode, size, color=0)
    Create a new image
	>>> im = Image.new('1', (600, 600), "white")
	>>> import ImageDraw
	>>> line1 = zip(list1[0::2], list1[1::2])
	>>> line2 = zip(list2[0::2], list2[1::2])
	>>> draw = ImageDraw.Draw(im)
	>>> draw.line(line1)
	>>> draw.line(line2)
	>>> im.show()

A bull showed on the screen.

<img class="shadow" src="/img/inPost/PythonChallenge-bull.png" width="320">

Well, same old, changing the url to get to Level10:
[http://www.pythonchallenge.com/pc/return/bull.html](http://www.pythonchallenge.com/pc/return/bull.html)

#### The Related

##### functions

* **Image.new(mode, size, color) ⇒ image**  
Creates a new image with the given mode and size. Size
is given as a (width, height)-tuple, in pixels. The
color is given as a single value for single-band 
images, and a tuple for multi-band images (with one 
value for each band). In 1.1.4 and later, you can also 
use color names (see the ImageColor module 
documentation for details) If the color argument is 
omitted, the image is filled with zero (this usually 
corresponds to black). If the color is None, the image 
is not initialised. This can be useful if you’re going 
to paste or draw things in the image.
	
		from PIL import Image
		im = Image.new("RGB", (512, 512), "white")

* **Draw a Grey Cross Over an Image**
		
		import Image, ImageDraw

		im = Image.open("lena.pgm")

		draw = ImageDraw.Draw(im)
		draw.line((0, 0) + im.size, fill=128)
		draw.line((0, im.size[1], im.size[0], 0), fill=128)
		del draw

		# write to stdout
		im.save(sys.stdout, "PNG")

---

<p id="Level 10"></p>

## Level 10

**Riddle page Level 10**: [http://www.pythonchallenge.com/pc/return/bull.html](http://www.pythonchallenge.com/pc/return/bull.html)

There's a picture of a bull and the clue is "len(a[30]) = ?". Display the source page, and  clicking the href="sequence.txt" get to the another page which is reveals "a = [1, 11, 21, 1211, 111221, ".  Obviously, we're asked to solve the sequence puzzle. 

Type the numbers into the **[Online Encyclopedia of Integer Sequences,](https://oeis.org/search?q=1%2C11%2C21%2C1211%2C111221&language=english&go=Search) (OEIS)**. Turns out, this one is **A005150, "Look and say sequence."**

There's Python code in the OEIS for computing the values of the sequence, but it's simpler to follow the cross-reference for the length of the n-th term to find the sequence **[A005341](https://oeis.org/A005341)**, it gives the length of the 31st term as 5808.

So, here's the url of Level 11:
[http://www.pythonchallenge.com/pc/return/5808.html](http://www.pythonchallenge.com/pc/return/5808.html)

---


 