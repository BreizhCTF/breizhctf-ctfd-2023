FROM node AS theme-builder

COPY . /build
WORKDIR /build/CTFd/themes/breizhctf

RUN yarn && yarn build && bash -O extglob -c 'rm -rf -v !("assets"|"static"|"templates")'
RUN rm -rf .git

FROM python:3.9-slim-buster
WORKDIR /opt/CTFd

FROM python:3.9-slim-buster as build

WORKDIR /opt/CTFd

# hadolint ignore=DL3008
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        build-essential \
        libffi-dev \
        libssl-dev \
        git \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && python -m venv /opt/venv

ENV PATH="/opt/venv/bin:$PATH"

COPY . /opt/CTFd

RUN pip install --no-cache-dir -r requirements.txt \
    && for d in CTFd/plugins/*; do \
        if [ -f "$d/requirements.txt" ]; then \
            pip install --no-cache-dir -r "$d/requirements.txt";\
        fi; \
    done;


FROM python:3.9-slim-buster as release
WORKDIR /opt/CTFd

# hadolint ignore=DL3008
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        libffi6 \
        libssl1.1 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

COPY --chown=1001:1001 . /opt/CTFd

RUN useradd \
    --no-log-init \
    --shell /bin/bash \
    -u 1001 \
    ctfd \
    && mkdir -p /var/log/CTFd /var/uploads \
    && chown -R 1001:1001 /var/log/CTFd /var/uploads \
    && chmod +x /opt/CTFd/docker-entrypoint.sh

COPY --from=build /opt/venv /opt/venv
# COPY --from=theme-builder /build /opt/CTFd
ENV PATH="/opt/venv/bin:$PATH"

USER 1001
EXPOSE 8000
ENTRYPOINT ["/opt/CTFd/docker-entrypoint.sh"]
