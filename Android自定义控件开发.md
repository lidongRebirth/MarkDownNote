#第一章	绘图基础
###1、Paint画笔
* `void setColor(int color);`		设置颜色
	 `void setStyle(Style style);`		设置风格
```java
包含：Paint.Style.FILL/FILL_AND_STROKE/STROKE		仅填充内部、内部和描边、描边
```
* `void setStrokeWidth(float width);`	设置描边宽度
* `void setAntiAlias(boolean a)`		设置抗锯齿功能，可以让边缘更平滑
* 