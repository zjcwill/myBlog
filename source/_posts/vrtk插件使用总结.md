layout: unity
title: vrtk插件使用总结
date: 2017-04-20 8:26:42
tags: unity vrtk
---
在哈航科技项目中使用VRTK的心得和难点
<!--more-->
## 初始化对象:
     CameraRig
     创建空的对象，命名`VRTK`，给对象添加`VRTK_SDK_Manager`
     VRTK下创建子类空物体，命名左右手,然后将空左右手连接到`Vrtk`中
     给左右手添加`VRTK_Contrallor_Event`(监听控制器的交互)
     VRTK中创建空物体命名`PlayArea`并为其添加`basic Templot`
***
## 人物移动
所有的交互都是通过`VRTK_Contrallor_Event`进行反馈
1. 需要给控制器添加`VRTK_Pointer`
2. 控制器模型下面创建一个空物体，拖入需要的射线渲染器脚本（如`strightRender`）；
3. `PlayArea`里面添加传送器脚本如：`basic Teleport`
`Teleport`有三种模式，除了`Basic Teleport` 不能进行高度传送，其他的都可以
***
## 交互系统 （如抓取，碰撞，触摸）
抓取系统：
控制器上需要挂载
`interact Touch`  触摸
`interact Action` 不必要
`Interact Grabs` 抓取
`interact Use` 不必要
`swap_contrallor_grab_action` 这个脚本是用来控制手柄承载物体。物体可以在两个手柄中传递。
对象上面挂载
`VRTK_Interactable Object`  参数isgrab开启
`rigidity`刚体组件 
***
## 用户体验细节
`PlayArea`添加
`vrtk__headset collision` 给头部加一个碰撞体
`vrtk__headset fade`
`vrtk__headset collision fade` 当人物超出安全范围会有颜色的警示，并且有逐渐进入的过程

VRTK中有一个`RadioMenu`预制体，可以通过控制器的触摸板控制一些UI组件
使用方法：直接将预制体拖入到控制器中当作孩子。可以调整大小和方向
也可以将预制体挂载到对象上面，当控制器碰到对象后会显示出`RadioMeun`。（需要给对象和控制器添加一定的交互脚本）。给`RadioMeun`中的`panel`面板添加`VRTK_Independent_Radio_Meun`组件。和`Radio Menu`组件。

`VRTK_OutLine Object Copy Hightlight `
`VRTK_Controller Apperance_Example`
这两个脚本控制控制器的样式，当控制器碰到对象，控制器的body和外边缘会产生颜色的变化
***
## 开启可玩区域碰撞体，使玩家始终在合理位置
搭配贝尔曲线传送器使用
`VRTK_Bezier pointer renderer`
把`play area cursor`挂的物体附上去
nav渲染下可以移动的地方
demo16 模拟触发手柄震动
demo 17 使用触控板模拟人物运动
***
## 可交互物体触碰执行
给需要交互的物体添加脚本：
`VRTK interactable  object`
`VRTK__Button `
控制器需要的脚本同上面的交互事件。
所执行的方法：
`defalut`事件是触摸就执行脚本
`on push`事件是移动物体到指定距离执行脚本
还可以使用`unity event`事件移动完成后执行脚本 同`on pushed`
***
## UICanvas交互
创建一个`Canvas`，给其添加 `VRTK_UICanvas`
给控制器添加`VRTK_UIPointer` 、`VRTK_Pointer`（给其指定渲染器）
这样就可以通过控制器射线来交互UI元素

___UI元素拖拽___
给UI元素添加脚本`UI_Draggable Item` 脚本
操作方法：先用射线指定要拖拽的元素，然后按住`Trigger`键进行拖拽，拖拽过程中射线不能停止，到指定地点后再松开`Trigger`
`blink transition speed` 眨眼过渡速度
