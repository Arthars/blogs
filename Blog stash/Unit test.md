# Unit Tests

## 定义
    Unit test 是一段代码, 它可以快速, 稳定, 独立的调用被测试的Unit, 并对**单个**最终结果进行检验.
### 什么是一个好的单元测试
* 快速
* 稳定
* 完全隔离
  * 不可有真实依赖物, 例如系统时间，真实的文件系统，或者一个真实的数据库
  * 独立于其他单元测试
* 可维护性
* 可读性

## Unit test的好处
* 更好的理解需求
* 促使写出更好更以维护的代码
* 提高代码的质量
* 重构的时候，可以在一定程度上保证重构的正确性

## 如何进行好的Unit test命名
    目前来说，本人觉得比较好的Unit test的命名为以下两种。 
    如果大家有好的命名，请不吝赐教。
    如果在给一个UT命名的时候，发现很难用一句话写出命名，说明这个UT里面做了太多的事情，应该拆分成多个UT

1. 三元素命名: [UnitOfWorkName]\_[SenarioUnderTest]\_[ExpectedBehavior]
   1. UnitOfWorkName: 被测试的一个方法，一组方法，或者一个类
   2. SenarioUnderTest: 假设的测试条件，例如 EmailIsRegistered
   3. ExpectedBehavior: 对于被测试单元的行为预期, 例如：ReturnFalse, CallThirdAPI
   4. Examples
      1. IsValidFileName_BadExtension_ReturnFalse()
2. 自然语言命名: [UnitOfWorkName]_[DescriptionSentence]
   1. UnitOfWorkName: 被测试的一个方法，一组方法，或者一个类
   2. DescriptionSentence: 一个句子，用于描述测试内容
   3. Examples:
      1. IsValidFileName_Should_return_false_case_the_extension_of_file_is_not_exist()

## Unit test三大步骤
    一般在UT内都会分成三个小块

1. Arrange: 创建必须的对象并进行设置，Mock掉必要的依赖
2. Act:     调用被测试单元
3. Assert:  断言某个事情是预期的

```C#
[Test]
public void IsValidFileName_Should_return_false_case_the_extension_of_file_is_not_exist()
{
    // Arrange
    FileHelper fileHelper = new FileHelper();

    // Act
    var result = fileHelper.IsValidFileName("fileNameWithoutExtesion");

    // Assert
    Assert.False(result);
}
```

## 如何破除依赖
什么是依赖?
> 被测试的单元与一个对象发生了交互，但是我们不能完全控制这个对象。例如系统时间

如何用可控制的代替物来代替不可控制的对象?
> 没有什么面向对象的问题不能通过增加一个间接层解决，除了间接层过多这个问题
> 因此，我们可以发现一个固定的模式来破除每个依赖项
> 
> 1. 找到被测试单元的依赖项
> 2. 如果依赖项是被测试单元直接引用，则添加一个间接层
> 3. 把间接层的底层实现替换成可以控制的代码

破除依赖项的时候，必然会导致一些重构，如何保证不会导致bug?
> 在修改现有项目之前，要准备一些集成测试作为保护

## TDD
TDD的三个核心技能

1. 知道怎么写好的单元测试
2. 良好的测试设计
3. 在coding前写测试

## 如何在团队中推行Unit test

## 如何在现有项目中开始单元测试

## Discussion
### 测试的单元是否越小越好?
> 不是，如果你试图将工作单元缩到最小，最终会不得不伪造一堆东西，这些东西并不是最终的结果，只是生成最终结果的中间状态。
> 
> 因此单纯的将测试单元缩小没有意义，我们应该对最终结果进行单元测试。如果发现无法对最终结果进行单元测试，这说明一个方法内部做了太多的事情，这些代码需要进行一些重构。

### Question 2
