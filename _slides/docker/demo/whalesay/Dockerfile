FROM docker/whalesay

RUN apt-get -y update && apt-get install -y fortunes

CMD /usr/games/fortune -oa | cowsay
