#Addison's Objective-C Style Guide

Apple's style guide: https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html

Google's Objective-C style guide: https://google.github.io/styleguide/objcguide.xml

####braces
The first brace should be one space from the end of the line.

	- (void)aMethod {
		
	}

####if
If statements should always include braces.
	
	if {
		// code here
	}
	

##Comments
Comments should be used to clarify your code. **Never** use inline comments.

### Comment Blocks
Comment blocks should be formatted in the following way.
	
	/*
 	 * 1st comment line
 	 * 2nd comment line
 	 */


###Imports
Imports should be grouped into sections and annotated with comments.
	
	#import "exampleClass.h"
	
	// Frameworks
	#import <ReactiveCocoa/ReactiveCocoa.h>
	#import <libextobjc/EXTScope.h>

	// Child View Controllers
	#import "childViewController.h"
	#import "anotherChildViewController.h"
	