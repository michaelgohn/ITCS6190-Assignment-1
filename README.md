This project uses Docker to build a stack with two containers using PostgreSQL and Python.
The database service initializes a trips table with seeded data and the Python service connects to the database, computes basic statistics, and writes results to a JSON file.

There are two ways to run this project:

    If you have make installed, you can just run:
        make
    in the root folder and the Make file will build the app for you.

    If you do not have make installed or want to build the app manually, run:
        docker compose up --build

To stop the containers:
    docker compose down

Example Output:

```
{
  "total_trips": 6,
  "avg_fare_by_city": [
    {
      "city": "Charlotte",
      "avg_fare": 16.25
    },
    {
      "city": "New York",
      "avg_fare": 19.0
    },
    {
      "city": "San Francisco",
      "avg_fare": 20.25
    }
  ],
  "top_by_minutes": [
    {
      "city": "San Francisco",
      "minutes": 28,
      "avg_fare": 29.3
    },
    {
      "city": "New York",
      "minutes": 26,
      "avg_fare": 27.1
    },
    {
      "city": "Charlotte",
      "minutes": 21,
      "avg_fare": 20.0
    },
    {
      "city": "Charlotte",
      "minutes": 12,
      "avg_fare": 12.5
    },
    {
      "city": "San Francisco",
      "minutes": 11,
      "avg_fare": 11.2
    },
    {
      "city": "New York",
      "minutes": 9,
      "avg_fare": 10.9
    }
  ]
}
```

Outputs:
    Outputs are written to ./out/summary.json

Troubleshooting:
    If the terminal prints "Waiting for database..." and ends in a failure try restarting everything with:
        docker compose down -v
        docker compose up --build

    If an authentication failure occurs, ensure both services use the same docker credentials:
        POSTGRES_USER
        POSTGRES_PASSWORD
        POSTGRES_DB