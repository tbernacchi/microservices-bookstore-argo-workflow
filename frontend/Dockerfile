FROM python:3.7-slim

RUN mkdir -p /app 
WORKDIR /app/
COPY . /app/

RUN pip freeze > requirements.txt

RUN pip3 install -r /app/src/frontend/requirements.txt && chmod a+rwx /app/src/frontend/frontend.py

EXPOSE 8000

CMD [ "python", "/app/src/frontend/frontend.py" ] 
