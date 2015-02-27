FROM 	    ubuntu:trusty
MAINTAINER  Sergio Luceno <sluceno.a@gmail.com> 

# Install needed packages
RUN apt-get update
RUN apt-get install -y \
  wget \
  build-essential \
  libcurl4-openssl-dev \
  python-dev \
  python-setuptools \
  python-software-properties \
  software-properties-common \
  make \
  libyaml-dev \
  libgdbm-dev \
  libreadline-dev \
  libncurses5-dev \
  libffi-dev \
  libxml2-dev \
  libxslt1-dev \
  vim
  
# Install ruby-intall and chruby
RUN wget -O /tmp/ruby-install-0.4.3.tar.gz https://github.com/postmodern/ruby-install/archive/v0.4.3.tar.gz && \
  tar -xzvf /tmp/ruby-install-0.4.3.tar.gz -C /tmp && \
  cd /tmp/ruby-install-0.4.3/  && \
  sudo make install && \
  cd

RUN wget -O /tmp/chruby-0.3.8.tar.gz https://github.com/postmodern/chruby/archive/v0.3.8.tar.gz && \
  tar -xzvf /tmp/chruby-0.3.8.tar.gz -C /tmp && \
  cd /tmp/chruby-0.3.8/ && \
  sudo make install && \
  cd

# ADD nginx stable repository
RUN apt-add-repository ppa:nginx/stable

# Install git 
RUN apt-get install -y git-core 

# Install nginx
RUN apt-get install -y nginx

# Clean up APT and temporary files when done
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Insall Ruby 2.1.2
RUN ruby-install ruby 2.1.2
ENV PATH $PATH:/opt/rubies/ruby-2.1.2/bin

# Enable chruby

RUN echo "source /usr/local/share/chruby/chruby.sh" > /etc/profile.d/chruby.sh && \
  chmod +x /etc/profile.d/chruby.sh

# Install bundler
RUN gem install bundler

# Configure the container to start nginx process when running

RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf

# Define working directory.
WORKDIR /etc/nginx

# Define default command.
CMD ["nginx"]

EXPOSE 80
