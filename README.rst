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

INFMIDI是一个用Python编写的Midi编辑库，有很多高级的语法帮助你快速编辑和生成Midi文件。你也可以用它来辅助编曲、用代码创作音乐。

文档: `English <https://infmidi.readthedocs.io/en/latest/>`_  | `中文文档 <https://infmidi.readthedocs.io/zh/latest/>`_ .


安装
----

如果你只需要编辑Midi文件，在终端中使用以下命令进行安装:

::

    pip install infmidi

如果你需要播放Midi、用图片显示Midi、与编曲软件交互，在终端中使用以下命令进行安装:

::

    pip install "infmidi[all]"

总览
----

基础类
^^^^^^

- ``Event``: Midi事件类。一般情况下，你不需要直接使用它。
- ``Note``: 包含了 ``note_off`` 与 ``note_off`` 两个事件，帮助你快速生成音符。
- ``Clip``: INFMIDI的核心类，相当于一个音乐片段。用来组织你的音符( ``Note`` )和事件( ``Event`` ), 有很多高级操作。
- ``Track``: ``Clip`` 的子类，附加了一些额外属性 （ ``name`` 、 ``instrument`` 和 ``mute`` 等）。
- ``Midi``: 由多个轨道（ ``Track`` ）组成。

附加包
^^^^^^

- ``generator``: 一些快速生成 ``Clip`` 的函数集。
- ``effects``: 一写快速处理 ``Clip`` 的函数集.
- ``devices``: 一些用于播放Midi，与编曲软件交互的对象。
- ``utils``: 一些额外功能的函数， 如通过图片来显示 ``Midi``。

一些例子
--------

基础
^^^^^

创建 ``Note`` 对象.

.. code-block:: python
    
    Note('A4') # Note(name="A4", value=69, frequency=440.00, location=0.00, length=1.00, velocity=127, channel=0)

    # 
    Note('A4') == Note(69) == Note(440.) # True

    # 将音符升高8个半音
    Note('A4') + 8

    # 将音符延迟8拍
    Note('A4') >> 8


创建 ``Clip`` 对象.

.. code-block:: python

    from infmidi import Note, Clip

    clip = Clip()

    # 将 note 加入 clip.
    for i in range(127):
        # 这里也可以用 clip.add()
        clip += Note(i, velocity=i, locationa=i)

    # 获得clip的前8拍的副本
    new = clip[:8]

    # 拼接clip
    clip |= new

    # 将clip的前8拍升高10个半音
    clip[:8] += 10

    # 将前 8 拍的音符和事件延迟 16 拍.
    clip[:8] >>= 16

    # 删除前8拍的音符和事件
    clip[:8] = None 

    # 将 clip 重复 4 次.
    clip **= 4

    # 还有很多操作，就不一一举例了
    ...


创作一首完整的歌

.. code-block:: python

    from infmidi import Midi
    song = Midi(name='My song', bpm=123, time_signature='4/4', key_signature='C')

    track1 = song.new_track(name='Melody track', instrument='Acoustic Guitar(steel)')

    # 生成一些 Clip 并加到轨道里
    ...

    track2 = song.new_track(name='Chord track', instrument='Acoustic Grand Piano')

    # 生成一些 Clip 并加到轨道里
    ...

    track3 = song.new_track(name='Drum track', is_drum=True)

    # 生成一些 Clip 并加到轨道里
    ...



读取和保存Midi文件

.. code-block:: python

    from infmidi import Midi
    mid = Midi.read('/path/to/xxx.mid')

    # 做一些修改
    ...

    mid.save('/path/to/xxx.mid')


生成器
^^^^^^^^^

用 ``chord()`` 来生成和弦.

.. code-block:: python 

    from infmidi.generator import sheet
    
    # 使用全名来初始化
    Cm7 = chord('C4:m7')

    # 使用根音与和弦类型来初始化
    CM7 = chord('C4', 'M7')

    # 使用音程来初始化
    C7 = chord('C4', [4, 3, 3])

    # 使用音级来初始化
    CmM7 = chord('C4', ['1', 'b3', '5', '7'])
    


用 ``sheet()`` 来生成和弦进行。

.. code-block:: python 

    from infmidi.generator import sheet
    from infmidi.utils import plot

    txt = '''
        A4:m7 | D4:m9   | G4:7 | C4:M7     |
        F4:M7 | B3:m7-5 | E4:7 | A4:m7 A4:7
    '''

    progression = sheet(txt)
    plot(progression)

.. image:: https://raw.githubusercontent.com/gongyibei/infmidi/master/assets/readme/sheet1.png

用 ``sheet()`` 来生成一段鼓。

.. code-block:: python 

    # 语法受lisp语言启发， 一个小节和一个括号内的元素平分当前长度
    HitHat = sheet('0 H 0 H | 0 H 0 (H H H) | 0 H 0 H | (0 H) (H H H)', length_per_bar=2)
    Snare  = sheet('0 0 S 0 | 0 0 S 0       | 0 0 S 0 |  0    (S 0)  ', length_per_bar=2)
    Kick   = sheet('K       | K K 0 0       | K       | (K K)  0     ', length_per_bar=2)

    # 进行叠加
    drum = Kick + Snare + HitHat

    plot(drum ** 2)



.. image:: https://raw.githubusercontent.com/gongyibei/infmidi/master/assets/readme/sheet2.png

更多的生成器函数还在路上 ...

效果器
^^^^^^^

.. code-block:: python

    from infmidi import Midi
    from infmidi.effects import scale_map

    filename = '/path/to/xxx.mid'
    mid = Midi.read(filename)
    for track in mid.tracks:
        if track.is_drum:
            continue
        scale_map(track, key=mid.key_signature, scale='宫', inplace=True)

更多的效果器函数还在路上 ...

设备
^^^^^^^

.. code-block:: python

    from infmidi.devices import FluidSynth
    synth = FluidSynth('/path/to/xxx.sf2')

    # to generate your item (Note, Clip, Track or Midi).
    ...

    synth(item)

更多的设备函数还在路上 ...

其他小工具
^^^^^^^^^^^^^^^^^

.. code-block:: python

    from infmidi.utils import plot

    # 生成item (Note、 Clip、 Track 或 Midi).
    ...

    plot(item)


许可条款
-------
INFMIDI 使用 `MIT license
<http://en.wikipedia.org/wiki/MIT_License>`_.
