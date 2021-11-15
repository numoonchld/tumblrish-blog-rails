## Usage

- in terminal do `docker-compose up`

- create DB
  `docker-compose run web rake db:create`

## Notes

- in rails, convention is preferred over configuration

  - model name is singular
  - controler is plural

- in controller, the names of the functions must match the route name

  - use `rails routes` to get all enabled route names

- to run migrations, use: `rails db:migrate`
- `db/schema.rb` has the current snapshot of the model's table

  - i.e. the columns and the types for each column

- this `schema.rb` definition is the authoritative source for your database schema
  - if you need to create the application database on another
    system, you should be using `db:schema:load`,
  - not running all the migrations from scratch
    - this is a flawed and unsustainable approach
    - the more migrations you'll amass, the slower it'll run and the greater likelihood for issues

### Posts

#### Posts - Controller

- `rails generate controller posts`

#### Posts - Model

- `rails generate model post title:string body:text`

## Initial Setup

- Generate ruby app within `web` docker container
  `docker-compose run --no-deps web rails new . --force --database=postgresql`

- Then, build the app after rails genrates new app
  `docker-compose build`

- Then configure DB in `config/database.yml` by linking host to `db`, and setting username and password

```
default: &default
adapter: postgresql
encoding: unicode
host: db
username: postgres
password: password
pool: 5
```

- Then run the entire docker composite
  `docker-compose up`

- Then create DB
  `docker-compose run web rake db:create`

## Reference

- https://docs.docker.com/samples/rails/
