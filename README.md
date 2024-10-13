
今天早上，OpenAI实施团队的 @shyamal在Github上开源了[Swarm](https://github.com)这个OpenAI官方的多智能体框架。不得不说，OpenAI官方下场，获得的社区影响就是不一样，在微信群、朋友圈里已经出现大量的解析文章。

[![image](https://img2023.cnblogs.com/blog/510/202410/510-20241012155240654-1509198195.png "image")](https://github.com)

这个多智能体框架确实已经把多智能体的关键，说的很透彻了，Swarm 里面定义了两个核心**「Agents」**和**「Handoffs」，多智能体的核心是在这个Handoffs上面。**简单看了下examples 之后我觉得这个多智能体框架并不够好，恰巧的是，我对云原生技术很熟，借用一下云原生的发展历程，给这个\[Swarn]框架做个简要点评：从云原生容器发展的历史来看，相当于docker swarm 和 k8s， 我们需要的智能体框架应该是k8s 这样的一个框架，如果你是一位云原生技术熟悉的同学很容易就知道我在说什么了。

单Agent这块，简单封装提示词和使用函数调用就可以完成业务，OpenAI就一个 /api/chatcompletions 接口就帮我们搞定了，市场上大量的Agent 产品都停留在单Agent 上，但是「Handoffs」这块，Swarm的确做的非常优雅了。

[![swarm_diagram](https://img2023.cnblogs.com/blog/510/202410/510-20241012161250458-1886204852.png "swarm_diagram")](https://github.com)

个人观点认为他的设计还没有我们的多智能体框架好用，OpenAI的\[Swarm]是docker swarm，我们的多智能体框架就是k8s，我需要的是像k8s编排容器那样编排智能体，我们刚刚在9月26日对外发布了多智能体的工业设计产品，详见：[智用研究院AI Agent Foundry赋能的首个多Agent驱动的工业设计平台圆满发布](https://github.com):[milou加速器](https://xinminxuehui.org)。

多智能体的核心难题其是不同智能体之间的通信问题。怎麼传递信息，传哪些信息，这些都很重要。多个智能体协作，也只需要在必要的时候被调用起来就可以了。看我们智能体协作图：

[![image](https://img2023.cnblogs.com/blog/510/202410/510-20241012155242031-815943946.png "image")](https://github.com)

当我们多智能体应用接收到用户的请求，借用Semantic kernel的设计理念叫实现“目标导向”的AI应用，这意味着它能够帮助确定目标，然后寻找实现这些目标的方法和步骤。在“目标导向”的方法中，首先需要确定目标，然后通过规划器（Planner）将目标分解为一系列需要执行的任务。这些任务可以逐个执行，以实现最终目标。这个过程对于人类来说是很自然的，但对于机器来说则相对复杂。借助LLM AI的力量，我们可以更轻松地实现这一过程。

这个接收到用户请求的智能体我们叫做路由智能体，他负责路由到具体执行任务的任务智能体。我们的智能体框架的Planner 也是类似于OpenAI的Swarm的「Handoffs」处理了交接的逻辑，我们的Planner 要比Handoffs处理的更完美。OpenAI的Swarm 目前还处于实验阶段，期望他发展成为k8s 这样的一个多智能体编排框架：

[![image](https://img2023.cnblogs.com/blog/510/202410/510-20241012155243189-1989411799.png "image")](https://github.com)

这个框架是python写的，大家觉得用python 写多智能体应用是好选择吗？ 我个人认为做应用开发，Python并不是好选择，Python之所以用的多，是因为这一波人工智能的主导者是算法工程师，他们习惯用的编程语言是Python罢了，随着复杂场景的人工智能应用需求的增加，控制权逐步要回归到应用开发者的手中，对于复杂度高、需要长期维护的应用系统还是需要用c\# 、java等业务系统开发类的编程语言来主导。

[![image](https://img2023.cnblogs.com/blog/510/202410/510-20241012163033789-436534059.png "image")](https://github.com)


