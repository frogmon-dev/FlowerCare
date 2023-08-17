# Flower Care BLE-MQTT Bridge

이 프로젝트는 Flower Care 디바이스에서 BLE를 사용하여 센서 데이터를 수집하고 MQTT 서버에 전송하는 기능을 제공합니다.

## 주요 기능
1. Flower Care 디바이스로부터 센서 데이터(온도, 습도, 빛, 전도도) 수집.
2. 수집된 데이터를 MQTT 서버에 전송.
3. 주기적인 배터리 수준 체크.
4. 비상 상황에 디바이스를 수면 상태로 전환.

## 주요 구성요소
- **BLEClient**: Flower Care 디바이스와의 BLE 통신을 관리.
- **WiFiClient & PubSubClient**: MQTT 서버와의 통신을 관리.
- **Heltec OLED Display**: 상태 및 오류 메시지 출력.

## 코드 스니펫

```cpp
// Flower Care 서비스와 특성 UUID
static BLEUUID serviceUUID("..."); 
static BLEUUID uuid_version_battery("...");
// ... (다른 UUIDs)

// WiFi 및 MQTT 연결 설정
void connectWifi() {...}
void connectMqtt() {...}

// Flower Care 디바이스에서 데이터 읽기
bool readFloraDataCharacteristic(BLERemoteService* floraService, String baseTopic) {...}
bool readFloraBatteryCharacteristic(BLERemoteService* floraService, String baseTopic) {...}

// OLED 디스플레이 출력 함수
void dspPrintln(String str) {...}
```

## 시작하기
이 소스 코드를 사용하려면 `config.h`에 MQTT 및 WiFi 설정을 지정해야 합니다. 설정을 완료한 후, 메인 루프에서 디바이스는 주기적으로 깨어나 센서 데이터를 수집하고 MQTT로 전송한 다음 다시 수면 상태로 들어갑니다.
