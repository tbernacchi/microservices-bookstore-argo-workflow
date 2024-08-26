FROM python:3.7-slim

RUN mkdir -p /app/
WORKDIR /app/

ADD ./src/frontend/ /app/

RUN pip3 freeze > /app/requirements.txt

RUN pip3 install -r /app/requirements.txt && chmod a+rwx /app/frontend.py

EXPOSE 8000

CMD [ "python", "/app/src/frontend/frontend.py" ] 
