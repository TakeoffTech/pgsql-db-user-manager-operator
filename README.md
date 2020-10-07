# PostgreSQL database user manager operator for kubernetes

## Features
* Create a user with read-only access to a single database

## Installation
Unknown at this time

## CRs

### ReadOnlyDBUser
```yaml
apiVersion: pgsql.takeoff.io/v1alpha1
kind: ReadOnlyDBUser
metadata:
  name: testdbrouser # name of dbuser to create
spec:
  db_name: testdb # name of database to give select, use (readonly) access to
  password: changeme1234 # password for user
  pghost: cloudsql-postgres # host to connect to
  pguser: postgres # admin user to connect and create user as
  pgpass: donotuseme1234 # password for admin user
```

This creates a user called `testdbrouser` with a password of `changeme1234` and is given read-only access to `testdb`.
It performs the same operations as these SQL statements:
1. \connect postgres
2. CREATE USER testdbrouser WITH PASSWORD 'changeme1234'
3. \connect testdb 
4. GRANT USAGE ON SCHEMA public TO testdbrouser
5. GRANT SELECT ON ALL TABLES IN SCHEMA public TO testdbrouser
6. ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT ON TABLES TO testdbrouser
>>>>>>> 3ef00b5... initial working MVP
