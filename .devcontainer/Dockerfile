FROM ruby:3.2-alpine

RUN apk add --no-cache build-base git

WORKDIR /workspace

COPY Gemfile ./
RUN bundle install

EXPOSE 4000 35729
