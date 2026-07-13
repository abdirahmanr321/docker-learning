FROM python:3.8-slim AS build

WORKDIR /app

RUN apt-get update && apt-get install -y \
    gcc \
    python3-dev \
    libmariadb-dev \
    pkg-config

COPY . .
RUN pip install flask mysqlclient

FROM python:3.8-slim

WORKDIR /app

RUN apt-get update && apt-get install -y \
    libmariadb3 \
    pkg-config

COPY --from=build /usr/local /usr/local
COPY --from=build /app /app

EXPOSE 5003

CMD ["python", "app.py"]