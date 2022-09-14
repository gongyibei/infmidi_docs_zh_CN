快速开始
========

导入包
------

.. code-block:: python

    from infmidi import *


创建音符
--------

创建 ``Note`` 对象.

.. code-block:: python
    
    Note('A4') # Note(name="A4", value=69, frequency=440.00, location=0.00, length=1.00, velocity=127, channel=0)

    # 可以使用音名、Midi值或者频率来初始化音符
    Note('A4') == Note(69) == Note(440.) # True

    # 将音符升高8个半音
    Note('A4') + 8

    # 将音符延迟8拍
    Note('A4') >> 8


创建Clip
--------

创建 ``Clip`` 对象.

.. code-block:: python

    clip = Clip()

    # 在第0拍添加音符音符 C4
    clip += Note('C4')
    # 删除第0拍的音符 C4
    clip += Note('C4')

    # 在第4拍添加音符音符 C4
    clip += Note('A4') >> 4
    # 删除该音符
    clip -= Note('A4') >> 4

    # 在第 8 拍添加一个力度微 77 的音符 C4
    clip += Note('C4', velocity=77, location=8)
    # 删除该音符 （通过名字和位置就可以确定该音符啦）
    clip -= Note('C4', location=8)


    # 随机添加音符
    import random
    for i in range(16):
        name = random.choice(['C4', 'E4', 'G4', 'B4'])
        clip += Note(name, location=i/2, length=1/2)


    # clip里的音符升高一个8度
    clip += 8
    # clip里的音符降低一个8度
    clip -= 8

    # clip里的音符右移动2拍
    clip >>= 2
    # clip里的音符左移2拍
    clip <<= 2
    
    # 将 clip 重复 4 次.
    clip **= 4

    # 将clip拉伸2倍
    clip ^= 2
    # 将clip压缩一半
    clip ^= 0.5

    # 前8拍音符升高一个8度
    clip[:8] += 8
    # 前8拍音符降低一个8度
    clip[:8] -= 8

    # 删除4到8拍的音符和事件
    clip[4:8] = None 

    # 前4拍拉升2倍
    clip[:4] ^= 2

    # 还有很多操作，就不一一举例了
    ...

.. hint:: 

    点击 :doc:`Clip <./core/clip>` 查看更多操作。


生成旋律
--------

用 ``sheet()`` 来生成旋律。

.. code-block:: python
    
    txt = '''
        C4 C4 G4 G4 | A4 A4 G4 - | F4 F4 E4 E4 | D4 D4 C4 -
    '''
    melody = sheet(txt)

.. image:: ../../_static/imgs/sheet/note_sheet.png
    :align: center


生成和弦
--------

用 ``chord()`` 来生成和弦。

.. code-block:: python 
    
    # 使用全名来初始化
    Cm7 = chord('C4:m7')

    # 使用根音与和弦类型来初始化
    CM7 = chord('C4', 'M7')

    # 使用音程来初始化
    C7 = chord('C4', [4, 3, 3])

    # 使用音级来初始化
    CmM7 = chord('C4', ['1', 'b3', '5', '7'])

.. hint:: 

    点击 :doc:`速查表/chord <./cheat>` 查看和弦列表。目前和弦种类还不多，后续会进行添加。


用 ``sheet()`` 来生成和弦进行。

.. code-block:: python 

    txt = '''
        A4:m7 | D4:m9   | G4:7 | C4:M7     |
        F4:M7 | B3:m7-5 | E4:7 | A4:m7 A4:7
    '''

    progression = sheet(txt)
    plot(progression)

.. image:: https://raw.githubusercontent.com/gongyibei/infmidi/master/assets/readme/sheet1.png


生成鼓
------

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


读写MIDI文件
------------

.. code-block:: python

    mid = Midi.read('/path/to/xxx.mid')

    # 做一些修改
    ...

    mid.save('/path/to/xxx.mid')



创作一首完整的歌
----------------


.. code-block:: python

    from infmidi import Midi
    
    song = Midi(name='My song', bpm=123, time_signature='4/4', key_signature='C')

    track1 = song.new_track(name='Melody track', instrument='Acoustic Guitar(steel)')

    # 生成一些 Clip 加到轨道里
    ...

    track2 = song.new_track(name='Chord track', instrument='Acoustic Grand Piano')

    # 生成一些 Clip 加到轨道里
    ...

    track3 = song.new_track(name='Drum track', is_drum=True)

    # 生成一些 Clip 加到轨道里
    ...

.. hint:: 

    点击 :doc:`速查表/GM Instrument <./cheat>` 查看GM 乐器的完整列表。


使用效果器
----------

.. code-block:: python

    from infmidi import Midi
    from infmidi.effects import scale_map

    filename = '/path/to/xxx.mid'
    mid = Midi.read(filename)
    for track in mid.tracks:
        if track.is_drum:
            continue
        scale_map(track, key=mid.key_signature, scale='宫', inplace=True)


播放MIDI
--------


使用 :doc:`FluidSynth <./devices/fluidsynth>` 来播放Midi。

.. code-block:: python

    from infmidi.devices import FluidSynth
    synth = FluidSynth()

    # to generate your item (Note, Clip, Track or Midi).
    ...

    synth(item)


与编曲软件交互
--------------

使用 :class:`Controller <./devices/controller>` 来与编曲软件交互。

.. code-block:: python

    from infmidi.devices import Controller

可视化
------

.. code-block:: python

    from infmidi.utils import plot

    # 生成item (Note、 Clip、 Track 或 Midi).
    ...

    plot(item)