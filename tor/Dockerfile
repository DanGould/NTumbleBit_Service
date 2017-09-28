FROM debian:jessie
LABEL maintainer="dan@dannygould.com"

# Install tor
RUN echo "deb http://deb.torproject.org/torproject.org jessie main" >> /etc/apt/sources.list
RUN echo "deb-src http://deb.torproject.org/torproject.org jessie main" >> /etc/apt/sources.list
RUN gpg --keyserver keys.gnupg.net --recv A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89
RUN gpg --export A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89 | apt-key add -
RUN apt-get update
RUN apt-get install -y tor deb.torproject.org-keyring

# Run as non-root user. Consider adding usergroup for mounted vol
RUN useradd -r -u 1001 tor
RUN mkdir /home/tor
RUN chown 1001 /home/tor
USER tor

# Copy runtime config
COPY torrc /etc/tor/torrc

CMD ["tor"]

