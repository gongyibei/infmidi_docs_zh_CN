INFMIDI
=======

.. image:: https://img.shields.io/badge/License-MIT-yellow.svg
    :target: https://opensource.org/licenses/MIT
    :alt: License: MIT

.. image:: https://img.shields.io/badge/pypi-0.1.0-blue
    :target: https://pypi.org/project/infmidi/0.1.0

.. image:: https://readthedocs.org/projects/infmidi/badge/?version=latest
    :target: https://infmidi.readthedocs.io/en/latest/?badge=latest
    :alt: Documentation Status


INFMIDI是一个用Python编写的MIDI编辑库，有很多高级的语法帮助你快速编辑和生成MIDI文件。你也可以用它来辅助编曲、用代码创作音乐。


文档
----
`English <https://infmidi.readthedocs.io/en/latest/>`_  | `中文文档 <https://infmidi.readthedocs.io/zh/latest/>`_

以下是本项目文档的列表，点击关键词跳转到你想要了解的主题页面。

- `🔌【安装】 <https://infmidi.readthedocs.io/zh/latest/start/install.html>`_ : 详细安装教程。如果只想使用基础功能，可以使用 ``pip install infmidi`` 进行安装。
- `🚀【快速开始】 <https://infmidi.readthedocs.io/zh/latest/start/quickstart.html>`_ : 一些基础示例，帮助你快速入门。
- `🎹【基础】 <https://infmidi.readthedocs.io/zh/latest/start/core/index.html>`_: 核心类（ ``Event``, ``Note``, ``Clip``, ``Track``, ``Midi`` ）的用法介绍。
- `🎸【生成器】 <https://infmidi.readthedocs.io/zh/latest/start/generator/index.html>`_ : 一些快速生成 ``Clip`` 的函数集。
- `🎨【效果器】 <https://infmidi.readthedocs.io/zh/latest/start/effects/index.html>`_ : 一些快速处理 ``Clip`` 的函数集.
- `📻【设备】 <https://infmidi.readthedocs.io/zh/latest/start/devices/index.html>`_ :  一些用于播放MIDI，与编曲软件交互的对象。
- `🎼【示例】 <https://infmidi.readthedocs.io/zh/latest/start/examples/index.html>`_ :  一些例子帮助你学习INFMIDI的用法。
- `📑【速查表】 <https://infmidi.readthedocs.io/zh/latest/start/cheat.html>`_ : 查询核心类的用法，以及音乐和MIDI的相关信息汇总。

特性
----

- **绝对时间**：使用绝对时间而不是事件间隔来确定MIDI事件，意味着你可以很方便的在任何时间点向MIDI中添加音符或者MIDI事件。

.. code:: python
    
    # 在第8拍添加音符C4
    clip.add(Note('C4'), 8)

- **时间切片**：通过时间切片，可以选定特定时间段的MIDI事件进行修改。

.. code:: python
    
    # 8拍到16拍音符升高4个半音
    clip[8:16] += 4

- **生成器**： 通过生成器函数，来快速生成特定MIDI片段

.. code:: python

    # 和弦进行
    progression = sheet('C4:M7 A4:m9|F4:M7 G4:7')

- **效果器**：通过效果器函数来处理MIDI

.. code:: python

    # 延迟
    delay(clip, n=3, length=0.5, decay=0.9)



相关项目
--------
目前已有很多优秀的MIDI和音乐相关Python库，不同的项目都有自己各自的特点和优势。本项目不是为了替代他们，而是作为一个补充。

- `mido <https://github.com/mido/mido>`_: MIDI底层库，本项目也是基于mido开发的。
- `music21 <https://github.com/cuthbertLab/music21>`_: 由MIT开发的计算音乐分析库，可以处理多种音乐格式。
- `pretty-midi <https://github.com/craffel/pretty-midi>`_: 包含用于处理MIDI数据的实用函数和类，用于从MIDI中提取和修改信息。
- `musicpy <https://github.com/Rainbow-Dreamer/musicpy>`_: Musicpy是一种基于Python的音乐编程语言，通过音乐理论和算法以非常方便的语法编写音乐。
- `muspy <https://github.com/salu133445/muspy>`_: 主要为深度学习中符号音乐生成任务，提供包括数据集管理、数据 I/O、数据预处理和模型评估等工具。



许可条款
--------
INFMIDI 使用 `MIT license
<http://en.wikipedia.org/wiki/MIT_License>`_.
