# Addict

> Get a full Active Directory REST API in 30 seconds

---

Addict is a drop-in REST API microservice for Active Directory implementations. Just like that.


Gives you a web server with REST endpoints to add, remove, move, disable, enable, unlock or list Users, Groups and Organizational Units. It includes result caching by default and flexible filters for querying, sorting, pagination and column selection.

There's interactive API docs at `/api`:



These docs let you add arguments, try the requests and see the results.


## API

```js
# Users

GET /user
POST /user
GET /user/:user
PUT /user/:user
GET /user/:user/exists
GET /user/:user/member-of/:group
POST /user/:user/authenticate
PUT /user/:user/password
PUT /user/:user/password-never-expires
PUT /user/:user/password-expires
PUT /user/:user/enable
PUT /user/:user/disable
PUT /user/:user/move
PUT /user/:user/unlock
DELETE /user/:user

# Groups

GET /group
POST /group
GET /group/:group
GET /group/:group/exists
POST /group/:group/user/:user
DELETE /group/:group/user/:user
DELETE /group/:group

# Organizational Units

GET /ou
POST /ou
GET /ou/:ou
GET /ou/:ou/exists
DELETE /ou/:ou

# Other

GET /other
GET /all
GET /find/:filter
GET /status

# Monitoring

GET /status

```

Want more? [Just ask](https://github.com/dthree/addict/wiki/Roadmap).

### Filters

#### Fields

Choose which fields to include in the results:

`GET /user?_fields=description,cn`

#### Filter

Filter any field with `fieldName=value`.

`GET /group?cn=Guests`

We've got operators as well:

`GET /user?userAccountControl_gte=500`

##### Operators

 - `=`: Equals
 - `_ne=`: Not equals
 - `_lt=`: Less than
 - `_gt=`: Greater than
 - `_gte=`: Greater than or equal to
 - `_lte=`: Less than or equal to
 - `_like=`: Like (fuzzy search)

#### Sort

`GET /ou?_sort=whenCreated,dn&_order=desc,asc`

#### Paginate

`GET /user?_page=6&limit=10`

#### Slice

Add `_start` and `_end` or `_limit`:

`GET /user?_start=20&_limit=40`

#### Full Text Search

`GET /group?_q=addict`



## The Nitty Gritty

#### Passing Secrets

You can pass the AD details at runtime:

```bash
addict --url ldaps://[address] --user [user]@[domain] --pass [pass] --port [port]
```
`Port` is optional and defaults to `3000`.

As environmental variables:

```bash
export ADDICT_URL=ldaps://[address]
export ADDICT_USER=[user]@[domain]
export ADDICT_PASS=[pass]
export ADDICT_PORT=[port] # optional
```


{
  ...
  "user": "[user]@[domain]",
  "pass": "[pass]",
  "url": "ldaps://[address]",
  "port": 3000
}
```


## License

MIT
