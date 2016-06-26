---
layout:     post
title:      "Python Challenge"
subtitle:   "\" The first programming riddle on the net \" "
date:       2016-06-25
author:     "Ethan"
header-img: "img/inPost/PythonChallenge.png"
tags:
    - Python
    - PythonChallenge
    
---

> [PythonChallenge](http://www.pythonchallenge.com/)  
> To read the pre-Level of PythonChallenge at this site: [Ethan.Penx Blog in ITeye](http://jnstar.iteye.com/admin/blogs/2214796) 

## Level 7  

**Riddle Page L7:** [http://www.pythonchallenge.com/pc/def/oxygen.html](http://www.pythonchallenge.com/pc/def/oxygen.html) 

The title of the page is "smarty", and there's a picture which with a strip of greyscale squares across the middle is in the top of the page. At the sight of the clue "smarty", what coming to my mind is the **Python Module** named **Smartypants**, but, sadly, there's nothing I can get through the **smartypants.**

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

#### Relative

There's something to help understanding all the Image stuff as following:

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



**-- Continuing**

 