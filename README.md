### 一、双线程模型：
##### 小程序是基于双线程模型的，在这个模型中，小程序的渲染层跟逻辑层分开在不同的线程。这是小程序框架跟前端流行的大部分框架的不同之处。
##### 基于这个模型，小程序框架可以做到更好的管控以及更安全的环境。但同时也带来了无处不在的异步问题。
##### 不过我们在框架层面去封装好异步带来的时序问题，让开发者只需要懂得上层更易为理解的接口。

### 二、性能优化：
##### 1、代码包下载---可以使用缓存
##### 2、分包下载---先下载"主包"，包含小程序打开时马上要加载的代码跟资源。然后在下载"分包"，包含剩余的代码跟资源。这样主包下载完成就可以立刻启动小程序。

### 三、视图渲染：
##### 1、初始渲染：初始渲染发生在页面刚刚创建时。初始渲染时，将初始数据套用在对应的WXML片段上生成节点树。节点树也就是在开发者工具WXML面板中看到的页面树结构，它包含页面内所有组件节点的名称、属性值和事件回调函数等信息。最后根据节点树包含的各个节点，在界面上依次创建出各个组件。【减少节点数量可以降低渲染开销】
#####
##### 2、重渲染：初始渲染完毕后，视图层可以多次应用setData的数据。每次应用setData数据时，都会执行重渲染来更新界面。初始渲染中得到的data和当前节点树会保留下来用于重渲染。每次重渲染时，将data和setData数据套用在WXML片段上，得到一个新节点树。然后将新节点树与当前节点树进行比较，这样可以得到哪些节点的哪些属性需要更新、哪些节点需要添加或移除。最后，将setData数据合并到data中，并用新节点树替换旧节点树，用于下一次重渲染。【合理使用setData，减少setData的调用次数跟数据量】
##### 