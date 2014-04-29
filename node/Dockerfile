FROM phusion/passenger-nodejs:0.9.9

# Set correct environment variables.
ENV HOME /root

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Run Passenger and Nginx
RUN rm -f /etc/service/nginx/down

# nginx conf
ADD nginx.conf /etc/nginx/sites-enabled/default

# install node modules and cache it
ADD package.json /tmp/package.json
RUN cd /tmp && npm install --production
RUN mkdir -p /home/app/node_app && cp -a /tmp/node_modules /home/app/node_app

# All the stuff that wee need for app to run
ADD /path/to/node_app /home/app/node_app

# This needs to be called last If we want it to run
# Use baseimage-docker's init process.
CMD ["/sbin/my_init"]