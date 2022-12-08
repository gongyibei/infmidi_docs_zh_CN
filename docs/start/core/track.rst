Track
=====


名字
----

.. code:: python 

    Track(name='Melody track')


乐器
----

.. code:: python 

    # 设置乐器
    track = Track(instrument=0)
    track = Track(instrument="Acoustic Grand Piano")
    track.instrument = "Acoustic Guitar(nylon)"

.. note::

    点击 :doc:`速查表/GM Instrument <../cheat>` 查看GM 乐器的完整列表。


通道
-----
``Track`` 有一个通道属性 ``channel``，如果该属性会不为 ``None`` 则会用其覆盖音符与事件的通道。
使用该属性的好处是不用单独设置音符和事件的通道。

.. code:: python 


    # 设置通道
    Track(channel=5)

    # 设置鼓 ``Track``
    Track(is_drum=True)
    Track(channel=9)

    # 更改channel
    track.channel = 6

静音
-----
设置 ``Track`` 为静音并不会改变音符和事件。只是在调用 ``messages()`` 方法时，不会返会音符与事件的message， 这些message会在播放的时候以及保存称MIDI文件时会用到。

.. code:: python

    # 初始化时设置静音
    Track(mute=True)

    # 改变属性
    track.mute = True


