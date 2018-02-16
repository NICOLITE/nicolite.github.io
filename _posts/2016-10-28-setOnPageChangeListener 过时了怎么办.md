---
title: setOnPageChangeListener 过时了怎么办？
date: 2016-10-24 17:46:15
categories:
- Android
tags: 
---
<h2>今天使用ViewPager发现setOnPageChangeListener的方法居然过期了，而且AS编译不通过了，最后查了一下原来把set换成add了，代码如下：</h2>

<h3>setOnPageChangeListener</h3>

<pre class="prettyprint linenums" >
mViewPager.setOnPageChangeListener(new ViewPager.OnPageChangeListener() {
@Override
public void onPageScrolled(int position, float positionOffset, int positionOffsetPixels) {

}

@Override
public void onPageSelected(int position) {

}

@Override
public void onPageScrollStateChanged(int state) {

}
});
</pre>

<h3>addOnPageChangeListener</h3>

<pre class="prettyprint linenums" >
mViewPager.addOnPageChangeListener(new ViewPager.OnPageChangeListener() {
@Override
public void onPageScrolled(int position, float positionOffset, int positionOffsetPixels) {

}

@Override
public void onPageSelected(int position) {
    selectedTab(position);
}

@Override
public void onPageScrollStateChanged(int state) {

}
});
</pre>