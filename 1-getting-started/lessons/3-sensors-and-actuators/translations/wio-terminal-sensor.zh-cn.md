# 添加传感器 - Wio 终端

在这部分课程里，你将向 Wio 终端添加光传感器。

## 硬件

本课程的传感器是使用 [光电二极管](https://wikipedia.org/wiki/Photodiode) 将光转换为电信号的 **光传感器**。这是一个模拟传感器，它发送一个从 0 到 1，023 的整数值，表示光照值的相对量而不对应任何比如[勒克斯（lux）](https://wikipedia.org/wiki/Lux)的标准计量单位。

光传感器内置于Wio终端中，可通过背面的透明塑料窗口看到。

![The light sensor on the back of the Wio Terminal](../../../images/wio-light-sensor.png)

## 对光传感器进行编程

现在设备可以用光照传感器来编程了。

### 任务

对设备进行编程。

1. 在 VS Code 中打开上一部分创建的夜灯项目。

2. 将以下代码添加到 `setup` 函数的尾部：

    ```cpp
    pinMode(WIO_LIGHT, INPUT);
    ```

    此行代码用于初始化与传感器通信的引脚。

    `WIO_LIGHT` 是连接到板载光传感器的 GPIO 引脚的编号。此引脚设置为 `INPUT`，表示将其连接到传感器后，从此引脚读取数据。

3. 删除 `loop` 函数的内容。

4. 将以下代码添加到 `loop` 函数中。

    ```cpp
    int light = analogRead(WIO_LIGHT);
    Serial.print("Light value: ");
    Serial.println(light);
    ```

    此代码从 `WIO_LIGHT` 引脚读取模拟值。即从板载光传感器读取 0-1，023 之间的值。然后此值将被发送到串口，以便代码运行时在串行监视器查看。 `Serial.print` 写入文本时并不回车换行，因此每行将以 `Light value:` 开头，实际光线值结尾。

5. 鉴于光线强度无需持续获取，可在 `loop` 结尾处添加一秒（1，000ms）的延迟。该延迟可降低设备功耗。

    ```cpp
    delay(1000);
    ```

1. 将 Wio 终端重新连接到计算机，然后像之前一样上传此代码。

1. 连接串行监视器。光线值将在终端输出。盖上或揭开 Wio 终端背面的光传感器，数值将发生变化。

    ```output
    > Executing task: platformio device monitor <

    --- Available filters and text transformations: colorize, debug, default, direct, hexlify, log2file, nocontrol, printable, send_on_enter, time
    --- More details at http://bit.ly/pio-monitor-filters
    --- Miniterm on /dev/cu.usbmodem101  9600,8,N,1 ---
    --- Quit: Ctrl+C | Menu: Ctrl+T | Help: Ctrl+T followed by Ctrl+H ---
    Light value: 4
    Light value: 5
    Light value: 4
    Light value: 158
    Light value: 343
    Light value: 348
    Light value: 344
    ```

> 💁 你可以在 [code-sensor/wio-terminal](code-sensor/wio-terminal) 文件夹中找到此代码。

😀 你已成功向夜灯添加了传感器！
