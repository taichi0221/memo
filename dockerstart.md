docker rails
----------ターミナル-----------
mkdir dockertest2
cd dockertest2
touch docker-compose.yml
touch Gemfile
touch Gemfile.lock
touch entrypoint.sh
touch Dockerfile
touch .gitignore
touch .env
code .


------gitignore------------
.env


------entrypoint.sh-----------
#!/bin/bash
set -e

# Remove a potentially pre-existing server.pid for Rails.
rm -f /myapp/tmp/pids/server.pid

# Then exec the container's main process (what's set as CMD in the Dockerfile).
exec "$@"

--------docker-compose.yml-----------
version: '3.7'

services:
  db:
    image: mysql:8.0
    platform: linux/x86_64
    command: --default-authentication-plugin=mysql_native_password
    ports:
      - "3306:3306"
    volumes:
      - db:/var/lib/mysql
    environment:
      MYSQL_ALLOW_EMPTY_PASSWORD: 'yes'
    env_file:
      - .env
    security_opt:
      - seccomp:unconfined
  app:
    build:
      context: ./
      dockerfile: Dockerfile
    env_file:
      - .env
    stdin_open: true
    tty: true
    volumes:
      - ./app:/myapp
      - bundle:/usr/local/bundle
      - /myapp/app/node_modules
    command: bash -c "rm -rf tmp/pids/server.pid && bundle exec rails s -p 3000 -b '0.0.0.0'"
    depends_on:
      - db
    ports:
      - "3000:3000"
    environment:
      TZ: Asia/Tokyo
volumes:
  db:
    driver: local
  bundle:
    driver: local

----------Dockerfile------------
FROM ruby:2.6.5
ENV TZ Asia/Tokyo

RUN curl -fsSL https://deb.nodesource.com/setup_14.x | bash - \
    && apt-get update -qq \
    && apt-get install -y nodejs \
    && npm install -g yarn

WORKDIR /myapp
COPY Gemfile /myapp/Gemfile
COPY Gemfile.lock /myapp/Gemfile.lock
RUN bundle install

# COPY app/package.json app/yarn.lock /myapp/app/
# WORKDIR /myapp/app
# RUN yarn install
# WORKDIR /myapp

COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000

CMD ["rails", "server", "-b", "0.0.0.0"]


----------Gemfile------------
source 'https://rubygems.org'
gem 'rails', '6.0.0'


----------ターミナル------------
docker-compose run --no-deps app rails new . --force --database=mysql --skip-test --skip-spring --webpack


pwd
pwdの結果
whoami
whoamiの結果

sudo chown -R whoamiの結果:whoamiの結果 pwdの結果　権限取る

--------database.yml----------
default: &default
  adapter: mysql2
  encoding: utf8mb4
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: root
  password:
  host: db

コメントアウト外す

--------ターミナル------------
docker-compose run app rails db:create
docker-compose up
rm -rf app/.git
git init



docker react on rails
-- ターミナル
mkdir todoapp todoappはディレクトリ名
cd todoapp
mkdir backend
mkdir frontend
touch docker-compose.yml
touch backend/Gemfile
touch backend/Gemfile.lock
touch backend/entrypoint.sh
touch backend/Dockerfile
touch frontend/Dockerfile

--entrypoint.sh
#!/bin/bash
set -e

# Remove a potentially pre-existing server.pid for Rails.
rm -f /myapp/tmp/pids/server.pid

# Then exec the container's main process (what's set as CMD in the Dockerfile).
exec "$@"

--backend/dockerfile
FROM ruby:3.1.0
RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs

WORKDIR /myapp
COPY Gemfile /myapp/Gemfile
COPY Gemfile.lock /myapp/Gemfile.lock
RUN bundle install
COPY . /myapp

# Add a script to be executed every time the container starts.
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000

# Start the main process.
CMD ["rails", "server", "-b", "0.0.0.0"]

--gemfile
source 'https://rubygems.org'
gem 'rails', '6.1.5'

--docker-compose.yml
version: '3.7'

services:
  db:
    image: mysql:8.0
    platform: linux/x86_64
    command: --default-authentication-plugin=mysql_native_password
    ports:
      - "4306:3306"
    volumes:
      - db:/var/lib/mysql
    environment:
      MYSQL_ALLOW_EMPTY_PASSWORD: 'yes'
    security_opt:
      - seccomp:unconfined
  backend:
    build:
      context: ./backend/
      dockerfile: Dockerfile
    stdin_open: true
    tty: true
    volumes:
      - ./backend:/myapp
      - bundle:/usr/local/bundle
    command: bash -c "rm -rf tmp/pids/server.pid && bundle exec rails s -p 3000 -b '0.0.0.0'"
    depends_on:
      - db
    ports:
      - "3001:3000"
    environment:
      TZ: Asia/Tokyo
volumes:
  db:
    driver: local
  bundle:
    driver: local

--ターミナル
docker-compose run --no-deps backend rails new . --force -d mysql --api --skip-test

--database.yml
default: &default
  adapter: mysql2
  encoding: utf8mb4
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: root
  password:
  host: db #ここを追加

--frontend/dockerfile
FROM node:14.17.1-alpine
WORKDIR /usr/src/app

--docker-compose.yml
version: '3.7'

services:
  db:
    image: mysql:8.0
    platform: linux/x86_64
    command: --default-authentication-plugin=mysql_native_password
    ports:
      - "4306:3306"
    volumes:
      - db:/var/lib/mysql
    environment:
      MYSQL_ALLOW_EMPTY_PASSWORD: 'yes'
    security_opt:
      - seccomp:unconfined
  backend:
    build:
      context: ./backend/
      dockerfile: Dockerfile
    stdin_open: true
    tty: true
    volumes:
      - ./backend:/myapp
      - bundle:/usr/local/bundle
    command: bash -c "rm -rf tmp/pids/server.pid && bundle exec rails s -p 3000 -b '0.0.0.0'"
    depends_on:
      - db
    ports:
      - "3001:3000"
    environment:
      TZ: Asia/Tokyo
  frontend:
    build:
      context: ./frontend/
      dockerfile: Dockerfile
    volumes:
      - ./frontend:/usr/src/app
    command: sh -c "cd app && npm start"
    ports:
      - "3000:3000"
volumes:
  db:
    driver: local
  bundle:
    driver: local

--ターミナル
docker-compose run --rm frontend sh -c "npx create-react-app app"
docker-compose up
docker-compose exec backend rails db:create

--ターミナル
rm -rf backend/.git
rm -rf frontend/.git
git init