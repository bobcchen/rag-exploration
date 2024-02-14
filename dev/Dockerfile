FROM python:3.9-slim

RUN pip install jupyter
EXPOSE 8888

WORKDIR /app

COPY requirements.txt /app/requirements.txt
RUN pip install -r requirements.txt

WORKDIR /app/data

CMD jupyter notebook --port=8888 --ip=0.0.0.0 --allow-root --no-browser .
