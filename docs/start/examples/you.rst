You
===


初始化
------

.. code-block:: python

    from infmidi import Clip, sheet, FluidSynth

    synth = FluidSynth()
    clip = Clip()

添加和弦分解
------------

.. code-block:: python

    txt = '''
        A2 E3 G3 - F2 C3 E3 - |
        G2 D3 F3 - C3 G3 B3 - 
    '''
    clip += sheet(txt) ** 2


添加旋律
--------

.. code-block:: python
    
    txt = '''
        D5 - (E5 D5) C5 D5 G4 (E5 D5) C5 |
        D5 - (E5 D5) C5 C5 G5 D5      -  |
        D5 - (E5 D5) C5 D5 G4 (E5 D5) C5 |
        D5 - (E5 D5) C5 C5 -  B4      -  
    '''
    clip += sheet(txt)


播放
----

.. code-block:: python

    synth(clip, bpm=80)


完整代码
--------

.. literalinclude:: ../../../examples/you.py
    :caption: you.py
    :language: python
    :linenos:
