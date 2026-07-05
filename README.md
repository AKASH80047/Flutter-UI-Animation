<h1 align="center" xmlns="http://www.w3.org/1999/html">
  <br>
   <img src="https://raw.githubusercontent.com/AKASH80047/Flutter-UI-Animation/main/assets/page1.png" alt="Liquid Swipe" title="Logo" />
  <br>
  Flutter UI Animation
</h1>

<p align="center">  
  <a href="https://github.com/AKASH80047/Flutter-UI-Animation/releases">
    <img height="20" alt="GitHub All Releases" src="https://img.shields.io/github/downloads/AKASH80047/Flutter-UI-Animation/total.svg?style=for-the-badge">
  </a>
  <a href="https://pub.dev/packages/liquid_swipe">
    <img height="20" alt="Pub" src="https://img.shields.io/pub/v/liquid_swipe.svg?style=for-the-badge">
  </a>
  <a href="https://github.com/AKASH80047/Flutter-UI-Animation/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/license-APACHE2.0-blue.svg?longCache=true&style=flat-square">
  </a>
  <a href="https://flutter.dev">
    <img src="https://img.shields.io/badge/Built%20for-Flutter-blue.svg?longCache=true&style=flat-square">
  </a>
  <a href="https://github.com/Solido/awesome-flutter">
    <img alt="Awesome Flutter" src="https://img.shields.io/badge/Awesome-Flutter-blue.svg?longCache=true&style=flat-square" />
  </a>
</p>

<p align="center">
  This repository contains high-quality <strong>Flutter UI Animations</strong>. 
  It features <strong>Liquid Swipe Flutter</strong>, an amazing revealing clipper that brings a smooth, liquid-like transition effect to stacked Containers/Widgets. Inspired by <a href="https://github.com/Cuberto/liquid-swipe">Cuberto's liquid swipe</a> and <a href="https://github.com/aagarwal1012/IntroViews-Flutter">IntroViews</a>.
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/AKASH80047/Flutter-UI-Animation/main/assets/example.gif" width="310" height="640" alt="Example GIF 1">
  <img src="https://raw.githubusercontent.com/AKASH80047/Flutter-UI-Animation/main/assets/another.gif" width="310" height="640" alt="Example GIF 2">
</p>

# Table of contents
* [Getting Started](#getting-started)
* [Usage](#usage)
* [Migration](#migration) 
* [Sample APK](#sample-apk)
* [Documentation](#documentation)
  * [LiquidSwipe](#liquidswipe)
  * [LiquidController](#liquidcontroller)  
* [Credits](#credits)
* [Author & Support](#author--support)
* [Contributors](#contributors-)

# Getting Started

* Add this to your `pubspec.yaml`:
  ```yaml
  dependencies:
    liquid_swipe: ^3.1.0
  ```
* Get the package from Pub:
  ```bash
  flutter packages get
  ```
* Import it in your file:
  ```dart
  import 'package:liquid_swipe/liquid_swipe.dart';
  ```
  
# Usage

* `Liquid Swipe` just requires a list of [`Widgets (like Containers)`](https://api.flutter.dev/flutter/widgets/Container-class.html) to allow developers complete flexibility in designing their UI.
  ```dart
  final pages = [
    Container(...),
    Container(...),
    Container(...),
  ];
  ```
  
* Now, simply pass these pages to the `LiquidSwipe` widget:
  ```dart
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Builder(
        builder: (context) => LiquidSwipe(
          pages: pages,
        ),
      ),
    );
  }
  ```

* Check out the complete [Example](https://github.com/AKASH80047/Flutter-UI-Animation/tree/main/example)

# Migration

Some things to keep in mind while updating to v2.0.0 from any older version:
* v2.0.0 is migrated to null safety. See [migration guide](https://dart.dev/null-safety/migration-guide).
* Attribute `enableSlideIcon` is removed from `LiquidSwipe`. You can simply pass `null` to `slideIconWidget` to disable it.
* Attribute `positionSlideIcon` is now ranged from `0.0` to `1.0`.
* Next Reveal is enabled by default. If you want to disable it, you might want to make changes in your fork. Open an issue and I'll help.

That's it ;)

# Sample APK

Please download the APK from the [Releases](https://github.com/AKASH80047/Flutter-UI-Animation/releases) or the [Assets](https://github.com/AKASH80047/Flutter-UI-Animation/tree/main/assets) folder.

# Documentation  

## LiquidSwipe

Please refer to the [API documentation](https://pub.dev/documentation/liquid_swipe/latest/liquid_swipe/LiquidSwipe-class.html) for more details. 

| Property | Type | Description | Default Value |
|-|:-:|-|:-:|
| pages | `List<Widget>` | Set Pages/Views/Containers. See complete example for usage. | @required value |
| fullTransitionValue | `double` | Handle swipe sensitivity through it. Lower the value faster the animation | 400.0 |
| initialPage | `int` | Set initial page value, wrong position will throw exception. | 0 |
| slideIconWidget | `Widget` | Icon/Widget you want to display for swipe indication. Remember the curve will be created according to it. | null |
| positionSlideIcon | `double` | Icon position on vertical axis. Must satisfy this condition `0.0 <= value <= 1.0` | 0.8 |
| enableLoop | `bool` | Whether you want to loop through all those `pages`. | true |
| liquidController | `LiquidController` | Controller to handle some runtime changes. [Refer](#liquidcontroller) | null |
| waveType | `WaveType enum` | Type of clipper you want to use. | WaveType.liquidReveal |
| onPageChangeCallback | `Callback` | Triggered whenever page changes. | null |
| currentUpdateTypeCallback | `Callback` | Triggered whenever UpdateType changes. [Refer](https://pub.dev/documentation/liquid_swipe/latest/Helpers_Helpers/UpdateType-class.html) | null |
| slidePercentCallback | `Callback` | Triggered on Swipe animation. Use carefully as its quite frequent on swipe. | null |
| ignoreUserGestureWhileAnimating | `bool` | If you want to block gestures while swipe is still animating. See #5 | false |
| disableUserGesture | `bool` | Disable user gesture, always. | false |
| enableSideReveal | `bool` | Enable/Disable side reveal | false |
| preferDragFromRevealedArea | `bool` | Disabling the drag from the whole page and allowing only from the revealed part of the screen and the icon | false |

## LiquidController

A Controller class with utility fields and methods.

### Simple Usage

1. Create a `LiquidController` object and initialize it in `initState()`:
   ```dart
   late LiquidController liquidController;

   @override
   void initState() {
     super.initState();
     liquidController = LiquidController();
   }
   ```

2. Add it to the `LiquidSwipe` constructor:
   ```dart
   LiquidSwipe(
     pages: pages,
     liquidController: liquidController,
   )
   ```

Note: You cannot invoke methods on the controller before the `build` method has initialized `LiquidSwipe`.

* **Properties**
  * `currentPage` - Getter to retrieve the current page index. Default value is `0`.
  * `isUserGestureDisabled` - Check if user gestures are disabled. Default value is `false`.
* **Methods**
  * `animateToPage({required int page, int duration = 600})` - Animates to the target page index. The duration is the total duration of the animation.
  * `jumpToPage({required int page})` - Instantly jumps to the target page index without animation.
  * `shouldDisableGestures({required bool disable})` - Use this method to disable gestures dynamically, e.g., on specific pages within `onPageChangeCallback`.

Please refer to the [API documentation](https://pub.dev/documentation/liquid_swipe/latest/PageHelpers_LiquidController/LiquidController-class.html) for more details. 

# Credits

* [Cuberto](https://github.com/Cuberto) for the awesome Swift implementation of [Liquid Swipe](https://github.com/Cuberto/liquid-swipe).
* [@aagarwal1012](https://github.com/aagarwal1012) for [IntroViews](https://github.com/aagarwal1012/IntroViews-Flutter), which inspired parts of this project.

### Disclaimer: This project is not affiliated with Cuberto, but we have notified them through this [issue](https://github.com/Cuberto/liquid-swipe/issues/10).

# Author & Support

This project is created by [Sahdeep Singh](https://github.com/iamSahdeep) with lots of support.
> If you appreciate the work, connect with the author on [LinkedIn](https://www.linkedin.com/in/iamsahdeep/) to keep them motivated.

<img src="https://cdn-images-1.medium.com/max/1200/1*2yFbiGdcACiuLGo4dMKmJw.jpeg" width="90" height="35" alt="Medium Logo">

# Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://sahdeepsingh.com"><img src="https://avatars1.githubusercontent.com/u/26563213?v=4" width="100px;" alt=""/><br /><sub><b>Sahdeep Singh</b></sub></a><br /><a href="https://github.com/AKASH80047/Flutter-UI-Animation/commits?author=iamSahdeep" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/YasserOJ"><img src="https://avatars0.githubusercontent.com/u/26030291?v=4" width="100px;" alt=""/><br /><sub><b>Yasser Omar Jammeli</b></sub></a><br /><a href="https://github.com/AKASH80047/Flutter-UI-Animation/commits?author=YasserOJ" title="Code">💻</a> <a href="https://github.com/AKASH80047/Flutter-UI-Animation/issues?q=author%3AYasserOJ" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/mourad-brahim"><img src="https://avatars1.githubusercontent.com/u/17046133?v=4" width="100px;" alt=""/><br /><sub><b>Mourad Brahim</b></sub></a><br /><a href="https://github.com/AKASH80047/Flutter-UI-Animation/commits?author=mourad-brahim" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/heshesh2010"><img src="https://avatars1.githubusercontent.com/u/16393042?v=4" width="100px;" alt=""/><br /><sub><b>heshesh2010</b></sub></a><br /><a href="https://github.com/AKASH80047/Flutter-UI-Animation/issues?q=author%3Aheshesh2010" title="Bug reports">🐛</a> <a href="#userTesting-heshesh2010" title="User Testing">📓</a></td>
    <td align="center"><a href="https://github.com/ssoldy"><img src="https://avatars2.githubusercontent.com/u/45917574?v=4" width="100px;" alt=""/><br /><sub><b>Federico Tarascio</b></sub></a><br /><a href="https://github.com/AKASH80047/Flutter-UI-Animation/commits?author=ssoldy" title="Code">💻</a></td>
  </tr>
</table>

<!-- markdownlint-enable -->
<!-- prettier-ignore-end -->
<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!
