# Using (and accidentally overwriting) PATH

`PATH` tells Linux where to look for executable binary files in response to specific user commands.  It lives in `~/.bash_rc` and should be added to `~/.profile` or `~/.bash_profile` on an interactive basis. 

 E.g. if you type `ls folder` , it needs to know how to execute `ls`. That command is located in the `/bin` folder (usually): 

	computer:bin user$ ls

	[		df		launchctl	pwd		tcsh
	bash		domainname	link		rcp		test
	cat		echo		ln		rm		unlink
	chmod		ed		ls		rmdir		wait4path
	cp		expr		mkdir		sh		zsh
	csh		hostname	mv		sleep
	date		kill		pax		stty
	dd		ksh		ps		sync

The PATH variable allows Unix to look for it in /bin or /usr/sbin or other folders. 

	computer:user$ echo $PATH
	/Users/vboykis/anaconda/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin

To show what's currently in the path variable: 

	echo $PATH 

To add a directory to the PATH variable, either at the beginning or end of the string. The elements are checked left to right, and the standard is to add these strings to the end. 

	PATH=$PATH:~/opt/bin
	PATH=~/opt/bin:$PATH
	
To add more than one additional folder, add a colon after each folder.  

	PATH=$PATH:~/opt/bin:~/opt/node/bin
	

The default path variable varies by Linux distribution. For example, for CentOS, it's usually: 

	/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbin

To test that PATH is working correctly, test some common Unix element, like vi: 

	[computer]$ which vi
	alias vi='vim'
		/usr/bin/vim
		
And it should give you back both the correct alias and the correct pointer to path. 

To set a generic environmental variable:

`[lib]$ FLUME_HOME=/usr/lib/flume-ng`

`[lib]$ export FLUME_HOME`

`[lib]$ echo $FLUME_HOME`

