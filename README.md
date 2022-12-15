# Python SDK for OpenFGA

[![pypi](https://img.shields.io/pypi/v/openfga_sdk.svg?style=flat)](https://pypi.org/project/openfga_sdk)
[![Release](https://img.shields.io/github/v/release/openfga/python-sdk?sort=semver&color=green)](https://github.com/openfga/python-sdk/releases)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](./LICENSE)
[![FOSSA Status](https://app.fossa.com/api/projects/custom%2B4989%2Fgithub.com%2Fopenfga%2Fpython-sdk.svg?type=shield)](https://app.fossa.com/reports/824fbc44-7513-4496-84a4-f7ffb3fa23f7)
[![Discord Server](https://img.shields.io/discord/759188666072825867?color=7289da&logo=discord "Discord Server")](https://discord.com/channels/759188666072825867/930524706854031421)
[![Twitter](https://img.shields.io/twitter/follow/openfga?color=%23179CF0&logo=twitter&style=flat-square "@openfga on Twitter")](https://twitter.com/openfga)

This is an autogenerated python SDK for OpenFGA. It provides a wrapper around the [OpenFGA API definition](https://openfga.dev/api).

## Table of Contents

- [About OpenFGA](#about)
- [Resources](#resources)
- [Installation](#installation)
- [Getting Started](#getting-started)
  - [Initializing the API Client](#initializing-the-api-client)
  - [Get your Store ID](#get-your-store-id)
  - [Calling the API](#calling-the-api)
    - [List All Stores](#list-stores)
    - [Create a Store](#create-store)
    - [Get a Store](#get-store)
    - [Delete a Store](#delete-store)
    - [Write Authorization Model](#write-authorization-model)
    - [Read a Single Authorization Model](#read-a-single-authorization-model)
    - [Read Authorization Model IDs](#read-authorization-model-ids)
    - [Check](#check)
    - [Write Tuples](#write-tuples)
    - [Delete Tuples](#delete-tuples)
    - [Expand](#expand)
    - [Read Tuples](#read-tuples)
    - [Read Changes (Watch)](#read-changes-watch)
    - [List Objects](#list-objects)
  - [API Endpoints](#api-endpoints)
  - [Models](#models)
- [Contributing](#contributing)
  - [Issues](#issues)
  - [Pull Requests](#pull-requests)
- [License](#license)

## About

[OpenFGA](https://openfga.dev) is an open source Fine-Grained Authorization solution inspired by [Google's Zanzibar paper](https://research.google/pubs/pub48190/). It was created by the FGA team at [Auth0](https://auth0.com) based on [Auth0 Fine-Grained Authorization (FGA)](https://fga.dev), available under [a permissive license (Apache-2)](https://github.com/openfga/rfcs/blob/main/LICENSE) and welcomes community contributions.

OpenFGA is designed to make it easy for application builders to model their permission layer, and to add and integrate fine-grained authorization into their applications. OpenFGA’s design is optimized for reliability and low latency at a high scale.


## Resources

- [OpenFGA Documentation](https://openfga.dev/docs)
- [OpenFGA API Documentation](https://openfga.dev/api/service)
- [Twitter](https://twitter.com/openfga)
- [OpenFGA Discord Community](https://discord.gg/8naAwJfWN6)
- [Zanzibar Academy](https://zanzibar.academy)
- [Google's Zanzibar Paper (2019)](https://research.google/pubs/pub48190/)

## Installation

### pip install

#### PyPI

The openfga_sdk is available to be downloaded via PyPI, you can install directly using:

```sh
pip3 install openfga_sdk
```
(you may need to run `pip` with root permission: `sudo pip3 install openfga_sdk`)

Then import the package:
```python
import openfga_sdk
```

#### GitHub

The openfga_sdk is also hosted in GitHub, you can install directly using:

```sh
pip3 install https://github.com/openfga/python-sdk.git
```
(you may need to run `pip` with root permission: `sudo pip3 install https://github.com/openfga/python-sdk.git`)

Then import the package:
```python
import openfga_sdk
```

### Setuptools

Install via [Setuptools](https://pypi.python.org/pypi/setuptools).

```sh
python setup.py install --user
```
(or `sudo python setup.py install` to install the package for all users)

Then import the package:
```python
import openfga_sdk
```


## Getting Started

### Initializing the API Client

[Learn how to initialize your SDK](https://openfga.dev/docs/getting-started/setup-sdk-client)

#### No Authentication ####

##### Without Store ID #####

To configure the SDK API client without store ID, we can initialize the api client by specifying the scheme and host.

```python
import openfga_sdk
from openfga_sdk.api import open_fga_api

configuration = openfga_sdk.Configuration(
    api_scheme = 'https',
    api_host = 'api.fga.example'
)

async def api_setup():
    # Enter a context with an instance of the API client
    async with openfga_sdk.ApiClient(configuration) as api_client:
        # Create an instance of the API class
        api_instance = open_fga_api.OpenFgaApi(api_client)

```

##### With Store ID #####

To configure the SDK API client store ID, we can initialize the api client by specifying the scheme, host and store_id.

```python
import openfga_sdk
from openfga_sdk.api import open_fga_api

configuration = openfga_sdk.Configuration(
    api_scheme = 'https',
    api_host = 'api.fga.example',
    store_id = 'YOUR_STORE_ID'
)

async def api_setup():
    # Enter a context with an instance of the API client
    async with openfga_sdk.ApiClient(configuration) as api_client:
        # Create an instance of the API class
        api_instance = open_fga_api.OpenFgaApi(api_client)

```

Another possibility is to use the existing configuration and add store id in its configuration

```python
import openfga_sdk
from openfga_sdk.api import open_fga_api

configuration = openfga_sdk.Configuration(
    api_scheme = 'https',
    api_host = 'api.fga.example'
)

async def api_setup():
    configuration.store_id = 'YOUR_STORE_ID'

    # Enter a context with an instance of the API client
    async with openfga_sdk.ApiClient(configuration) as api_client:
        # Create an instance of the API class
        api_instance = open_fga_api.OpenFgaApi(api_client)

```

#### Authentication via API Token ####

To configure the SDK API client with authentication via API TOKEN, we can initialize the api client by specifying the scheme, host and credentials.

```python
import openfga_sdk
from openfga_sdk.api import open_fga_api
from openfga_sdk.credentials import Credentials, CredentialConfiguration

credentials = Credentials(method='api_token', configuration=CredentialConfiguration(api_token='TOKEN1'))
configuration = openfga_sdk.Configuration(
    api_scheme = 'https',
    api_host = 'api.fga.example',
    credentials = credentials
)

async def api_setup():
    # Enter a context with an instance of the API client
    async with openfga_sdk.ApiClient(configuration) as api_client:
        # Create an instance of the API class
        api_instance = open_fga_api.OpenFgaApi(api_client)

```


### Get your Store ID

You need your store id to call the OpenFGA API (unless it is to call the [CreateStore](#create-store) or [ListStores](#list-stores) methods).

If your server is configured with [authentication enabled](https://openfga.dev/docs/getting-started/setup-openfga#configuring-authentication), you also need to have your credentials ready.

### Calling the API

#### List Stores

[API Documentation](https://openfga.dev/api/service/docs/api#/Stores/ListStores)

```python
configuration = openfga_sdk.Configuration(
    api_scheme = os.environ.get(OPENFGA_API_SCHEME),
    api_host = os.environ.get(OPENFGA_API_HOST),
)

# Get all stores
async def list_stores():
    # Create an instance of the API class
    api_client = openfga_sdk.ApiClient(configuration)
    api_instance = open_fga_api.OpenFgaApi(api_client)

    response = await api_instance.list_stores()
    # response = ListStoreResponse(...)
    # response.stores = [Store({"id": "01FQH7V8BEG3GPQW93KTRFR8JB", "name": "FGA Demo Store", "created_at": "2022-01-01T00:00:00.000Z", "updated_at": "2022-01-01T00:00:00.000Z"})]
    await api_client.close()
```

#### Create Store

[API Documentation](https://openfga.dev/api/service/docs/api#/Stores/CreateStore)

```python
configuration = openfga_sdk.Configuration(
    api_scheme = os.environ.get(OPENFGA_API_SCHEME),
    api_host = os.environ.get(OPENFGA_API_HOST),
)

# Create a store
async def create_store():
    # Create an instance of the API class
    api_client = openfga_sdk.ApiClient(configuration)
    api_instance = open_fga_api.OpenFgaApi(api_client)

    body = CreateStoreRequest(
        name = "FGA Demo Store",
    )
    response = await api_instance.create_store(body)
    # response.id = "01FQH7V8BEG3GPQW93KTRFR8JB"
    await api_client.close()
```


#### Get Store

[API Documentation](https://openfga.dev/api/service/docs/api#/Stores/GetStore)

> Requires a client initialized with a storeId

```python
configuration = openfga_sdk.Configuration(
    api_scheme = os.environ.get(OPENFGA_API_SCHEME),
    api_host = os.environ.get(OPENFGA_API_HOST),
    store_id = os.environ.get(OPENFGA_STORE_ID),
)

# Get a store
async def get_store():
    # Create an instance of the API class
    api_client = openfga_sdk.ApiClient(configuration)
    api_instance = open_fga_api.OpenFgaApi(api_client)

    response = await api_instance.get_store()
    # response = Store({"id": "01FQH7V8BEG3GPQW93KTRFR8JB", "name": "FGA Demo Store", "created_at": "2022-01-01T00:00:00.000Z", "updated_at": "2022-01-01T00:00:00.000Z"})
    await api_client.close()
```


#### Delete Store

[API Documentation](https://openfga.dev/api/service/docs/api#/Stores/DeleteStore)

> Requires a client initialized with a storeId

```python
configuration = openfga_sdk.Configuration(
    api_scheme = os.environ.get(OPENFGA_API_SCHEME),
    api_host = os.environ.get(OPENFGA_API_HOST),
    store_id = os.environ.get(OPENFGA_STORE_ID),
)

# Delete a store
async def delete_store():
    # Create an instance of the API class
    api_client = openfga_sdk.ApiClient(configuration)
    api_instance = open_fga_api.OpenFgaApi(api_client)

    await api_instance.delete_store()
    await api_client.close()
```

#### Write Authorization Model

[API Documentation](https://openfga.dev/api/service#/Authorization%20Models/WriteAuthorizationModel)

> Requires a client initialized with a storeId

> Note: To learn how to build your authorization model, check the Docs at https://openfga.dev/docs.

> Learn more about [the OpenFGA configuration language](https://openfga.dev/docs/configuration-language).

```python
configuration = openfga_sdk.Configuration(
    api_scheme = os.environ.get(OPENFGA_API_SCHEME),
    api_host = os.environ.get(OPENFGA_API_HOST),
    store_id = os.environ.get(OPENFGA_STORE_ID),
)

# Create a new authorization model
async def write_authorization_model():
    # Create an instance of the API class
    api_client = openfga_sdk.ApiClient(configuration)
    api_instance = open_fga_api.OpenFgaApi(api_client)
    type_definitions = WriteAuthorizationModelRequest(
        type_definitions=[
            TypeDefinition(
                type="user",
            ),
            TypeDefinition(
                type="document",
                relations=dict(
                    writer=Userset(
                        this=dict(),
                    ),
                    viewer=Userset(
                        union=Usersets(
                            child=[
                                Userset(this=dict()),
                                Userset(computed_userset=ObjectRelation(
                                    object="",
                                    relation="writer",
                                )),
                            ],
                        ),
                    ),
                )
            ),
        ],
    )

    response = await api_instance.write_authorization_model(type_definitions)
    # response.authorization_model_id = "1uHxCSuTP0VKPYSnkq1pbb1jeZw"
    await api_client.close()
```


#### Read a Single Authorization Model

[API Documentation](https://openfga.dev/api/service#/Authorization%20Models/ReadAuthorizationModel)

```python
configuration = openfga_sdk.Configuration(
    api_scheme = os.environ.get(OPENFGA_API_SCHEME),
    api_host = os.environ.get(OPENFGA_API_HOST),
    store_id = os.environ.get(OPENFGA_STORE_ID),
)

# Return a particular version of an authorization model
async def read_authorization_id():
    # Create an instance of the API class
    api_client = openfga_sdk.ApiClient(configuration)
    api_instance = open_fga_api.OpenFgaApi(api_client)
    id = "1uHxCSuTP0VKPYSnkq1pbb1jeZw" #  Assuming `1uHxCSuTP0VKPYSnkq1pbb1jeZw` is an id of an existing model

    response = await api_instance.read_authorization_model(id)
    # response.authorization_model =  AuthorizationModel(id='1uHxCSuTP0VKPYSnkq1pbb1jeZw', type_definitions=type_definitions[...])
    await api_client.close()
```

#### Read Authorization Model IDs

[API Documentation](https://openfga.dev/api/service#/Authorization%20Models/ReadAuthorizationModels)

```python
configuration = openfga_sdk.Configuration(
    api_scheme = os.environ.get(OPENFGA_API_SCHEME),
    api_host = os.environ.get(OPENFGA_API_HOST),
    store_id = os.environ.get(OPENFGA_STORE_ID),
)

# Return all the authorization models for a particular store
async def read_authorization_models():
    # Create an instance of the API class
    api_client = openfga_sdk.ApiClient(configuration)
    api_instance = open_fga_api.OpenFgaApi(api_client)

    response = await api_instance.read_authorization_models()
    # response.authorization_models = [AuthorizationModel(id='1uHxCSuTP0VKPYSnkq1pbb1jeZw', type_definitions=type_definitions[...], AuthorizationModel(id='GtQpMohWezFmIbyXxVEocOCxxgq', type_definitions=type_definitions[...])]
    await api_client.close()
```


#### Check

[API Documentation](https://openfga.dev/api/service#/Relationship%20Queries/Check)

```python
configuration = openfga_sdk.Configuration(
    api_scheme = os.environ.get(OPENFGA_API_SCHEME),
    api_host = os.environ.get(OPENFGA_API_HOST),
    store_id = os.environ.get(OPENFGA_STORE_ID),
)

# Check whether a user is authorized to access an object
async def check():
    # Create an instance of the API class
    api_client = openfga_sdk.ApiClient(configuration)
    api_instance = open_fga_api.OpenFgaApi(api_client)
    body = CheckRequest(
        tuple_key=TupleKey(
            user="user:81684243-9356-4421-8fbf-a4f8d36aa31b",
            relation="viewer",
            object="document:roadmap",
        ),
        authorization_model_id="1uHxCSuTP0VKPYSnkq1pbb1jeZw",
    )

    response = await api_instance.check(body)
    # response.allowed = True
    await api_client.close()
```


#### Write Tuples

[API Documentation](https://openfga.dev/api/service#/Relationship%20Tuples/Write)

```python
configuration = openfga_sdk.Configuration(
    api_scheme = os.environ.get(OPENFGA_API_SCHEME),
    api_host = os.environ.get(OPENFGA_API_HOST),
    store_id = os.environ.get(OPENFGA_STORE_ID),
)

# Add tuples from the store
async def write():
    # Create an instance of the API class
    api_client = openfga_sdk.ApiClient(configuration)
    api_instance = open_fga_api.OpenFgaApi(api_client)
    body = WriteRequest(
        writes=TupleKeys(
            tuple_keys=[
                TupleKey(
                    user="user:81684243-9356-4421-8fbf-a4f8d36aa31b",
                    relation="viewer",
                    object="document:roadmap",
                ),
            ],
        ),
        authorization_model_id="1uHxCSuTP0VKPYSnkq1pbb1jeZw",
    )

    response = await api_instance.write(body)
    await api_client.close()
```

#### Delete Tuples

[API Documentation](https://openfga.dev/api/service#/Relationship%20Tuples/Write)

```python
configuration = openfga_sdk.Configuration(
    api_scheme = os.environ.get(OPENFGA_API_SCHEME),
    api_host = os.environ.get(OPENFGA_API_HOST),
    store_id = os.environ.get(OPENFGA_STORE_ID),
)

# Delete tuples from the store
async def delete():
    # Create an instance of the API class
    api_client = openfga_sdk.ApiClient(configuration)
    api_instance = open_fga_api.OpenFgaApi(api_client)
    body = WriteRequest(
        deletes=TupleKeys(
            tuple_keys=[
                TupleKey(
                    user="user:81684243-9356-4421-8fbf-a4f8d36aa31b",
                    relation="viewer",
                    object="document:roadmap",
                ),
            ],
        ),
        authorization_model_id="1uHxCSuTP0VKPYSnkq1pbb1jeZw",
    ) 

    response = await api_instance.write(body)
    await api_client.close()
```

#### Expand

[API Documentation](https://openfga.dev/api/service#/Relationship%20Queries/Expand)

```python
configuration = openfga_sdk.Configuration(
    api_scheme = os.environ.get(OPENFGA_API_SCHEME),
    api_host = os.environ.get(OPENFGA_API_HOST),
    store_id = os.environ.get(OPENFGA_STORE_ID),
)

# Expand all relationships in userset tree format, and following userset rewrite rules.  Useful to reason about and debug a certain relationship
async def expand():
    # Create an instance of the API class
    api_client = openfga_sdk.ApiClient(configuration)
    api_instance = open_fga_api.OpenFgaApi(api_client)
    body = ExpandRequest(
        tuple_key=TupleKey(
            relation="viewer",
            object="document:roadmap",
        ),
        authorization_model_id="1uHxCSuTP0VKPYSnkq1pbb1jeZw",
    )

    response = await api_instance.expand(body)
    # response = ExpandResponse({"tree": UsersetTree({"root": Node({"name": "document:roadmap#viewer", "leaf": Leaf({"users": Users({"users": ["user:81684243-9356-4421-8fbf-a4f8d36aa31b", "user:f52a4f7a-054d-47ff-bb6e-3ac81269988f"]})})})})})
    await api_client.close()
```

#### Read Changes

[API Documentation](https://openfga.dev/api/service#/Relationship%20Tuples/Read)

```python
configuration = openfga_sdk.Configuration(
    api_scheme = os.environ.get(OPENFGA_API_SCHEME),
    api_host = os.environ.get(OPENFGA_API_HOST),
    store_id = os.environ.get(OPENFGA_STORE_ID),
)

async def read():
    # Create an instance of the API class
    api_client = openfga_sdk.ApiClient(configuration)
    api_instance = open_fga_api.OpenFgaApi(api_client)

    # Find if a relationship tuple stating that a certain user is a viewer of certain document
    body = ReadRequest(
        tuple_key=TupleKey(
            user="user:81684243-9356-4421-8fbf-a4f8d36aa31b",
            relation="viewer",
            object="document:roadmap",
        ),
    ) 

    # Find all relationship tuples where a certain user has a relationship as any relation to a certain document
    body = ReadRequest(
        tuple_key=TupleKey(
            user="user:81684243-9356-4421-8fbf-a4f8d36aa31b",
            object="document:roadmap",
        ),
    ) 

    # Find all relationship tuples where a certain user is a viewer of any document
    body = ReadRequest(
        tuple_key=TupleKey(
            user="user:81684243-9356-4421-8fbf-a4f8d36aa31b",
            relation="viewer",
            object="document:",
        ),
    )

    # Find all relationship tuples where any user has a relationship as any relation with a particular document
    body = ReadRequest(
        tuple_key=TupleKey(
            object="document:roadmap",
        ),
    )

    // Read all stored relationship tuples
    body := ReadRequest()

    response = await api_instance.read(body)
    # response = ReadResponse({"tuples": [Tuple({"key": TupleKey({"user":"...","relation":"...","object":"..."}), "timestamp": datetime.fromisoformat("...") })]})
    await api_client.close()
```

#### Read Changes (Watch)

[API Documentation](https://openfga.dev/api/service#/Relationship%20Tuples/ReadChanges)

```python
configuration = openfga_sdk.Configuration(
    api_scheme = os.environ.get(OPENFGA_API_SCHEME),
    api_host = os.environ.get(OPENFGA_API_HOST),
    store_id = os.environ.get(OPENFGA_STORE_ID),
)

# Return a list of all the tuple changes
async def read_changes():
    # Create an instance of the API class
    api_client = openfga_sdk.ApiClient(configuration)
    api_instance = open_fga_api.OpenFgaApi(api_client)

    type = "document"
    page_size = 25
    continuation_token = "eyJwayI6IkxBVEVTVF9OU0NPTkZJR19hdXRoMHN0b3JlIiwic2siOiIxem1qbXF3MWZLZExTcUoyN01MdTdqTjh0cWgifQ=="

    response = await api_instance.read_changes(type=type, page_size=page_size, continuation_token=continuation_token)
    # response.continuation_token = ...
    # response.changes = [TupleChange(tuple_key=TupleKey(object="...",relation="...",user="..."),operation=TupleOperation("TUPLE_OPERATION_WRITE"),timestamp=datetime.fromisoformat("..."))]
    await api_client.close()
```

#### List Objects

[API Documentation](https://openfga.dev/api/service#/Relationship%20Queries/ListObjects)

```python
configuration = openfga_sdk.Configuration(
    api_scheme = os.environ.get(OPENFGA_API_SCHEME),
    api_host = os.environ.get(OPENFGA_API_HOST),
    store_id = os.environ.get(OPENFGA_STORE_ID),
)

# ListObjects lists all of the object ids for objects of the provided type that the given user has a specific relation with.
async def list_objects():
    # Create an instance of the API class
    api_client = openfga_sdk.ApiClient(configuration)
    api_instance = open_fga_api.OpenFgaApi(api_client)
    body = ListObjectsRequest(
        authorization_model_id="1uHxCSuTP0VKPYSnkq1pbb1jeZw",
        user="user:81684243-9356-4421-8fbf-a4f8d36aa31b",
        relation="viewer",
        type="document",
        contextual_tuples=ContextualTupleKeys( # optional
            tuple_keys=[
                TupleKey(
                    user="user:81684243-9356-4421-8fbf-a4f8d36aa31b",
                    relation="writer",
                    object="document:budget",
                ),
            ],
        ),
    )

    response = await api_instance.list_objects(body)
    # response.objects = ["document:roadmap"]
    await api_client.close()
```


### API Endpoints

Class | Method | HTTP request | Description
------------ | ------------- | ------------- | -------------
*OpenFgaApi* | [**check**](docs/OpenFgaApi.md#check) | **POST** /stores/{store_id}/check | Check whether a user is authorized to access an object
*OpenFgaApi* | [**create_store**](docs/OpenFgaApi.md#create_store) | **POST** /stores | Create a store
*OpenFgaApi* | [**delete_store**](docs/OpenFgaApi.md#delete_store) | **DELETE** /stores/{store_id} | Delete a store
*OpenFgaApi* | [**expand**](docs/OpenFgaApi.md#expand) | **POST** /stores/{store_id}/expand | Expand all relationships in userset tree format, and following userset rewrite rules.  Useful to reason about and debug a certain relationship
*OpenFgaApi* | [**get_store**](docs/OpenFgaApi.md#get_store) | **GET** /stores/{store_id} | Get a store
*OpenFgaApi* | [**list_objects**](docs/OpenFgaApi.md#list_objects) | **POST** /stores/{store_id}/list-objects | [EXPERIMENTAL] Get all object ids of the given type that the user has a relation with
*OpenFgaApi* | [**list_stores**](docs/OpenFgaApi.md#list_stores) | **GET** /stores | List all stores
*OpenFgaApi* | [**read**](docs/OpenFgaApi.md#read) | **POST** /stores/{store_id}/read | Get tuples from the store that matches a query, without following userset rewrite rules
*OpenFgaApi* | [**read_assertions**](docs/OpenFgaApi.md#read_assertions) | **GET** /stores/{store_id}/assertions/{authorization_model_id} | Read assertions for an authorization model ID
*OpenFgaApi* | [**read_authorization_model**](docs/OpenFgaApi.md#read_authorization_model) | **GET** /stores/{store_id}/authorization-models/{id} | Return a particular version of an authorization model
*OpenFgaApi* | [**read_authorization_models**](docs/OpenFgaApi.md#read_authorization_models) | **GET** /stores/{store_id}/authorization-models | Return all the authorization models for a particular store
*OpenFgaApi* | [**read_changes**](docs/OpenFgaApi.md#read_changes) | **GET** /stores/{store_id}/changes | Return a list of all the tuple changes
*OpenFgaApi* | [**write**](docs/OpenFgaApi.md#write) | **POST** /stores/{store_id}/write | Add or delete tuples from the store
*OpenFgaApi* | [**write_assertions**](docs/OpenFgaApi.md#write_assertions) | **PUT** /stores/{store_id}/assertions/{authorization_model_id} | Upsert assertions for an authorization model ID
*OpenFgaApi* | [**write_authorization_model**](docs/OpenFgaApi.md#write_authorization_model) | **POST** /stores/{store_id}/authorization-models | Create a new authorization model


### Models

## Documentation For Models

 - [Any](docs/Any.md)
 - [Assertion](docs/Assertion.md)
 - [AuthorizationModel](docs/AuthorizationModel.md)
 - [CheckRequest](docs/CheckRequest.md)
 - [CheckResponse](docs/CheckResponse.md)
 - [Computed](docs/Computed.md)
 - [ContextualTupleKeys](docs/ContextualTupleKeys.md)
 - [CreateStoreRequest](docs/CreateStoreRequest.md)
 - [CreateStoreResponse](docs/CreateStoreResponse.md)
 - [Difference](docs/Difference.md)
 - [ErrorCode](docs/ErrorCode.md)
 - [ExpandRequest](docs/ExpandRequest.md)
 - [ExpandResponse](docs/ExpandResponse.md)
 - [GetStoreResponse](docs/GetStoreResponse.md)
 - [InternalErrorCode](docs/InternalErrorCode.md)
 - [InternalErrorMessageResponse](docs/InternalErrorMessageResponse.md)
 - [Leaf](docs/Leaf.md)
 - [ListObjectsRequest](docs/ListObjectsRequest.md)
 - [ListObjectsResponse](docs/ListObjectsResponse.md)
 - [ListStoresResponse](docs/ListStoresResponse.md)
 - [Metadata](docs/Metadata.md)
 - [Node](docs/Node.md)
 - [Nodes](docs/Nodes.md)
 - [NotFoundErrorCode](docs/NotFoundErrorCode.md)
 - [ObjectRelation](docs/ObjectRelation.md)
 - [PathUnknownErrorMessageResponse](docs/PathUnknownErrorMessageResponse.md)
 - [ReadAssertionsResponse](docs/ReadAssertionsResponse.md)
 - [ReadAuthorizationModelResponse](docs/ReadAuthorizationModelResponse.md)
 - [ReadAuthorizationModelsResponse](docs/ReadAuthorizationModelsResponse.md)
 - [ReadChangesResponse](docs/ReadChangesResponse.md)
 - [ReadRequest](docs/ReadRequest.md)
 - [ReadResponse](docs/ReadResponse.md)
 - [RelationMetadata](docs/RelationMetadata.md)
 - [RelationReference](docs/RelationReference.md)
 - [Status](docs/Status.md)
 - [Store](docs/Store.md)
 - [Tuple](docs/Tuple.md)
 - [TupleChange](docs/TupleChange.md)
 - [TupleKey](docs/TupleKey.md)
 - [TupleKeys](docs/TupleKeys.md)
 - [TupleOperation](docs/TupleOperation.md)
 - [TupleToUserset](docs/TupleToUserset.md)
 - [TypeDefinition](docs/TypeDefinition.md)
 - [Users](docs/Users.md)
 - [Userset](docs/Userset.md)
 - [UsersetTree](docs/UsersetTree.md)
 - [UsersetTreeDifference](docs/UsersetTreeDifference.md)
 - [UsersetTreeTupleToUserset](docs/UsersetTreeTupleToUserset.md)
 - [Usersets](docs/Usersets.md)
 - [ValidationErrorMessageResponse](docs/ValidationErrorMessageResponse.md)
 - [WriteAssertionsRequest](docs/WriteAssertionsRequest.md)
 - [WriteAuthorizationModelRequest](docs/WriteAuthorizationModelRequest.md)
 - [WriteAuthorizationModelResponse](docs/WriteAuthorizationModelResponse.md)
 - [WriteRequest](docs/WriteRequest.md)



## Contributing

### Issues

If you have found a bug or if you have a feature request, please report them on the [sdk-generator repo](https://github.com/openfga/sdk-generator/issues) issues section. Please do not report security vulnerabilities on the public GitHub issue tracker.

### Pull Requests

All changes made to this repo will be overwritten on the next generation, so we kindly ask that you send all pull requests related to the SDKs to the [sdk-generator repo](https://github.com/openfga/sdk-generator) instead.

## Author

[OpenFGA](https://github.com/openfga)

## License

This project is licensed under the Apache-2.0 license. See the [LICENSE](https://github.com/openfga/python-sdk/blob/main/LICENSE) file for more info.

The code in this repo was auto generated by [OpenAPI Generator](https://github.com/OpenAPITools/openapi-generator) from a template based on the [python legacy template](https://github.com/OpenAPITools/openapi-generator/tree/master/modules/openapi-generator/src/main/resources/python-legacy), licensed under the [Apache License 2.0](https://github.com/OpenAPITools/openapi-generator/blob/master/LICENSE).
