# SDLCarWindow Video Projection Developer Interface
:
:
/**
 *  Touch Manager responsible for providing touch event notifications.
 */
@property (nonatomic, strong, readonly) SDLTouchManager *touchManager;

/**
* Car Window instance responsible for providing video projection.
* /
@property (nonatomic, strong, readonly) SDLCarWindow *carWindow;
:
:
```

```objc
@interface SDLCarWindow : NSObject

/**
 *  View Controller that will be streamed.
 */
@property (strong, nonatomic, nullable) UIViewController *streamingViewController;

/**
 * Dimensions of the target in-car screen
 */
@property (assign, nonatomic, readonly) CGSize screenDimensions;

/**
 * SDLInterfaceManager instance for head-unit focusing and selection
 */
@property (strong, nonatomic) SDLInterfaceManager *interfaceManager;

@end
```

### Handling focusable UIButtons
The UIButton class returns NO for the UIFocusItem canBecomeFocused method unless it is being displayed on a CarPlay window. However, the SDLInterfaceManager relies on the canBecomeFocused property to determine which buttons should have spatial data sent to the head unit. To overcome this issue, the SDL proxy will implement the following category on UIButton that will return YES for canBecomeFocused.

```objc
@interface UIButton (SDLFocusable)

@property(nonatomic, readonly) BOOL canBecomeFocused;

@end
```

For head units that allow the app to manage focus and selection, the SDLInterfaceManager provides the local logic to do so and interacts with the views through the [UIFocusEnvironment protocol](https://developer.apple.com/documentation/uikit/uifocusenvironment).