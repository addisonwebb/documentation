#Addison's Objective-C Style Guide

Apple's style guide: https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html

Google's Objective-C style guide: https://google.github.io/styleguide/objcguide.xml

#### Variables

Pointers should hug the variable name.

`NSString *foo = @"bar";`

NOT

`NSString* foo = ...`

`NSString * foo = ...`

#### braces
The first brace should be one space from the end of the line.

```
- (void)aMethod {
		
}
```

#### Methods
Method declarations and calls should be on 1 line. 

#### if
If statements should always include braces.

```	
if {
	// code here
}
```

Or, you too can be cleaning up a mess after a simple mistake like Apple's SSL bug from 2014:

```
...
hashOut.data = hashes + SSL_MD5_DIGEST_LEN;
hashOut.length = SSL_SHA1_DIGEST_LEN;
if ((err = SSLFreeBuffer(&hashCtx)) != 0)
    goto fail;
if ((err = ReadyHash(&SSLHashSHA1, &hashCtx)) != 0)
    goto fail;
if ((err = SSLHashSHA1.update(&hashCtx, &clientRandom)) != 0)
    goto fail;
if ((err = SSLHashSHA1.update(&hashCtx, &serverRandom)) != 0)
    goto fail;
if ((err = SSLHashSHA1.update(&hashCtx, &signedParams)) != 0)
    goto fail;
    goto fail;  /* MISTAKE! THIS LINE SHOULD NOT BE HERE */
if ((err = SSLHashSHA1.final(&hashCtx, &hashOut)) != 0)
    goto fail;

err = sslRawVerify(...);
...
```	

https://nakedsecurity.sophos.com/2014/02/24/anatomy-of-a-goto-fail-apples-ssl-bug-explained-plus-an-unofficial-patch/


Else statements should be on the same line as the ending brace of the condition it follows.

```
if (foo) {
	// code if statement is true
} else {
	// code if statement is false
}
```

```
if (foo) {
	// code if statement is true
} else if (bar) {
	// code if statement is false
}
```


##Comments
Comments should be used to clarify your code. **Never** use inline comments.

### Comment Blocks
Comment blocks should be formatted in the following way.
	
	/*
 	  1st comment line
 	  2nd comment line
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
	