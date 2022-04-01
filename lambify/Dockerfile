FROM public.ecr.aws/sam/build-ruby2.7 AS build

## Node for JavaScript.
# RUN curl -sL https://rpm.nodesource.com/setup_14.x | bash - && \
#     yum install -y nodejs && \
#     curl --silent --location https://dl.yarnpkg.com/rpm/yarn.repo | tee /etc/yum.repos.d/yarn.repo && \
#     rpm --import https://dl.yarnpkg.com/rpm/pubkey.gpg && \
#     yum install -y yarn

COPY . .
RUN CI='true' bin/_build

FROM public.ecr.aws/lambda/ruby:2.7
ARG RAILS_ENV
ENV RAILS_ENV=$RAILS_ENV

COPY --from=build /var/task .

CMD ["app.handler"]
