# Easy Hit Collision Plugin

## 1. 从Fab市场下载插件后，在UE插件栏下搜索 "Easy Hit Collision System"，勾选后，再搜索 State Tree，启用UE自带的状态树插件，重启UE。

<img src="./IMG/1.png">

## 2. 按图片的标记顺序进行设置！--添加自定义碰撞通道
    1.点击项目设置里的碰撞
    2.添加一个新的Trace Channel,默认为忽略。
   
<img src="./IMG/2.png">

## 3. 给武器添加插槽--静态网格体或骨骼网格体均可。
    1.右键选择根树，添加插槽。至少添加2个插槽。
    **可以为武器添加多段插槽，如果武器非弯曲度高的武器，建议都只添加两个插槽。
    **角色上添加的Easy Hit Collision 可以设置多个分段，所以没必要在这里添加非常多的插槽。

<img src="./IMG/3.png">

## 4. 按图片的标记顺序进行设置！--组件功能设置
    1. 在你的角色蓝图，点击添加组件（Add），搜索Easy Hit Collision
    2.点击组件 Easy Hit Collision
    3.选择我们上面新建的  检测通道
    4.选择 以线条模式检测，还是以合体模式检测。
    5.添前面在武器上添加的槽名称，顺序一定要和武器上添加的插槽一致。
    其它功能设置保持默认即可。或者自行摸索。
    **注意：本插件本来是写给我自己的项目用的，由于我的游戏项目没双武器，所以我留了双武器功能的接口，但并没有实现双武器功能。所以武器类型，你目前只能选择单武器。

<img src="./IMG/4.jpg">

## 5. 按图片的标记顺序进行设置！--状态树设置
    1.在你的角色蓝图，点击添加组件（Add），搜索 State Tree Component (注意：不要选择AI State Tree)
    2.点击添加进角色的State Tree
    3.在状态树的细节面板，点击选择状态树资产.
    (下来款找不到StateTree_EasyHitCollision时，执行4.5操作)
    6.选择状态树 StateTree_EasyHitCollision.

<img src="./IMG/5.jpg">

## 6. 按图片的标记顺序进行设置！--动画蒙太奇通知设置<必选>

    1.在玩家角色攻击动画蒙太奇中，选一个轨道，鼠标右键选择蒙太奇状态通知，找到AnimNotify_HitCollision.
    调整需要开始检测碰撞和结束结束检测的位置。
    可以设置一下动画通知的名称，Easy Hit Collision 组件会返回 动画通知名称，这样你就可以对不同动画做出不同的逻辑。

<img src="./IMG/7.png">

## 7. 按图片的标记顺序进行设置！--动画蒙太奇通知设置<额外项，非必选>

    1.这是插件额外带的卡帧功能，只需简单的添加动画状态通知AnimNotify_FrameFrop.
    2.细节面板中勾选你想要的模式即可。
    **模式1** --Frame Rate Down: 命中->减速->持续时间->恢复到默认速率（Default Rate）
    **模式2** --Frame Rate Up: 命中->停止->持续时间->加速到默认速率 （Default Rate）

    游戏中可以通过，拖出Easy Hit Collision 找到下面的函数之一来设置开启或关闭！ 
    PrimaryManualSetFrameDrop函数，同时设置两种模式的开启或关闭。
    PrimaryManualSetFrameDropDown函数，设置模式1的开启或关闭。
    PrimaryManualSetFrameDropUp函数，设置模式2的开启或关闭。

<img src="./IMG/New.jpg">

## 8. 按图片的标记顺序进行设置！--注册武器设置
    1.打玩家开角色蓝图，在Event Game Begin 后，拖出Easy Hit Collison 组件，找到 Register Weapon Mesh Component.
    2.从Weapon Skeletal Mesh Comps拖出，创建数组（Make Array）。**注意：这里可以传入骨骼网格体或静态网格体，我这里输入参数命名没修正。**
    3.将你得武器组件传入上去。

<img src="./IMG/8.png">

## 9. 按图片的标记顺序进行设置！--敌人蓝图设置
    1.将敌人蓝图的碰撞预设，改为自定义.
    2.找到我们之前在项目设置里添加的自定义通道。将它勾选为阻挡。

<img src="./IMG/9.png">

## 10. 打开玩家角色蓝图。--完成了所有设置

    1.选择Easy Hit Collision 组件，在细节面板，有碰撞返回的事件。
    On Trace Started--蒙太奇播放时，动画通知AnimNotify_HitCollision开始时执行，无论有没有碰撞到敌人。
    On Trace Ended--蒙太奇播放时，动画通知AnimNotify_HitCollision结束时执行，无论有没有碰撞到敌人。
    On Unique Hit--仅碰到第一个敌人时，执行此事件。
    On Hit--每碰到一个不同敌人时，都会执行此事件。
    
    ---当Easy Hit Collision 组件中 Trace hit Mode 设置为“Single”时，用 On Unique Hit 或 On Hit 都一样。

<img src="./IMG/10.png">