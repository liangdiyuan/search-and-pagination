在开发后台管理系统中，有不少页面是头部表单搜素，中间是表格展示，底部是分页。从页面中可抽象出，表格的内容根据表单的变化或分页的变化而变化。既然如此，设计该业务组件时，表格部分可以通过vue中插槽插入组件内。搜素表单一般是输入表单、选择表单、时间选择器等，这些可以通过传入自定义配置自动生成。底部分页一般是不会有什么变化的。如此一来，我们便可以通过搜素表单数据的变化或底部分页的数据变化，通知父组件，父组件发送请求，获取数据重新渲染表格。组件依赖于elementUI。<a href="https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz=MzUxMzExMTM5MA==&uin=&key=&devicetype=Windows+10+x64&version=63010043&lang=zh_CN&a8scene=7&fontgear=2">更多<a/>

个人公众号：假装没名字
