# SQL injection

Never pass non sanitized strings to DB. This isSql Injectable:

```python
# WARNING THIS IS VULNERABLE TO SQL INJECTION
#  if request.GET['id] == "2; DROP TABLE users"
statement ="select * form users where id = %s" % request.GET['id']
results = database.execute(statement)
```

Using an ORM like **SQLAlchemy** presents an abstraction layer where no non sanitized string is passed to the DB.  This is nos SQL injectable

```python
Session.execute(model.users.__table__.select().where(model.users.name == request.GET['name']))
```
