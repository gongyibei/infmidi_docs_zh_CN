Note
====

``Note`` 包含了 ``NoteOn`` 与 ``NoteOff`` 两个事件，可以帮助你快速生成音符。


初始化
----------

.. admonition:: A4=69 or 81?
    :class: note

    不同的库、编曲软件可能会有不同的标准，本项目中设定 A4=69


不同方法初始化 ``Note``。

.. code-block:: python


    >>> from infmidi import Note
    >>> Note('A4')
    Note(name="A4", value=69, frequency=440.00, location=0.00, length=1.00, velocity=127, channel=0)
    >>> Note('A4') == Note(69) == Note(440.)
    True


.. hint:: 

    ``name``、 ``value`` 和 ``frequency`` 这三个属性是相互关联的，改变其中一个，另外两个也会改变。



转调
----

Use ``-`` or ``+`` to change the value.

.. code-block:: python

    >>> Note('A4') - 12 == Note('A3')
    True
    >>> Note('A4') + 12 == Note('A5')
    True
    >>> Note('A4') + 8
    Note(name="F5", value=77, frequency=698.46, location=0.00, length=1.00, velocity=127, channel=0)


平移
----

Use ``>>`` or ``<<`` to change the location.

.. code-block:: python

    >>> Note('A4', location=2.) >> 4
    Note(name="A4", value=69, frequency=440.00, location=6.00, length=1.00, velocity=127, channel=0)
    >>> Note('A4', location=4.) << 2
    Note(name="A4", value=69, frequency=440.00, location=2.00, length=1.00, velocity=127, channel=0)


缩放
---- 

Use ``^`` and ``*`` to zoom and scale the note.

.. code-block:: python

    >>> Note('A4', location=2., length=3.) ^ 3
    Note(name="A4", value=69, frequency=440.00, location=6.00, length=9.00, velocity=127, channel=0)
    >>> Note('A4', location=2., length=3.) * 3
    Note(name="A4", value=69, frequency=440.00, location=2.00, length=9.00, velocity=127, channel=0)

通道
----

使用 ``@`` 来修改音符的通道

.. code-block:: python

    >>> Note('A4', channel=7)
    Note(name="A4", value=69, frequency=440.00, location=0.00, length=1.00, velocity=127, channel=7)
    >>> Note('A4', channel=7) @ 12
    Note(name="A4", value=69, frequency=440.00, location=0.00, length=1.00, velocity=127, channel=12)

.. hint:: 

    All operators above have an inpalce version and an method version, click :doc:`here <../cheat>` to see the cheat sheet.