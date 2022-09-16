### kanban

#### Flow
- Backlog queue
- Current top priority queue - TO DO
- In progress
- To be verified
- Done
- In prod


### Scrum

*Product Backlog*
- 所有产品features都大杂烩在Product Backlog里面。
- 任何人都可以往里面添加东西，只要你觉得是产品需要的。
- 抢任务不在这里。
- Wish List。

*Sprint Planning Meeting*
- 添加到Product Backlog的东西不一定会做。由sprint planning meeting来决定。
- 有哪些内容会从Product Backlog（Wish List）添加到Sprint Backlog（TO DO List）。
- 由Business主导。

>说明：  
*Product Owner*
- 对产品具有最终解释权，决定产品开发方向。
- 大家是平级。
- PO对产品进行设计和解释。
- PO会维护milestone。Milestone-1：Sprint 1-3。M2：S4-6。M3：S7-10。
- 要开发一个feature，不可能在一个任务中完成。PO说要3个sprint做完。再用3个sprint把另一个feature做完。
- 开发新功能同时，还有修bug，优化性能，改UI……
- 以上都是PO决定的。

*Sprint Backlog*
- 抢任务在这里。
- TO DO List。

>Q&A:
1. Senior不会take简单的task？
- A：Be professional。
- 每一个task都会有一个effort，effort会对应打一个分。难的分高，简单的分低。
- sprint的时候，首先考虑team里哪些人员存在senior、junior。
- sprint里会搭配难易。junior take简单的。
- review机制：sprint结束的时候，每个人贡献多少effort的任务。

*定义*
- Scrum is a framework within which people can address complex adaptive problems, while productively and creatively delivering products of the highest possible value.
- Scrum is:
    - Lightweight tool for enabling business agility
    - Simple to understand, yet difficult to master

*Certificate of Scrum Master*
- 敏捷开发证书。
- 有难度。
- 有项目管理经验，带过怎样的团队，有多少年工作经验。
- Scrum Master是一个角色。三种角色之一。



***Scrum 3355***

*Roles：三种角色*
- **Product Owner**
- **Development Team**
- **Scrum Master**

*Artifacts: 产物*
- **Product Backlog**：Wish List。可能项目都终止了，这里依然积压很多任务。
- **Sprint Backlog**: TODO List. Must DO.在这个sprint中必须要完成的。
- **Increment**: sprint结束后，给产品增加的东西。

*Events*
- **Sprint**：整个迭代的过程，冲刺。
- **Sprint Planning**：决定把哪些任务从Wish List放到TODO List里面。
- **Daily Scrum**：每天抢任务，抢ticket。
- **Sprint Review**：对开发出来的东西进行评测，看看是否符合要求。
- **Sprint Retrospective**

*Value propositions*
- **Commitment**
- **Focus**
- **Openness**
- **Respect**
- **Courage**

>***Q&A***
1. Sprint Review和Sprint Retrospective区别？
- A：review看做出来的东西是否符合要求。做完多少task、哪些没做完、做完的质量都OK吗？有没有什么问题。没有问题，上到product环境里。
- Retrospective：kanban上匿名写，在这个sprint里，哪些做的好，延续做法；哪些做得不好，怎样提升。不会上升到人，只会针对design。或者工作环境如果改善。解决人的问题。



***Scrum Team Roles***
- **Product Owner**：任务是客户所需要的，是产品所需要的。
- **Development Team**：把代码写对。
- **Scrum Master**：确保团队高效工作。
    - Scrum process Mgt
    - Team Protection
    - Effective Communication
    - Quality check
    - Progress tracking
    - Team building
 


### Kanban

![Kanban](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/Nodejs%E6%96%B9%E5%90%91/img/Kanban.png)

***Standup***

*Run meeting*: PO(比较多) 或者 Scrum Master 或者轮着Run

*发言说的内容：*
1. What I done - Yesterday
2. What I'm doing - If not finished, tell everyone
3. What will I do -  Take task 541, will finish it in 1 day

- **一个人说完之后，Host把任务拖到Doing里。**
- **旁边有任务的effort point**

***Who is People Manager***: 有实权，老板。
- 各种人给他汇报工作，各种report给他看。


### Agile Backlog

***Work Item***
![workItem](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/Nodejs%E6%96%B9%E5%90%91/img/workItem.png)

***Product Backlog Items (PBIs)***
![productBacklogItems](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/Nodejs%E6%96%B9%E5%90%91/img/ProductBacklogItems.png)

***让团队里的人有时间学习新知识。***
- **technical work**：refactor、version update
- **Knowledge acquisition**
- refactor、version update etc.

***User Story – New Features***
- User Story = persona(我是谁) + need(我要什么) + purpose(我要达到怎样的目的)
![UserStory](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/Nodejs%E6%96%B9%E5%90%91/img/UserStory.png)


***举牌子*** 
- Round 1：1,2,1,3,4,6,8,8,10h
    - 感觉用时很长的：没有相关knowledge；没有相关experience；采购用时；整个过程不是很熟悉。
    - 感觉用时短的：有经验。
- Round 2：3,3,4,4,5,5
    - PM或PO说：做过的考虑一下没做过的，没做过的确实需要多花一些时间，没做过的多问做过的人。
    - 取中间值，大概是4，这个任务的effort确定下来是4.
- 这个effort不是针对最强定的，也不是针对最弱定的。考虑不同成员情况，讨论出来的结果。


>***Q&A***
1. Sprint里，有很多workItems。SprintPlanningMeeting所有人都参加吗？每个workItems都需要讨论一遍吗？
- A：不会的。
- 实际PlanningMeeting中，并不需要所有人都参加：
    - PM：确定哪些任务放在Sprint中。不懂技术，根据以往团队进度，有一个大概的感觉。
    - ScrumMaster/TeamLead：可以一起看，任务1234哪些可以放进当前sprint中来。难易搭配。懂技术，知道一个workItem对senior来说多久，对于junior来说做多久。
    - 可能1-2个SeniorDeveloper参会：一起看任务。
    - 根据team配备，几个senior，几个junior，大概能做多少个任务；这些任务的effort是多少。
    - 确保WorkItems不会太多、不会太少，难易搭配适当。
    - 如果一个任务，这次sprint一定需要做，只能把别的任务拿走。
    - effort有的时候是SprintPlanningMeeting进行评估，有的时候在建立task的时候就评估了，直接把effort放上来。



### 作业

**课后阅读**

**Questions**：
- 可以在tutorial上讨论
- 或者和班长一起写下来，都是面试中很有可能会被问到的点
    - sprint是否会被取消掉
    - 一些true or false的问题
    - 我们如何描述PO的responsibility


**Hands-on的作业**
- 不需要写code，需要用Azure DevOps Lab去follow一个task：
    - 里面一共有6个tasks，把6个都做完最好。
    - 做task之前，必须完成prerequisite：只做task 1，就是导入一个sampleProject，不用管task 2，follow tutorial，一步步跟着做，就会知道，
        - 如何setUp一个Agile团队；
        - 如何创建workItems；
        - 如何管理sprint；
        - 如何定义sprint的周期；
        - capacityManagement：知道teamCapacity：senior和junior是不一样的；
            - 团队中每周都会有人请假，我们的capacity就会变少，就会影响团队的进度。如何make sure能继续progress，这些都是capacityManagement内容。
        - 如何针对你们公司的process去定制、修改kanban，修改为符合自己公司逻辑的。
        - 如何用各种各样的可视化工具，把团队成员的开发的量化统计出来。
        - 开发流程的东西。




### Case Study

**大公司的大项目如何用敏捷开发**

*微软的敏捷开发*
- Windows完全是基于敏捷开发去做的。
- Windows版本以前用waterfall，是三年更新。
- win10采用敏捷开发：Windows as a Service - rings
    1. developer开发出来新feature之后，先在内部进行测试，看看有没有bug或issue。
    2. release给内部员工，员工就会拿到internal version。
    3. 有些用户申请加入预览版，进行测试。
    4. release到public。


*企业级敏捷开发案例*
- 700 people, 40 teams, 4 location.
- waterfall -> agile.
- 2010.8-2019.1完成147sprint.
- 每三周发布一个新版本到online service上。
- 每12周发布一个server版（自己download安装）。

>结果：
- 正是用了agile，团队才能响应客户和市场的变化，不断对产品进行调整，频繁的去发布功能和feature。


*waterfall和agile的区别*
- 之前4-6months一个milestone；现在3 weeks一个sprint；
- personal offices -> open room
- PM, Dev, Test -> PM & Engineering
- 20+ person teams -> 8-12 person team
- 100 page spec documents -> specs in PPT
- Features shipped once a year -> Features shipped every sprint

*Roles的变更*
- waterfall有入场和离场：
    - dev入场coding，结束了离开，go on next project。
    - 后面都是test在工作。
- agile中engineering：
    - 每个iteration都需要不同的role。
    - 不能工作完就走，还有下一个iteration，每三周一个iteration。
    - 给每个engineering的小team assign一个PM，确保开发的东西都是客户所需要的。


*TEAMS*
- Cross discipline
    - 自己写代码，写完代码还要做Q&A。
    - 不光前端，还有后端，是full-stack。feature从头做到位，fix bug，test，测试结果有问题也要修。
    - 职责变得更加广泛。
- 10-12 people：team规模比较小。
- Co-located (for the most part)：大家共同在一个office里work
- Physical team rooms
- Self managing
    - agile12条原则里，第5和第11条。
        - motivated individual：每个人在team中，每天的工作都要有动力。
        - self-organizing team：要想在工作中取得好的result，一定是从self-organizing team而来的。
    - 如何确保每个人每天都充满了激情？而且大家都在做最喜欢做和最想做的事情？
        - 这就要对team进行organizing。
        - 每18个月，对team进行重组一次。
        - 如何重组？每个人匿名表达：我想学什么，我想做什么，我想去参与什么？
        - 通过这样self-forming的形式，形成自发性非常强的team。
- Clear charter and goals
- Intact for 12-18 months
- Own features in production
- Own deployment of features


*3 week sprint*
- sprint交接：
    - 上一个sprint结束，下一个sprint planning开始。
    - 每个sprint结束，就会做deployment
    - 每个sprint结束都会有一个邮件出来：sprint结束了，summary是什么，deliver了什么，哪些做完了，deliver到product上了，开发速度，开发状况，有多少bug。
    - 邮件中还包括：下一个sprint，我们要做什么，解决哪些问题。（由PO发出来）


*Benefits*
1. Dependencies between teams are minimized
2. Teams learn how to work together
3. We always have cross-discipline ownership
4. Teams have autonomy
5. Progress is shared continually
    - 我们每个人开发的速度，每个团队开发的进展，整个project开发的进展，全部都是公开透明的。

