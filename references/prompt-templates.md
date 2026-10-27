# 提示词模板

以下模板使用变量，不提供固定尺寸、时长或镜头数量。将花括号内容替换为用户输入或上游规格。

## 文生图

```text
{主体与关系}位于{场景}，正在{清晰可读的日常动作}，情绪为{情绪}。采用原创温馨日常像素风：{正交俯视或轻微斜俯视}，稳定像素密度，网格化瓦片环境，分层组织地表、道路、围栏、建筑、家具与植被，小型角色精灵以{比例与轮廓锚点}保持识别。{季节}的色彩关系，{时段/天气}，主光源来自{可定位的环境实用光源}，有限色阶，硬边像素簇，成块高光与阴影，局部抖色表现纹理。构图为{景别与主体位置}，保留{可行走留白或文字区域}，加入{生活化物件与叙事细节}。所有角色、地点、道具、标志、文字、界面与图标均为原创。输出规格严格采用{用户或上游 output_spec}。
```

负面提示词：

```text
photorealistic, semi-realistic, 3D render, vector art, smooth gradient, anti-aliasing, glossy material, cinematic depth of field, bokeh, motion blur, noisy pixel filter, melted outlines, inconsistent pixel scale, perspective drift, deformed hands, extra people, duplicated props, unrelated modern UI, unreadable text, copyrighted character, recognizable franchise location, brand logo, copied game interface, signature icon, proprietary symbol
```

## 图生图

```text
参考职责：{逐一说明 reference_id 负责身份、服装、场景、构图或通用风格规则中的哪一项}。
将画面完整重绘为原创温馨日常像素风，而不是叠加像素滤镜。
必须保留：{身份识别线索、人数、主体关系、主要姿态、构图、关键道具、需要保留的背景结构或用户文字}。
允许改变：将写实材质、光影和背景细节重构为{正交俯视或轻微斜俯视}的网格瓦片世界；角色转为小型精灵比例，以发型轮廓、服装主色和配饰维持识别；环境转为分层的道路、围栏、建筑、树木、作物、家具与生活化场景模块。
重绘规则：统一{像素密度}，使用有限色阶、硬边像素簇、成块阴影和局部抖色；主光源为{可定位的环境实用光源}，像素光晕分层成块。重新设计所有可能对应既有作品的角色、地点、建筑、道具、标志、文字、界面、图标与标志性物件，保持主题功能但不复制专有设计。输出规格严格采用{用户或上游 output_spec}。
```

多人图片要为每个人建立稳定锚点，例如“角色 A：短卷发、蓝色外套、黄色背包；角色 B：长直发、红色围巾、白色裙装”。后续提示词逐字复用这些锚点。

## 风格基准图

```text
建立本项目的原创温馨日常像素风基准：{主题场景与主体}。锁定{像素密度}、正交或轻微斜俯视、角色比例、轮廓粗细、地图层级、场景模块、季节性色彩关系、环境实用光源、阴影色阶、植被形态和离散像素特效。画面优先展示{最重要的角色与场景元素}，保留清楚的可行走留白与生活化物件，避免无关风格变体。不得出现可识别的专有角色、地点、标志、文字、界面、图标或标志性物件。输出规格采用{output_spec}。
```

## 图生视频 / 文生视频单镜头

```text
参考职责：{逐一说明 reference_id 负责身份、服装、场景、构图或通用风格规则中的哪一项}。
起始状态：{角色位置、朝向、姿势、道具、环境与光线}。
主体动作：角色以清晰的精灵动画节拍完成{准备动作}→{主要动作}→{结果动作}→{短暂停顿}；轮廓始终可读，身份、服装与道具不改变。
环境响应：{作物/树叶/水面/动物/门窗/灯光}以短循环像素帧产生{响应}。
镜头运动：{静止、横向跟随、纵向跟随、缓慢推进、分层平移或用户指定运动}，保持正交俯视或轻微斜俯视，不产生写实透视漂移。
像素特效：使用{离散星点、十字闪光、原创几何符号、像素环、雨线、雪片、落叶、烟团、脚步尘点等}，粒子沿像素网格移动，边缘硬朗，无连续体积雾。
结束状态：{角色与场景最终位置}，为{下一镜头或循环}保留连续性。
风格锁定：原创温馨日常像素风，稳定像素密度，网格瓦片环境，小型角色精灵，有限色阶，硬边像素簇，成块阴影、局部抖色、季节性色彩关系、环境实用光源、生活化物件和可行走留白。
原创约束：不复制任何既有作品的专有角色、地点、建筑、道具、标志、文字、界面、图标或标志性物件。
时长、画幅、分辨率、帧率：严格继承{用户或上游 output_spec}。
```

视频负面提示词：

```text
no photorealism, no semi-realism, no 3D depth drift, no smooth vector edges, no anti-aliasing, no motion blur, no depth-of-field blur, no frame interpolation wobble, no half-pixel jitter, no melting sprites, no color relationship shift, no changing clothes, no identity drift, no extra limbs, no duplicated characters, no unrelated modern UI, no subtitles unless explicitly requested, no copyrighted character, no recognizable franchise location, no brand logo, no copied game interface, no signature icon, no proprietary symbol
```

## 多镜头连续性块

把以下块附加到每个镜头，只有剧情明确变化时才修改：

```yaml
continuity_lock:
  character_anchor: "{发型、服装、肤色、配饰、角色比例、朝向规则}"
  scene_anchor: "{地面瓦片、建筑、围栏、路径、家具、固定物件位置}"
  color_anchor: "{季节主色关系、阴影色关系、强调色、夜景或室内光色}"
  light_anchor: "{可定位主光源、方向、强度与时段}"
  pixel_anchor: "{像素密度、轮廓粗细、色阶与抖色方式}"
  camera_anchor: "{视角、景别、机位、路径与结束构图}"
  motion_anchor: "{动作节拍、循环方式、环境响应与结束状态}"
  prop_anchor: "{关键道具外形、颜色、持握方式}"
```

## 动作与特效搭配示例

浇水：角色抬壶、前倾、倾倒、回正；水流使用断续蓝色像素弧，落地后土壤瓦片整体变深并出现少量高光。

收获：角色蹲下或伸手、作物轻弹、原创收获物图形被举起、离散星点短暂闪烁；不要表现写实拔根和复杂布料摆动。

行走或骑行：采用规律摆臂或蹬踏循环，地面出现少量尘点，背景前后层轻微差速平移；禁止运动模糊。

拥抱或团聚：角色先转向、靠近、轮廓短暂重叠、轻微弹跳或出现原创几何情绪符号；避免写实肢体缠绕。

幻想时刻：主体保持稳定，周围出现离散星点、十字闪光与扩散像素环，环境亮度按整块色阶短暂提升后恢复。
