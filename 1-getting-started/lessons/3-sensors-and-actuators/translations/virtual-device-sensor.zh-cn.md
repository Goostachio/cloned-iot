# 制作夜灯 - 利用虚拟 IOT 硬件

在这部分课程里，你将向虚拟 IOT 硬件添加光传感器。

## 虚拟硬件

制作夜灯需要在 CounterFit 应用程序中添加一个传感器。

这就是 **光传感器**。 在实际的 IOT 设备中，它是可将光转换为电信号的 [光电二极管](https://wikipedia.org/wiki/Photodiode)。 光传感器是模拟信号传感器，可感知光的强度并发送对应数值，但其并使用任何标准测量单位，如[lux](https://wikipedia.org/wiki/Lux)。

### 添加传感器到 CounterFit

要使用虚拟光传感器，需将其添加到 CounterFit 应用程序中

#### 任务 - 在 CounterFit 中添加传感器

在 CounterFit 应用程序中添加传感器。

1. 请确保 CounterFit web 应用接着上一部分的任务继续运行。否则，重启app。

1. 添加光传感器:

    1. 在 *Sensors* 窗格的 *Create sensor* 框中，下拉 *Sensor type* 并选择 *light*

    1. 将 *Units* 设置为 *NoUnits*

    1. 确保*Pin* 设置为 *0*

    1. 点击 **Add** 按钮在 *pin 0* 添加光传感器

    ![光传感器设置](../../../images/counterfit-create-light-sensor.png)

    The light sensor will be created and appear in the sensors list.

    ![成功添加光传感器](../../../images/counterfit-light-sensor.png)

## 对光传感器进行编程

该设备现在可作为内置光传感器编程使用。

### 任务 - 对光传感器进行编程

对设备进行编程。

1. 在 VS Code 中打开上一部分创建的夜灯项目。如有必要，重启终端以确保它使用虚拟环境运行。

1. 打开 `app.py`

1. 将以下代码添加到 `app.py` 中的 `import` 关键字后以添加依赖库。

    ```python
    import time
    from counterfit_shims_grove.grove_light_sensor_v1_2 import GroveLightSensor
    ```

    `import time` 语句添加了 Python的 `time` 模块，此模块将在后续代码中使用。

    `from counterfit_shims_grove.grove_light_sensor_v1_2 import GroveLightSensor` 语句从 CounterFit Grove shim Python 库导入  `GroveLightSensor` 模块。其作用是在 CounterFit 应用中与光传感器交互。

1. 将以下代码添加到代码底部，以初始化管理光传感器的实例：

    ```python
    light_sensor = GroveLightSensor(0)
    ```

    `light_sensor = GroveLightSensor(0)` 语句创建 `GroveLightSensor` 实例 - 并将光传感器连接到 CounterFit Grove 的引脚 **0** 上。

1. 在以上代码后添加一个无限循环，以轮询光传感器值并在控制台显示：

    ```python
    while True:
        light = light_sensor.light
        print('Light level:', light)
    ```

    使用 `GroveLightSensor` 类中的 `light` 属性获取当前光线强度。该属性从引脚读取模拟信号值，此值将被在控制台显示。

1. 鉴于光线强度无需持续获取，可在 `while` 循环结尾处添加 1 秒的睡眠。睡眠可降低设备功耗。

    ```python
    time.sleep(1)
    ```

1. 在 VS 终端运行 Python 程序：

    ```sh
    python3 app.py
    ```

    光线值将输出到控制台。此值初始为 0。

1. 在 CounterFit 应用中可修改光传感的值。可通过如下方法：

    * 在光传感器的 *Value* 框中输入所需数值，然后点击 **Set** 按钮。该数值将被传感器返回。

    * 点击 *Random* 选项, 在 *Min* 和 *Max* 中分别输入数值，然后点击 **Set** 按钮。每次的传感器数值将在 *Min* and *Max* 之间波动。

	设置的值将在控制台显示。通过选择 *Value* 或 *Random* 方式来改变数值。

    ```output
    (.venv) ➜  GroveTest python3 app.py 
    Light level: 143
    Light level: 244
    Light level: 246
    Light level: 253
    ```

> 💁 你可以在 [code-sensor/virtual-device](code-sensor/virtual-device) 文件夹中找到此代码。

😀 你的夜灯程序很成功！
