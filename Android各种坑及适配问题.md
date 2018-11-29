1、布局背景设置为白色，却运行时有时显示白色，有时候为透明色

在布局中多个控件同时使用一个资源的时候，这些控件会共用一个状态，例如ColorState，如果你改变了一个控件的状态，其他的控件都会接收到相同的通知。这时我们可以使用mutate()方法使该控件状态不定，这样不定状态的控件就不会共享自己的状态了。 

解决：在全文中更改透明度的操作统一由`myLinearLayout.getBackground().setAlpha(255);更改为`myLinearLayout.getBackground().mutate().setAlpha(255);`

