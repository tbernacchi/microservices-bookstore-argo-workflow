# Copyright 2017 Istio Authors
#
#   Licensed under the Apache License, Version 2.0 (the "License");
#   you may not use this file except in compliance with the License.
#   You may obtain a copy of the License at
#
#       http://www.apache.org/licenses/LICENSE-2.0
#
#   Unless required by applicable law or agreed to in writing, software
#   distributed under the License is distributed on an "AS IS" BASIS,
#   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#   See the License for the specific language governing permissions and
#   limitations under the License.
FROM python:3.7.4-slim

RUN mkdir -p /opt/microservices/

ADD ./productpage /opt/microservices

RUN pip install --no-cache-dir -r /opt/microservices/requirements.txt

RUN pip install --no-cache-dir -r /opt/microservices/test-requirements.txt

ARG flood_factor
ENV FLOOD_FACTOR ${flood_factor:-0}

EXPOSE 9080

WORKDIR /opt/microservices
RUN python -m unittest discover /opt/microservices/tests/unit

USER 1

CMD ["python", "productpage.py", "9080"]
