# Secrets

## The Secret Resource

> `Note`

```python
# include this code when using cloudify python client-
from cloudify_rest_client import CloudifyClient
client = CloudifyClient(
        host='<manager-ip>',
        username='<manager-username>',
        password='<manager-password>',
        tenant='<manager-tenant>')
```

A Secret resource is a key-value pair saved per tenant.
A user can ensure all secrets (such as credentials to IaaS environments, passwords, etc) are kept in a secured manner,
and adhere to isolation requirements between different tenants.



### Attributes:

Attribute | Type | Description
--------- | ------- | -------
`key` | string | The secret's key, unique per tenant.
`value` | string | The secret's value.
`created_at` | datetime | The time when the secret was created.
`updated_at` | datetime | The time the secret was last updated at.


## Get Secret

> Request Example

```shell
$ curl -X GET --header "tenant: <tenant-name>" -u user:password "http://<manager-ip>/api/v3/secrets/<secret-key>"
```

```python
# Python Client-
client.secrets.get(<secret-key>)
```

> Response Example

```json
{
    "key": "key1",
    "value": "value1",
    "created_at": "2017-03-20T08:23:31.276Z",
    "updated_at": "2017-03-20T08:43:19.468Z",
    "permission": "creator",
    "tenant_name": "default_tenant",
    "created_by": "admin"
}
```

`GET "{manager-ip}/api/v3/secrets/{secret-key}"`

Retrieves a specific secret.

### URI Parameters
* `secret-key`: The key of the secret to retrieve.

### Response
A `Secret` resource.





## List Secrets

> Request Example

```shell
$ curl -X GET --header "tenant: <tenant-name>" -u user:password "http://<manager-ip>/api/v3/secrets"
```

```python
# Python Client-
client.secrets.list()
```

> Response Example

```json
{
 "items":
    [
        {
            "key": "key1",
            "created_at": "2017-03-20T08:23:31.276Z",
            "updated_at": "2017-03-20T08:43:19.468Z",
            "permission": "creator",
            "tenant_name": "default_tenant",
            "created_by": "admin"
        }
    ]
}
```

`GET "{manager-ip}/api/v3/secrets"`

List all secrets.

### Response
Field | Type | Description
--------- | ------- | -------
`items` | list | A list of `Secret` resources without the secret's value.





## Create Secret

> Request Example

```shell
$ curl -X PUT -H "Content-Type: application/json" -H "tenant: <tenant-name>" -d '{"value": <new-secret-value>}' -u user:password "http://<manager-ip>/api/v3/secrets/<new-secret-key>"
```

```python
# Python Client-
client.secrets.create(<new-secret-key>, <new-secret-value>)
```

> Response Example

```json
{
    "key": "key1",
    "value": "value1",
    "created_at": "2017-03-20T08:23:31.276Z",
    "updated_at": "2017-03-20T08:23:31.276Z",
    "permission": "creator",
    "tenant_name": "default_tenant",
    "created_by": "admin"
}
```

`PUT -d '{"value": <new-secret-value>}' "{manager-ip}/api/v3/secrets/{new-secret-key}"`

Creates a secret.

### URI Parameters
* `new-secret-key`: The key of the secret to create.

### Request Body
Property | Type | Description
--------- | ------- | -----------
`value` | string | The secret's value.

### Response
A `Secret` resource.





## Update Secret

> Request Example

```shell
$ curl -X PATCH -H "Content-Type: application/json" -H "tenant: <tenant-name>" -d '{"value": <new-value>}' -u user:password "http://<manager-ip>/api/v3/secrets/<secret-key>"
```

```python
# Python Client-
client.secrets.update(<secret-key>, <new-value>)
```

> Response Example

```json
{
    "key": "key1",
    "value": "value1",
    "created_at": "2017-03-20T08:23:31.276Z",
    "updated_at": "2017-03-20T08:43:19.468Z",
    "permission": "creator",
    "tenant_name": "default_tenant",
    "created_by": "admin"
}
```

`PATCH -d '{"value": <new-value>}' "{manager-ip}/api/v3/secrets/{secret-key}"`

Updates a secret.

### URI Parameters
* `secret-key`: The key of the secret to update.

### Request Body
Property | Type | Description
--------- | ------- | -----------
`value` | string | The secret's new value.

### Response
A `Secret` resource.





## Delete Secret

> Request Example

```shell
$ curl -X DELETE -H "Content-Type: application/json" -H "tenant: <tenant-name>" -u user:password "http://<manager-ip>/api/v3/secrets/<secret-key>"
```

```python
# Python Client-
client.secrets.delete(<secret-key>)
```

> Response Example

```json
{
    "key": "key1",
    "value": "value1",
    "created_at": "2017-03-20T08:23:31.276Z",
    "updated_at": "2017-03-20T08:43:19.468Z",
    "permission": "creator",
    "tenant_name": "default_tenant",
    "created_by": "admin"
}
```

`DELETE "{manager-ip}/api/v3/secrets/{secret-key}"`

Deletes a secret.

### URI Parameters
* `secret-key`: The key of the secret to delete.

### Response
A `Secret` resource.