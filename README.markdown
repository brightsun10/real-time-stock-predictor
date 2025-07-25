# Real time Stock Prediction Engine

A real-time stock prediction system built with Python, Apache Kafka, Apache Spark, and machine learning using the Random Forest algorithm. This application uses historic data generated by geometric brownian motion to train a predictive model, and streams predictions via Kafka.

## Overview

- **Data Source**: Generated by Geometric Brownian Motion.
- **Model**: Random Forest Regressor for predicting next-day closing prices.
- **Pipeline**: Kafka for message queuing, Spark for streaming, and Python for data processing.
- **Deployment**: Dockerized with Compose for easy setup.

## Prerequisites

- **Python 3.8+**
- **Docker** and **Docker Compose**
- **Internet Connection** 

## Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/yourusername/stock-prediction-engine.git
   cd stock-prediction-engine
   ```
   
2. **Set Up Docker**:
   - Ensure Docker and Docker Compose are installed.
   - Verify with:
    
   ```bash
   docker --version
   docker-compose --version
   ```

3. **Run deploy.bat**:

   Just run deploy.bat in command prompt

   ```
   /scripts/deploy.bat
   ```

## Usage

### 1. Train the Model
Run the training script with real historic data:
```bash
python train_model.py
```
- This generates and saves a `stock_model.pkl` file in the `models` directory.
- Data is fetched for AAPL, MSFT, and GOOGL from January 1, 2020, to July 1, 2025.

### 2. Deploy with Docker
Start the entire stack:
```bash
docker-compose up -d --build
```
- This launches Kafka, Zookeeper, and the application container.

### 3. Monitor Logs
Check the application logs:
```bash
docker logs app -f
```
- Look for transaction sends and predictions.

### 4. Consume Predictions
Run the consumer in a separate terminal (outside Docker for testing):
```bash
python consumer.py
```
- This prints predictions from the `stock-predictions` topic.

### 5. Stop the Application
Gracefully stop the containers:
```bash
docker-compose stop
```
Or remove and recreate:
```bash
docker-compose down
```

## File Structure

- `app.py`: Main application with Spark streaming and prediction logic.
- `producer.py`: Sends real-time stock data to Kafka.
- `consumer.py`: Consumes and logs predictions.
- `train_model.py`: Trains the Random Forest model with historic data.
- `config/config.yaml`: Configuration file for Kafka and Spark.
- `docker-compose.yml`: Docker Compose configuration.
- `models/`: Directory for the trained model (`stock_model.pkl`).
- `checkpoint/`: Spark checkpoint location.

## Features

- **Real-Time Prediction**: Fetches 1-minute interval data and predicts next closing prices.
- **Historic Training**: Uses data from 2020 to 2025 for robust model training.
- **Scalable**: Leverages Kafka and Spark for distributed processing.
- **Modular**: Separate scripts for training, producing, and consuming.

## Contributing

1. Fork the repository.
2. Create a feature branch (`git checkout -b feature-name`).
3. Commit changes (`git commit -m "Add feature"`).
4. Push to the branch (`git push origin feature-name`).
5. Open a Pull Request.

## License

MIT License - See `LICENSE` file for details.

## Contact

For issues or questions, open an issue on GitHub or contact nithinpsea10@gmail.com.

## Version

- **Last Updated**: July 22, 2025, 07:46 PM IST
- **Version**: 1.0.0
