# Typora - Markdown编辑工具

## 1. 调整源码编辑区域宽度

Typora的源码编辑宽度很窄，可能是为了照顾老用户？只有800px，对当前流行电脑的分辨率来说，实在是太窄了，工作起来也非常别扭。

- 在 `C:\Program Files\Typora\resources\app\style\` 下，找到 `base-control.css` 文件；

  最新版本已经修改为 `C:\Program Files\Typora\resources\style` 的目录下，找不到的话，可以直接搜索该文件。

- 打开后搜索 `#typora-source` 更改其最大宽度 `max-width` 为`1200` ，不过设置文件中有多处 `max-width` ，应该是第三个的位置？原始数值是`800` ；

  懒惰的话，可以直接搜索 `padding-right:30px;max-width:` ，这个项目只有 1 个，找起来很方便。
  
  修改的情况如图所示：
  
  ![Typora 更改编辑器的宽度](https://www.likecs.com/default/index/img?u=L2RlZmF1bHQvaW5kZXgvaW1nP3U9YUhSMGNITTZMeTl3YVdGdWMyaGxiaTVqYjIwdmFXMWhaMlZ6THpFek9DOWtaREEyT0RSaU1USTBZMkZsWkRVNVlUVm1NV0kyWWpCaFpEQTFabUpoWVM1d2JtYz0=)
  
  

## 2. 修改编辑器（主题） 的宽度

这个编辑宽度也可能是为了照顾所有的显示器，编辑宽度显得比较局促。

- 普通编辑器的配置文件 并不在 Typora 的安装目录， 是在 `C:\Users\Administrator\AppData\Roaming\Typora\themes` 目录下；

  ※`Administrator`是电脑当前的用户名，按照自己的实际用户名替换该字符。

- 主题有 github.css、newsprint.css、night.css、pixyll.css、whitey.css 。

  选择使用主题的css文件，搜索 `#write` ，修改其属性 `max-width` 为 `1060px` 。所图所示：

  ![Typora 更改编辑器的宽度](https://www.likecs.com/default/index/img?u=L2RlZmF1bHQvaW5kZXgvaW1nP3U9YUhSMGNITTZMeTl3YVdGdWMyaGxiaTVqYjIwdmFXMWhaMlZ6THpReE5pOHdNbU00TjJFeU1UVTJOamd4WVdSa09HTXlZamRtWlRreE9EWXlPVFV6TUM1d2JtYz0=)

  现在大家的屏幕宽度至少都是 1920 ，应该是修改下面的区域的数据：

  ```
  @media only screen and (min-width: 1800px) {
  	#write {
  		max-width: 1200px;
  	}
  }
  ```

  如果不想用像素 1200px ，可以设置为 `90%` 的比例数据；考虑到个人一直会在左侧显示大纲内容，用比例方式是更为合适的。