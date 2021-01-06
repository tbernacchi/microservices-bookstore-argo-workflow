FROM python:3.7-slim

RUN mkdir -p /app/
WORKDIR /app/
#COPY . /app/src/frontend

ADD ./frontend /app/

RUN pip3 freeze > /app/src/frontend/requirements.txt

RUN pip3 install -r /app/src/frontend/requirements.txt && chmod a+rwx /app/src/frontend/frontend.py

EXPOSE 8000

CMD [ "python", "/app/src/frontend/frontend.py" ] 
