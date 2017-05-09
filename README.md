# Sublime Javascript iTerm2

Based on the wonderful build system created by @dwkns entitled - sublime-terminal, this one is the same thing except for JavaScript.

> A build system for Sublime Text 3 which runs your .js files in iTerm2. OS X only.

### Important 
You must use v2.9 or later of [iTerm2](http://iterm2.com/downloads).

### What does it do?
Opens a terminal window and passes your current .js file to the default Javascript. 

With Javascript this is useful when you have a script which requires user input (such as gets.chomp) something the Sublime console doesn't allow. 

---

### Installation
Clone the repo into the right place

    $ cd ~/Library/Application\ Support/Sublime\ Text\ 3/Packages/
    $ git clone https://github.com/chrisdobler/Javascript-iTerm2.git

Make `Javascript-iterm2.sh` executable

    $ chmod u+x Javascript-iTerm2/Javascript-iterm2.sh

Add a link from `/usr/local/bin` to the build script to ensure it runs
	
	$ ln -s ~/Library/Application\ Support/Sublime\ Text\ 3/Packages/Javascript-iTerm2/Javascript-iTerm2.sh /usr/local/bin

Set Javascript-terminal to be the default build system in Sublime

`Tools > Build System > Javascript-iTerm2`


### Usage

**Javascript**
In sublime create a new Javascript file such as `main.js` :

	console.log "Enter some text : "

	var stdin = process.openStdin();

	stdin.addListener("data", function(d) {
	    console.log("you entered: [" + 
	        d.toString().trim() + "]");
	  });

Hit <kbd>⌘B</kbd> to run the file.


The Terminal will open and `Javascript path/to/main.js` will be run.


### How it works
`Javascript-iTerm2.sh` uses some Applescript (hence OS X only) to open iTerm2 and pass in your .js file.

If iTerm2 is not open, it will be opened.

If iTerm2 is open the front window will be used. If no window is open one will be created.

If iTerm2 is open and the front window is busy, a new Tab will be created and used.

### Version history
**v0.0.4** - 21th Feb 2017 - Latest version
- Fixed some bugs in the Applescript

**v0.0.3** - 21th March 2015 
- Updated to use iTerm2 rather than Terminal. This is now possible because of the updated Applescript support in v2.9

**v0.0.2** - 25th October 2013 
- increased the Applescript delay before commands are run.
Sometimes (depending on system load) the AppleScript would try and run the commands before iTerm2 was ready. This occasionally led to unpredictable behaviour.

- added an Applescript command to automatically scroll the window to the end. Useful if you've previously scrolled up to review your RSpec output

- code snippets removed. They should be in thier own package, not bundeled in with a build system. 

**v0.0.1** - 5th October 2013 - intial version
