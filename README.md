# iOS 11 Large-title navigation bars don't work properly

*This is a demonstration project for the following question on Stackoverflow.com: https://stackoverflow.com/questions/46373055/ios-11-large-title-navigation-bar-not-collapsing*

The Apple guy in the [What's new in Cocoa Touch WWDC video said][1] that the new large-title navigation bar will magically hook into the top-level scroll view of the underlying view controller and collapse/expand itself automatically while scrolling up and down. (And by "magically", he probably meant that they failed to monkey patch this functionality into the already embarassing `UINavigationController`-`UINavigationBar`-`UINavigationitem` APIs in a usable way, so they had to resort to hooking into some heuristically chosen scroll view behind the scenes)

Even though I was prepared that this "automatic" collapse/expand wouldn't work if I deviate the slightest from the basic `UINavigationController` + `UITableView`/`UICollectionView` setup, it seems that even in this simplest case it doesn't work as expected. 

Here's what I have:

A `UITabBarController` which contains a `UINavigationController`, which contains a `UIViewController`, which has a `UITableView` as its `view`. Tapping the first cell in the table will push a second view controller on the navigation stack:

[![storyboard][2]][2]

No code, just the storyboard. 

I've checked *"Prefers large titles"* for the navigation bar to activate large titles. Now, if I run the app and scroll up/down on the table view, the navigation bar stays the same - large - size; it doesn't collapse:

[![stuck with large title][3]][3]

However, I've found that if I set the second view controller's navigation item to use the small navigation bar (by setting *"Large Title"* to the value *"Never"*), then if I open that page and navigate back, the interactive collapse magically starts working on the first page:

[![interactive collapse works after back navigation][4]][4]

Am I missing something here, or is this feature not working properly? Here's the sample project I'm using: https://github.com/tzahola/iOS-11-Large-Title-Navigation-Bar

And by the way, I'm using the officially released iOS 11, not the betas. 


  [1]: https://developer.apple.com/videos/play/wwdc2017/201/
  [2]: https://i.stack.imgur.com/hnSlK.png
  [3]: https://i.stack.imgur.com/PM0ru.gif
  [4]: https://i.stack.imgur.com/pJBD9.gif
