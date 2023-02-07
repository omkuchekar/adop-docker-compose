FROM ruby:2.1.9-alpine@sha256:5424642552f987ccf7eda903d238abbc037bef15c287e253babe4763f129206c

MAINTAINER Nick Griffin <nicholas.griffin@accenture.com>

EXPOSE 4000

ENV JEKYLL_SOURCE="." JEKYLL_DEST="${JEKYLL_SOURCE}/_site"

# Install dependencies
RUN apk add --update build-base libxml2-dev libxslt-dev nodejs git && rm -rf /var/cache/apk/*

# Use libxml2, libxslt a packages from alpine for building nokogiri
# See: https://github.com/gliderlabs/docker-alpine/issues/53
RUN bundle config build.nokogiri --use-system-libraries

# This is where to mount into
RUN mkdir -p /site/
WORKDIR /site

CMD bundle install && bundle exec jekyll serve --baseurl '/adop-docker-compose' --host=0.0.0.0 --source "${JEKYLL_SOURCE}" --destination "${JEKYLL_DEST}" 2>&1
