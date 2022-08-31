Controller
==========

Controller 用来与编曲软件交互。

配置
----

Linux
^^^^^

Mac
^^^

1. 打开 **音频MIDI设置**。
2. 在顶部菜单栏选择 **窗口>显示MIDI工作室**。
3. 打开 **IAC Driver** 新建端口。
4. 修改编曲软件轨道的输入设备。

Windows
^^^^^^^



获取可用设备
------------

下面是我的Mac上的输出，其中 **IAC Driver Bus 1** 是我在Mac上配置的虚拟MIDI设备

    >>> from infmidi import Controller
    >>> Controller.get_avaliable_devices()
    ['IAC Driver Bus 1',
    'IAC Driver Bus 1',
    'to Max 1',
    'to Max 2',
    'FluidSynth virtual port (84878)']

初始化
------

    >>> ctl = Controller('IAC Driver Bus 1')

发送MIDI信息
------------
    
    >>> ctl(item) # item 可以是 Event、 Note、 Clip、 Track 或 Midi。
