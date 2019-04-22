FROM python:3.6-stretch

ENV LANGUAGE en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV LC_CTYPE en_US.UTF-8
ENV LC_MESSAGES en_US.UTF-8

RUN set -ex \
    && apt-get update -yqq \
    && apt-get upgrade -yqq \
    && apt-get install -yqq --no-install-recommends \
        $buildDeps \
        python3-pip \
        python3-requests \
        apt-utils \
        curl \
        rsync \
        netcat \
        locales \
        default-libmysqlclient-dev \
        chromium \
        pigz \
        wget \
        unzip \
        man-db \
        default-jre \
        xvfb \
        xauth \
        firefox-esr \
    && sed -i 's/^# en_US.UTF-8 UTF-8$/en_US.UTF-8 UTF-8/g' /etc/locale.gen \
    && locale-gen \
    && update-locale LANG=en_US.UTF-8 LC_ALL=en_US.UTF-8 \
    && pip install --upgrade pip \
    && pip install pystrich \
    && pip install pyvirtualdisplay \
    && pip install selenium \
    && pip install pystrich \
    && pip install pyyaml \
    && pip install matplotlib \
    && wget https://github.com/mozilla/geckodriver/releases/download/v0.23.0/geckodriver-v0.23.0-linux64.tar.gz && tar -x geckodriver -zf geckodriver-v0.23.0-linux64.tar.gz -O > /usr/bin/geckodriver && chmod +x /usr/bin/geckodriver \
    && apt-get purge --auto-remove -yqq $buildDeps \
    && apt-get autoremove -yqq --purge \
    && apt-get clean \
    && rm -rf \
        /var/lib/apt/lists/* \
        /tmp/* \
        /var/tmp/* \
        /usr/share/man \
        /usr/share/doc \
        /usr/share/doc-base

COPY selenium_test_script.py /selenium_test_script.py

CMD ["python","./selenium_test_script.py"]
