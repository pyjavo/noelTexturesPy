FROM python:3.8-slim-bullseye as builder

RUN adduser --quiet --disabled-password noel

RUN apt-get update && apt-get install -y --no-install-recommends \
	build-essential libssl-dev \
	git bash nano wget curl htop \
	&& rm -rf /var/lib/apt/lists/* /tmp/* ~/.cache

COPY requirements.txt /tmp/requirements.txt

RUN python -m pip install -r /tmp/requirements.txt

# production image
FROM python:3.8-slim-bullseye as app
ENV TZ=America/Montreal
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
COPY --from=builder /usr/local /usr/local