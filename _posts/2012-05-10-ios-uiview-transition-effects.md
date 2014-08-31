---
layout:     post
title:      iOS – UIView transition effects
date:       2012-05-10 10:00:00
summary:    How to push/pop iOS UINavigationControllers using other animations besides the default one, like flip or curl.
categories: ios
---

![ios-animation](/pixyll/images/2012-05-10-ios-uiview-transition-effects/ios_animation.png)

I have seen lots of people asking on how to push/pop UINavigationControllers using other animations besides the default one, like flip or curl.

One problem that you will find is that either the question/answer was relatively old, which means that it included have some things not used anymore like `[UIView beginAnimations:]` and `[UIView commitAnimations]` (example [here](http://stackoverflow.com/questions/2215672/how-to-change-the-push-and-pop-animations-in-a-navigation-based-app)) but if you searched enough you will see the use two different approaches nowadays

## UIView Animations only

The first is to use UIView‘s `transitionFromView:toView:duration:options:completion:` selector before pushing the controller (with the animation flag set to `NO`), like the following:

{% highlight objc %}
UIViewController *ctrl = [[UIViewController alloc] init];
[UIView transitionFromView:self.view toView:ctrl.view duration:1 options:UIViewAnimationOptionTransitionFlipFromTop completion:nil];
[self.navigationController pushViewController:ctrl animated:NO];
{% endhighlight %}

This is pretty straightforward and might be good enough for most projects as the options parameter gives you some nice transitions by default:

- [UIViewAnimationOptionTransitionNone](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/UIView/UIView.html#//apple_ref/doc/uid/TP40006816-CH3-SW105)
- [UIViewAnimationOptionTransitionFlipFromLeft](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/UIView/UIView.html#//apple_ref/doc/uid/TP40006816-CH3-SW105)
- [UIViewAnimationOptionTransitionFlipFromRight](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/UIView/UIView.html#//apple_ref/doc/uid/TP40006816-CH3-SW105)
- [UIViewAnimationOptionTransitionCurlUp](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/UIView/UIView.html#//apple_ref/doc/uid/TP40006816-CH3-SW105)
- [UIViewAnimationOptionTransitionCurlDown](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/UIView/UIView.html#//apple_ref/doc/uid/TP40006816-CH3-SW105)
- [UIViewAnimationOptionTransitionCrossDissolve](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/UIView/UIView.html#//apple_ref/doc/uid/TP40006816-CH3-SW105)
- [UIViewAnimationOptionTransitionFlipFromTop](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/UIView/UIView.html#//apple_ref/doc/uid/TP40006816-CH3-SW105)
- [UIViewAnimationOptionTransitionFlipFromBottom](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UIView_Class/UIView/UIView.html#//apple_ref/doc/uid/TP40006816-CH3-SW105)

One key aspect is to note that the `animated:` parameter is set to `NO`, as we are performing the animation from one view to another manually, avoiding the default one that the `UINavigationController` provides.

Ok, but sometimes you want some more radical animations, and thats when Core Animation calls you to action

## Using CoreAnimation

This second approach uses CoreAnimation explicitly with a `CATransaction` like the following:

{% highlight objc %}
CATransition* transition = [CATransition animation];
transition.timingFunction = [CAMediaTimingFunction functionWithName:kCAMediaTimingFunctionEaseIn];
transition.duration = 1.0f;
transition.type =  @"flip";
transition.subtype = @"fromTop";
[self.navigationController.view.layer removeAllAnimations];
[self.navigationController.view.layer addAnimation:transition forKey:kCATransition];

UIViewController *ctrl = [[UIViewController alloc] init];
[self.navigationController pushViewController:ctrl animated:NO];
{% endhighlight %}

First observation, you will have to have the [QuartzCore framework](http://developer.apple.com/library/mac#documentation/graphicsimaging/reference/QuartzCoreRefCollection/_index.html) added to your project for this approach and also add `<QuartzCore/QuartzCore.h>` to the class this code is used to make it work.

There are several aspects that this approach differs from the first one. The main one is that the first one results in a code that looks a lot cleaner the the Core Animation one, but there is a big trade-off as CoreAnimation opens the gate to several really cool transitions like “suckEffect”, “cube”, and [others](http://iphonedevwiki.net/index.php/CATransition). Here is a list of some of the possible native effects.

- cameraIris
- cube
- fade (kCATransitionFade)
- moveIn (kCATransitionMoveIn)
- oglFlip
- pageCurl
- pageUnCurl
- push (kCATransitionPush)
- reveal (kCATransitionReveal)
- rippleEffect
- suckEffect
- genieEffect
…

As you might have noticed, a lot of the transitions does not have a native constant value, so you might get worried about using these undocumented transitions types (i.e. not present in the [Common transition types documentation](http://developer.apple.com/library/iOS/#documentation/GraphicsImaging/Reference/CATransition_Class/Introduction/Introduction.html#//apple_ref/doc/constant_group/Common_Transition_Types) from [CATransition Class Reference](https://developer.apple.com/library/IOS/documentation/GraphicsImaging/Reference/CATransition_class/Introduction/Introduction.html)) which could get your app rejected from App Store (I mean could as there is no explicit documentation or reference about apps being rejected due to Core Animation transactions). There are some [alternatives to perform these kind of animations using openGL](https://web.archive.org/web/20120622232021/http://www.aderstedtsoftware.com/users/erik/weblog/c7cb9/), for example, but this is not the focus right now.

## Besides UINavigationController transition

I believe you noticed that the transitions I showed were all `UIView` transitions, which means they could all be used to animate `UIView`, regardless of an UIViewController.

A good example of these flip transitions being used for `UIView`s only is inside of [Google Places’s App](https://web.archive.org/web/20130525075242/https://itunes.apple.com/us/app/google-places/id406513617?mt=8) when you tap to change the places view mode from map to list (and vice-versa)

![google-placs-app](/pixyll/images/2012-05-10-ios-uiview-transition-effects/googleplacesapp.png)

---

Originally posted by me at [http://i.ndigo.com.br/2012/05/ios-uiview-transition-effects/](https://web.archive.org/web/20130727085842/http://i.ndigo.com.br/2012/05/ios-uiview-transition-effects/)
