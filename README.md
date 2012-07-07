# Filepicker iOS Library


The easiest way to import content into your application. 
[Filepicker.io](www.filepicker.io)

## Dependancies

- Software
	- Built targeting iOS 4.3
	- XCode 4
	
- Frameworks
	- AssetsLibrary.framework
	- QuartzCore.framework
	- CoreGraphics.framework
	- MobileCoreServices.framework
	- Foundation.framework
	- CoreFoundation.framework


## Installation Instructions


### For iOS Pros:

1. Get an APIKEY
	- Go to [Filepicker.io](www.filepicker.io) to register an account
	- Api Keys are typically randomized and 20 characters long.

2. Insert the framework and bundle
	- Download or clone the repository.
	- Under `/library`, you'll find `FPPicker.framework` and `FPPicker.bundle`
	- Drag both into your project, typically in your framework folder

3. Settings
	- In your application's info.plist, add the following key/value:
	
	```
	Key: "Filepicker APIKEY"
	Value: YOUR_API_KEY (from step 1)
	```
	- If this doesn't build, I've had luck adding `-all_load -ObjC` in `Build_Settings/Other_Linker_Flags`
	- You may need to add additional frameworks
		- AssetsLibrary.framework
		- QuartzCore.framework
		- CoreGraphics.framework
		- MobileCoreServices.framework
		- Foundation.framework
		- CoreFoundation.framework
	

4. Use it
	- Initialize it:
	
	```
    FPPickerController *fpController = [[FPPickerController alloc] init];
    fpController.fpdelegate = self;
	- Delegate Methods:
    - (void)FPPickerController:(FPPickerController *)picker didFinishPickingMediaWithInfo:(NSDictionary *)info;
    - (void)FPPickerControllerDidCancel:(FPPickerController *)picker;
```


### Running the Demo Project:

1. Get an Api Key:
	- Go to [Filepicker.io](www.filepicker.io) to register an account
	- Api Keys are typically randomized and 20 characters long.

2. Insert the framework and bundle:
	- Download or clone the repository.
	- Open the `/Examples/FPDemo.xcodeproj`

3. Settings:
	- In your application's info.plist, add the following key/value:
	
	```
	Key: "Filepicker APIKEY"
	Value: YOUR_API_KEY (from step 1)
	```

4. Build and Run


### Starting from scratch:

1. Get an Api Key:
	- Go to [Filepicker.io](www.filepicker.io) to register an account
	- Api Keys are typically randomized and 20 characters long.

2. Start a new Project
	<img src="https://github.com/Filepicker/ios/raw/master/Documenation%20Files/10.png" class="center">
	- File/New/Project or Shift-Apple N
	- Single View Project
	
	<img src="https://github.com/Filepicker/ios/raw/master/Documenation%20Files/20.png" class="center">
	- Name: FilepickerDemo
	- Device Family: iPad
	- Use Storyboards: False
	- Use Automatic Reference Counting: True
	
2. Insert the framework and bundle
	- Download or clone the repository.
	<img src="https://github.com/Filepicker/ios/raw/master/Documenation%20Files/30.png" class="center">
	- You can do this at the top of this git repository with either `ZIP` to get the zip or `git clone https://github.com/Filepicker/ios.git`.
	- Open up the folder.
	- Under `library/`, you'll find `FPPicker.framework` and `FPPicker.bundle`
	<img src="https://github.com/Filepicker/ios/raw/master/Documenation%20Files/35.png" class="center">	
	- Drag both into your project, typically in your framework folder
	<img src="https://github.com/Filepicker/ios/raw/master/Documenation%20Files/40.png" class="center">	
	- Choose to `Copy items into Destination Folder`
	
	
3. Adding Additional Frameworks

	<img src="https://github.com/Filepicker/ios/raw/master/Documenation%20Files/45.png" class="center">	
	- Click on the .xcodeProj
	<img src="https://github.com/Filepicker/ios/raw/master/Documenation%20Files/50.png" class="center">	
	<img src="https://github.com/Filepicker/ios/raw/master/Documenation%20Files/60.png" class="center">	
	- Under `Build Phases -> Link Binary with Libraries`, add the following:
		- AssetsLibrary.framework
		- QuartzCore.framework
		- CoreGraphics.framework
		- MobileCoreServices.framework
		- Foundation.framework
		- CoreFoundation.framework
	<img src="https://github.com/Filepicker/ios/raw/master/Documenation%20Files/70.png" class="center">	


4. Write the code

```
//
//  ViewController.h
//  FilepickerDemo
//
//  Created by Liyan David Chang on 7/6/12.
//  Copyright (c) 2012 __MyCompanyName__. All rights reserved.
//

#import <UIKit/UIKit.h>

#import <FPPicker/FPPicker.h>

@interface ViewController : UIViewController <FPPickerDelegate, UIPopoverControllerDelegate> {
    IBOutlet UIButton *button;
    IBOutlet UIImageView *image;
    UIPopoverController *popoverController;
}
@property (nonatomic, retain) UIImageView *image;
@property (nonatomic, retain) UIPopoverController *popoverController;

@end
```

```
//
//  ViewController.m
//  Filepicker Demo
//
//  Created by Liyan David Chang on 7/5/12.
//  Copyright (c) 2012 filepicker.io (Cloudtop Inc). All rights reserved.
//

#import "ViewController.h"
#import <FPPicker/FPPicker.h>

@interface ViewController ()

@end

@implementation ViewController

@synthesize image, popoverController;

- (void)viewDidLoad
{
    [super viewDidLoad];
	// Do any additional setup after loading the view, typically from a nib.
}

- (void)viewDidUnload
{
    [super viewDidUnload];
    // Release any retained subviews of the main view.
}

- (BOOL)shouldAutorotateToInterfaceOrientation:(UIInterfaceOrientation)interfaceOrientation
{
    if ([[UIDevice currentDevice] userInterfaceIdiom] == UIUserInterfaceIdiomPhone) {
        return (interfaceOrientation != UIInterfaceOrientationPortraitUpsideDown);
    } else {
        return YES;
    }
}

- (IBAction)pickerAction: (id) sender {
    
    
    FPPickerController *fpController = [[FPPickerController alloc] init];
    fpController.fpdelegate = self;
    //fpController.sourceNames = [[NSArray alloc] initWithObjects: (NSString *) FPSourceDropbox, (NSString *) FPSourceImagesearch, nil];
    
    UIPopoverController *popoverControllerA = [UIPopoverController alloc];
    
    self.popoverController = [popoverControllerA initWithContentViewController:fpController];
    popoverController.popoverContentSize = CGSizeMake(320, 520);
    [popoverController presentPopoverFromRect:[sender frame] inView:self.view permittedArrowDirections:UIPopoverArrowDirectionAny animated:YES];
}

- (void)FPPickerController:(FPPickerController *)picker didFinishPickingMediaWithInfo:(NSDictionary *)info
{
    NSLog(@"FILE CHOSEN: %@", info);
    
    image.image = [info objectForKey:@"FPPickerControllerOriginalImage"];
    [popoverController dismissPopoverAnimated:YES];
    
}
- (void)FPPickerControllerDidCancel:(FPPickerController *)picker
{
    NSLog(@"FP Canceled.");
    //[picker removeFromParentViewController];
    [popoverController dismissPopoverAnimated:YES];
}

@end
```

