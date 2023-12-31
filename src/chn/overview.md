概述
=======================

序数是一种比特币的编号方案，允许跟踪和转移单个聪。这些数字被称作[序号](https://ordinals.com)。
比特币是按照它们被挖掘的顺序编号的，并从交易输入转移到交易输出（遵循先进先出原则）。
编号方案和传输方案都依赖于*顺序*，编号方案依赖于比特币被挖掘的*顺序*，而传输方案依赖于交易输入和输出的*顺序*。
因此得名，*序数（Ordinals）*。

技术细节可以在[the BIP](https://github.com/ordinals/ord/blob/master/bip.mediawiki)获取.

序数理论不需要一个单独的代币，单独区块链，或者对比特币进行任何更改。它即刻可以有效运转。

序号有几种不同的表示方式：

- *整数符号*:
  [`2099994106992659`](https://ordinals.com/sat/2099994106992659) 这个序号是根据挖掘聪的顺序分配。

- *十进制符号*:
  [`3891094.16797`](https://ordinals.com/sat/3891094.16797) 第一个数字是挖掘聪的区块高度，第二个数字是区块内聪的偏移量。

- *度数符号*:
  [`3°111094′214″16797‴`](https://ordinals.com/sat/3%C2%B0111094%E2%80%B2214%E2%80%B316797%E2%80%B4).
  我们马上就会讲到。

- *百分数*:
  [`99.99971949060254%`](https://ordinals.com/sat/99.99971949060254%25) .
  T以百分比表示聪在比特币供应中的位置。

- *名字*: [`satoshi`](https://ordinals.com/sat/satoshi). 使用字符 `a`到`z`对序号进行编码。

任意资产，如NFT、安全令牌、帐户或稳定币，都可以使用序数作为稳定标识符附加到聪上。

Ordinals是一个开源项目， [在 GitHub](https://github.com/ordinals/ord)。
该项目包括一个描述序数方案的BIP、一个与比特币核心节点通信以跟踪所有聪位置的索引、一个允许
进行序号感知交易的钱包、一个用于区块链交互探索的区块资源管理器、用数字文物嵌入聪的功能，
以及本手册。

稀缺度
------

人类是收藏者。由于聪现在可以被追踪和转移，人们自然会想要收藏它们。序数理论家可以自己决定哪些
聪是稀有和合意的，这里有一些提示……

比特币有周期性的事件，有些频繁，有些不常见，这些事件自然而然地形成了一个稀有系统。这些周期性事件是:

- *区块*: 从现在到时间结束，大约每10分钟挖掘一个新区块。

- *难度调整*: 每2016个区块，或大约每两周，比特币网络通过调整区块必须满足的难度目标来响应哈希率的变化。

- *减半*: 每21万个区块，或者大约每四年，每个区块产生的新聪的数量就会减半。

- *循环*: 每六次减半就会发生一些神奇的事情：减半和难度调整会同时发生，这就是所谓的相合，相合之间的时间周期是一个周期。
大约每24年就会发生一次相合，第一次相合应该会发生在2032年的某个时候。

这给了我们以下稀缺度等级:

- `普通common`:指所有不是其区块第一个聪的聪
- `非普通uncommon`:每个区块的第一个聪
- `罕见rare`:每个难度调整期的第一个聪
- `史诗epic`:每个难度调整期的第一个聪
- `传奇legendary`:每个循环周期的第一个聪
- `神话mythic`:创世块的第一个聪

这给我们带来了度数表示法，它以一种使 satoshi 的稀有性一目了然的方式明确地表示一个序数：

```text
A°B′C″D‴
│ │ │ ╰─ Index of sat in the block 聪的索引位置
│ │ ╰─── Index of block in difficulty adjustment period 难度调整期的区块位置 
│ ╰───── Index of block in halving epoch 减半周期区块位置
╰─────── Cycle, numbered starting from 0 循环周期 从0开始
```

序数理论家经常使用术语 "小时", "分钟", "秒", and "第三"
for *A*, *B*, *C*, and *D*, respectively.

现在举一些例子。 这是一颗普通的聪：

```text
1°1′1″1‴
│ │ │ ╰─ Not first sat in block 不是区块的第一颗聪
│ │ ╰─── Not first block in difficulty adjustment period 不是难度调整的第一个区块
│ ╰───── Not first block in halving epoch 不是减半周期的第一个区块
╰─────── Second cycle 第二个循环周期
```

这是一颗 不普通 的聪

```text
1°1′1″0‴
│ │ │ ╰─ First sat in block 区块的第一颗聪
│ │ ╰─── Not first block in difficulty adjustment period 不是难度调整的第一个区块
│ ╰───── Not first block in halving epoch 不是减半周期的第一个区块
╰─────── Second cycle 第二个循环周期
```

这是一颗 罕见 的聪:

```text
1°1′0″0‴
│ │ │ ╰─ First sat in block 区块的第一颗聪
│ │ ╰─── First block in difficulty adjustment period 难度调整的第一个区块
│ ╰───── Not the first block in halving epoch 不是减半周期的第一个区块
╰─────── Second cycle 第二个循环周期
```

这是一颗 史诗 级的聪

```text
1°0′1″0‴
│ │ │ ╰─ First sat in block 区块的第一颗聪
│ │ ╰─── Not first block in difficulty adjustment period 不是难度调整的第一个区块
│ ╰───── First block in halving epoch 减半周期的第一个区块
╰─────── Second cycle 第二个循环周期
```

这是一颗 传奇级 的聪:

```text
1°0′0″0‴
│ │ │ ╰─ First sat in block 区块的第一颗聪
│ │ ╰─── First block in difficulty adjustment period 难度调整的第一个区块
│ ╰───── First block in halving epoch 减半周期的第一个区块
╰─────── Second cycle 第二个循环周期
```

这是一颗 神话级 的聪:

```text
0°0′0″0‴
│ │ │ ╰─ First sat in block 区块的第一颗聪
│ │ ╰─── First block in difficulty adjustment period 难度调整的第一个区块
│ ╰───── First block in halving epoch 减半周期的第一个区块
╰─────── First cycle 第一个循环周期
```

如果区块偏移量为零，则可以省略。这是对比以上的非普通的聪:

```text
1°1′1″
│ │ ╰─ Not first block in difficulty adjustment period 非难度调整的第一个区块
│ ╰─── Not first block in halving epoch 非减半第一个区块
╰───── Second cycle 第二个循环周期
```

稀有聪的总供给量
-------------------

总供给量
--------

- `普通common`: 2.1 quadrillion （两千一百万亿）
- `非普通uncommon`: 6,929,999
- `罕见rare`: 3437
- `史诗epic`: 32
- `传奇legendary`: 5
- `神话mythic`: 1

现时供给量
---------

- `普通common`: 1.9 quadrillion （一千九百万亿）
- `非普通uncommon`: 745,855
- `罕见rare`: 369
- `史诗epic`: 3
- `传奇legendary`: 0
- `神话mythic`: 1

目前即使是非普通的聪也非常罕见。 截至撰写本文时，已开采出 745,855 个非普通的聪
-大约在每 25.6个流通比特币中会有一个。

名字
-----

每个聪都有一个名字，由字母 *A* 到 *Z*组成, 随着聪被开采的时间越长，名字越短。 如果他们从短开始，
然后变得更长，那么所有好的、短的名字都会被困在无法使用的创世块中。

例如，1905530482684727°的名字是“iaiufjszmoba”。 最后被开采的聪的名字是“a”。
每个 10 个或更少字符的组合都存在，或者总有一天会存在。

奇特的
-------

除了它们的名字或稀有性之外，聪可能还因为其他原因而受到重视。这可能是由于数字本身的性质，
比如具有整数的平方根或立方根。或者它与某件历史事件有关，例如来自区块477,120的聪（SegWit激活的区块）是 2099999997689999°，这是最后一个被挖出来的聪。

这种比特币被称为“奇特的”。哪些聪是“奇特的”？是什么让他们如此被重视？
序数理论家被鼓励根据他们自己设计的标准来寻找“奇特的”聪。

铭文
------------

聪可以刻有任意内容，从而创建比特币原生的数字文物（数字艺术）。铭刻是通过将要铭刻的内容发送到交易中来完成的，
该交易会在链上显示铭文内容。由于铭文内容与聪有着密不可分的联系，从将创造了一个不可改变的数字人工制品。
这个数字文物可以被追踪、转移、储存、购买、出售、丢失和重新发现。

考古
-----------

致力于编目和收集早期 NFT 的活跃考古学家社区如雨后春笋般涌现。这是 [Chainleft对历史NFT的精彩总结](https://mirror.xyz/chainleft.eth/MzPWRsesC9mQflxlLo-N29oF4iwCgX3lacrvaG9Kjko)

普遍接受的古老NFT 的截止日期是 2018 年 3 月 19 日，即第一个 ERC-721 合约[SU SQUARES](https://tenthousandsu.com/), 被部署在以太坊上的时间。

NFT 考古学家是否对序数感兴趣是一个悬而未决的问题！ 从某种意义上说，序数是在 2022 年初创建的，当时序数规范已定稿。

从这个意义上说，它们不具有历史意义。 但从另一种意义上说，序数实际上是由中本聪在 2009 年开采比特币创世块时创造的。
从这个意义上说，序数，尤其是早期的序数，当然具有历史意义。

许多序数理论家赞成后一种观点。这不仅仅是因为序数是在至少两个不同的场合独立发现的，远早于现代 NFT 时代开始。

2012 年 8 月 21 日，Charlie Lee 在 Charlie Lee [在Bitcoin Talk论坛上发布一项将比特币权益证明Proof-of-stake添加的提案](https://bitcointalk.org/index.php?topic=102355.0)。这不是资产方案，但确实使用了序数算法，并且已实施但从未部署过。

2012 年 10 月 8 日，jl2012 在[同一论坛上发布了一个方案](https://bitcointalk.org/index.php?topic=117224.0) 该方案使用十进制表示法并具有序数的所有重要属性。 该计划进行了讨论，但从未实施。

这些序数的独立发明在某种程度上表明序数是被发现的，或者是重新发现的，而不是发明的。 序数是比特币数学的必然性，
不是源于它们的现代文档，而是源于它们古老的起源。 它们是许多年前随着第一个区块的开采而启动的一系列事件的高潮。
