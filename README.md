## ARM HAR File Config

This Repo will contain the default configuration for the application that will allow parsing HAR Files that are generated on the Azure Portal.

### Aliases

In the *aliases.json* you will find a JSON that defines where and how information extracted from a HAR file can be extracted/viewed. I will use the word *entry* to refer
to a Log Entry which is a Request/Response pair.

#### Syntax

The payload is composed by an array which contains several objects, each defines one alias and allow access to the value of one property.

##### Creating Aliases

To create an alias, you can add a new object to the *requestAliases* or *responseAliases* arrays depending on where this information can be found.

The following properties are part of the alias object syntax:
- *aliasName*: Here you can give a name to the Alias, this will be used when trying to load the information in the application. The syntax follows somewhat the Azure Policy Syntax: PATH/Friendly Name of child Property/Friendly Name of next child Property/...
- *path*: Where the value will be extracted from, please refer to the examples below:
    Give the following request:
      {
        "request":{
          "headers":{
            "someHeader":"someValue",
            ...
          },
          "httpMethod":"GET",
          ...
        },
        "response":{
          ...
        }
      }
  The Path we can use to extract the header *someHeader* is the following: ***request.headers.someHeader***, the application will expand the object and return the value found on the path specified.
- *displayName*: Name this alias with a friendly name based on the value it returns
- *conditions*: Work in progress, this might be a feature on the future to allow displaying aliases based on certain conditions.
