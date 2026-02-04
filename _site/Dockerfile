# Build stage
FROM ruby:3.2-alpine AS builder

RUN apk add --no-cache build-base

WORKDIR /site

COPY Gemfile ./
RUN bundle install

COPY . .
RUN bundle exec jekyll build

# Production stage
FROM nginx:alpine

COPY --from=builder /site/_site /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
