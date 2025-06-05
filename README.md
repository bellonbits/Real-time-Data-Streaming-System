# Real-time Weather Data Streaming System

A distributed real-time data processing system that streams weather data using Apache Kafka, processes it with Apache Spark, and provides live analytics for multiple cities.

## Features

- **Real-time Data Streaming**: Continuous weather data ingestion using Apache Kafka
- **Distributed Processing**: Apache Spark for scalable stream processing
- **Live Analytics**: Real-time temperature monitoring and analysis
- **Multi-city Support**: Weather data processing for multiple locations including:
  - Nairobi, Kenya
  - Kampala, Uganda  
  - Dodoma, Tanzania
  - Addis Ababa, Ethiopia
  - Kigali, Rwanda
  - Juba, South Sudan
  - Bujumbura, Burundi
  - Mogadishu, Somalia

## Architecture

```
Weather API → Kafka Producer → Kafka Topics → Spark Streaming → Real-time Analytics
```

## Tech Stack

- **Apache Kafka**: Message streaming platform
- **Apache Spark**: Unified analytics engine for large-scale data processing
- **Apache ZooKeeper**: Centralized service for maintaining configuration information
- **Python**: Weather data producer and processing scripts

## Prerequisites

- Java 8 or higher
- Apache Kafka 2.8+
- Apache Spark 3.0+
- Apache ZooKeeper 3.6+
- Python 3.7+
- Weather API access (OpenWeatherMap or similar)

## Installation

### 1. Clone the Repository
```bash
git clone https://github.com/bellonbits/Real-time-Data-Streaming-System.git
cd Real-time-Data-Streaming-System
```

### 2. Install Dependencies
```bash
# Install Python dependencies
pip install -r requirements.txt

# Ensure Kafka, Spark, and ZooKeeper are installed and configured
```

### 3. Configuration
Create a `.env` file in the project root:
```env
WEATHER_API_KEY=your_weather_api_key
KAFKA_BOOTSTRAP_SERVERS=localhost:9092
SPARK_MASTER=local[*]
```

## Quick Start

### 1. Start ZooKeeper
```bash
zookeeper-server-start.sh config/zookeeper.properties
```

### 2. Start Kafka Server
```bash
kafka-server-start.sh config/server.properties
```

### 3. Create Kafka Topic
```bash
kafka-topics.sh --create --topic weather-data --bootstrap-server localhost:9092 --partitions 3 --replication-factor 1
```

### 4. Start Weather Data Producer
```bash
python weather_producer.py
```

### 5. Start Spark Streaming Application
```bash
spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.0.0 spark_streaming_app.py
```

## System Components

### Weather Producer (`weather_producer.py`)
- Fetches real-time weather data from weather APIs
- Publishes data to Kafka topics
- Supports multiple cities with configurable intervals
- Handles API rate limiting and error recovery

### Spark Streaming Application
- Consumes weather data from Kafka topics
- Performs real-time aggregations and analytics
- Calculates temperature trends and anomalies
- Outputs processed data for visualization

### Configuration Files
- `kafka/server.properties`: Kafka broker configuration
- `zookeeper/zoo.cfg`: ZooKeeper configuration
- `spark/spark-defaults.conf`: Spark application settings

## Monitoring and Analytics

The system provides real-time monitoring through:
- **Temperature Tracking**: Current temperature readings for all cities
- **Batch Processing**: Configurable batch intervals for stream processing
- **Data Persistence**: Weather data logging and archival
- **Performance Metrics**: Throughput and latency monitoring

## Configuration Options

### Kafka Configuration
```properties
# Server settings
num.network.threads=3
num.io.threads=8
socket.send.buffer.bytes=102400
socket.receive.buffer.bytes=102400
socket.request.max.bytes=104857600

# Log settings
log.retention.hours=168
log.segment.bytes=1073741824
log.retention.check.interval.ms=300000
```

### Spark Configuration
```properties
spark.sql.streaming.checkpointLocation=/tmp/checkpoint
spark.sql.streaming.forceDeleteTempCheckpointLocation=true
spark.serializer=org.apache.spark.serializer.KryoSerializer
```

## Troubleshooting

### Common Issues

1. **ZooKeeper Connection Issues**
   ```bash
   # Check ZooKeeper status
   echo stat | nc localhost 2181
   ```

2. **Kafka Broker Not Starting**
   ```bash
   # Verify Java installation
   java -version
   
   # Check port availability
   netstat -an | grep 9092
   ```

3. **Spark Streaming Failures**
   ```bash
   # Check Spark logs
   tail -f $SPARK_HOME/logs/spark-*.log
   ```

### Performance Tuning

- Adjust Kafka partition count based on throughput requirements
- Configure Spark executor memory and cores for optimal performance
- Set appropriate batch intervals for stream processing
- Monitor consumer lag and adjust parallelism

## API Documentation

### Weather Data Schema
```json
{
  "city": "string",
  "temperature": "float",
  "humidity": "integer",
  "pressure": "float",
  "timestamp": "datetime",
  "weather_condition": "string"
}
```

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Apache Software Foundation for Kafka, Spark, and ZooKeeper
- Weather data providers
- Open source community contributors

## Support

For support and questions:
- Create an issue on GitHub
- Contact: petergatitu61@gmail.com
- Documentation: [Wiki](https://github.com/bellonbits/Real-time-Data-Streaming-System/wiki)
