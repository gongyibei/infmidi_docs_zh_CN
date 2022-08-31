Midi
====

初始化
------

.. code:: python

    mid = Midi(bpm=123, time_signature='4/4', key_signature='C')


读写MIDI文件
------------

.. code-block:: python

    from infmidi import Midi
    mid = Midi.read('/path/to/xxx.mid')

    # 做一些修改
    ...

    mid.save('/path/to/xxx.mid')


添加轨道
--------

``Midi`` 的轨道储存在属性 ``tracks`` 里。

.. code:: python

    # 在初始化时
    track0 = Track(name='Chord Track', channel=0, instrument=0)
    mid = Midi([track0])

    # 使用函数 new_track, 会根据已有轨道数量来设置通道
    track1 = mid.new_track(name='Melody Track', instrument="Acoustic Guitar(nylon)")

    # 直接添加
    track2 = Track(name='Drum track', is_drum=True)
    mid.tracks.append(track2)


名字
----
用 ``name`` 属性给你的歌曲命名

.. code:: python 

    Midi(name="Fly Me to The Moon")


静音
----

.. code:: python

    # 把轨道0、 1、 7静音
    mid.mute([0, 1, 7])

    # 激活轨道0、 1、 2，并把剩余轨道静音
    mid.activate([0, 1, 2])