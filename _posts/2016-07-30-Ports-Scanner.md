---
layout:     post
title:      " Network Ports Scanner "
subtitle:   " \" A low-level Multiple Thread network ports scanner with python\""
date:       2016-07-30
author:     "Ethan"
header-img: "img/Hello-Blog.jpg"
tags:
    - Python

---

## Port Scanner

Port scanner is an application designed to probe a **server** or **host** for open ports. A port scan is a process that sends client requests to a range of server port addresses on a host, with a goal of finding an active port.

<img class="shadow" src="/img/inPost/PortScanner-execute.png" width="820">

#### TCP/IP basic knowledge

The design and operation of the internet is based on the **Internet Protocol Suite**, commonly also called **TCP/IP**. In this system, hosts and host services are referenced using two components: an address and a port number. There are 65536 distinct and usable port numbers.

### Types

##### 1. TCP scanning  
The simplest port scanners use the operating system's network function and are generally the next option to go to when **SYN** is not a feasible option. **Nmap** calls this mode connect scan, named after the Unix connect() system call. if a port is open, the operating system completes the **TCP three-way handshake**, and the port scanner immediately closes the connection to avoid performing a **Denial-of-service attack**. Otherwise an error code is returned. This scan mode has the advantage that the user does not requires special privileges. However, using the OS network function prevents low-level control, so this scan type is less common.

##### 2. SYN scanning  
SYN scan is another form of TCP scanning. Rather than use the operating system's network functions, the port scanner generates raw IP packets itself, and monitor for responses. This scan type is also known as "half-open scanning", because it **never** actually opens a full TCP connection. The port scanner generates a SYN packet. If the target port is open, it will respond with a SYN-ACK packet. The scanner host responds with an RST packet, closing the connection before the handshake is completed. If the port is closed but unfiltered, the target will instantly respond with on RST packet.  
The use of raw networking has several advantages, giving the scanner full control of the packets sent and the timeout for responses, and allowing detailed reporting of the responses. There is debate over which scan is less intrusive on the target host. SYN scan has the advantage that the individual services never actually receive a connection. However, the RST during the handshake can cause problems for some network stacks, in particular simple devices like printers. There are no conclusive arguments either way.

### Implementation 

#### argsparse

[argparse – Command line option and argument parsing](https://pymotw.com/2/argparse/)

[Argparse](http://songpengfei.iteye.com/blog/1320877)

[introduction to Argparse](http://www.cnblogs.com/jianboqi/archive/2013/01/10/2854726.html)

	''' Use argparse module '''
			parser = argparse.ArgumentParser(usage='Network Port Scanner', description=' example of using: python PortScan.py -hn baidu.com -p 80-500 ')
		
			parser.add_argument('-hn', '--host')
			parser.add_argument('-p', '--port')
		
			args = parser.parse_args()
			argPort = args.port.split('-')
		
			HostOrHName = args.host
			StartPort, EndPort = int(argPort[0]), int(argPort[1])
			
<img class="shadow" src="/img/inPost/PortScanner-args-help.png" width="820">

#### Multiple Threading

[threading module](https://docs.python.org/2/library/threading.html) 
 
[threading – Manage concurrent threads](https://pymotw.com/2/threading/)

**Subclass Thread and Creates Subclass Instance**  

	class MyThread(threading.Thread):
			def __init__(self, func, port):
				threading.Thread.__init__(self)
				self.func = func
				self.port = port
		
			def run(self):
				apply(self.func, (self.port,))

### The whole code

	# -*- coding: utf-8 -*-
	
	import sys
	import argparse
	from socket import *
	import threading
	from time import sleep, ctime
	
	# ''' PortScan.py <host> <StartPort>-<EndPort> '''
	# host = sys.argv[1]
	# PortStrs = sys.argv[2].split('-')
	# 
	# StartPort = int(PortStrs[0])
	# EndPort = int(PortStrs[1])
	
	
	class MyThread(threading.Thread):
		def __init__(self, func, port):
			threading.Thread.__init__(self)
			self.func = func
			self.port = port
	
		def run(self):
			apply(self.func, (self.port,))
	
	def TcpTest(port):
		sock = socket(AF_INET, SOCK_STREAM)
		sock.settimeout(4)
		result = sock.connect_ex((targetIp, port))
		if result == 0: 
			print "Opened Port: ", port
	
	if __name__ == '__main__':
		''' Use argparse module '''
		parser = argparse.ArgumentParser(usage='Network Port Scanner', description=' example of using: python PortScan.py -hn baidu.com -p 80-500 ')
	
		parser.add_argument('-hn', '--host')
		parser.add_argument('-p', '--port')
	
		args = parser.parse_args()
		argPort = args.port.split('-')
	
		HostOrHName = args.host
		StartPort, EndPort = int(argPort[0]), int(argPort[1])
		targetIp = gethostbyname(HostOrHName)
		print 'HostOrHName: %s  and targetIp: %s' % (HostOrHName, targetIp)
		
		print 'start at: %s \n' % ctime()
		threads = []
	
		for port in range(StartPort, EndPort + 1):
			t = MyThread(TcpTest, port)
			threads.append(t)
		
		for i in range(len(threads)):
			threads[i].start()
		
		for i in range(len(threads)):
			threads[i].join()
		
		print '\nall DONE at: %s' % ctime()

The End.
		
---

		
		
		
	
		


			
			
			
			