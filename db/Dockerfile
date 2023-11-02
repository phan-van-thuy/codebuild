FROM python:3.10-slim-buster

# Install Postgres and configure a username + password
USER root

ARG DB_USERNAME=$DB_USERNAME
ARG DB_PASSWORD=$DB_PASSWORD

RUN apt update -y && apt install postgresql postgresql-contrib -y

USER postgres
WORKDIR /db
COPY ./db .

RUN service postgresql start && \
psql -c "CREATE USER $DB_USERNAME PASSWORD '$DB_PASSWORD'" && \
psql < 1_create_tables.sql && \
psql < 2_seed_users.sql && \
psql < 3_seed_tokens.sql && \
psql -c "GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO $DB_USERNAME;" && \
psql -c "GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA public TO $DB_USERNAME"

CMD service postgresql start