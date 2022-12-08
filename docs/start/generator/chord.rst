chord
=====

使用全名
--------------

.. code-block:: python

    >>> from infmidi import chord
    >>> chd = chord('C4:mM7')
    >>> chd.notes
    NoteSet([
      Note(name="C4", value=60, frequency=261.63, velocity=127, length=1.00, location=0.00, channel=0),
      Note(name="D#4", value=63, frequency=311.13, velocity=127, length=1.00, location=0.00, channel=0),
      Note(name="G4", value=67, frequency=392.00, velocity=127, length=1.00, location=0.00, channel=0),
      Note(name="B4", value=71, frequency=493.88, velocity=127, length=1.00, location=0.00, channel=0)
    ])



使用和弦类型
---------------

.. code-block:: python

    >>> chd = chord('C4', 'mM7')
    >>> chd.notes
    NoteSet([
      Note(name="C4", value=60, frequency=261.63, velocity=127, length=1.00, location=0.00, channel=0),
      Note(name="D#4", value=63, frequency=311.13, velocity=127, length=1.00, location=0.00, channel=0),
      Note(name="G4", value=67, frequency=392.00, velocity=127, length=1.00, location=0.00, channel=0),
      Note(name="B4", value=71, frequency=493.88, velocity=127, length=1.00, location=0.00, channel=0)
    ])


使用音程
--------------

.. code-block:: python

    >>> chd = chord('C4', [3, 4, 4])
    >>> chd.notes
    NoteSet([
      Note(name="C4", value=60, frequency=261.63, velocity=127, length=1.00, location=0.00, channel=0),
      Note(name="D#4", value=63, frequency=311.13, velocity=127, length=1.00, location=0.00, channel=0),
      Note(name="G4", value=67, frequency=392.00, velocity=127, length=1.00, location=0.00, channel=0),
      Note(name="B4", value=71, frequency=493.88, velocity=127, length=1.00, location=0.00, channel=0)
    ])


使用音级
-------------

.. code-block:: python

    >>> chd = chord('C4', ['1', 'b3', '5', '7'])
    >>> chd.notes
    NoteSet([
      Note(name="C4", value=60, frequency=261.63, velocity=127, length=1.00, location=0.00, channel=0),
      Note(name="D#4", value=63, frequency=311.13, velocity=127, length=1.00, location=0.00, channel=0),
      Note(name="G4", value=67, frequency=392.00, velocity=127, length=1.00, location=0.00, channel=0),
      Note(name="B4", value=71, frequency=493.88, velocity=127, length=1.00, location=0.00, channel=0)
    ])    
