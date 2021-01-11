FROM nvidia/cuda:11.1-devel

ENV TZ=Europe/Berlin
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

WORKDIR /eth/

RUN apt-get update \
    && apt-get install -y wget

RUN wget https://github.com/trexminer/T-Rex/releases/download/0.19.5/t-rex-0.19.5-linux-cuda11.1.tar.gz

RUN tar xfvz t-rex-0.19.5-linux-cuda11.1.tar.gz

RUN chmod +x ./t-rex
ENTRYPOINT ["./t-rex"]