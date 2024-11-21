# Cloud Predictive Maintenance System

A cloud-based predictive maintenance system utilizing IoT and AWS services to monitor temperature and humidity levels, provide real-time visualization, and send user alerts when thresholds are exceeded.

---

## Features

1. **IoT Integration**:  
   - Uses **ESP32** with a **DHT11** sensor to measure temperature and humidity.
   - Data is sent to **AWS IoT Core** for further processing.

2. **Cloud Data Pipeline**:  
   - Data is forwarded from **AWS IoT Core** to **AWS Timestream** for storage and querying.
   - Real-time visualization is powered by **AWS Managed Grafana**.

3. **Alerts and Notifications**:  
   - If temperature exceeds a predefined threshold, **AWS SNS** sends alerts to subscribed users.
   - Configured with **IAM** roles for secure access.

4. **Scalability and Real-Time Insights**:  
   - Scalable architecture with real-time data streaming and visualization.

---

## Technology Stack

### Hardware
- **ESP32**: Microcontroller for sensor data acquisition and Wi-Fi connectivity.
- **DHT11 Sensor**: Measures temperature and humidity.

### Software & Cloud
1. **AWS IoT Core**: Ingests IoT data securely.
2. **AWS Timestream**: Stores time-series data for querying and analysis.
3. **AWS SNS**: Sends notifications based on defined thresholds.
4. **AWS Managed Grafana**: Visualizes data on customizable dashboards.
5. **IAM (Identity and Access Management)**: Configures secure access for services and users.

### Programming Languages
- **C++**: ESP32 programming.
- **Python**: AWS Lambda (optional, if custom processing is added).

---

## How It Works

1. **Data Acquisition**:  
   - The ESP32 reads temperature and humidity data using the DHT11 sensor.
   - Data is transmitted to **AWS IoT Core** via MQTT.

2. **Data Processing & Storage**:  
   - IoT Core forwards the data to **AWS Timestream**, where it is stored as time-series data.

3. **Alerts**:  
   - A monitoring rule checks if the temperature exceeds the threshold.
   - If triggered, **AWS SNS** sends alerts (via email or SMS) to notify users.

4. **Data Visualization**:  
   - Data from Timestream is visualized on a real-time dashboard in **AWS Managed Grafana**.

---

## Installation and Setup

### ESP32 and Sensor Configuration

1. **Connect the DHT11 Sensor to ESP32**:
   - Connect VCC to 3.3V pin.
   - Connect GND to GND pin.
   - Connect DATA to GPIO pin (e.g., GPIO4).

2. **Flash the ESP32**:
   - Install the necessary libraries in the Arduino IDE:
     - `DHT` library for sensor reading.
     - `PubSubClient` library for MQTT communication.
   - Upload the provided code to the ESP32.

---

### AWS Setup

#### 1. **AWS IoT Core**:
   - Create an IoT Thing and attach certificates.
   - Set up an IoT Core rule to forward data to **AWS Timestream**.

#### 2. **AWS Timestream**:
   - Create a Timestream database and table for storing time-series data.
   - Set up retention policies.

#### 3. **AWS SNS**:
   - Create an SNS topic.
   - Subscribe users (email or SMS) to the topic.
   - Configure IoT Core rules to trigger SNS alerts when thresholds are breached.

#### 4. **AWS Managed Grafana**:
   - Integrate Timestream as a data source.
   - Create a dashboard to visualize temperature and humidity in real time.

#### 5. **IAM**:
   - Set up IAM roles and policies to securely connect AWS services:
     - IoT Core → Timestream
     - Timestream → Grafana
     - IoT Core → SNS

---

## File Structure

```plaintext
cloud-predictive-maintenance/
├── esp32-code/             # ESP32 code for DHT11 and MQTT
├── aws-setup/              # AWS IoT Core, Timestream, SNS configuration scripts
├── grafana-dashboard/      # Grafana JSON configuration for dashboards
└── README.md               # Documentation
```

## Usage

1. Flash the ESP32 with the provided code:
   - Connect the DHT11 sensor to the ESP32.
   - Install necessary libraries (`DHT`, `PubSubClient`) in the Arduino IDE.
   - Upload the code to the ESP32 via USB.

2. Configure AWS Services:
   - Ensure **AWS IoT Core** is receiving data from ESP32.
   - Verify **AWS Timestream** is storing time-series data.
   - Check the **AWS SNS** topic subscription to receive alerts.
   - Open the **AWS Managed Grafana** dashboard to view real-time data.

3. Monitor and Respond:
   - Track temperature and humidity on the Grafana dashboard.
   - React to **AWS SNS** notifications when thresholds are exceeded.

---

## Future Enhancements

1. Add support for additional sensors:
   - Include vibration or gas sensors for extended monitoring capabilities.
   
2. Implement predictive analytics:
   - Use **AWS SageMaker** or other ML services to predict failures or anomalies.

3. Develop a mobile app:
   - Integrate real-time dashboards and alert notifications for users on-the-go.
