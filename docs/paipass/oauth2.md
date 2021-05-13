# OAuth2

This is largely an extension of the OAuth2 code supplied by  [django-oauth-toolkit](https://github.com/jazzband/django-oauth-toolkit)  to make up for its ostensible shortcomings.

## Models

### Paipass Application

An extension of the AbstractApplication model in order to add in namespaces, a validator for the namespace (not working), and a description of the application.


### Paipass Access Token
This is largely to prevent usage of this in Jazzband's code in ways we don't want. That is, we don't have the scope set here; it should be set in AccessTokenScopes.


### Access Token Scopes
This sort of wraps PaipassAccessToken and adds on the custom modifications as per the requirements document. 

You can effectively think of this as a way to attach multiple scopes to one PaipassAccessToken. It also adds on some "permissions" for the scopes.

It uses an Attribute model to store the scope name itself.

An example of the usage can be found in [validators_redux.py](https://github.com/projectpai/paipass/blob/main/backend/oauth2/validators_redux.py).

```python
def generate_ats_from_rt(self, refresh_token, access_token, request):
        for scope in request.scopes:
            rw, namespace, name = scope_expression_to_symbols(scope)
            application = PaipassApplication.objects.all().get(namespace__iexact=namespace)
            attr = Attribute.objects.all().get(application=application,
                                               name__iexact=name)
            ats = AccessTokenScopes.objects.create(access_token=access_token,
                                                   attribute=attr,
                                                   max_perms=attributes.convert_to_enum_perms(rw),
                                                   status=ATS_StatusChoices.APPROVED,
                                                   user=request.user)
            ats.access_token = access_token
            ats.save()

```


### Paipass Grant