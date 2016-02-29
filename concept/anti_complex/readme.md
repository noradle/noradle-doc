中文版
======

本目录包含了 noradle 设计中关于对 web 信息系统开发复杂性的认识，包括：

1. 识别和意识到复杂性的存在
2. 为什么说现有的传统web开发语言和架构开发中比较累赘啰嗦
3. 一些复杂性的存在没有绝对的存在道理
4. noradle 是如何避免陷入复杂性

方向包含：

1. [避免所有和数据库连接和执行SQL方面的麻烦](anti_complex_db_access.zh.md)
  - 有关数据库客户端驱动环境的安装、配置、版本匹配的繁冗工作
  - 有关应用服务器连接池的管理、参数配置策略的繁冗工作
  - 有关拼接SQL、执行SQL、取结果的繁琐代码
  - 烦人的异常处理
  - 各种宿主语言和数据库库表字段类型和数据结构之间的对应
2. [对象关系模型更多的是烦恼而不是便利](anti_or_mapping.zh.md) 
3. [避免使用某种页面模板语言](anti_templating.zh.md)
4. [避免使用服务器端存储的会话存储](anti_session.zh.md)

English Version
===============

This directory include what noradle consider complexity to develop web information system, including:

1. recognize the existence of complexity
2. why traditional web development languages and tech-stack is some what verbose
3. why the above tech is unnecessarily complex
4. how noradle is design to avoid all the complexity other tech all popular practice will encounter

The aspect include

1. [connection to db and SQL executing is headache](anti_complex_db_access.en.md)
2. [avoid (html/xml/...) templating language](anti_templating.en.md)
3. [the badness of server-side session store](anti_session.en.md)
