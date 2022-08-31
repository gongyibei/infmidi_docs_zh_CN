基础
====

INFMIDI抽象出了5种核心类(``Event``, ``Note``, ``Clip``, ``Track``, ``Midi``)来构建整个MIDI世界。

- :doc:`event` : Midi事件类。一般情况下，你不需要直接使用它。
- :doc:`note`  : 包含了 ``NoteOn`` 与 ``NoteOff`` 两个事件，帮助你快速生成音符。
- :doc:`clip`  : INFMIDI的核心类，相当于一个音乐片段。用来组织你的音符( ``Note`` )和事件( ``Event`` ), 有很多高级操作。
- :doc:`track` : ``Clip`` 的子类，附加了一些额外属性 （ ``name`` 、 ``instrument`` 和 ``mute`` 等）。
- :doc:`midi`  : 由多个轨道（ ``Track`` ）组成。


.. toctree::
    :hidden:
    
    event
    note
    clip
    track
    midi

