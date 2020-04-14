
## 安装
```
go mod init fyneDemo
go get fyne.io/fyne
```
## 各种软件包说明
### fyne
1. 用途：提供所有fyne代码中共有的基本定义，包含数据类型和接口

| 命令  | 说明 |
| ------------ | ------------ |
| `fyne.NewSize(200, 400)` | 设置应用的宽高，需配合`widget`使用 |
| `fyne.NewPos(20, 20)` | 设置一个偏移量 |
| `container := fyne.NewContainer(text1, text2, text3)` | 新建一个容器 |

### app
1. 用途：提供用于启动新应用程序的api
2.
| 命令  | 说明  |
| ------------ | ------------ |
| `myApp ：= app.New()` | 新建一个应用  |
| `myWindow := myApp.NewWindow("hello")` | 新建一个窗口 |
| `myWindow.ShowAndRun()` | 显示窗口，并运行，等同于`myWindow.Show()`和`myApp.Run()`，若有第二个窗口，则第二个窗口只可调用`myWindow.Show()`方法 |
| `myWindow.SetContent()` | 给窗口设置内容 |

### widget
1. 用途：提供各种各样的小部件(如按钮、标签等)

|  命令 | 说明  |
| ------------ | ------------ |
| `w.Resize(fyne.NewSize(200, 400))`  | 设置宽高  |
| `widget.NewHyperlink("百度", url)` | 设置一个超链接，需配合`url, _ := url.Parse("http://www.baidu.com")`使用 |
| `content := widget.NewLabel("text")` | 设置一段文字 |
| `content := widget.NewButton("click me", clickFunc())` | 设置一个按钮，`clickFunc()为点击事件后进行的操作` |
| `content := widget.NewButtonWithIcon("Home", theme.HomeIcon(), clickFunc())` | 设置一个带图标的点击按钮 |
| `content := widget.NewVBox()` | 创建一个盒子 |
| `content.Append()` | 追加元素 |
| `input := widget.NewEntry()` | 设置一个输入框 |
| `textArea := widget.NewMultiLineEntry()` | 设置多行输入框 |
| `input.SetPlaceHolder("Enter text...")` | 设置输入框的提示内容 |
| `check := widget.NewCheck("Optional", test()` | 设置复选框 |
| `radio := widget.NewRadio([]string{"Option 1", "Option 2"}, test())` | 设置单选框 |
| `combo := widget.NewSelect([]string{"Option 1", "Option 2"}, test())` | 设置select选择器|
| `progress := widget.NewProgressBar()` | 设置进度条 |
| `progress.SetValue(i)` | 设置进度 |
| `infinite := widget.NewProgressBarInfinite()` | 设置无限进度条 |

设置一个表单
```
form := &widget.Form{
		Items: []*widget.FormItem{ // we can specify items in the constructor
			{"Entry", entry}},
		OnSubmit: func() { // optional, handle form submission
			log.Println("Form submitted:", entry.Text)
			log.Println("multiline:", textArea.Text)
			myWindow.Close()
		},
	}

	// we can also append items
	form.Append("Text", textArea)
```
设置tab栏
```
tabs := widget.NewTabContainer(
   widget.NewTabItem("Tab 1", widget.NewLabel("Hello")),
  widget.NewTabItem("Tab 2", widget.NewLabel("World!")))
tabs.SetTabLocation(widget.TabLocationLeading) // 设置为竖向的tab
```
设置工具栏
```
toolbar := widget.NewToolbar(
		widget.NewToolbarAction(theme.DocumentCreateIcon(), func() {
			log.Println("New document")
		}),
		widget.NewToolbarSeparator(),
		widget.NewToolbarAction(theme.ContentCutIcon(), func() {}),
		widget.NewToolbarAction(theme.ContentCopyIcon(), func() {}),
		widget.NewToolbarAction(theme.ContentPasteIcon(), func() {}),
		widget.NewToolbarSpacer(),
		widget.NewToolbarAction(theme.HelpIcon(), func() {
			log.Println("Display help")
		}),
	)

	content := fyne.NewContainerWithLayout(layout.NewBorderLayout(toolbar, nil, nil, nil),
		toolbar, widget.NewLabel("Content"))
```

### canvas
1. 用途：提供绘图api

| 命令  | 说明  |
| ------------ | ------------ |
| `myCanvas := myWindow.Canvas()`  | 创建一个新画布 |
| `text := canvas.NewText("Text", color.White)`  | 创建白色的文字  |
| `text.TextStyle.Bold = true` | 设置文字的样式  |
| `text2.Move(fyne.NewPos(20, 20))` | 移动文字 |
| `canvas.NewRectangle(color.Black)` | 创建一个矩形 |
| `canvas.NewLine(color.Gray{0x66})` | 创建一条线段 |
| `circle := canvas.NewCircle(color.White)` | 创建一个圆 |
| `canvas.NewImageFromResource(theme.FyneLogo())` | 创建一个图片资源 |
| `myCanvas.SetContent(text)`  | 将文字添加到画布上 |


### dialog
1. 用途：处理弹出框
设置一个询问按钮
```
dialog.NewConfirm("标题", "内容", func(checked bool) {
   fmt.Println("333")
}, myWindow)
```

### layout
1. 用途：提供各种布局使用的容器
设置grid布局
```
    text1 := canvas.NewText("1", color.White)
	text2 := canvas.NewText("2", color.White)
	text3 := canvas.NewText("3", color.White)
	grid := fyne.NewContainerWithLayout(layout.NewGridLayout(2),
		text1, text2, text3)
```
设置`fixed`布局
```
    text1 := canvas.NewText("1", color.White)
	text2 := canvas.NewText("2", color.White)
	text3 := canvas.NewText("3", color.White)
	grid := fyne.NewContainerWithLayout(layout.NewFixedGridLayout(fyne.NewSize(50, 50)),
		text1, text2, text3)
```
设置边界布局
```
    top := canvas.NewText("top bar", color.White)
	left := canvas.NewText("left", color.White)
	middle := canvas.NewText("content", color.White)
	content := fyne.NewContainerWithLayout(layout.NewBorderLayout(top, nil, left, nil),
		top, left, middle)
```
设置表单布局
```
	label1 := canvas.NewText("Label 1", color.Black)
	value1 := canvas.NewText("Value", color.White)
	label2 := canvas.NewText("Label 2", color.Black)
	value2 := canvas.NewText("Something", color.White)
	grid := fyne.NewContainerWithLayout(layout.NewFormLayout(),
		label1, value1, label2, value2)
```
设置居中布局
```
	img := canvas.NewImageFromResource(theme.FyneLogo())
	img.FillMode = canvas.ImageFillOriginal
	text := canvas.NewText("Overlay", color.Black)
	content := fyne.NewContainerWithLayout(layout.NewCenterLayout(),
		img, text)
```
设置占满布局
```
    img := canvas.NewImageFromResource(theme.FyneLogo())
	text := canvas.NewText("Overlay", color.Black)
	content := fyne.NewContainerWithLayout(layout.NewMaxLayout(),
		img, text)
```

### test
1. 用途：测试包



