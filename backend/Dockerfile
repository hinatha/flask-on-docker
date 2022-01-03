FROM python:3.9-alpine

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
WORKDIR /src
COPY ./backend ./
RUN ls -la && sleep 10
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
