---
layout: post
music-id:'26135471'
categories: "游戏设计编程"
title:  "Unity-PlayMaker Note3"
date:   2020-07-15 14:05:21 +0800
tags: Unity PlayMaker 
color: '#525252'
cover: '../assets/test.png'
subtitle: 'Ref: Playmaker 101 The Complete Course[Chapter 9]'
---
1. **注意：是触发器，一定要勾选“Is Trigger** <font color=#6495ED size=3 >(Ref.:Chapter 9.18 Enemy Weak Spot)</font> 
      <img src="https://i.loli.net/2020/04/02/HSxkETG6YMt39py.png" style="zoom:100%;" />

2. **Set Is Kinematic：**
      （1）.Kinematic: It's a way for us to use as a rigid body, what apply to an object maybe we don't want to grab to or apply to, like moving a platform or so on.
      （2）. [运动学刚体碰撞体 (Kinematic Rigidbody Collider)](http://docs.manew.com/Components/31.html) 

> > A. 此游戏对象 (GameObject) **包含碰撞体 (Collider)** 和标记有“**为运动学”(IsKinematic)** 的刚体 (Rigidbody)。要移动此游戏对象(GameObject)，请修改其变换组件 (Component)，而不是应用力。它们类似于静态碰撞体 (Static Collider)，但是**更适合于要经常四处移动碰撞体 (Collider) 的情况**。有一些使用此游戏对象 (GameObject)的其他专业方案。 此对象**可以用于通常希望静态碰撞体 (Static Collider) 发送触发器 (Trigger)事件**的情况。因为触发器 (Trigger) 必须附加刚体 (Rigidbody)，所以应添加刚体(Rigidbody)，然后启用“为运动学”(IsKinematic)。这可防止对象脱离物理影响，并使您可以在需要时接收触发器(Trigger) 事件。
> >B.  运动学刚体 (Kinematic Rigidbody) **可以方便地打开和关闭**。这**适合于在以下情况中创建布娃娃**：通常希望角色跟随在动画之后，然后在发生碰撞时（通过爆炸或所选的任何其他事物进行提示）变为布娃娃。发生这种情况时，只需通过脚本将所有运动学刚体 (Kinematic Rigidbody) 转变为普通刚体 (Rigidbody)。
> >C. 如果让刚体 (Rigidbody) 静止下来以便在一段时间内不移动，它们会“入睡”。即，它们在物理更新过程中不会进行计算，因为它们不会前往任何位置。如果将运动学刚体(Kinematic Rigidbody) 从休眠的普通刚体 (Rigidbody) 下边移走，则休眠的刚体 (Rigidbody)将被唤醒并在物理更新中重新准确计算。因此如果您具有许多要四处移动的静态碰撞体 (Static Collider)并且让不同对象正确落到其上，请使用运动学刚体碰撞体 (Kinematic Rigidbody Collider)。

（3）. 用以下 “I Tween Stop”停止 itween add运动命令的时候，Ground enemy还是会因为有rigibody 控件而下落，这时候，可以用 “Set is kinematic”来停止rigibody 控件 【[Chapter 9.21 Pause Scene](http://jonathan-oduffy.thinkific.com/courses/take/playmaker-101-the-complete-course/lessons/232756-chapter-9-21-pause-scene)】：
![enter image description here](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200407210933.png)

3.  **Character Look Direction 角色朝向: [Chapter 9.12 Character Look Direction](http://jonathan-oduffy.thinkific.com/courses/take/playmaker-101-the-complete-course/lessons/232730-chapter-9-12-character-look-direction)**
      （1）.小白色方块 注意取消 Box Collider，因为它不需要有碰撞事件  只是作为朝向面
      （2）.同时取消 RigidBody，否则测试时候，Cube就很快在运动过程中脱离下方小黄色方块而掉落
      ![](https://i.loli.net/2020/04/06/wJmWXzjVNbRlqfs.png)
      ![image-20200407002053401](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200408153425.png)

4. **I Tween Stop函数：可以停止指定的I Tween命令，通过设置ID（变量）来确定指定哪几个itween 函数停止。**
    下面例子，是选择将要停止的Itween add命令，设置他们的ID 为变量id，并在 i tween stop 中引用关联 【[Chapter 9.21 Pause Scene](http://jonathan-oduffy.thinkific.com/courses/take/playmaker-101-the-complete-course/lessons/232756-chapter-9-21-pause-scene)】：
      （1）![image-20200407190224601](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200408152559.png)
      （2）![image-20200407195051175](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200407201352.png)
      （3） 在用 set is kinematic 和 itween stop 把会动的物体设置成，当玩家触碰时就不动，即使停在半空中也不动的全局暂停的状态：
         ![image-20200407220254091](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200407220300.png)

5. **Edit Box Collider:**  通过编辑Box Collider 的大小，从而实现hit enemy头部 的时候，不会误碰他身体的死亡点从而停止游戏 【[Chapter 9.22 Refining Enemy Weak Spot](http://jonathan-oduffy.thinkific.com/courses/take/playmaker-101-the-complete-course/lessons/232766-chapter-9-22-refining-enemy-weak-spot)】   
     ![enter image description here](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200408153853.png)
      ![image-20200408153903093](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200408153904.png)

6. **UGUI system**
   	（1）.打开UGUI 的两种方式
      	- 方法一：![image-20200408161206545](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200408161208.png)
              	- 方法二：![image-20200408161220063](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200408163226.png)
              	- ![image-20200408161551437](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200408163232.png)
                    	打开UGUI panel 后会出现 Canvas-Panel 以及EventSystem   	
               	（2）.**Reference**：区别“[unity 3d中 NGUI和UGUI分别是什么？](https://blog.csdn.net/sinat_23079759/article/details/52868256)”
               	（3）.Canvas-**Panel编辑大小**的时候，注意选择Rect Tool再编辑 
               	- ![enter image description here](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200408163245.png)
                       	- ![!\[image-20200408163255364\](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200408163256.png](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200408163256.png)
                       	- ![image-20200408163305190](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200408163306.png)

7. **PlayMaker uGui Proxy**：It's to listen what is the event.	That's gona be listened, and allow us to pass it from the uGui system and the PlayMaker. It acts as like a middleman.
   	![image-20200408195832485](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200408195834.png)	

8. **EventSystem**: Listen for mouse click, for drag and so on.
       ![image-20200408195455331](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200408195456.png)
       ![image-20200408195719504](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200408195720.png)

9. **Play Maker U Gui Component**: It allow us to add events in the FSM.([Chapter 9.25 Playmaker Button Command](http://jonathan-oduffy.thinkific.com/courses/take/playmaker-101-the-complete-course/lessons/232760-chapter-9-25-playmaker-button-command))
       ![image-Play Maker U Gui Component](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200408185153.png)
       ![image-20200408201425734](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200408201428.png)  
10.   一个可以重新启动关卡的按钮：Drag a proxy, to get it from an event, then add the script onto the button, so that we can listen from click.
        ![image-20200408194625525](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200408194626.png)

11. **Creat a win state** [Chapter 9.26 Loading Next Level or Main Menu](http://jonathan-oduffy.thinkific.com/courses/take/playmaker-101-the-complete-course/lessons/232743-chapter-9-26-loading-next-level-or-main-menu)
    （1）.  先用UGUI用Load Level Num 命令选择这一关赢了之后触发的下一个关卡
        ![image-20200408210551612](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200408210552.png)
         （2）.也可以用Load Level，但是选择Load Level Num 可以选关
         ![image-20200408210616890](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200408210618.png)
         （3）.注意：最后保存scene，然后进入 build Settings中把所有Scenes放入 Scenes in build里面
         ![image-20200408210915952](https://raw.githubusercontent.com/YDTRINLEY/PicGo/master/img/20200408210917.png)

