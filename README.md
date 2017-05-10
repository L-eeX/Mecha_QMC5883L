# Mechasolution QMC5883 Library

HMC5883 지자기 나침반 센서의 수명 만료(EOL)로인해 그동안의 HMC5883 센서는 생산이 중단 되었고, 중국의 대체 상품인 QMC5883으로 변경이 되었습니다.

## Arduino Code

There are a few simple rules for using that library. Please read the following summary and apply it to your project

### Basic Elements

Required header files (#include ...) and Setup side code.

```cpp
#include <Wire.h>
#include <MechaQMC5883.h>

void setup(){
  Wire.begin();
}
```

### Object Declaration

The object declaration method. It is used outside the setup statement, and a name such as qmc can be changed to any other name you want.

```cpp
#include <Wire.h>
#include <MechaQMC5883.h>

MechaQMC5883 qmc;
```

### initialization

QMC5883 Sensor's setting function.

The init function allows you to take advantage of the features of the QMC5883 sensor by default.

```cpp
void setup(){
    Wire.begin();
    qmc.init();
}
```

If you want more detailed settings, you can use it as follows.

```cpp
void setup(){
  Wire.begin();
  qmc.init();
  qmc.setMode(Mode_Standby,ODR_200Hz,RNG_8G,OSR_512);
}
```

The values ​​used for setMode can take the following values:

```
Mode : Mode_Standby / Mode_Continuous

ODR : ODR_10Hz / ODR_50Hz / ODR_100Hz / ODR_200Hz
ouput data update rate

RNG : RNG_2G / RNG_8G
magneticfield measurement range

OSR : OSR_512 / OSR_256 / OSR_128 / OSR_64
over sampling rate
```

### Read values

How to read the measured sensor value is as follows.

```cpp
void loop(){
  int x,y,z;

  qmc.read(&x,&y,&z);
}
```

## Basic example

It can be seen as a collection of the contents mentioned above.

```cpp
#include <Wire.h>
#include <MechaQMC5883.h>

MechaQMC5883 qmc;

void setup() {
  Wire.begin();
  Serial.begin(9600);
  qmc.init();
  //qmc.setMode(Mode_Continuous,ODR_200Hz,RNG_2G,OSR_256);
}

void loop() {
  int x,y,z;
  qmc.read(&x,&y,&z);

  Serial.print("x: ");
  Serial.print(x);
  Serial.print(" y: ");
  Serial.print(y);
  Serial.print(" z: ");
  Serial.print(z);
  Serial.println();
  delay(100);
}
```
