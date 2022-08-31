Event
=====


.. note::
    如果你对MIDI协议不太熟悉，建议你先学习后续核心类( :doc:`Note <./note>`, :doc:`Clip<./clip>`, :doc:`Track <./track>` 和 :doc:`Midi <./midi>` ) 。


Channel events
--------------
下列事件都有一个 ``channel`` 属性，

NoteOff
^^^^^^^

    >>> from infmidi import NoteOff
    >>> NoteOff('A4')
    NoteOff(name="A4", value=69, frequency=440.00, velocity=127, location=0.00, channel=0)

.. note::
    使用 :doc:`Note <./note>` 可以更方便的创建音符。



NoteOn
^^^^^^

    >>> from infmidi import NoteOn
    >>> NoteOn('A4')
    NoteOn(name="A4", value=69, frequency=440.00, velocity=127, location=0.00, channel=0)

.. note::
    使用 :doc:`Note <./note>` 可以更方便的创建音符。


NotePressure
^^^^^^^^^^^^

    >>> from infmidi import NotePressure
    >>> NotePressure('A4')
    NotePressure(name="A4", value=69, frequency=440.00, pressure=127, location=0.00, channel=0)


.. todo:: 

    该事件后续可能会添加到 :doc:`Note <./note>` 中。




ControlChange
^^^^^^^^^^^^^

    >>> from infmidi import ControlChange as CC
    >>> CC(0, 66)
    >>> ControlChange(control=0, value=66, description="Bank Select", location=0.00, channel=0)

.. hint:: 

    点击 :doc:`速查表/CC <../cheat>`  查看CC的完整列表


ProgramChange
^^^^^^^^^^^^^


    >>> from infmidi import ProgramChange as PC
    >>> PC(0)
    ProgramChange(id=0, name="Acoustic Grand Piano", location=0.00, channel=0)
    >>> PC("Acoustic Guitar(nylon)")
    ProgramChange(id=24, name="Acoustic Guitar(nylon)", location=0.00, channel=0)

.. hint:: 

    点击 :doc:`速查表/GM Instrument <../cheat>` 查看GM 乐器的完整列表。

ChannelPressure
^^^^^^^^^^^^^^^

    >>> from infmidi import ChannelPressure as CP
    >>> CP(66, channel=10)
    ChannelPressure(pressure=66, location=0.00, channel=10)


PitchBend
^^^^^^^^^

    >>> from infmidi import PitchBend as PB
    >>> PB(0.5)
    PitchBend(pitch=0.50, location=0.00, channel=0)


.. todo::

    该事件后续可能会添加到 :doc:`Note <./note>` 中，来实现微分音。



Sysex events
------------

TODO.
^^^^^

Meta events
-----------

Text
^^^^

    >>> from infmidi import Text
    >>> Text('text')
    Text(text="text", location=0.00)

Copyright
^^^^^^^^^

    >>> from infmidi import Copyright
    >>> Copyright('text')
    Copyright(text="text", location=0.00)

Lyric
^^^^^

    >>> from infmidi import Lyric
    >>> Lyric('text')
    Lyric(text="text", location=0.00)

Marker
^^^^^^

    >>> from infmidi import Marker
    >>> Marker('text')
    Marker(text="text", location=0.00)

CuePoint
^^^^^^^^

    >>> from infmidi import CuePoint
    >>> CuePoint('text')
    CuePoint(text="text", location=0.00)

TrackName
^^^^^^^^^

    >>> from infmidi import TrackName
    >>> TrackName("Melody track")
    TrackName(name="Melody track", location=0.00)

.. warning::
    你不需要使用这个事件， ``Track`` 和 ``Midi`` 都有一个 ``name`` 属性，设置该属性会自动生成``TrackName``事件。


SetBpm
^^^^^^

    >>> from infmidi import SetBpm
    >>> SetBpm(123. , location=32.)
    SetBpm(bpm=123.00, location=32.00)

.. note::



TimeSignature
^^^^^^^^^^^^^

如果你的 midi 文件只有一个主要的拍号，使用类似 ``Midi(time_signature="4/4")`` 来初始化你的 ``Midi`` 对象。 否则， 使用 ``mid.add(TimeSignature("3/4"), location)`` 在 ``location`` 节拍处添加额外的拍号。

    >>> from infmidi import TimeSignature
    >>> TimeSignature('4/4')
    >>> TimeSignature(signature="4/4", location=0.00)
    >>> signature = TimeSignature('3/4')
    >>> signature.numerator
    >>> 3
    >>> signature.denominator
    >>> 4


KeySignature
^^^^^^^^^^^^

如果你的 midi 文件只有一个主调，使用 like ``Midi(key_signature="C#")`` 来初始化你的 ``Midi`` 对象。 否则，使用 ``mid.add(KeySignature("C#"), location)`` 在``location`` 节拍处添加额外的调号。

    >>> from infmidi import KeySignature
    >>> KeySignature('C#')
    >>> KeySignature(signature="C#", location=0.00)


SequencerSpecific
^^^^^^^^^^^^^^^^^
    
    >>> from infmidi import SequencerSpecific
    >>> SequencerSpecific(data=(11, 22, 33))
    SequencerSpecific(data=(11, 22, 33), location=0.00)