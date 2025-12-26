# cardFrameS - Godot卡牌游戏框架

一个基于Godot 4.4引擎开发的太空题材卡牌资源管理游戏框架。

## 项目概述

这个项目主要完成了一个完整的卡牌游戏框架，玩家在太空环境中通过收集、管理各类卡牌（矿石、物品、NPC、地点等）来推进游戏进程。项目提供了完整的卡牌系统、背包管理、对话系统和存档功能。

## 核心功能

### 1. 卡牌系统 (Card System)
- **卡牌类型**：
  - 普通物品卡（item）：冰、石头、各类金属等
  - 矿石卡（ore）：铁矿、硅矿、金矿等可加工资源
  - 地点卡（site）：可进入的场景位置
  - NPC卡（npc）：可互动的角色
  - 商店卡（shop）：购买物品的商人
  
- **卡牌特性**：
  - 重量系统：每张卡牌都有重量属性
  - 堆叠机制：同类卡牌可以堆叠，节省空间
  - 拖拽交互：流畅的物理效果拖拽系统
  - 视觉反馈：卡牌移动、堆叠有丰富的动画效果

### 2. 背包管理系统 (Deck Management)
- **重量限制**：背包有最大承重限制，需要合理分配空间
- **多个背包**：支持手牌、商店背包等多个独立背包
- **自动排序**：卡牌根据位置自动排序
- **实时更新**：重量和容量实时显示
- **拖拽管理**：在不同背包间自由拖拽卡牌

### 3. 互动系统
- **NPC对话**：
  - 集成Dialogue Manager插件
  - 支持多分支对话
  - 角色展开动画效果
  
- **商店系统**：
  - 商人卡牌可展开为商店界面
  - 动态价格系统（基于价格比率）
  - 购买物品添加到背包
  
- **场景切换**：
  - 地点卡可以进入新场景
  - 自动保存当前状态
  - 场景间无缝切换

### 4. 存档系统 (Save System)
- **自动存档**：场景切换时自动保存
- **玩家数据**：
  - 金钱、生命值、背包容量
  - 玩家名称、所在星球和位置
  - 配方列表等游戏进度
- **背包持久化**：所有背包内容完整保存
- **继续游戏**：支持加载已有存档

### 5. 数据驱动架构
- **CSV配置**：所有卡牌数据存储在`cardsInfo.csv`
- **灵活扩展**：新增卡牌只需编辑CSV文件
- **多语言支持**：卡牌名称、描述支持翻译
- **动态加载**：运行时从CSV读取并生成卡牌

## 技术特点

### 框架设计
- **模块化架构**：卡牌、背包、对话系统各自独立
- **场景自动加载**：使用Autoload管理全局单例
- **资源序列化**：使用Godot资源系统保存游戏状态
- **组系统**：使用节点组管理可交互对象

### 核心类
- `card`: 基础卡牌类，包含拖拽、堆叠等基础功能
- `siteCard`: 地点卡，可进入场景
- `shopCard`: 商店卡，可展开购买界面
- `npcCard`: NPC卡，可触发对话
- `deck`: 背包类，管理卡牌容器
- `player`: 玩家资源类，保存游戏数据
- `cardInfos`: 卡牌信息管理单例

### 物理效果
- 弹簧阻尼系统实现平滑跟随
- 补间动画实现展开/收起效果
- 视觉反馈增强用户体验

## 项目结构

```
├── cards/              # 卡牌场景和脚本
│   ├── card.gd        # 基础卡牌类
│   ├── site_card.gd   # 地点卡
│   ├── shop_card.gd   # 商店卡
│   └── npc_card.gd    # NPC卡
├── deck/               # 背包系统
│   ├── deck.gd        # 背包基类
│   └── hand_deck.gd   # 手牌背包
├── assets/             # 资源文件
│   ├── cardsInfo.csv  # 卡牌数据配置
│   ├── cardsInfo.gd   # 卡牌信息管理
│   └── balloon.tscn   # 对话气泡
├── data/               # 数据类
│   ├── playerInfo.gd  # 玩家数据类
│   └── deckSavedCards.gd # 背包存档类
├── site/               # 游戏场景
├── dialogue/           # 对话文件
├── cardImg/            # 卡牌图片资源
└── addons/             # 第三方插件
    └── dialogue_manager/ # 对话管理器插件
```

## 使用方法

### 环境要求
- Godot Engine 4.4 或更高版本
- 支持Forward Plus渲染

### 运行游戏
1. 使用Godot编辑器打开项目
2. 主场景将自动加载
3. 点击"新游戏"开始或"继续游戏"加载存档

### 添加新卡牌
1. 在`assets/cardsInfo.csv`中添加新行
2. 填写卡牌属性（名称、类型、重量、价格等）
3. 在`cardImg/`文件夹添加对应图片
4. 游戏将自动识别新卡牌

### 创建新场景
1. 在`site/`文件夹创建新场景文件
2. 在CSV中添加对应的地点卡
3. 卡牌会自动链接到场景

## 游戏玩法

1. **收集卡牌**：从商店或场景中获取各类卡牌
2. **管理背包**：注意重量限制，合理堆叠卡牌
3. **探索世界**：使用地点卡进入不同场景
4. **对话互动**：与NPC对话获取信息或任务
5. **商店交易**：在商人处购买所需物品
6. **资源管理**：收集矿石，加工成有用物品

## 开发计划

- [ ] 完善战斗系统
- [ ] 添加更多NPC和对话分支
- [ ] 扩展物品制造系统
- [ ] 优化UI和视觉效果
- [ ] 添加音效和音乐
- [ ] 多语言完整支持

## 技术栈

- **引擎**: Godot 4.4
- **语言**: GDScript
- **插件**: Dialogue Manager
- **分辨率**: 1920x1080
- **渲染**: Forward Plus

## 许可证

详见 LICENSE 文件

---

## English Version

# cardFrameS - Godot Card Game Framework

A space-themed card-based resource management game framework developed with Godot 4.4 engine.

## What This Project Accomplishes

This project implements a complete card game framework where players manage various cards (ores, items, NPCs, locations) in a space environment. It provides a comprehensive card system, inventory management, dialogue system, and save/load functionality.

## Key Features

### 1. Card System
- Multiple card types: items, ores, sites, NPCs, shops
- Weight-based inventory management
- Card stacking mechanism
- Drag-and-drop interactions with physics effects

### 2. Inventory Management
- Weight limit system
- Multiple deck support
- Auto-sorting and real-time updates
- Cross-deck card transfers

### 3. Interaction Systems
- NPC dialogue with branching conversations
- Shop system with dynamic pricing
- Scene transitions via location cards

### 4. Save System
- Auto-save on scene changes
- Player data persistence (money, HP, inventory)
- Complete deck serialization

### 5. Data-Driven Architecture
- CSV-based card configuration
- Easy expansion through data files
- Multi-language support framework

## Technical Highlights

- Modular architecture with independent systems
- Resource-based serialization
- Spring-damping physics for smooth animations
- Node group system for object management
