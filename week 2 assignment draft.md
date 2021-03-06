## Week 2 Project: Carousel

**Due:** {{PROJECT(2) | longdate}} at 11:59pm

### Overview

The purpose of this homework is to leverage views, view properties, and events to create a high fidelity prototype that is difficult to distinguish from a production app. We're going to use the techniques from this week to implement the Carousel app from the signed out state to the basic signed in state.

![Carousel GIF|250](http://i.imgur.com/TBJkE46.gif)

### Project Requirements

- Static photo tiles on the initial screen
  - **Optional**: Photo tiles move with scrolling
- Sign In
  - Tapping on email/password reveals the keyboard and shifts the scrollview and Sign In button up.
  - Upon tapping the Sign In button.
     - If the username or password fields are empty, user sees an error alert.
     - If credentials are incorrect, user sees a loading indicator for 2 seconds followed by an error alert.
     - If the credentials are correct, user sees a loading indicator for 2 seconds followed by a transition to the Tutorial screens.
  - Optional: When the keyboard is visible, if the user pulls down on the scrollview, it will dismiss the keyboard.
  - Optional: On appear, scale the form up and fade it in.
- Optional: Create a Dropbox
  - Optional: Tapping in the form reveals the keyboard and shifts the scrollview and "Create a Dropbox" button up.
  - Optional: Tapping the Agree to Terms checkbox selects the checkbox.
  - Optional: Tapping on Terms shows a webview with the terms.
  - Optional: User is taken to the tutorial screens upon tapping the "Create a Dropbox" button.
- Tutorial Screens
  - User can page between the screens
  - Optional: User can page between the screens with updated dots
  - Optional: Upon reaching the 4th page, hide the dots and show the "Take Carousel for a Spin" button.
- Image Timeline
  - Display a scrollable view of images.
  - User can tap on the conversations button to see the conversations screen (push).
  - User can tap on the profile image to see the settings view (modal from below).
- Settings
  - User can dismiss the settings screen.
  - User can log out
- Optional: Learn more about Carousel
  - Optional: Show the "Learn more about Carousel" button in the photo timeline.
  - Optional: Tap the X to dismiss the banner
  - Optional: Track the 3 events:
     - View a photo full screen
     - Swipe left and right
     - Share a photo
  - Optional: Upon completion of the events, mark them green.
  - Optional: When all events are completed, dismiss the banner.

### Assets

You can download the Carousel assets [here](https://www.dropbox.com/s/53llomcr20qicxo/Carousel%20Assets.zip).

### Milestones

The key to implementing a complex app is to break it up into a bunch of small pieces until it's easy to implement any given piece. You should try implementing this homework by following the milestones below. Be sure to run the simulator frequently as you hit milestones.

0. **Setup:**
  - Create a new project (disable Auto Layout). [New Project](https://guides.codepath.com/ios/New-Project-%28designers%29)
  - Add the image assets above. [Adding Image Assets](https://guides.codepath.com/ios/Adding-Image-Assets)
  - Configure the app icon and splash screen. [App icon and launch image](https://guides.codepath.com/ios/Adding-Image-Assets#app-icon-and-launch-image)
  - Add the [Common.swift](https://www.dropbox.com/s/van89swo47j0im1/Common.swift?dl=0) file to your project. Be sure to select "Copy items if needed".
1. **Intro Screen**
  - In the Storyboard, add a custom view controller for the IntroViewController. [Creating Custom View Controller](https://guides.codepath.com/ios/Creating-Custom-View-Controllers)
  - Configure the view controller to be freeform, so that you can make it long enough to see the entire intro page. [Creating Free Form View Controller](https://guides.codepath.com/ios/Creating-a-Free-Form-View-Controller)
  - Add UIImageViews for each photo tile in the region below. [Using UIImageView](https://guides.codepath.com/ios/Using-UIImageView)
  - Configure the content size of the scroll view. ``scrollView.contentSize = imageView.size``[Using UIScrollView](https://guides.codepath.com/ios/Using-UIScrollView)
  - **Optional:** Tiles translate, scale and rotate into place as user scrolls
     - Register for the scroll view scroll events [Registering for scroll events](https://guides.codepath.com/ios/Using-UIScrollView#registering-for-scroll-events)
     - Whenever a scroll event happens, configure the transform property on the image view. [Using View Transforms](https://guides.codepath.com/ios/Using-View-Transforms)
2. **Sign In Screen**
  - Add all the view elements for the Sign In View Controller in Storyboard
     - *Sign_in_nav_bar* as UIImageView 
     - UIScrollView
     - background as a blank UIView 
     - *sign_in_text* as UIImageView 
     - *sign_in_form* as UIImageView
     - email and password fields as UITextFields
     - *sign_in_buttons* as UIImageView
     - UIButton placed over Sign In button, transparent
  - When the user touches either textField and the keyboard shows:
     - The scrollView should scroll up to it's fully scrolled position. ``scrollView.contentOffset.y = // max offset ``
     - The button should animate up above the top of the keyboard. ``button.transfrom = CGAffineTransformMakeTranslation( x, y)``
  - Tapping the Sign In button
     - If either of the email or ``||`` password fields are empty, ``textField.text!.isEmpty``, show an error alert using a UIAlertViewController. [Using UIAlertController](https://guides.codepath.com/ios/Using-UIAlertController)
     - If the populated email or ``||`` password fields do not match ``!=`` your correct email and password:
        - Display an UIActivityIndicator for 2 seconds using a delay closure. (Hint: Make sure to download and copy the common.swift file you your project)[Calling a Method After Delay](https://guides.codepath.com/ios/Calling-a-Method-After-Delay
        - After the delay, display an error for incorrect email/password using a UIAlertController. 
     - If the populated email and ``&&`` password fields match ``==`` your correct credentials:
        - Display a UIActivityIndicator for 2 seconds using a delay closure.
        - After the delay, transition to the tutorial screen
           - Create, ``ctrl + drag`` a modal Segue from the Sign In UIViewController to the Tutorial UIViewController
           - Trigger the segue, ``performSegueWithIdentifier("loginSegue", sender: nil)``
  - **Optional:** The scrollview should only be scrollable when the keyboard is shown.
     - ``scrollView.scrollEnabled = true``, ``scrollView.scrollEnabled = false``
  - **Optional:** Scrolling down a specific amount should: 
     - Dismiss the keyboard ``view.endEditing(true)``
     - Animate the button back to it's original position ``button.transform = CGAffineTransformIdentity``
  - **Optional:** ScrollView should smoothly animate to a specific scrolled up position any time either of the textFields are tapped. 
     - Get the textField events by ``right-clicking`` the text fields and ``ctrl + drag`` to your ViewController code file. Have them share the same method. [Registering For TextField Events](https://github.com/codepath/ios_guides/wiki/Registering-for-text-field-events), [Animating View Properties](https://guides.codepath.com/ios/Animating-View-Properties)
3. **Tutorial Screens**
  - Create a custom free form view controller that is wide enough for 4 screens. [Creating Custom View Controllers](https://guides.codepath.com/ios/Creating-Custom-View-Controllers), [Creating a Free Form View Controller](https://guides.codepath.com/ios/Creating-a-Free-Form-View-Controller)
  - Add a UIScrollView with paging enabled. 
  - Add 4 UIImageViews for the tutorial screens (Note: we're explicitly **NOT** using **UIPageViewController**, which requires extra coding)
  - Add a UIPageControl 
     - The UIPageControl should be outside and in front of the scrollview. 
     - Set the page of the UIPageControl by referencing events from the UIScrollView. [Using UIPageControl](https://guides.codepath.com/ios/Using-UIPageControl)
     - Note: You may need to adjust the *Tint Color* and *Current Page* color for the page indicators to be visible on top of the white background.
  - Add the "Take Carousel for a Spin" button (should be outside the scrollview). 
  - Tapping the "Take Carousel for a Spin" button should launch the Image Timeline modally.
     - Since the Image Timeline will have a NavigationController, the above modal Segue should point to the Image Timeline NavigationController. 
  - **Optional:** Upon reaching the 4th page, ``page == 3``, because *page 1* is really *page 0*:
     - The PageContol indicators disappear
        - ``pageControl.hidden = true`` 
     - The *take_for_a_spin* button should fade in. 
        - ``button.alpha = 0`` within ``viewDidLoad()`` method   
        - animate ``button.alpha = 1``
4. **Image Timeline**
  - Add a UIImageView for the custom nav bar
  - Add a UIScrollView for the image feed.
  - Add UIButtons for Settings and Conversations.
  - Tapping the Conversation button should *push* the ConversationsViewController.
  - Tapping the Settings button should *modally* present the SettingsViewController.
5. **Create Account**
  - Add custom nav bar, form background, text fields, text, terms text and button, and Create Account button.
  - Add all the view elements for the Create Account View Controller in Storyboard
     - Sign in nav bar as UIImageView 
     - ScrollView
     - Form the background with a blank UIView 
     - Sign In text as UIImageView 
     - Sign In Form as UIImageView
     - UITextFields
     - Create Account button as UIImageView
  - Upon showing the keyboard, move the elements to be visible. [Registering for Keyboard Events](https://guides.codepath.com/ios/Registering-for-Keyboard-Events)
  - Add a selected state for the terms button. [Configure a Button](https://guides.codepath.com/ios/Configure-a-Button)
  - Terms opens webview w/ mobile terms of service page.

### Submission instructions

Follow the guide for [[Submitting Assignments]]. Remember to include an animated gif and # of hours spent in the README.
