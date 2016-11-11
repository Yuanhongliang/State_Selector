##仿QQ消息/电话状态切换##

公司项目有这样一个需求，跟QQ消息/电话切换的功能类似，网上看了许多，没有几个是自己特别满意的。要么是点击的时候字颜色不变，要么是弄几个selector来回切换，看得头疼，还是自己来弄一个吧。先上图：
![](screenshots/screenshot.gif)


看起来跟QQ的没什么区别了，有需要圆角的同学再自己处理一下，很简单的。
下面是我的思路：

  -  用两个RadioButton代替button(利用checked属性)
  -  掌握操作时的3种状态 选中 未选中 和 未选中时点击
  -  写出背景的selector和字体的selector


背景selector：

		<?xml version="1.0" encoding="utf-8" ?>
		<selector xmlns:android="http://schemas.android.com/apk/res/android">
	
		    <item android:state_checked="true">
		        <shape android:shape="rectangle">
		            <solid android:color="@color/colorWhite" />
		        </shape>
		    </item>
		    <item android:state_checked="false" android:state_pressed="true">
		        <shape android:shape="rectangle">
		            <solid android:color="@color/colorWhite" />
		        </shape>
		    </item>
		    <item android:state_checked="false">
		        <shape android:shape="rectangle">
		            <stroke android:width="1dp" android:color="@color/colorWhite" />
		            <solid android:color="@color/colorAccent" />
		        </shape>
		    </item>
		</selector>
字体selector:
	
	<?xml version="1.0" encoding="utf-8"?>
	<selector xmlns:android="http://schemas.android.com/apk/res/android">
    	<item android:color="@color/colorAccent" android:state_checked="true" />
    	<item android:color="@color/colorAccent" android:state_checked="false" android:state_pressed="true" />
    	<item android:color="@color/colorWhite" android:state_checked="false" />
	</selector>
在布局中引用：

 		<RadioGroup
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:orientation="horizontal">

            <RadioButton
                android:id="@+id/message"
                android:layout_width="0dp"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:background="@drawable/radio_selector"
                android:button="@null"
                android:checked="true"
                android:gravity="center"
                android:text="消息"
                android:textColor="@drawable/text_selector" />

            <RadioButton
                android:id="@+id/phone"
                android:layout_width="0dp"
                android:layout_height="match_parent"
                android:layout_weight="1"
                android:background="@drawable/radio_selector"
                android:button="@null"
                android:checked="false"
                android:gravity="center"
                android:text="电话"
                android:textColor="@drawable/text_selector" />
        </RadioGroup>
-----
这时候就大功告成啦，几个值得记下来的点：

 - 字体颜色的selector不能用android:drawable，用android:color（没有提示的，很坑）
 - RadioButton不让其显示选中状态的圈 android:button="@null"
 - 没了。希望能帮到大家

