# ruby 2.1.1, nginx, passenger
FROM zigomir/passenger-ruby211

# Set correct environment variables.
ENV HOME /root

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Run Passenger and Nginx
RUN rm -f /etc/service/nginx/down

# nginx conf
ADD nginx/default.conf /etc/nginx/sites-enabled/default

# install gems and cache them
WORKDIR /tmp
ADD Gemfile /tmp/Gemfile
ADD Gemfile.lock /tmp/Gemfile.lock
RUN bundle install --without development test

# All the stuff that wee need for app to run
ADD /path/to/your/ruby/app /home/app/webapp

# Remove git files
RUN rm -rf /home/app/webapp/.git

# This needs to be called last If we want it to run
# Use baseimage-docker's init process.
CMD ["/sbin/my_init"]