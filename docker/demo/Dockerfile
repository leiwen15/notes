FROM python:3.7
LABEL version="3.2"
LABEL desc="test engine3.2"

WORKDIR /
ENV VIRTUAL_ENV=/venv
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

ADD . /app
# COPY ./mald-python/rebuildPython3.sh .

RUN python3 -m venv $VIRTUAL_ENV \
    && pip install -U pip setuptools -i https://mirrors.aliyun.com/pypi/simple/ \
    && pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/ \
    && pip config set global.extra-index-url http://161.189.130.167:8080/simple/ \
    && pip config set install.trusted-host 161.189.130.167 
# && scl enable devtoolset-8 bash \
# && ./rebuildPython3.sh

ENTRYPOINT ["python3", "/app/test.py"]