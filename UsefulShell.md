# Useful Shell Commands



# Kali Linux Commands

## *************************************************************************************************


## PEN testing 
 * download device driver for host
 * add device filter in virtual box
 * airmon-ng
 * if it doesn't show download 
 * https://www.youtube.com/redirect?v=6cCwsno-ty4&event=video_description&redir_token=g6WYwaKHJoDB_MUujqrktQsGkAh8MTUyMzkwOTA1MEAxNTIzODIyNjUw&q=http%3A%2F%2Flinuxwireless.sipsolutions.net%2Fdownload%2Fcompat-wireless-2.6%2Fcompat-wireless-2010-06-26-p.tar.bz2

		  cd into it
		  make unload 
		  make load
		  airmon-ng (Do you see it? ) 
		  airmon-ng start wlan0
		  airodump-ng wlan0mon
		  airodump-ng -c [channel] --bssid [bssid] -w /root/Desktop/ [monitor interface] (airodump-ng -c 10 --bssid 00:14:BF:E0:E8:D5 -w /root/Desktop/ mon0)
		  Leave airodump-ng running and open a second terminal. In this terminal, type this command: aireplay-ng –0 2 –a [router bssid] –c [client bssid] mon0
		  	EX. aireplay-ng –0 2 –a 00:14:BF:E0:E8:D5 –c 4C:EB:42:59:DE:31 mon0
 		  Open a new Terminal. Type in this command: aircrack-ng -a2 -b [router bssid] -w [path to wordlist] /root/Desktop/*.cap


 * Scan available networks 

 	sudo iwlist scan

 * Get installed wireless card info 

	lspci
	lspci | grep -i wireless
	lspci | egrep -i --color 'wifi|wlan|wireless'

 * Get wireless card driver info 

 	lspci -vv -s 0c:00.0


## *************************************************************************************************

# Perl for string replacement, because sed with OSX is weird 
 * perl -pi -w -e 's/SEARCH_FOR/REPLACE_WITH/g;' *.txt


# GITHUB UPDATE STUFF
 * find . -maxdepth 1 -type d \( ! -name . \) -exec bash -c "cd '{}' && perl -pi -w -e 's/You are/I am/g;' git.txt" \; 


# Replace all instances of one string with another 
## Note below options use sed... and sed isn't that great with mac.. now you know. 
				The -type f is just good practice; sed will complain if you give it a directory or so. -exec is preferred over xargs; you needn't bother with -print0 or anything. The {} + at the end means that find will append all results as arguments to one instance of the called command, instead of re-running it for each result. (One exception is when the maximal number of command-line arguments allowed by the OS is breached; in that case find will run more than one instance.)
  * find . -type f -name '*.txt' -exec sed -i '' s/this/that/ {} +
  * find . -maxdepth 1 -type d \( ! -name . \) -exec bash -c "cd '{}' && echo 'I am a git update script' >> git.txt" \;


# Exceucte Find and Sed together
 * find . -name "*.java" -exec sed -i '' s/foo/bar/g {} +






# Compare two directories 
a treats all files as text, r recursively searched subdirectories, q reports 'briefly', only when files differ
 * diff -arq folder1 folder2
will do this, telling you both if any files have been added or deleted, and what's changed in the files that have been modified.
 	diff -r 
 * Show files side by side, ignore white space and capitals
 	diff file1 file2 -iawy

# Limit number of lines in output 
	| head -n 10

# Verify Sha256 checksum 
 * openssl dgst -sha256 path/to/file | 
 grep -i -a developerchecksum

# Verify Sha1 checksum 
 * openssl sha1 /full/path/to/file

# Verify md5 checksum, even though it is no longer recommended as a checksum 
 * openssl md5 /full/path/to/file
 
 
# Use grep to find all files containing a certain string 
	
		grep -rl "string" /directory
		grep -i -a -v -r "<<<<.*" . 
		
# Use sed to replace lines matching regex pattern 

		sed -i '' '/>>>>.*/d' file/path
		sed '/>>>>.*/d' fild/path (This will just test in terminal, -i actually executes)
 

# Create bootable Kali_Linux usb stick 
 First open USB in Disk utility, Format as MS-DOS (Fat) w/ GUID Partition Map
Next... 
 * diskutil list 
Unmount usb to verify the right one 
 * diskutil unmountDisk /dev/disk6
 * diskutil mountDisk /dev/disk6
 
Image the Kali ISO file on the USB 
 * sudo dd if=kali-linux-2017.1-amd64.iso of=/dev/disk6 bs=1m

If you get a resource busy error just unmount the usb.

# Get hardware info on mac
 * system_profiler SPHardwareDataType
 
# Create a disc image 
	Move all the files to archive into the same folder.
	Open Disk Utility, in the Utilities folder in Launchpad.
	Choose File > New > “Disk Image from Folder.”
	Choose the folder you want, and click Image.
	Type a name for the disk image, and select where to save it.

# Run NodeJS code in Atom
	
# List all variable names and their current value 
	* printenv

# Add Useful Plugins to Android Studio or Any IntelliJ app on Mac
 * Plugins are stored in the following locations the first one works for me, just put plugin in latest version of Android Studio
    ~/Library/Application Support/Android Studio/
    /Applications/Application Support/Android Studio .app/contents/plugins
 * Below didn't work for me
    /Applications/Android Studio.app/Contents/plugins/android/lib/templates
 * So just copy plugins from IntelliJ community version, which can also be found at the same relative location, and paste them into those locations

# Set Up Firebase Cloud Functions
 * First set up Firebase CLI
    brew install node
    node -v
    npm -v
    npm install -g firebase-tools
 * Run PATH=/Users/myName/.node-modules/bin/firebase:$PATH
 * Configure gmail account and password 
 	    firebase functions:config:set gmail.email="myusername@gmail.com" gmail.password="secretpassword"
 * For some reason after everything, it only worked if alias was set 
    alias firebase='/Users/myName/.npm-packages/bin/firebase'
 * firebase init
 * Configure firebase with 
    firebase login 
 * Set up my firebase project to handle the events
    firebase use --add 
    - Then select your project from the list
 * firebase deploy 

# Android, separate thread on main thread 

        public class Utils {
            public static void runOnUiThread(Runnable runnable){
                final Handler UIHandler = new Handler(Looper.getMainLooper());
                UIHandler .post(runnable);
            } 
        }

        Utils.runOnUiThread(new Runnable() {
            @Override
            public void run() {
            // UI updation related code.
            }
        });


# Check Mac System specs 
    system_profiler SPSoftwareDataType


#Uninstall and Reinstall for Firebase CLI
        rm -rf node_modules
        npm uninstall -g firebase-tools
        npm uninstall -g @google-cloud/functions-emulator
        npm install -g firebase-tools
        npm install --save firebase-functions
        npm install
        firebase serve --only functions --project XXX


# Set Up Firebase Cloud Functions Shell
    npm install --save firebase-functions@latest
 * If you have a custom .runtimeconfig.json then run this first
        firebase functions:config:get > .runtimeconfig.json
 * Run below line, regardless of custom runtimeconfig
        firebase experimental:functions:shell

# Search Directories and files for a specific string 
 * This will search every file in every directory
    grep -lr "text to find" *


# Open Command Mac
 * -a The -a option means "open the file argument with the named application":
 
		 open -a TextWrangler file.txt

 * -e The -e option means "open the file argument with the TextEdit application":

		 open -e file.txt

 * -t Open with the default application 

 		 open -t file.txt
 		
# Change default text editor file from terminal 
 * Add the following to your ~/.bashrc file:
		 export EDITOR="/Applications/WhateverEditor.app/Contents/MacOS/TextEdit"
 * or just type the following command into your Terminal:
	   	 echo "export EDITOR=\"/Applications/TextEdit.app/Contents/MacOS/TextEdit\"" >> ~/.bashrc


# Brew information
Install Brew
	* ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
Uninstall Brew
	* ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"
 * Cellar is located in 
    	 /usr/local/Cellar
 * Switching from node v6 to v8 I had to run 
   		 brew switch node 8.9.1
    	 brew link --overwrite node
 * Search 
    	 brew search postgresql
 * Swich to older version
    	 brew switch homebrew/versions/postgresql8
 * Or if 8 is not already installed in Brew cellar
    	 brew install homebrew/versions/postgresql8
 

## General
 * find location -name 'name.ext'
 * mdfind string (will find all the files with text "string" in them)
 * mdfind mysearch -onlyin "root locadtion" (Only looks in that one directory)
 * mdfind -name FileName
 * find ~ -iname "value*" (Finds anything in home directory with word "value" in it)
 * find ~ -iname "value*" | more  (If lots of results) 
 * echo "string" >> README.md
 * nano ~/.Profile (Put your export path statements here) 
 * nano ~/Bashrc (Put alias here so you can use from command line) 
	 
	
## Git Commands 
 * Get the url of local git repo
 			git config --get remote.origin.url
 * git clone "git_repo_url"
 * git add . 
 * git commit 
 * git push (If you get error try)
 * git push origin master 
 * git stash 
 * git stash pop 

 * git config --get remote.origin.url
 * git config --global user.email

# Delete everything from remote repo and replace with local directory 
 * git push origin --delete master
  	Or you could also do 
  	* git push -f 

Then create a master branch and push your new code .
 
 
## (FIND CMD) Exececute a command in all subdirectories of current directory
        
        find . -maxdepth 1 -type d \( ! -name . \) -exec bash -c "cd '{}' && pwd" \;
        The \( ! -name . \) avoids executing the command in current directory.

 * Execute a mvn package to all sub directories in directory 

        find . -maxdepth 1 -type d \( ! -name . \) -exec bash -c "cd '{}' && mvn package" \;
        
 * Remove all git files from directory
        
        find . -name "*.git" -exec {} rm -R \; 

	

#### To solve git status --porcelain failed in 'directory'
 1. Have to delete all the .git files located in the 'directory'
 2. Run this command : 
    * find . -name ".git*" -exec rm -R {} \;

 1. To solve git status --porcelain failed in 'directory'
 * Have to delete all the .git files located in the 'directory'
 * Run this command : 
 * find . -name ".git*" -exec rm -R {} \;
	
#### A blackened unclickable folder in Github represent an old repo that wasn't removed locally properly. 
 1. git fetch

#### Create a bash script to make the github repository 
 1. create script.sh inside a file called my_scripts on the Desktop with this 
 
  			#!bin/bash
		        curl -u 'UserName' https://api.github.com/user/repos -d "{\"name\":\"$1\"}";
			git init;
			git remote add origin https://github.com/myName/$1.git;
			
 2. chmod 755 githubscript.sh
 3. nano ~/.profile;
 
			export PATH="$PATH:$HOME/Desktop/my_scripts" 
			(to exit nano use)
			ctrl x (Then answer yes about saving press enter )
			
 4.  also do nano ~/.bashrc 
			alias githubrepo="bash githubscript.sh"
 5. source ~/.bashrc ~/.profile; cd (to reload bash in termial) 
 6. Then use command githubrepo nameOfRepository
 7. Also make sure to put 
  * source ~/.bashrc 
 	in the bottom of .bash_profile

	
# The Ultimate Method for creating a repository and pushing code to it 
 * githubrepo "name_for_repo" (Now it's created on github) 
 * mkdir where you want it 
 * switch into directory and run echo "# Website" >> README.md
 * git init 
 * git add . 
 * git commit -m "Initial Commit"
 * git remote add origin https://github.com/myName/Demo.git (This only needs to be done on the inital creation) 
 * git push -u origin master
	
	
## Setting up User login information for GITHUB 
 * ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
 * eval "$(ssh-agent -s)"
 * ssh-add -K ~/.ssh/id_rsa

## Add images to README 
 * ![Alt text](/relative/path/to/img.jpg?raw=true "Optional Title")

	
## Generating SSH keys
 * Check if you have one already with cat ~/.ssh/id_rsa.pub
 * If you don't have one, generate one with ssh-keygen -t rsa -C "myEmail@domain.com"
 * When prompted for location and file name just press enter
 * use this to change password ssh-keygen -p <keyname>
	
## Creating Branches in GitLab
 * git clone                   //clone what branch you want
 * git checkout -b new_branch  //this will create a new local branch
 * git push origin new_branch  //this will create a new origin branch
	
### Push branches to master
 * first get all changes in branch from git pull origin branchName
 * git checkout master
 * git pull origin master
 * git merge test
 * git push origin master
	
### Refusing to merge unrelated histories
 * git pull origin branchName --allow-unrelated-histories
	
	
### Generate Key for Login with Facebook 
	
		**OSX**
		keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore | openssl sha1 -binary | openssl base64
		**Windows**
		keytool -exportcert -alias androiddebugkey -keystore %HOMEPATH%\.android\debug.keystore | openssl sha1 -binary | openssl base64
	
### Install Cordova Plugin for Facebook 
	
		ionic plugin add cordova-plugin-facebook4 --variable APP_ID="123456789" --variable APP_NAME="myApplication"

## To list all processes running 
	
		ps -ax 
   		lsof -i tcp:3000 
		killall (kills all processes)
	
## Kill all non essential processes 
	
		kill -9 -1
	

## Find if port is in use 

    sudo lsof -i TCP:$PORT | grep LISTEN (replace $port with port number)

## For Angular2 error with cannot find hmr 

    sudo npm install @angularclass/hmr @angularclass/hmr-loader

## USE sftp to copy file from local to server

    sftp usrname@orgname.edu
    Enter password
    cd <directory where you want to transfer the file>
    put <name of file you want to transfer>

 * Copy from server to local 
 	get -R directory 
 * Local commands 
 	lls
 * Server commands 
 	ls 
    
    
## Make Android Studio Run Faster 

	Add this to gradle properties 
		org.gradle.daemon=true
	
	Android -> Preferences -> Build, Execution, Deployment -> Compiler
		Check the Option -
		Compile independent modules in parallel (may require larger heap size)
		
	Set VM Options to :
		  -Xmx2048m -XX:MaxPermSize=512
		  
		  
# Find wifi password Windows and Mac

	* Windows 
	  - Remember to replace labnol with the name of your Wireless SSID 
	  (this is the name of the Wi-Fi network that you connect your computer to)
		netsh wlan show profile name=labnol key=clear
	* If you just wanna see the password and nothing else use 
		netsh wlan show profile name=labnol key=clear | findstr Key
		
GET WIFI PASSWORDS WITH WINDOWS 
	* netsh wlan show profiles 
Then pick a profile and type this 
	* netsh wlan show profiles profileName key=clear
Password is shown at key content row
		
	* MAC 
	 - replace labnol with your WiFi name
	 security find-generic-password -wa labnol, then enter your Mac username and password 
	 to access the OS X keychain and the Wi-FI network password would be displayed on the screen in plain text.
	 
	* security find-generic-password -wa labnol
	

# Find where java is installed on mac

		/usr/libexec/java_home -v 1.
	
# Remove \r characters from a windows file to use on mac 

		sed $'s/\r$//' ./install.sh > ./install.sh
		
		
# Find available wifi networks from command line. 
 * Make a symbolic link with 
 	sudo ln -s /System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport /usr/local/bin/airport
 * airport -s 
 * airport --getinfo
 
# Join wifi network from command line 
 * networksetup -setairportnetwork en0 WIFI_SSID_I_WANT_TO_JOIN WIFI_PASSWORD
 - If you know the connections, you can write a script 
 				If you know the wifi connections name you can write a script to switch:
 				
 				
 * networksetup -listallhardwareports  (Shows what type of connection it is, en0, en1 .. etc) 

case "$1" in

   wifi1)
       printf "Switching to wifi1 ...\n"
       networksetup -setairportnetwork en0 wifi1 password1
       ;;

   wifi2)
       printf "Switching to wifi2 ...\n"
       networksetup -setairportnetwork en0 wifi2 password2
       ;;

   *)
       printf "Unknown wifi"
       exit -1
esac

exit 0

# See who is connected to your wifi 

		arp -a
 
 
# Install aircrack 
	
		brew install aircrack-ng
		
# Crack WPA WPA2 pass

		sudo ln -s /System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport /usr/sbin/airport
		sudo airport -s

		sudo airport en1 sniff [CHANNEL]

		//New Terminal Window
		aircrack-ng -1 -a 1 -b [TARGET_MAC_ADDRESS] [CAP_FILE]
		// Notes: the cap_file will be located in the /tmp/airportSniff*.cap.
 
# Android/adb command not recognized
 * set up ~/.profile with 
 
    export PATH="$PATH:$HOME/Library/Android/sdk/platform-tools"  (For adb)
	export PATH="$PATH:$HOME/Library/Android/sdk/tools"   (For android) 
	
# If you delete gradle files from android studio project, you can reset using these steps 

	1. Close the project in Android Studio (so it doesn't open the project automatically in later steps) 
		and then close Android Studio
	2. Clean the project (delete the ".idea" and "build" folders, .iml files, etc.) so you only have the source 
		files remaining
    3. Set up gradle by adding the appropriate settings.gradle and build.gradle files 
    	(test your setup using the command line)
	4. Open Android Studio and choose "Import project" and choose to use Gradle as the external model
	5. Pick your settings.gradle file as the Gradle project
	6. [Optional] Set your "Gradle home" folder (so the text turns black instead of gray). 
		Earlier versions of Android Studio caused problems for me if I didn't do this. 
		Make sure you use Gradle 0.1.10 or newer (earlier versions do not work with the current Gradle build tools).
		
		
# See all wifi connection history on mac

		defaults read /Library/Preferences/SystemConfiguration/com.apple.airport.preferences| sed 's|\./|`pwd`/|g' | sed 's|.plist||g'|grep 'LastConnected' -A 7


# Set default text editor 
	
 * Open ~/.bashrc
 		
 		export EDITOR="path"
 		
 		
# Display free disk space
  * Get size of files in current directory 
  		
  			du -sh * 
  
  * Get free disk space 
  		
  		df -h

  * Size of a single file 
  		du -h

# Use curl with redirects to download from sourceforge 

		curl -L http://somewhere.com
		
		
		
# GMAIl server port info

		Incoming Mail (IMAP) Server - Requires SSL
		imap.gmail.com
		Port: 993
		Requires SSL:Yes

		Incoming Mail (POP3) Server - requires SSL:
		pop.gmail.com
		Use SSL: Yes
		Port: 995

		Outgoing Mail (SMTP) Server - Requires TLS or SSL
		smtp.gmail.com
		Port: 465 or 587
		Requires SSL: Yes
		Requires authentication: Yes
Use same settings as incoming mail server


# Create a virtualenv in Python 
	# Install pip
	sudo easy_install pip
# Install virtualenv 
	python -m pip install --user virtualenv
# Create virtual environment 
	python -m virtualenv env

# Activate virtual env
	source env/bin/activate
#  Deactivate
	deactivate

# Installing imports
	pip install requests 
	pip install package_name
# Install all imports at once 
	Add all your imports in a single txt file, say requirements.txt and every time you run 
	your program on a new system, just do a

 * pip install -r requirements.txt



# Scan for open ports on network 
		
		nmap 192.168.1.1
		hydra -l admin -P password.txt -v -f  192.168.1.1 ftp  // Could also use http-get

# Generate a random mac adress 

		openssl rand -hex 6 | sed ‘s/\(..\)/\1:/g; s/.$//’

 * Change MAC address, must be disconnected from wifi networks for this to work (Press and hold option, then click wifi icon)
		
		sudo ifconfig en0 ether xx:xx:xx:xx:xx:xx


# Selenium Webdriver with firefox
 * brew install geckodriver


