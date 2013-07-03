# PLEASE NOTE, THIS PROJECT IS NO LONGER BEING MAINTAINED

* * *

# Pull To Refresh Views for Android

## 本分支修改


* 列表快速滚动到达边缘时，限制回弹的最大距离。
* Title拉伸监听

### 滚动中断

添加了一个接口，主要用于以下场景：

**使用场景的全部实现代码在sample项目的PullToRefreshListActivity中**

* 列表滚动开始时，隐藏列表上面的View。如图，titleView在列表开始向下滚动时，隐藏起来以留下更多空间给列表。列表再滚回到顶部时，下拉可以显示titleView。

    -----------
    |  title  |
    | ------- |
    |-1-------|
    |-2-------|
    |-3-------|
    |-4-------|
    |-5-------|

接口如下代码。修改的位置在PullToRefreshBase中，代码位置都被 TODO 标识。

```java

    public interface HeaderPullingListener{
        
        int PULLING_ORIENTATION_HORIZONTAL = 0;
        int PULLING_ORIENTATION_VERTICAL = 1;
        
        /**
         * 列表LoadingHeader被拉动
         * @param orientation
         * @param scrollDistance
         */
        void onHeaderPulling(int orientation, int scrollDistance);
        
    }

```

监听使用方法

```java

    // 创建
    private PullToRefreshBase.HeaderPullingListener listener = new PullToRefreshBase.HeaderPullingListener(){

        @Override
        public void onHeaderPulling(int orientation, int scrollDistance) {
            long currentTime = System.currentTimeMillis();
            long diff = currentTime - lastDelayTime;
            if(mallLayoutHasHide && !isAnimationPlaying && diff >= ANIMATIONS_MIN_DELAY){
                forAnimation.startAnimation(showAnimation);
                lastDelayTime = System.currentTimeMillis();
                mallLayoutHasHide = false;
            }
        }
        
    };

    ...

    // 添加
    mPullRefreshListView.setOnHeaderPullingListener(listener);
        
```



---

![Screenshot](https://github.com/chrisbanes/Android-PullToRefresh/raw/master/header_graphic.png)

This project aims to provide a reusable Pull to Refresh widget for Android. It was originally based on Johan Nilsson's [library](https://github.com/johannilsson/android-pulltorefresh) (mainly for graphics, strings and animations), but these have been replaced since.

## Features

 * Supports both Pulling Down from the top, and Pulling Up from the bottom (or even both).
 * Animated Scrolling for all devices.
 * Over Scroll supports for devices on Android v2.3+.
 * Currently works with:
 	* **ListView**
 	* **ExpandableListView**
 	* **GridView**
 	* **WebView**
 	* **ScrollView**
 	* **HorizontalScrollView**
 	* **ViewPager**
 * Integrated End of List Listener for use of detecting when the user has scrolled to the bottom.
 * Maven Support.
 * Indicators to show the user when a Pull-to-Refresh is available.
 * Support for **ListFragment**!
 * Lots of [Customisation](https://github.com/chrisbanes/Android-PullToRefresh/wiki/Customisation) options!

Repository at <https://github.com/chrisbanes/Android-PullToRefresh>.

## Sample Application
The sample application (the source is in the repository) has been published onto Google Play for easy access:

[![Get it on Google Play](http://www.android.com/images/brand/get_it_on_play_logo_small.png)](http://play.google.com/store/apps/details?id=com.handmark.pulltorefresh.samples)

## Usage
To begin using the library, please see the [Quick Start Guide](https://github.com/chrisbanes/Android-PullToRefresh/wiki/Quick-Start-Guide) page.

### Customisation
Please see the [Customisation](https://github.com/chrisbanes/Android-PullToRefresh/wiki/Customisation) page for more information on how to change the behaviour and look of the View.

### Pull Up to Refresh
By default this library is set to Pull Down to Refresh, but if you want to allow Pulling Up to Refresh then you can do so. You can even set the View to enable both Pulling Up and Pulling Down using the 'both' setting. See the [Customisation](https://github.com/chrisbanes/Android-PullToRefresh/wiki/Customisation) page for more information on how to set this.

## Apps
Want to see which Apps are already using Android-PullToRefresh? Have a look [here](https://github.com/chrisbanes/Android-PullToRefresh/wiki/Apps). If you have an App which is not on the list, [let me know](http://www.senab.co.uk/contact/).

## Changelog
Please see the new [Changelog](https://github.com/chrisbanes/Android-PullToRefresh/wiki/Changelog) page to see what's recently changed.

## Pull Requests

I will gladly accept pull requests for fixes and feature enhancements but please do them in the dev branch. The master branch is for the latest stable code,  dev is where I try things out before releasing them as stable. Any pull requests that are against master from now on will be closed asking for you to do another pull against dev.

## Acknowledgments

* [Stefano Dacchille](https://github.com/stefanodacchille)
* [Steve Lhomme](https://github.com/robUx4)
* [Maxim Galkin](https://github.com/mgalkin)
* [Scorcher](https://github.com/Scorcher)

----

## 捐助

  开源是一种态度，不是义务。
    
	如果您觉得本开源项目对你有帮助，您可以对作者捐助 1 元以示支持。
	
支付宝捐助地址： [桥下一粒砂](https://me.alipay.com/yoojiachen)

----

## License

    Copyright 2011, 2012 Chris Banes

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
