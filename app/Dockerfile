FROM ruby:2.3.1
RUN apt-get update && \
    apt-get install -y net-tools

#Install gems
ENV APP_HOME /opt/sinatra
RUN mkdir $APP_HOME
WORKDIR $APP_HOME
COPY Gemfile $APP_HOME/
RUN bundle install

#Upload Source Code
COPY hello-world.rb $APP_HOME/

#Setting the Redis Host
ENV REDIS_HOST=redis

#Running the APP
EXPOSE 4567
CMD ["ruby", "hello-world.rb"]
