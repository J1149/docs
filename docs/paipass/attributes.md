# Attributes


So this works hand-in-hand with the OAuth2 system to manage permissions to the data, manage how the data is allowed to manifest, and to store the data itself.


It's essentially a key/value pairing. The Attribute corresponds to the key the AttributeData corresponds to the value. The OAuth2 Application creates the Attribute and the user creates AttributeData corresponding to that attribute.

## Models


### Attribute

- application corresponds to the application


### AllowedValue

This corresponds to the allowed values the attribute is allowed to take on. This is set by the owning_app when it creates the attribute

### AttributeApproval

Manages the approval of access to the attribute. 

- owning_app corresponds to the application that owns the attribute

- requesting_app corresponds to the application that is requesting the data

- user corresponds to the user who owns the AttributeData

### AttributeData

This holds the data itself.