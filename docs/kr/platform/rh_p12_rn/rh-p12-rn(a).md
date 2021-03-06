---
layout: archive
lang: kr
ref: rh_p12_rn(a)
read_time: true
share: true
author_profile: false
permalink: /docs/kr/platform/rh_p12_rn(a)/
sidebar:
  title: RH-P12-RN(A)
  nav: "rh_p12_rn(a)"
---

# [개요](#개요)

![](/assets/images/platform/rh_p12_rn/rh-p12-rn_product.png)

> RH_P12_RN(A)

# [주요 사양](#주요-사양)

| 항목                | 사양                                                                                           |
|:--------------------|:-----------------------------------------------------------------------------------------------|
| MCU                 | ST CORTEX-M4 (STM32F405 @ 168Mhz, 32bit)                                                       |
| 위치 센서           | Contactless Absolute Encoder (12bit, 360&deg;)<br />Maker : ams(www.ams.com), Part No : AS5045 |
| 모터                | Coreless                                                                                       |
| 통신 속도           | 9,600 bps ~ 10.5 Mbps                                                                          |
| 제어 알고리즘       | PID Control                                                                                    |
| 정밀도              | 0.088&deg;                                                                                     |
| 동작 모드           | 전류제어 모드<br />전류기반 위치제어 모드                                                |
| 무게                | 500g                                                                                           |
| 스트로크            | 0 ~ 109mm                                                                                      |
| 감속비              | 1295.7 : 1                                                                                     |
| 최대 파지력         | 170N                                                                                           |
| 권장 가반하중       | 5kg                                                                                            |
| 동작 온도           | -5&deg;C ~ 55&deg;C                                                                            |
| 사용 전압           | 24V                                                                                            |
| Command Signal      | Digital Packet                                                                                 |
| Protocol Type       | RS485 Asynchronous Serial Communication<br />(8bit, 1stop, No Parity)                          |
| Physical Connection | RS485 Multidrop Bus                                                                            |
| ID                  | 0 ~ 252                                                                                        |
| Feedback            | Position, Velocity, Current, Temperature, Input Voltage, etc                                   |
| Material            | Full Metal Gear, Metal Body                                                                    |
| Standby Current     | 30mA                                                                                           |
| Peak Current        | 3.33A                                                                                          |

{% include kr/dxl/warning.md %}

{% include kr/dxl/control_table_protocol2.md %}

## [EEPROM 영역](#eeprom-영역)

| 주소 | 크기<br>(Byte) | 명칭                                        | 의미                 | 접근 | 기본값 |             범위               | 단위 |
|:----:|:--------------:|:--------------------------------------------|:--------------------|:----:|:------:|:----------------------------:|:------:|
|  0   |       2        | [Model Number](#model-number)               | 보델 번호            |  R   | 51,201  |              -               | - |
|  2   |       4        | [Model Information](#model-information)     | 모델 정보            |  R   |   -    |              -               | - |
|  6   |       1        | [Firmware Version](#firmware-version)       | 펌웨어 버전          |  R   |   -    |              -               | - |
|  7   |       1        | [ID](#id)                                   | 통신 ID             |  RW  |   1    |           0 ~ 252            | - |
|  8   |       1        | [Baud Rate](#baud-rate)                     | 통신 속도            |  RW  |   1    |            0 ~ 9              | - |
|  9   |       1        | [Return Delay Time](#return-delay-time)     | 응답 지연 시간       |  RW  |  250   |           0 ~ 255            | 2 [μsec] |
|  10  |       1        | [Drive Mode](#drive-mode)                   | 구동모드             |  RW  |   0    |            0 ~ 1             | - |
|  11  |       1        | [Operating Mode](#operating-mode)           | 동작모드             |  RW  |   5    |            0, 5              | - |
|  12  |       1        | [Sencondary ID](#secondary-id)              | 보조 ID              |  RW  |  255   |           0 ~ 255           | - |
|  20  |       4        | [Homing Offset](#homing-offset)             | 0점 위치 조정 값     |  RW  |   0    | -2,147,483,648 ~<br> 2,147,483,647 | 1 [pulse] |
|  24  |       4        | [Moving Threshold](#moving-threshold)       | 움직임 감지 기준 값  |  RW  |   50   | -2,147,483,648 ~<br> 2,147,483,647 | 0.01 [rev/min] |
|  31  |       1        | [Temperature Limit](#temperature-limit)     | 내부 한계 온도       |  RW  |   80   |           0 ~ 100            | 1 [℃] |
|  32  |       2        | [Max Voltage Limit](#max-voltage-limit)     | 최대 한계 전압       |  RW  |  350   |           0 ~ 350            | 0.1 [V] |
|  34  |       2        | [Min Voltage Limit](#min-voltage-limit)     | 최소 한계 전압       |  RW  |  150   |           0 ~ 350            | 0.1 [V] |
|  36  |       2        | [PWM Limit](#pwm-limit)                     | PWM 한계값           |  RW  | 2,009  |         0 ~ 2,009           | - |
|  38  |       2        | [Current Limit](#current-limit)             | 최대 한계 전류       |  RW  |  1,984 |          0 ~ 1,984          | 1 [mA] |
|  40  |       4        | [Acceleration Limit](#acceleration-limit)   | 가속도 최대 값       |  RW  |  3,447 |          0 ~ 1,378,788      | 1 [rev/min²] |
|  44  |       4        | [Velocity Limit](#velocity-limit)           | 최대 속도 값         |  RW  |  2,970 |          0 ~ 2,970          | 0.01 [rev/min] |
|  48  |       4        | [Max Position Limit](#max-position-limit)   | 최대 위치 제한 값    |  RW  |  1,150 |         0 ~<br> 1,150      | 1 [pulse] |
|  52  |       4        | [Min Position Limit](#min-position-limit)   | 최소 위치 제한 값    |  RW  |   0    |          0 ~<br> 1,150     | 1 [pulse] |
|  57  |       1        | [External Port Mode 2](#external-port-mode) | 외부 포트 모드 2     |  RW  |   3    |            0 ~ 3             | - |
|  56  |       1        | [External Port Mode 1](#external-port-mode) | 외부 포트 모드 1     |  RW  |   3    |            0 ~ 3             | - |
|  58  |       1        | [External Port Mode 3](#external-port-mode) | 외부 포트 모드 3     |  RW  |   3    |            0 ~ 3             | - |
|  59  |       1        | [External Port Mode 4](#external-port-mode) | 외부 포트 모드 4     |  RW  |   3    |            0 ~ 3             | - |
|  63  |       1        | [Shutdown](#shutdown)                       | 셧다운 에러 정보     |  RW  |   52   |           0 ~ 255            | - |
| 168  |       2        | [Indirect Address 1](#indirect-address)     | 간접 주소값 1        |  RW  |  634   |          512 ~ 1,023          | - |
| 170  |       2        | [Indirect Address 2](#indirect-address)     | 간접 주소값 2        |  RW  |  635   |          512 ~ 1,023          | - |
| 172  |       2        | [Indirect Address 3](#indirect-address)     | 간접 주소값 3        |  RW  |  636   |          512 ~ 1,023          | - |
| ...  |      ...       | ...                                         | ...                 | ...  |  ...   |             ...               | ... |
| 422  |       2        | [Indirect Address 128](#indirect-address)   | 간접 주소값 128      |  RW  |  761   |          512 ~ 1,023          | - |

## [RAM 영역](#ram-영역)

| 주소 | 크기<br />(Byte) | 명칭                                              | 의미                    | 접근 | 기본값 |                        범위                            |  단위 |
|:----:|:----------------:|:--------------------------------------------------|:------------------------|:----:|:------:|:---------------------------------------------------:|:------:|
| 512  |        1         | [Torque Enable](#torque-enable)                   | 토크 On/Off             |  RW  |   0    |                        0 ~ 1                        | - |
| 513  |        1         | [LED Red](#led-red)                               | Red LED 밝기 값         |  RW  |   0    |                       0 ~ 255                       | - |
| 514  |        1         | [LED Green](#led-green)                           | Green LED 밝기 값       |  RW  |   0    |                       0 ~ 255                       | - |
| 515  |        1         | [LED Blue](#led-blue)                             | Blue LED 밝기 값        |  RW  |   0    |                       0 ~ 255                       | - |
| 516  |        1         | [Status Return Level](#status-return-level)       | 응답 레벨               |  RW  |   2    |                        0 ~ 2                        | - |
| 517  |        1         | [Registered Instruction](#registered-instruction) | Instruction의 등록 여부 |  R   |   0    |                          -                          | - |
| 518  |        1         | [Hardware Error Status](#hardware-error-status)   | 하드웨어 에러 상태       |  R   |   0    |                          -                          | - |
| 524  |        2         | [Velocity I Gain](#velocity-i-gain)               | 속도 I 게인             |  RW  |   -    |                      0 ~ 32,767                      | - |
| 526  |        2         | [Velocity P Gain](#velocity-p-gain)               | 속도 P 게인             |  RW  |   -    |                      0 ~ 32,767                      | - |
| 528  |        2         | [Position D Gain](#position-p-gain)               | 위치 P 게인             |  RW  |   -    |                      0 ~ 32,767                      | - |
| 532  |        2         | [Position P Gain](#position-p-gain)               | 위치 P 게인             |  RW  |   -    |                      0 ~ 32,767                      | - |
| 530  |        2         | [Position I Gain](#position-p-gain)               | 위치 P 게인             |  RW  |   -    |                      0 ~ 32,767                      | - |
| 536  |        2         | [Feedforward 2nd Gain](#feedforward-2nd-gain)     | 피드포워드 2차 게인     |  RW  |   -    |                      0 ~ 32,767                      | - |
| 538  |        2         | [Feedforward 1st Gain](#feedforward-1st-gain)     | 피드포워드 1차 게인     |  RW  |   -    |                      0 ~ 32,767                      | - |
| 546  |        1         | [Bus Watchdog](#bus-watchdog)                     | 통신 워치독 시간        |  RW  |   -    |                       0 ~ 127                       | 20 [msec] |
| 548  |        2         | [Goal PWM](#goal-pwm)                             | 목표 PWM 값             |  RW  |   -    |         -PWM Limit(36) ~<br> PWM Limit(36)          | - |
| 550  |        2         | [Goal Current](#goal-current)                     | 목표 전류값             |  RW  |   0    |     -Current Limit(38) ~<br> Current Limit(38)      | 1 [mA] |
| 552  |        4         | [Goal Velocity](#goal-velocity)                   | 목표 속도값             |  RW  |   0    |    -Velocity Limit(44) ~<br> Velocity Limit(44)     | 0.01 [rev/min] |
| 556  |        4         | [Profile Acceleration](#profile-acceleration)     | 프로파일 가속도 값      |  RW  |   0    |           0 ~<br> Acceleration Limit(40)            | 1 [rev/min²] |
| 560  |        4         | [Profile Velocity](#profile-velocity)             | 프로파일 속도 값        |  RW  |   0    |             0 ~<br> Velocity Limit(44)              | 0.01 [rev/min] |
| 564  |        4         | [Goal Position](#goal-position)                   | 목표 위치 값            |  RW  |   -    | Min Position Limit(52) ~<br> Max Position Limit(48) | 1[pulse] |
| 568  |        2         | [Realtime Tick](#realtime-tick)                   | 실시간 타임 값          |  R   |   -    |                      0 ~ 32,767                     | 1 [msec] |
| 570  |        1         | [Moving](#moving)                                 | 움직임 유무             |  R   |   -    |                          -                          | - |
| 571  |        1         | [Moving Status](#moving-status)                   | 움직임 상태 값          |  R   |   -    |                          -                          | - |
| 572  |        2         | [Present PWM](#present-pwm)                       | 현재 PWM 값             |  R   |   -    |                          -                          | - |
| 574  |        2         | [Present Current](#present-current)               | 현재 전류 값            |  R   |   -    |                          -                          | 1 [mA] |
| 576  |        4         | [Present Velocity](#present-velocity)             | 현재 속도 값            |  R   |   -    |                          -                          | 0.01 [rev/min] |
| 580  |        4         | [Present Position](#present-position)             | 현재 위치 값            |  R   |   -    |                          -                          | 1 [pulse] |
| 584  |        4         | [Velocity Trajectory](#velocity-trajectory)       | 속도 궤적 값            |  R   |   -    |                          -                          | 0.01 [rev/min] |
| 588  |        4         | [Position Trajectory](#position-trajectory)       | 위치 궤적 값            |  R   |   -    |                          -                          | 1 [pulse] |
| 592  |        2         | [Present Input Voltage](#present-input-voltage)   | 입력 전압               |  R   |   -    |                          -                          | 0.1 [V] |
| 594  |        1         | [Present Temperature](#present-temperature)       | 현재 온도               |  R   |   -    |                          -                          | 1 [℃] |
| 600  |        2         | [External Port Data 1](#external-port-data)       | 외부 포트 데이터 1      | R/RW |   0    |                       0 ~ 4095                      | - |
| 602  |        2         | [External Port Data 2](#external-port-data)       | 외부 포트 데이터 2      | R/RW |   0    |                       0 ~ 4095                       | - |
| 604  |        2         | [External Port Data 3](#external-port-data)       | 외부 포트 데이터 3      | R/RW |   0    |                       0 ~ 4095                       | - |
| 606  |        2         | [External Port Data 4](#external-port-data)       | 외부 포트 데이터 4      | R/RW |   0    |                       0 ~ 4095                       | - |
| 634  |        1         | [Indirect Data 1](#indirect-data)                 | 간접 주소 데이터 1      |  RW  |   0    |                       0 ~ 255                       | - |
| 635  |        1         | [Indirect Data 2](#indirect-data)                 | 간접 주소 데이터 2      |  RW  |   0    |                       0 ~ 255                       | - |
| 636  |        1         | [Indirect Data 3](#indirect-data)                 | 간접 주소 데이터 3      |  RW  |   0    |                       0 ~ 255                       | - |
| ...  |       ...        | ...                                               | ...                    | ...  |  ...   |                         ...                         | ... |
| 761  |        1         | [Indirect Data 128](#indirect-data)               | 간접 주소 데이터 128    |  RW  |   0    |                       0 ~ 255                       | - |


## [컨트롤 테이블 설명](#컨트롤-테이블-설명)

`주의` EEPROM Area에 존재하는 모든 Data는 Torque Enable(562)의 값이 ‘0’일 때만 변경할 수 있습니다.
{: .notice--warning}

**NOTE** : RH_P12_RN(A)는 RH_P12_RN의 개선된 firmware 입니다. 두 firmware의 Control table이 다르니, 사용 전에 Control table의 주소를 필히 확인해 주세요.

### <a name="model-number"></a>**[Model Number(0)](#model-number0)**
RH-P12-RN(A)의 모델 번호입니다.

|    모델명     |  Model Number  |
|:-------------:|:--------------:|
| RH_P12_RN(A)  | 35,074 (0x8902) |

### <a name="firmware-version"></a>**[Firmware Version(6)](#firmware-version6)**
RH-P12-RN(A)의 펌웨어 버전입니다.

### <a name="id"></a>**[ID(7)](#id7)**
{% include kr/dxl/pro-plus/control_table_7_id.md %}

### <a name="baud-rate"></a>**[Baud Rate(8)](#baud-rate8)**
{% include kr/dxl/pro-plus/control_table_8_baud_rate.md %}

### <a name="return-delay-time"></a>**[Return Delay Time(9)](#return-delay-time9)**
{% include kr/dxl/pro-plus/control_table_9_return_delay_time.md %}

### <a name="drive-mode"></a>**[Drive Mode(10)](#drive-mode10)**
{% include kr/dxl/pro-plus/control_table_10_drive_mode.md %}

### <a name="operating-mode"></a>**[Operating Mode(11)](#operating-mode11)**
장치의 제어 모드를 설정합니다. 각 제어 모드마다 특성이 다르기 때문에, 구현하려는 시스템에 적합한 제어 모드를 설정하시기 바랍니다.

| Value      | Operating Mode         | Description                                 |
|:-----------|:-----------------------|:--------------------------------------------|
| 0          | 전류제어 모드           | 속도와 위치는 제어하지 않고, 전류를 제어합니다. |
| 1 ~ 4      | Reserved               | -                                           |
| 5(Default) | 전류기반 위치제어 모드   | 위치와 전류를 제어합니다.                     |

### <a name="secondary-id"></a>**[Secondary ID(12)](#secondary-id12)**
{% include kr/dxl/pro-plus/control_table_12_secondary_id.md %}

### <a name="homing-offset"></a>**[Homing Offset(20)](#homing-offset20)**
{% include kr/dxl/pro-plus/control_table_20_homing_offset.md %}

### <a name="moving-threshold"></a>**[Moving Threshold(24)](#moving-threshold24)**
{% include kr/dxl/pro-plus/control_table_24_moving_threshold.md %}

### <a name="temperature-limit"></a>**[Temperature Limit(31)](#temperature-limit31)**
{% include kr/dxl/pro-plus/control_table_31_temperature_limit.md %}

### <a name="max-voltage-limit"></a><a name="min-voltage-limit"></a>**[Max/Min Voltage Limit(32, 34)](#maxmin-voltage-limit32-34)**
{% include kr/dxl/pro-plus/control_table_32_voltage_limit.md %}

### <a name="pwm-limit"></a>**[PWM Limit(36)](#pwm-limit36)**
{% include kr/dxl/pro-plus/control_table_36_pwm_limit.md %}

### <a name="current-limit"></a>**[Current Limit(38)](#current-limit38)**
목표 전류 값의 한계 값입니다. Goal Current(550)은 이 값보다 큰 값을 쓸 수 없습니다. 이 값보다 큰 값을 쓰려 하면, 값이 써지지 않고, Status packet의 error 에 Limit error bit가 set 됩니다.

| 단위   | 범위 |
| :---:  | :---: |
| 1 [mA] | 0 ~ 1,984|

### <a name="acceleration-limit"></a>**[Acceleration Limit(40)](#acceleration-limit40)**
프로파일 가속도 값의 한계 값입니다. Profile Acceleration(556)은 이 값보다 큰 값을 쓸 수 없습니다. 이 값보다 큰 값을 쓰려 하면, 값이 써지지 않고, Status packet의 error 에 Limit error bit가 set 됩니다.

| 단위         | 범위           |
| :---:        | :---:         |
| 1 [rev/min²] | 0 ~ 1,378,788 |

### <a name="velocity-limit"></a>**[Velocity Limit(44)](#velocity-limit44)**
목표 속도 값과 프로파일 속도 값의 한계 값입니다. Goal Velocity(552)와 Profile Velocity(560)는 이 값보다 큰 값을 쓸 수 없습니다. 이 값보다 큰 값을 쓰려 하면, 값이 써지지 않고, Status packet의 error 에 Limit error bit가 set 됩니다.

| 단위            | 범위     |
| :---:          | :---:     |
| 0.01 [rev/min] | 0 ~ 2,970 |

### <a name="max-position-limit"></a><a name="min-position-limit"></a>**[Max/Min Position Limit(48, 52)](#maxmin-position-limit48-52)**
전류 기반 위치 제어 모드에서 목표 위치의 제한 값으로써, 0 ~ 1,150 범위 내에서 목표 위치를 제한 합니다.  
따라서 위치 제어 모드에서 Goal position(564)은 이 값보다 클 수 없습니다. 이 값보다 큰 값을 쓰려 하면, 값이 써지지 않고, Status packet의 error 에 Limit error bit가 set 됩니다.

| 단위       | 값의 범위 |
| :---:     | :---:     |
| 1 [pulse] | 0 ~ 1,150 |

`주의` 동작 모드가 확장 위치 제어 모드일 때는 Position Limit이 적용되지 않습니다.
{: .notice}

### <a name="external-port-mode"></a><a name="external-port-data"></a>**[External Port Mode](#external-port-mode)**, **[External Port Data](#external-port-data)**
장치에는 다용도의 외부확장포트가 있습니다.

|항목   | 범위      |
| :---: | :---:    |
|전압   | 0 ~ 3.3 [V] |
|전류   | 0 ~ 5 [mA]  |

|External Port Mode| 명칭                     |설명|
| :---:            | :---:                    | :---: |
|0                 | Analogue Input           | External Port 신호를 12[bit] Digital로 변환|
|1                 | Digital Output Push-Pull | External Port를 0[V] 또는3.3[V]로 출력|
|2                 | Digital Input Pull-Up    | External Port 신호를 '0' 또는 '1'의 Digital 신호로 변경<br />External Port에 신호가 연결되어 있지 않을 경우 '1'|
|3(초기값)          | Digital Input Pull-Down  | External Port 신호를 '0' 또는 '1'의 Digital 신호로 변경<br />External Port에 신호가 연결되어 있지 않을 경우 '0'|

#### 외부 확장 포트의 위치 및 핀 기능
아래와 같이 나사를 제거하고 커버를 들어내면 외부 확장 포트가 드러납니다.

![](/assets/images/platform/rh_p12_rn/rh_p12_rn_external_port.png)

![](/assets/images/platform/rh_p12_rn/rh_p12_rn_external_port_pinout.png)

|핀 1|핀 2|핀 3|핀 4|핀 5|핀 6|
| :---: | :---: | :---: | :---: | :---: | :---: |
|GND|3.3V|PORT1|PORT2|PORT3|PORT4|

### <a name="shutdown"></a>**[Shutdown(63)](#shutdown63)**
{% include kr/dxl/pro-plus/control_table_63_shutdown.md %}

### <a name="indirect-address"></a><a name="indirect-data"></a>**[Indirect Address](#indirect-address)**, **[Indirect Data](#indirect-data)**
{% include kr/dxl/pro-plus/control_table_168_indirect.md %}

### <a name="torque-enable"></a>**[Torque Enable(512)](#torque-enable512)**
{% include kr/dxl/pro-plus/control_table_512_torque_enable.md %}

### <a name="led"></a>**[RGB LED(513)](#rgb-led513)**
{% include kr/dxl/pro-plus/control_table_513_led.md %}

### <a name="status-return-level"></a>**[Status Return Level(516)](#status-return-level516)**
{% include kr/dxl/pro-plus/control_table_516_status_return_level.md %}

### <a name="registered-instruction"></a>**[Registered Instruction(517)](#registered-instruction517)**
{% include kr/dxl/pro-plus/control_table_517_registered_instruction.md %}

### <a name="hardware-error-status"></a>**[Hardware Error Status(518)](#hardware-error-status518)**
{% include kr/dxl/pro-plus/control_table_518_hardware_error_status.md %}

### <a name="velocity-i-gain"></a><a name="velocity-p-gain"></a>**[Velocity PI Gain(524, 526), Feedforward 2nd Gains(536)](#velocity-pi-gain524-526, Feedforward 2nd Gains(536))**
{% include kr/dxl/pro-plus/control_table_524_velocity_gain.md %}

### <a name="position-d-gain"></a><a name="position-i-gain"></a><a name="position-p-gain"></a>**[Position PID Gain(528,530,532), Feedforward 1st Gains(538)](#position-pid-gain528-530-532, Feedforward 1st Gains(538))**
{% include kr/dxl/pro-plus/control_table_528_position_gain.md %}

### <a name="bus-watchdog"></a>**[Bus Watchdog(546)](#bus-watchdog546)**
{% include kr/dxl/pro-plus/control_table_546_bus_watchdog.md %}

### <a name="goal-pwm"></a>**[Goal PWM(548)](#goal-pwm548)**
{% include kr/dxl/pro-plus/control_table_548_goal_pwm.md %}

### <a name="goal-current"></a>**[Goal Current(550)](#goal-current550)**
{% include kr/dxl/pro-plus/control_table_550_goal_current.md %}

### <a name="goal-velocity"></a>**[Goal Velocity(552)](#goal-velocity552)**
{% include kr/dxl/pro-plus/control_table_552_goal_velocity.md %}

### <a name="profile-acceleration"></a>**[Profile Acceleration(556)](#profile-acceleration556)**
{% include kr/dxl/pro-plus/control_table_556_profile_acceleration.md %}

### <a name="profile-velocity"></a>**[Profile Velocity(560)](#profile-velocity560)**
{% include kr/dxl/pro-plus/control_table_560_profile_velocity.md %}

### <a name="goal-position"></a>**[Goal Position(564)](#goal-position564)**
이동시키고자 하는 곳의 위치 값입니다.  
값의 범위는 Min Position Limit(40) ~ Max Position Limit(36) 이며, 초기값은 0 ~ 1,150 (0x47E) 입니다.

|모델명|Goal Position = 0|Goal Position = 740|
| :-------: | :--------: | :--------: |
|RH-P12-RN|![](/assets/images/platform/rh_p12_rn/rh_p12_rn_position_open.png)|![](/assets/images/platform/rh_p12_rn/rh_p12_rn_position_close.png)|

### <a name="realtime-tick"></a>**[Realtime Tick(568)](#realtime-tick568)**
{% include kr/dxl/pro-plus/control_table_568_realtime_tick.md %}

### <a name="moving"></a>**[Moving(570)](#moving570)**
{% include kr/dxl/pro-plus/control_table_570_moving.md %}

### <a name="moving-status"></a>**[Moving Status(571)](#moving-status571)**
{% include kr/dxl/pro-plus/control_table_571_moving_status.md %}

### <a name="present-pwm"></a>**[Present PWM(572)](#present-pwm572)**
{% include kr/dxl/pro-plus/control_table_572_present_pwm.md %}

### <a name="present-current"></a>**[Present Current(574)](#present-current574)**
{% include kr/dxl/pro-plus/control_table_574_present_current.md %}

### <a name="present-velocity"></a>**[Present Velocity(576)](#present-velocity576)**
{% include kr/dxl/pro-plus/control_table_576_present_velocity.md %}

### <a name="present-position"></a>**[Present Position(580)](#present-position580)**
장치의 현재 위치 값입니다.

|Model|Goal Position = 0|Goal Position = 740|
| :-------: | :--------: | :--------: |
|RH-P12-RN|![](/assets/images/platform/rh_p12_rn/rh_p12_rn_position_open.png)|![](/assets/images/platform/rh_p12_rn/rh_p12_rn_position_close.png)|

### <a name="velocity-trajectory"></a>**[Velocity Trajectory(584)](#velocity-trajectory584)**
{% include kr/dxl/pro-plus/control_table_584_velocity_trajectory.md %}

### <a name="position-trajectory"></a>**[Position Trajectory(588)](#position-trajectory588)**
{% include kr/dxl/pro-plus/control_table_588_position_trajectory.md %}

### <a name="present-input-voltage"></a>**[Present Input Voltage(592)](#present-input-voltage592)**
{% include kr/dxl/pro-plus/control_table_592_present_input_voltage.md %}

### <a name="present-temperature"></a>**[Present Temperature(594)](#present-temperature594)**
{% include kr/dxl/pro-plus/control_table_594_present_temperature.md %}

# [조립 예시](#조립-예시)

## [옵션프레임 조립](#옵션프레임-조립)

![](/assets/images/platform/rh_p12_rn/rh-p12-rn_assembly.png)


# [참고자료](#참고자료)

## [커넥터 정보](#커넥터-정보)

|항목|RS-485|외부포트|
|:---:|:---:|:---:|
|핀 번호|`1` GND<br>`2` VDD<br>`3` DATA+<br>`4` DATA-|`1` GND<br>`2` VDD<br>`3` PORT 1<br>`4` PORT 2<br>`5` PORT 3<br>`6` PORT 4|
|다이어그램|![](/assets/images/dxl/jst_b4beha_diagram.png)|![](/assets/images/dxl/molex_5304706_diagram.png)|
|하우징|[JST EHR-04]|![](/assets/images/dxl/molex_510210600.png)<br />[MOLEX 51021-0600]|
|PCB 헤더|![](/assets/images/dxl/jst_b4beha.png)<br />[JST B4B-EH-A]|![](/assets/images/dxl/molex_530470610.png)<br />[MOLEX 53047-0610]|
|Crimp 터미널|[JST SHE-001T-P0.6]|[MOLEX 50079-8100]|
|Wire Gauge|21 AWG|21 AWG|

[JST EHR-04]: http://www.jst-mfg.com/product/pdf/eng/eEH.pdf
[JST B4B-EH-A]: http://www.jst-mfg.com/product/pdf/eng/eEH.pdf
[JST SHE-001T-P0.6]: http://www.jst-mfg.com/product/pdf/eng/eEH.pdf
[MOLEX 51021-0600]: http://www.molex.com/molex/products/datasheet.jsp?part=active/0510210600_CRIMP_HOUSINGS.xml
[MOLEX 53047-0610]: http://www.molex.com/molex/products/datasheet.jsp?part=active/0530470610_PCB_HEADERS.xml
[MOLEX 50079-8100]: http://www.molex.com/molex/products/datasheet.jsp?part=active/0500798100_CRIMP_TERMINALS.xml

## [도면](#도면)
`Download` [RH-P12-RN(PDF).zip](http://www.robotis.com/service/download.php?no=740)  
`Download` [RH-P12-RN(STP).zip](http://www.robotis.com/service/download.php?no=741)


[PDF]: http://support.robotis.com/en/baggage_files/dynamixel/rh-p12-rn.pdf
[Torque Enable(562)]: #torque-enable562
