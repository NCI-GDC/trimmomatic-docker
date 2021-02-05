FROM quay.io/ncigdc/bio-u20:latest
MAINTAINER Charles Czysz <czysz@uchicago.edu>

ARG VERSION=0.38

RUN apt-get update \
	&& apt-get install -y \
	  wget \
	  openjdk-8-jre-headless \
	  unzip \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*

RUN cd /opt \
    && wget http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/Trimmomatic-${VERSION}.zip \
    && unzip Trimmomatic-${VERSION}.zip \
    && ln -s /opt/Trimmomatic-${VERSION}/trimmomatic-${VERSION}.jar /bin/trimmomatic.jar \
    && rm Trimmomatic-${VERSION}.zip

ENTRYPOINT ["java"]

CMD ["-Xmx4G", "-jar", "/bin/trimmomatic.jar"]

