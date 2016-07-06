---
layout:     post
title:      " Get the Subtitle"
subtitle:   " \" get the subtitle with Python from .srt file! \""
date:       2016-07-06
author:     "Ethan"
header-img: "img/inPost/GettheSubtitle.jpg"
tags:
    - Python
    - English
---

## Get the Subtitle

Avatar: The last Airbender, 起初是为了练习英语听力及口语而了解的一部动漫，评价很是不错，看了下来之后确实很是喜欢。从网上 Download 下来 .srt 文件，打印之的话，其中的时间行却是无用。 自己写了个小脚本将字幕提取了出来。
这部剧有三季，Download 下来三季的 zip 包，解压缩后放置在桌面上各季的文件夹中。分别新建文件夹用来保存脚本生成的 .txt 文件。

	import re
	import os

	fPath = "/Users/xing/Desktop/Avatar_The_Last_Airbender - season 1.en"
	sPath = "/Users/xing/Desktop/Avatar_The_Last_Airbender_subtitle/"

	os.chdir(fPath)
	flist = os.listdir(fPath)

	for eachFile in flist[1:]:
		with open(eachFile) as F:
			subTxt = F.read()
			subTxtList = re.findall(r'[^\n][a-zA-Z]+.*\n', subTxt)
			print subTxtList
			fullSPath = os.path.join(sPath, eachFile+'.txt')
			fileSave = open(fullSPath, 'w')
			for eachline in subTxtList[:-2]:
				fileSave.write(eachline+'\n')
			fileSave.close()

## Avatar: The last Airbender

这部剧在 IMDB 的评分：[Avatar: The Last Airbender(IMDB)](http://www.imdb.com/title/tt0417299/)

#### Basic

《最后的风之子》是由派拉蒙影业公司出品，由M·奈特·沙马兰执导，诺亚·林格、戴夫·帕特尔、妮可拉·佩尔茨、杰克逊·拉斯波恩领衔主演的奇幻片。
该片根据动画系列片《降世神通：最后的气宗》改编，讲述了世界被四大神力“气、火、水、土”支配着，其中被称为“神通”的便是世上唯一同时拥有这四种神力的人，他可以阻止邪恶的火烈国征服世界的故事。
影片于2010年7月1日在美国上映，2010年8月23日在中国内地上映。

#### BackStory

全世界被战火吞噬，没有人能够阻止无法避免的毁灭。一个世纪以来，烈火国一直在全世界开战，企图征服其它的三个部族，大气牧族、水族部落以及大地国。烈火国对于被他们强大的军力击败的村落只给了一个选择，完全投降或是彻底毁灭。当世界各地的村民徒然地试着自卫，同时也极力保护少数拥有他们部族的神力，并且能够随心所欲驾驭属于他们部族的元素的神通。但是拥有模庞大的军队以及毁灭性强大的武器的烈火国，早就消灭了地球上每一个风之子。如今他们把目标转向水族部落，准备攻下北极水族的城堡。某天，一名年轻的截水神通凯塔拉（妮可拉·佩尔茨饰）和她的哥哥苏卡（杰克逊·拉斯波恩饰）一起练习她的截水技巧，意外发现一个名字叫安的小男孩（诺亚·林格饰），但是当安展现出御气的能力，凯塔拉和苏卡发现，他们找到的不只是最后的风之子。身为被预言的降世神通－唯一能够同时拥有四大神力的人，这个小小的风之子是唯一拥有击退烈火国猛烈攻击的能力，并且最后将为饱受战火荼毒的世界带来和谐的神通王。但是他能学会其它的三大神力，成为他注定要当的英雄，并且及时拯救世界吗。

#### Wikipedia: The last Airbender

This article is about the TV series. For the 2010 film, see The Last Airbender.
Avatar: The Last Airbender
Avatar The Last Airbender logo.svg
Also known as	Avatar: The Legend of Aang
Genre	
Action/Adventure
Fantasy
Comedy-drama
Created by	
Michael Dante DiMartino
Bryan Konietzko
Written by	
Michael Dante DiMartino
Bryan Konietzko
Aaron Ehasz
Tim Hedrick
John O'Bryan
Elizabeth Welch Ehasz
Joshua Hamilton
May Chan
Matthew Hubbard
James Eagan
Directed by	
Lauren MacMullan
Dave Filoni
Giancarlo Volpe
Ethan Spaulding
Joaquim Dos Santos
Voices of	
Zach Tyler Eisen
Mae Whitman
Jack DeSena
Jessie Flower
Dante Basco
Dee Bradley Baker
Jennie Kwan
Mako (Seasons 1–2)
Greg Baldwin (Season 3)
Mark Hamill
Grey DeLisle
Jason Isaacs
Clancy Brown
Composer(s)	Jeremy Zuckerman, Benjamin Wynn
Country of origin	United States
Original language(s)	English
No. of seasons	3
No. of episodes	61 (list of episodes)
Production
Executive producer(s)	
Michael Dante DiMartino
Bryan Konietzko
Aaron Ehasz
Running time	22 minutes
Production company(s)	
Nickelodeon Animation Studios
DR Movie
JM Animation
MOI Animation
Titmouse (opening)[1]
Release
Original network	Nickelodeon
Picture format	NTSC 4:3 (480i)
Original release	February 21, 2005 – July 19, 2008
Chronology
Followed by	
Avatar: The Last Airbender (comics)
The Legend of Korra (TV series)
External links
Official website
	This article contains Chinese text. Without proper rendering support, you may see question marks, boxes, or other symbols instead of Chinese characters.
Avatar: The Last Airbender (Avatar: The Legend of Aang in some regions) is an American animated television series that aired for three seasons (referred to as "books" in each episode's title card) on Nickelodeon from 2005 to 2008. Avatar: The Last Airbender is set in an Asiatic-like world[2] in which some people are able to manipulate the classical elements by use of psychokinetic variants of Chinese martial arts, known as "bending". The show combines the styles of anime and American cartoons, and relies on the imagery of various East Asian, Inuit, Southeast Asian, South Asian, and New World societies. Therefore, whether or not the series can be considered as an anime work is often discussed.[3]

The series follows the adventures of protagonist twelve-year-old Aang and his friends, who must bring peace and unity to the world by ending the Fire Lord's war against the other three nations.[4] The pilot episode first aired on February 21, 2005,[5] and the series concluded with a widely praised two-hour episode on July 19, 2008.[6] The show is obtainable from various sources, including DVD, the iTunes Store, the Zune Marketplace, the Xbox Live Marketplace, the PlayStation Store, Netflix, Amazon Video, and the Nicktoons Network.[7]

Throughout its run, Avatar: The Last Airbender was universally acclaimed by audiences and critics alike.[8] Praises went to the art direction, humor, cultural references, characters, and themes. It was also commercially successful, garnering 5.6 million viewers on its best-rated showing and receiving high ratings in the Nicktoons lineup, even outside of its 6- to 11-year-old demographic.[4][9] The series has been nominated for and won awards from the Annie Awards, the Genesis Awards, a Primetime Emmy Award and a Peabody Award, among others. The first season's success prompted Nickelodeon to order second[10] and third[11] seasons.

In other media, the series has spawned a critically panned, but financially successful, live-action film, titled The Last Airbender, directed by M. Night Shyamalan; scaled action figures;[12] a trading card game;[13][14] three video games; stuffed animals distributed by Paramount Parks and two Lego sets. An art book was also released in mid-2010.[15][16] A sequel series, The Legend of Korra, aired from 2012 to 2014.[17]
