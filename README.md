# ETLWeather: Weather Data ETL Pipeline with Apache Airflow

This project provides an ETL pipeline using [Apache Airflow](https://airflow.apache.org/) to extract, transform, and load weather data from the Open-Meteo API into a PostgreSQL database. The project is containerized using Docker and managed with the Astronomer CLI.



## Main Features

- **ETL DAG**: [`dags/etlweather.py`](dags/etlweather.py)  
  - Extracts current weather for London from Open-Meteo API.
  - Transforms the data to select relevant fields.
  - Loads the data into a `weather_data` table in PostgreSQL.
- **Dockerized**: Uses a custom Airflow image ([Dockerfile](Dockerfile)) and local Postgres ([docker-compose.yml](docker-compose.yml)).
- **Testing**: Example tests in [`tests/dags/test_dag_example.py`](tests/dags/test_dag_example.py).

## Getting Started

### Prerequisites

- [Docker](https://www.docker.com/)
- [Astronomer CLI](https://docs.astronomer.io/astro/cli/install-cli)

### Setup

1. **Clone the repository**
    ```sh
    git clone <your-repo-url>
    cd ETLWeather
    ```

2. **Start services**
    ```sh
    astro dev start
    ```

    This will:
    - Build the Airflow image.
    - Start Airflow and Postgres containers.
    - Open Airflow UI at [http://localhost:8080](http://localhost:8080).

3. **Access Postgres**
    - Host: `localhost`
    - Port: `5432`
    - User: [postgres](http://_vscodecontentref_/6)
    - Password: [postgres](http://_vscodecontentref_/7)
    - Database: [postgres](http://_vscodecontentref_/8)

4. **Configure Airflow Connections**
    - Add an HTTP connection named `open_meteo_api` with:
      - Host: `https://api.open-meteo.com`
    - Ensure the default Postgres connection (`postgres_default`) is set to your local Postgres.

### Running the ETL DAG

- In the Airflow UI, enable the `weather_etl_pipeline` DAG.
- The DAG will run daily, fetching and storing weather data.

## Customization

- Change the latitude/longitude in [etlweather.py](http://_vscodecontentref_/9) to fetch weather for a different location.
- Add more transformations or destinations as needed.

## Testing

Run tests using:

```sh
astro dev pytest
