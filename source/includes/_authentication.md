# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl https://api.peoplepattern.com/... \
  -H "Authorization: secretkey"
```

> Make sure to replace `secretkey` with your API key.

To access the People Pattern APIs you must acquire an authorization
key. This may be retrieved from the People Pattern dashboard application
via the following steps.


### Acquire your key from the People Pattern dashboard

**Step 1** Go to your company administration page

![Click Company administration from account menu](images/to-co-admin.png)

**Step 2** Select "Manage API key" tab

![Click Manage API key tab](images/to-manage-keys.png)

**Step 3** I really don't know how the rest of this is going to
play out, consider this just a template or example.

### Using your key

Requests to the API must contain an authorization header of the
following form.

`Authorization: token secretkey`

<aside class="notice">
You must replace <code>secretkey</code> with your personal API key.
</aside>