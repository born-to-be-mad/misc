# Equivalent notation

```yaml
list_by_dash:
  - foo
  - bar
list_by_square_bracets: [ foo, bar ]
map_by_indentation:
  foo: bar
  bar: baz
map_by_curly_braces: { foo: bar, bar: baz }
string_no_quotes: Monty Python
string_double_quotes: "Monty Python"
string_single_quotes: 'Monty Python'
bool_english: yes
bool_english_no: no
bool_python: True
bool_json: true
```

# Dangerous

```yaml
time: 4:30 #  4*60 + 30 = 270
number: 013 # octal => 11
```

# Long strings

```yaml
disclaimer: >
  Lorem ipsum dolor sit amet, consectetur adipiscing elit.
  In nec urna pellentesque, imperdiet urna vitae, hendrerit
  odio. Donec porta aliquet laoreet. Sed viverra tempus fringilla.
```

is equal to
JSON `{"disclaimer": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. In nec urna pellentesque, imperdiet urna vitae, hendrerit odio. Donec porta aliquet laoreet. Sed viverra tempus fringilla."}`

# Multiline strings

```yaml
mail_signature: |
  Martin Thoma
  Tel. +49 123 4567
```

is equal to JSON `{"mail_signature": "Martin Thoma\nTel. +49 123 4567"}`

# Placeholder

```yaml
email: &emailAddress "info@example.de"
id: *emailAddress
```

is equal to JSON `{"email": "info@example.de", "id": "info@example.de"}`

```yaml
foo: &default_settings
  db:
    host: localhost
    name: main_db
    port: 1337
  email:
    admin: admin@example.com
prod: *default_settings
dev: *default_settings
```

is equal to JSON `

```json
{
  "dev": {
    "db": {
      "host": "localhost",
      "name": "main_db",
      "port": 1337
    },
    "email": {
      "admin": "admin@example.com"
    }
  },
  "foo": {
    "db": {
      "host": "localhost",
      "name": "main_db",
      "port": 1337
    },
    "email": {
      "admin": "admin@example.com"
    }
  },
  "prod": {
    "db": {
      "host": "localhost",
      "name": "main_db",
      "port": 1337
    },
    "email": {
      "admin": "admin@example.com"
    }
  }
}
```

## Merge key(<<)

```yaml
foo: &default_settings
  db:
    host: localhost
    name: main_db
    port: 1337
  email:
    admin: admin@example.com
prod:
  <<: *default_settings
  app:
    port: 80
dev: *default_settings
```
