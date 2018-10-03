>
> **首先，这只是一些个人的不成熟的小想法...**
>

## 前 / 后端交互接口字段命名规范（草案）
以下规定了前后端交互过程中需要商定的字段名应遵守的基本规范，通常会附上 “DO”  “DONT” 以及为何如此约束的理由。


**建议级别**
> :bangbang: 要求：通常有充分理由，应严格在所有涉及前 / 后端交互的字段命名中遵守。
>
> :exclamation: 建议：通常是一些现有接口规范中的约束，建议在所有前 / 后端交互的字段命名中遵守。
>
> :grey_exclamation: 推荐：通常是经讨论或有特殊效益的约束，推荐在前 / 后端交互的字段命名中遵守。
>
> :grey_question: 待议：通常是一些效益尚不明确、实现成本偏高的约束。

**其它符号**
> :white_check_mark: DO：符合该条约束的写法
>
> :x: DONT：不符合该条约束的写法

以下为文档正文。

---

### 通用
1. :bangbang: **所有唯一ID，均命名为 `id`。**

    > :white_check_mark: `contest.id` `problem.id` 
    >
    > :x: `user.uuid` `problem.uid`
    >
    > 这可以保证全局的命名一致性。

2. :bangbang: **使用全小写下划线命名法。**

    > :white_check_mark: `time_limit` `create_time` `to_next_level_honor`
    >
    > :x: `memberSince` `memoryId`
    >
    > 如 Google、GitHub 和 Twitter 等公司的开放API几乎清一色使用全小写下划线命名法。另见： [json串中的key全大写好？还是全小写好？还是驼峰命名好？ - llun的回答 - 知乎](https://www.zhihu.com/question/57760702/answer/154272848) / [前后端设置json传递数据的时候为了规范key使用驼峰还是下划线？](https://segmentfault.com/q/1010000012714537)

3. :exclamation: **对于有明显层级关系的字段，使用嵌套对象。**

    > :white_check_mark: `channel.{id name}`
    >
    > :x: `channel_id` `channel_name`
    >
    > “使用嵌套对象有助于对关联实体字段的扩展，也更易于业务的切割和理解。”， 见[前后端接口规范#实体定义2 - CSDN博客](https://blog.csdn.net/xiaoxuan2015/article/details/53556541)

4. :grey_exclamation: **在字段不具有明显语义的情况下，使用复数形式标志所有类型为数组的字段。**

    > :white_check_mark: `contest.problems[Array<Object>]` `problem.solutions[Array<Object>]`
    >
    > :x: `contest.tag[Array<String>]`
    >
    > 有助于提升字段命名的语义性。

5. :bangbang: **保证 JSON 数据中`Object`严格静态映射。**

    > :white_check_mark: `problem.id` `contest.headline`
    >
    > :x: `contests[contest_ids[0]]` `problem_datail[problems[0]]`
    >
    > 意在保证 JSON 数据的独立性，所有的动态映射请使用`Array`实现，务必保证 JSON 数据中`Object`严格静态映射，也就是说`Object`中的`key -> value`映射中的`key`是维持一个常值。