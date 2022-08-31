快速开始
========

Let's start by creating a simple version of  *Fly Me to the Moon*.


初始化Midi对象
--------------

.. code-block:: python

    from infmidi import Midi
    song = Midi(bpm=123, time_signature='4/4', key_signature='C')


轨道1
------------------

使用 :func:`sheet() <infmidi.generate.sheet>` 快速生成一段和弦进行。


.. code-block:: python
    
    track1 = song.new_track('chord track', instrument="Acoustic Grand Piano")

    txt = '''
        A4:m7 | D4:m9   | G4:7 | C4:M7     |
        F4:M7 | B3:m7-5 | E4:7 | A4:m7 A4:7
    '''

    progression = sheet(txt)
    track1.add(progression)

轨道2
-------------------

.. code-block:: python
    
    track2 = song.new_track('melody track', instrument="Acoustic Grand Piano")

    txt = '''
        (C5 -)  (-  B4)  (A4 G4)  (- F4) | (-  -)  (- G4)  (A4 C5)  (- B4) | 
         -      (-  A4)  (G4 F4)  (- E4) |  -               0              | 
        (A4 -)  (-  G4)  (F4 E4)  (- D4) |  -      (- E4)  (F4  A4)  -     |
         G#4    (F4 E4)  (-  D4)  (- C4) |  -       -       -        C#4   
    '''
    melody = sheet(txt)
    track2.add(melody)


播放Midi
-----------------


使用 :doc:`FluidSynth <./devices/fluidsynth>` 来播放Midi。

.. code-block:: python

    from infmidi.devices import FluidSynth


使用 :class:`Controller <./devices/controller>` 来与编曲软件交互。

.. code-block:: python

    from infmidi.devices import Controller