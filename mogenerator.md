#mogenerator

##Why use mogenerator?
When creating custom classes for your CoreData entities Xcode will replace the custom classes each time you change your data model and generate new custom classes to reflect those changes. This can be annoying if you add logic to the entity classes and would like to keep that logic through data model changes.

Mogenerator generates two files for each entity. One file is a machine file that is overwritten anytime your data model changes. The other file is the custom entity class that you can insert the custom logic you would like to maintain through any data model changes.

##Installing mogenerator
Install mogenerator via homebrew.
		
		brew install mogenerator 
		
You can also install via the OS X installer. Download here: http://rentzsch.github.io/mogenerator/

##Getting started with mogenerator
Follow the steps below if you are setting up a project from scratch and would like to use mogenerator.

1. Create data model in Xcode.
2. Make sure data model is same name as project (ie project name: "project" --> project.xcdatamodeld
3. Make sure entities point to classes of same name
<br><img src="http://addisonwebb.com/wp-content/uploads/2014/11/Screen-Shot-2014-11-15-at-11.52.19-AM.png" width="700px">
4. Add custom script to the build phases of the project

		PATH=${PATH}:/usr/local/bin
		mogenerator -m $SRCROOT/$TARGET_NAME/$TARGET_NAME.xcdatamodeld/$TARGET_NAME.xcdatamodel -H $SRCROOT/$TARGET_NAME/CoreData -M $SRCROOT/$TARGET_NAME/CoreData/machine --template-var arc=true

	<br><img src="http://addisonwebb.com/wp-content/uploads/2014/11/Screen-Shot-2014-11-15-at-11.51.16-AM.png" width="700px">

5. Build project.
6. mogenerator creates a new folder called "CoreData". Drag the folder from your finder into your project files in Xcode.
<br><img src="http://addisonwebb.com/wp-content/uploads/2014/11/Screen-Shot-2014-11-20-at-6.57.42-PM.png" height="50px">

You are now ready to use the entity classes!

### Update (9/4/2015)
Version 1.29 has updated the location of the executable to support OS X El Capitan's new security measures. When installing the program via the OS X installer, Mogenerator can be found in: `/usr/local/bin`. In Xcode 6.4 this requires that you update the PATH so that xcode can see mogenerator command.

### Uninstalling
To uninstall mogenerator simply run the bash script below that corresponds to the version you have on your machine. Use `mogenerator --version` to check which version you have installed.

**1.28**

https://gist.github.com/addisonwebb/231e24604f809948e589

**1.29**

https://gist.github.com/addisonwebb/cdebf1ff6399529eb201


###Related Links
http://rentzsch.github.io/mogenerator/

http://brew.sh

http://raptureinvenice.com/getting-started-with-mogenerator/
