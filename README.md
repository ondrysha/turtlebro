**МОДУЛЬ А**

Присвоенное имя робота в сети:
```
turtlebroXX    
```
IР-адрес робота в сети роутера-полигона:
```
192.168.1.XX
```
Текущая частота подключения робота к сети 5 ГГц:
```
iwconfig
```
Скорость передачи данных через сетевой интерфейс робота(Мбит/с):
```
iperf3 -c 192.168.1.XX
```
Название дистрибутива и кодовое имя сборки Linux:
```
lsb_release -a
```
Версия интерпретатора Python3:
```
python3 -V
```
Версия библиотеки rospy:
```
rosversion rospy
```
Версия библиотеки turtlebro:
```
rosversion turtlebro
```
Версия прошивки микроконтроллера материнской платы и серийный номер системной платы робота:
```
rosservice call /board_info {}
```
Размер оперативной памяти (Мбайт):
```
free -m
```
Текущий часовой пояс на роботе в формате "Time
zone:Continent/City (XXX, +XXXX)":
```
timedatectl|grep "Time zone"
```
Серийный номер Raspberry Pi 4:
```
cat /sys/firmware/devicetree/base/serial-number
```
Топики из инструкции к роботу присутствуют на роботе:
```
rostopic list
```
Температура процессора в градусах (С):
```
vcgencmd measure_temp
```
Текущее разрешение камеры(пикселей):
```
rostopic echo /camera/image_raw

```
Значение напряжения аккумуляторной сборки из топика батареи:
```
import rospy
from sensor_msgs.msg import BatteryState

def battery_callback(msg):
    # Вывод напряжения батареи
    print(f"Напряжение батареи: {msg.voltage} В")

# Инициализация ROS-ноды
rospy.init_node('battery_monitor_node')

# Подписка на топик с состоянием батареи
rospy.Subscriber('/battery_state', BatteryState, battery_callback)

# Ожидание сообщений
rospy.spin()
```
IMU датчик работает корректно:
```
rostopic list
rostopic echo /imu/data
```
Лидар работает корректно:
```
rostopic echo /scan

import rospy
from sensor_msgs.msg import LaserScan

def lidar_callback(msg):
    # Получение данных о расстояниях
    print(f"Расстояния до объектов: {msg.ranges[:10]} ...")  # Вывод первых 10 значений
    # Анализ ближнего объекта
    min_distance = min(msg.ranges)
    print(f"Минимальное расстояние: {min_distance:.2f} м")

# Инициализация ROS-ноды
rospy.init_node('lidar_test_node')
rospy.Subscriber('/scan', LaserScan, lidar_callback)
rospy.spin()

```
Стерео-акустическая система работает корректно:
```
rostopic echo /audio/left
```
Датчик тепловизор работает корректно:
```
rostopic echo /thermal_camera/image_raw
```
Концевой выключатель работает корректно:
```
rostopic echo /limit_switch

```
Светодиодная подсветка работает корректно:
```
rostopic echo /led_control
rostopic echo /led_state

```
Кнопки  D22-25 работают:
```
void setup() {
  // Инициализация пинов как входов с подтягивающими резисторами
  pinMode(22, INPUT_PULLUP);
  pinMode(23, INPUT_PULLUP);
  pinMode(24, INPUT_PULLUP);
  pinMode(25, INPUT_PULLUP);

  // Инициализация последовательного порта для вывода данных
  Serial.begin(9600);
}

void loop() {
  // Чтение состояния кнопок
  int buttonState22 = digitalRead(22);
  int buttonState23 = digitalRead(23);
  int buttonState24 = digitalRead(24);
  int buttonState25 = digitalRead(25);

  // Вывод состояния кнопок в консоль
  Serial.print("Button D22: ");
  Serial.println(buttonState22 == LOW ? "Pressed" : "Released");

  Serial.print("Button D23: ");
  Serial.println(buttonState23 == LOW ? "Pressed" : "Released");

  Serial.print("Button D24: ");
  Serial.println(buttonState24 == LOW ? "Pressed" : "Released");

  Serial.print("Button D25: ");
  Serial.println(buttonState25 == LOW ? "Pressed" : "Released");

  // Задержка перед следующим считыванием
  delay(100);
}

```
Связь контроллера расширения с ROS работает:
```

```
**МОДУЛЬ Б**
```
grep "ошибка" master.log > error message.txt
```
b2.2
```
from datetime import datetime
def counter(time1, time2, times_format="%H:%M:%S"):
    a1 = datetime.strptime(time1, times_format)
    a2 = datetime.strptime(time2, times_format)
    b = a2 - a1
    return b
time1 = "times"
time2 = "times"
c = counter(time1,time2)
print("Разница во времени:",с)
```
