---
title: Android可设置miniHight和miniWidth的webview
date:  2018-06-02 11:04:30
categories:
- Android
tags:
- Android
- webview
---
在使用webview时发现不能设置miniHeight，就算再layout里面设置了miniHeight属性也没有效果。  
一种解决方法就是在webview外层包裹一个FrameLayout,然后未FrameLayout设置miniHeight，这样做虽然可以，但是View的层次被加深了，影响性能。  


```kotlin
/**
 * Created by nicolite on 2018/5/20.
 * email nicolite@nicolite.cn
 * 能设置miniHeight，maxHeight，miniWidth，maxWidth的WebView
 */
class MMWebView : WebView {
    private var miniHeight = -1
    private var maxHeight = -1
    private var miniWidth = -1
    private var maxWidth = -1

    constructor(context: Context) : super(context)
    constructor(context: Context?, attrs: AttributeSet?) : super(context, attrs)
    constructor(context: Context?, attrs: AttributeSet?, defStyleAttr: Int) : super(context, attrs, defStyleAttr)

    fun setMiniHeight(miniHeight: Int) {
        this.miniHeight = miniHeight
    }

    fun setMaxHeight(maxHeight: Int) {
        this.maxHeight = maxHeight
    }

    fun setMiniWidth(miniWidth: Int) {
        this.miniWidth = miniWidth
    }

    fun setMaxWidth(maxWidth: Int) {
        this.maxWidth = maxWidth
    }

    override fun onMeasure(widthMeasureSpec: Int, heightMeasureSpec: Int) {
        super.onMeasure(widthMeasureSpec, heightMeasureSpec)
        var height = measuredHeight
        var width = measuredWidth

        if (miniHeight > -1 && maxHeight > -1) {
            if (miniHeight < maxHeight) {
                if (maxHeight < measuredHeight) {
                    height = maxHeight
                } else if (miniHeight > measuredHeight) {
                    height = miniHeight
                }
            } else if (maxHeight < measuredHeight) {
                height = maxHeight
            }
        } else if (miniHeight > -1) {
            if (miniHeight > measuredHeight) {
                height = miniHeight
            }
        } else if (maxHeight > -1) {
            if (maxHeight < measuredHeight) {
                height = maxHeight
            }
        }

        if (miniWidth > -1 && maxWidth > -1) {
            if (miniWidth < maxWidth) {
                if (maxWidth < measuredWidth) {
                    width = maxWidth
                } else if (miniWidth > measuredWidth) {
                    width = miniWidth
                }
            } else if (miniWidth > measuredWidth) {
                width = maxWidth
            }
        } else if (miniWidth > -1) {
            width = miniWidth
        } else if (maxWidth > -1) {
            width = maxWidth
        }

        setMeasuredDimension(width, height)
    }

}
```