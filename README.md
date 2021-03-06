# About
Android开关按钮

# Gradle
[![](https://jitpack.io/v/zj565061763/switchbutton.svg)](https://jitpack.io/#zj565061763/switchbutton)

# 默认效果
![](http://thumbsnap.com/i/KBISOucv.gif?0705)

## 覆盖全局默认效果
支持覆盖的默认配置：<br>
* colors <br>
可以在项目中定义colors覆盖库中的默认配置<br>
```xml
<!-- 正常view颜色 -->
<color name="lib_sb_color_normal_view">#E3E3E3</color>
<!-- 正常view边框颜色 -->
<color name="lib_sb_stroke_color_normal_view">#D2D2D2</color>

<!-- 选中view颜色 -->
<color name="lib_sb_color_checked_view">#4AD863</color>
<!-- 选中view边框颜色 -->
<color name="lib_sb_stroke_color_checked_view">@color/lib_sb_color_checked_view</color>

<!-- 手柄view颜色 -->
<color name="lib_sb_color_thumb_view">#FFFFFF</color>
<!-- 手柄view边框颜色 -->
<color name="lib_sb_stroke_color_thumb_view">#D2D2D2</color>
```
* dimens <br>
可以在项目中定义dimens覆盖库中的默认配置<br>
```xml
<!-- 圆角半径 -->
<dimen name="lib_sb_corner">50dp</dimen>
<!-- 手柄view上下左右间距 -->
<dimen name="lib_sb_margins">1dp</dimen>
<!-- 正常view边框大小 -->
<dimen name="lib_sb_stroke_width_normal_view">1px</dimen>
<!-- 选中view边框大小 -->
<dimen name="lib_sb_stroke_width_checked_view">1px</dimen>
<!-- 手柄view边框大小 -->
<dimen name="lib_sb_stroke_width_thumb_view">1px</dimen>
```
* drawable <br>
可以在项目中定义drawable覆盖库中的默认配置，覆盖drawable后以上的colors和dimens设置失效<br>
![](http://thumbsnap.com/i/vErZPQhN.png?0706)<br>

# xml属性
支持的xml属性配置：<br>
```xml
<declare-styleable name="LibSwitchButton">
    <!-- 正常view图片 -->
    <attr name="sbImageNormal" format="reference"/>
    <!-- 选中view图片 -->
    <attr name="sbImageChecked" format="reference"/>
    <!-- 手柄view图片 -->
    <attr name="sbImageThumb" format="reference"/>
    <!-- 是否选中 -->
    <attr name="sbIsChecked" format="boolean"/>
    <!-- 手柄view上下左右间距 -->
    <attr name="sbMargins" format="dimension"/>
    <!-- 手柄view左边间距 -->
    <attr name="sbMarginLeft" format="dimension"/>
    <!-- 手柄view顶部间距 -->
    <attr name="sbMarginTop" format="dimension"/>
    <!-- 手柄view右边间距 -->
    <attr name="sbMarginRight" format="dimension"/>
    <!-- 手柄view底部间距 -->
    <attr name="sbMarginBottom" format="dimension"/>
    <!-- 是否需要点击切换动画 -->
    <attr name="sbIsNeedToggleAnim" format="boolean"/>
</declare-styleable>
```

# 自定义效果
![](http://thumbsnap.com/i/YS9spIQs.gif?0706)<br>
1. xml中布局：<br>
```xml
<com.sd.lib.switchbutton.FSwitchButton
    android:id="@+id/sb_rect"
    android:layout_width="50dp"
    android:layout_height="25dp"
    android:layout_marginTop="10dp"
    app:sbImageChecked="@drawable/layer_checked_view"
    app:sbImageNormal="@drawable/layer_normal_view"
    app:sbImageThumb="@drawable/layer_thumb_view"
    app:sbIsChecked="true"
    app:sbMarginBottom="2dp"
    app:sbMarginLeft="0dp"
    app:sbMarginRight="2dp"
    app:sbMarginTop="2dp"/>
```
2. java文件中：<br>
```java
sb_rect.setOnViewPositionChangeCallback(new SwitchButton.OnViewPositionChangeCallback()
{
    @Override
    public void onViewPositionChanged(SwitchButton view)
    {
        float percent = view.getScrollPercent() * 0.8f + 0.2f;
        ViewCompat.setScaleY(view.getViewNormal(), percent);
        ViewCompat.setScaleY(view.getViewChecked(), percent);
    }
});
```

# SwitchButton接口
```java
public interface SwitchButton
{
    /**
     * 是否处于选中状态
     *
     * @return
     */
    boolean isChecked();

    /**
     * 设置选中状态
     *
     * @param checked        true-选中，false-未选中
     * @param anim           是否需要动画
     * @param notifyCallback 是否需要通知回调
     * @return true-调用此方法后状态发生了变化
     */
    boolean setChecked(boolean checked, boolean anim, boolean notifyCallback);

    /**
     * 切换选中状态
     *
     * @param anim           是否需要动画
     * @param notifyCallback 是否需要通知回调
     */
    void toggleChecked(boolean anim, boolean notifyCallback);

    /**
     * 设置选中变化回调
     *
     * @param onCheckedChangeCallback
     */
    void setOnCheckedChangeCallback(OnCheckedChangeCallback onCheckedChangeCallback);

    /**
     * 设置手柄view位置变化回调
     *
     * @param onViewPositionChangeCallback
     */
    void setOnViewPositionChangeCallback(OnViewPositionChangeCallback onViewPositionChangeCallback);

    /**
     * 获得滚动的百分比[0-1]
     *
     * @return
     */
    float getScrollPercent();

    /**
     * 返回正常状态view
     *
     * @return
     */
    View getViewNormal();

    /**
     * 返回选中状态view
     *
     * @return
     */
    View getViewChecked();

    /**
     * 返回手柄view
     *
     * @return
     */
    View getViewThumb();

    interface OnCheckedChangeCallback
    {
        /**
         * 选中状态变化回调
         *
         * @param checked
         * @param view
         */
        void onCheckedChanged(boolean checked, SwitchButton view);
    }

    interface OnViewPositionChangeCallback
    {
        /**
         * 手柄view滚动回调
         *
         * @param view
         */
        void onViewPositionChanged(SwitchButton view);
    }
}
```
