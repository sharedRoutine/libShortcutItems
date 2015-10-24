# libShortcutItems
libShortcutItems allows you to easily add shortcut items to applications on SpringBoard. It is a library for 3D Touch compatible devices.

## Usage ##

You need to import libShortcutItems.h first

```objc
#import <libShortcutItems/libShortcutItems.h>
```

### SpringBord ###
In SpringBoard you register the items you want to add to applications.

```objc
if ([LSIManager sharedManager].isRunningInsideSpringBoard) {
	LSISBSApplicationShortcutItem *item = [[LSIManager sharedManager] newShortcutItemType:@"test_icon" title:@"Test" subtitle:@"Testing libShortcutItems" iconType:UIApplicationShortcutIconTypeAdd];
	[[LSIManager sharedManager] addShortcutItems:@[item] toApplicationID:@"com.apple.Preferences"];
}
```

You can also have a callback that won't open the app and is handled on SpringBoard

```objc
LSISBSApplicationShortcutItem *sbItem = [[LSIManager sharedManager] newShortcutItemType:@"test_sb_icon" title:@"Test" subtitle:@"Testing SpringBoard" iconType:UIApplicationShortcutIconTypeAdd];
[sbItem setHandledBySpringBoard:YES];
[[LSIManager sharedManager] addShortcutItems:@[sbItem] toApplicationID:@"com.apple.iBooks"];
[[LSIManager sharedManager] setSBShortcutHandlerBlock:^(LSISBSApplicationShortcutItem *item) {
	NSLog(@"Handled %@ on SpringBoard",item.localizedTitle);
}];
```

### In Preferences (example) ###
In the Preferences Process you tell LSIManager that you want to be notified of any item that you added before

```objc
[[LSIManager sharedManager] setShortcutHandlerBlock:^(UIApplicationShortcutItem *item) {
  NSLog(@"Handled Shortcut Item: %@",item.localizedTitle);
}];
```

As easy as that :) a few lines of code enables lots of cool features.

## Future ##

- I am planning to add custom views inside the Shortcut Item Menu.

## Example ###

[Example Project on Github](https://github.com/sharedRoutine/test-libShortcutItems/)

![libShortcutItems in action](https://pbs.twimg.com/media/CRZN8iFVEAAZe7Z.jpg)
