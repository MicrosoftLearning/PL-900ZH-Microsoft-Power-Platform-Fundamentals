﻿---
lab:
    title: '实验室：数据建模'
    module: '模块 2：Common Data Service 简介'
---

# 模块 2：Common Data Service 简介
## 实验室：数据建模


应用场景
========
    
贝洛斯学院 (Bellows College) 是一所教育机构，校园内有多座建筑。目前，校园访问记录在纸质日报上。无法始终如一地捕获信息，也无法收集和分析有关整个校园的访问数据。 

校园管理部门希望对其访客登记系统进行现代化改造，在该系统中，由安全人员控制对建筑物的访问，并且所有访问都必须由其主人预先登记和记录。

在整个课程中，你将生成应用程序并执行自动化，以使 Bellows College 的管理和安全人员可以管理和控制校园建筑的出入情况。 

在本实验中，要设置环境、创建 Common Data Service (CDS) 数据库并创建解决方案以跟踪你的更改。你还将创建一个数据模型来满足以下要求：

-   R1 – 跟踪校园访问的位置（建筑物）
-   R2 - 记录基本信息以识别和跟踪访问者 
-   R3 - 安排、记录和管理访问 

最后，将示例数据导入 Common Data Service。

高级实验室步骤
======================

为了准备学习环境，你将：

* 创建解决方案和发布者
* 添加满足应用程序要求所需的新组件和现有组件。请参阅[数据模型文档](https://github.com/MicrosoftLearning/PL-900-Microsoft-Power-Platform-Fundamentals/raw/master/Allfiles/Labs/Campus%20Management.png)获取元数据说明（实体和关系）。可以按住 Ctrl 并单击或右键单击链接以在新窗口中打开数据模型文档。

完成所有定制后，你的解决方案将包含多个实体：

-   联系人
-   生成
-   访问权限

## 先决条件：

* 无

开始前要考虑的事项：
-----------------------------------

* 命名约定
* 数据类型、限制（例如，名称的最大长度）
* 日期/时间格式支持轻松本地化

练习 1：创建环境和解决方案
==================================================

**目标：**在本练习中，你将准备环境并创建支持数据建模过程的解决方案。 

任务 \#1：创建环境
-----------------------------

如果你在练习之前没有并且未得到环境，则在此任务中，你将创建一个新的工作环境。否则，你可以继续执行下一个任务。

1.  登录至 <https://aka.ms/ppac>

2.  选择 **“环境”**，然后单击顶部菜单中的 **“新建”**。这将打开
    窗口右侧的菜单。

3.  在 **“名称”** 中输入 **“Bellows College [你的姓氏]”**。

4.  对于 **“类型”**，在下拉菜单中选择 **“生产”**。

5.  选择你的 **“区域”**

6.  输入创建此环境的 **“目的”** （可选）。 
    
7.  如果你希望与此一起创建数据库，打开 **“切换”** 以**为此环境创建数据库**，
    否则，如果环境已经配置，
    你就可以与此一起创建数据库。

8.  单击 **“下一步”**。

9.  选择 **“语言”** 和 **“货币”**。出于这些实验室的目的，
    环境中已选择 **“英语”** 和 **“美元”** (USD)。

10. 出于这些实验室的目的，保持 **“启用 Dynamics 365 应用”** 为
    禁用状态。

11. 出于这些实验的目的，保持 **“部署示例应用和数据“** 为
    禁用状态。

12. 单击 **“保存”**。

13. 完成部署可能需要几分钟的时间。你可以单击 **“刷新”** 按钮刷新该列表。配置环境后，**“状态”** 将更改为“就绪”。

14. 如果以前未创建数据库，请选择你的环境，然后单击 **“创建我的数据库”**。否则，请跳过此步骤。

    - 选择 **“货币”** 和 **“语言”**。出于这些实验室的目的，
    环境中已选择 **“美元”** (USD) 和 **“英语”**。

    - 请单击 **“创建我的数据库”**。

任务 \#2：创建解决方案和发布者
---------------------------------------

1.  创建解决方案

    -   登录至 <https://make.powerapps.com>

    -   通过如下方式选择环境：单击屏幕右上角的 **“环境”**，然后从下拉菜单中选择环境。

    -   从左侧菜单中选择 **“解决方案”**，然后单击 **“新解决方案”**。

    -   对于 **“显示名称”**，输入 **“校园管理”**。

2.  创建发布者

    -   单击 **“发布者”** 下拉菜单并选择 **“+ 发布者”**。

    -   在弹出的窗口中，请为 **“显示名称”** 输入 **“Bellows College”**，并为 **“前缀”** 输入 **“bc”**

    -   依次单击 “保存”和 **“关闭”**。 
    
    -   请单击弹出窗口中的 **“完成”**。

3.  完成解决方案的创建。

    -   现在，单击 **“发布者”** 下拉菜单，然后选择 **“Bellows College”**，
        你刚刚创建的发布者。

    -   确认 **“版本”** 是否设置为 **“1.0.0.0”** 
    
    -   单击 **“创建”**。

任务 \#3：添加现有实体
-----------------------------

1.  单击打开你刚刚创建的 **“校园管理”** 解决方案。
2.  单击 **“添加现有”** 然后选择 **“实体”**。
3.  找到 **“Contact”** 实体并选中。
4.  单击 **“下一步”**。
5.  单击 **“选择组件”**。
6.  选择 **“视图”** 标签，然后选择 **“可用联系人”** 视图。单击
     **“添加”**。
7.  请再次点击 **“选择组件”**。
8.  选择 **“表单”** 标签，然后选择 **“联系人”** 表单。
9.  单击 **“添加”**。
10.  **“1 视图”** 和 **“1 表单”** 应属于选中状态。单击 **“添加”**。
    这会将具有选定视图和表单的 Contact 实体添加到新创建的解决方案中。 
11.  你的解决方案现在应具有一个实体：联系人。

练习 \#2：创建实体和关系
========================================

**目标：**在本练习中，你将在实体之间创建实体并添加关系。

任务 #1：创建“建筑物”实体和字段
-----------------------------------------

1.  你仍应打开浏览器以访问 Campus Management 解决方案。如果没有，请按照以下步骤打开 Campus Management 解决方案：
    * 登录到 <https://make.powerapps.com>（若尚未登录）
    * 选择 **“解决方案”** 并单击，以打开刚创建的 **“校园管理”**。
2.  创建“建筑物”实体

    -   单击 **“新建”**，然后选择 **“实体”**。
    -   为 **“显示名称”** 输入 **“Building”** 
    -   单击 **“完成”**。这将
            开始在后台预配实体，同时可以开始添加
            其他实体和字段。

## 任务 2：创建访问实体和字段

 **Visit** 实体将包含有关校园访问的信息，包括建筑、访问者、每次访问的计划时间和实际时间。 

我们希望为每次访问分配一个唯一的号码，当访客在访问签到过程中被询问时，他可以很容易地输入并解释该号码。

> [备注]
> 我们用 **“时区无关”** 行为记录日期和时间信息，因为访问时间*始终*与建筑物所在的本地时间一致，因此当从不同时区查看时，不应更改此信息。 

1.  选择 **“校园管理”** 解决方案
2. 创建“访问”实体

   * 单击 **“新建”**，然后选择 **“实体”**。
   * 为 **“显示名称”** 输入 **“Visit”** 
   * 单击 **“完成”**。这将开始在后台预配实体，同时可以开始添加其他字段。

3. 创建“计划开始时间”字段

   * 请确保 **“字段”** 选项卡已选中并单击 **“添加字段”**。
   * 为 **“显示名称”** 输入 **“计划开始时间”**。
   * 为 **“数据类型”** 选择 **“数据和时间”**。
   * 在 **“必填”** 字段中，选择 **“必填”**。
   * 展开 **“高级选项”** 部分。
   * 在 **“行为”** 字段中，选择 **“与时区无关”**。
   * 单击 **“完成”**。

4.  创建“计划结束”字段

    * 单击 **“添加字段”**。
    * 为 **“显示名称”** 输入 **“计划结束”**。
    * 为 **“数据类型”** 选择 **“日期和时间”**。
    * 在 **“必填”** 字段中，选择 **“必填”**。
    * 展开 **“高级选项”** 部分。
    * 在 **“行为”** 字段中，选择 **“与时区无关”**。
    * 单击 **“完成”**。
    
6.  创建“实际开始时间”字段

    * 单击 **“添加字段”**。
    * 为 **“显示名称”** 输入 **“实际开始时间”**。
    * 为 **“数据类型”** 选择 **“数据和时间”**。
    * 展开 **“高级选项”** 部分。
    * 在 **“行为”** 字段中，选择 **“与时区无关”**。
    * 单击 **“完成”**。
    
7.  创建“实际结束时间”字段

    * 单击 **“添加字段”**。
    * 为 **“显示名称”** 输入 **“实际结束时间”**。
    * 为 **“数据类型”** 选择 **“数据和时间”**。
    * 展开 **“高级选项”** 部分。
    * 在 **“行为”** 字段中，选择 **“与时区无关”**。
    * 单击 **“完成”**。
    
7.  创建“代码”字段

    * 单击 **“添加字段”**。
    * 为 **“显示名称”** 输入 **“代码”**。
    * 为 **“数据类型”** 选择 **“自动编号”**。
    * 为 **“自动编号类型”** 选择 **“带日期前缀的数字”**。
    * 单击 **“完成”**。
    
8.  单击 **“保存实体”**

任务 3：创建关系
------------------------------

1.  确保仍在查看 **“Campus Management”** 解决方案中的 **“Visit”** 实体。如果没有，请导航到该实体。
2.  创建访问到联系人的关系
    * 选择 **“关系”** 选项卡。
    * 单击 **“添加关系”**，然后选择 **“多对一”**
    * 为 **“相关(一个)”** 选择 **“Contact”**
    * 为 **“查找字段显示名称”** 输入 **“访客”**
    * 单击 **“完成”**。
3.  创建访问到建筑物的关系
    * 单击 **“添加关系”**，然后选择 **“多对一”**
    * 为 **“相关(一个)”** 选择 **“Building”**
    * 单击 **“完成”**。
4.  单击 **“保存实体”**。
5.  在顶部菜单中选择 **“解决方案”**，然后单击 **“发布全部自定义”**。

# 练习 3：导入数据

**目标：**在本练习中，你要将示例数据导入 Common Data Service 数据库。

## 任务 #1：导入数据映射

1. 如果还没有下载，请下载 [CampusDataMap.xml](../../Allfiles/Labs/CampusDataMap.xml)。
2. 导航到位于 <https://admin.powerplatform.microsoft.com> 的 Power Platform 管理中心，然后登录。
3. 选择“Bellows College”环境。
4. 单击顶部的 **“设置”**。
5. 展开 **“数据管理”** 部分，然后选择 **“数据映射”**。这将在新的浏览器选项卡中打开导入映射屏幕。
6. 请单击 **“导入”**，然后单击 **“选择文件”**。找到并选择较早前下载的 **CampusDataMap.xml**，然后按 **“确定”**。 
7. 应成功导入 Thew Campus 数据地图文件。如果遇到错误，请返回并确认已在先前的任务中创建了所有必需实体和字段。
8. 在顶部菜单中选择 **“解决方案”**，然后单击 **“发布全部自定义”**。

## 任务 2：导入数据  

1. 下载 [CampusData.zip](../../Allfiles/Labs/CampusData.zip)。
2. 导航到 Power Platform 管理中心，网址为 <https://admin.powerplatform.microsoft.com>。
3. 选择“Bellows College”环境。
4. 单击顶部的 **“设置”**。
5. 展开 **“数据管理”** 部分，然后选择**数据导入向导**。
6. 按 **“导入数据”**。
7. 请单击 **“选择文件”**，然后找到并选择较早前下载的 **CampusData.zip**。
8. 按 **“下一步”**，然后再次按 **“下一 步”**。
9. 选择 **“CampusImportDataMap”**， 按 **“下一步”**。
10. 查看映射摘要，然后按 **“下一步”**，然后按 **“提交”**。
11. 按 **“完成”**。
12. 现在将开始导入数据。现在可使用“我的导入”屏幕右侧的“刷新”按钮刷新表，直到所有四个导入的 **“状态描述”** 均为 **“已完成”**。这可能需要几分钟时间。

## 任务 3：验证数据导入

1. 选择 **“校园管理”** 解决方案。如果尚未打开，请导航至 make.powerapps.com，然后单击左窗格上的解决方案以找到你的解决方案。*
2. 选择 **“访问”** 实体，然后选择 **“数据”** 选项卡。
3. 单击右上角的 **“主动访问”** 以显示视图选择器，然后选择 **“所有字段”**
4. 如果导入成功，应该可以看到访问条目列表。
5. 单击 **“建筑物”** 列中的任意值，并确认“构建”窗体在单独窗口中打开。
6. 单击 **“访问者”**列中的任意值（可能需要向右滚动视图），请确认“联系人”窗体在单独窗口中打开。

# 挑战

* 你会考虑使用 *“约定”* 作为解决方案的一部分吗？它会改变什么？
* 如何将计划的开始强行安排在计划的结束之后？ 
* 在一次访问中增加对多个会议的支持。
* 不仅要确保外部联系人安全访问该建筑，而且要确保内部成员安全访问该建筑。
* 访问某些建筑需要管理层的批准。数据模型中的审批流程会发生什么变化？
