# Global vs Local Data

## Introduction

There are two types of data in Chain Core: global data that is committed to the blockchain and shared by all cores in a network, and local data that is private to a specific Chain Core. Transactions and assets are the only global objects. All other objects are local.

Each Chain Core privately annotates global transaction and asset objects with relevant local data, if any.

For field-specific details, see [API Objects](../reference/api-objects.md).

## User-supplied global data

The transaction builder and the asset builder both include methods for providing user-supplied data that is committed to the blockchain.

* Asset definition
* Transaction reference data

### Asset definition

An asset definition is data about an asset that is written to the blockchain when you first issue units of it. It can include any details that you want participants in the blockchain to see. For example:

```
{
    "type": "security",
    "sub-type": "corporate-bond",
    "entity": "Acme Inc.",
    "maturity": "2016-09-01T18:24:47+00:00"
}
```

Chain Core does not specify any semantics for the asset definition. It is up to the application to determine what data it should contain.

### Transaction reference data

Transaction reference data is included in a transaction when it is written to the blockchain. It is useful for any type of external data related to the transaction. For example:

```
{
    "external_reference": "123456"
}
```

Transaction reference data can be included at the top level of a transaction, or on individual actions when building a transaction.

## User-supplied local data

The account builder and the asset builder both include methods for providing user-supplied data that is saved privately in the Chain Core.

### Account and asset aliases

Aliases are user-supplied, unique identifiers. They supplement the identifiers generated by Chain Core, which are not meant to be human readable. Using aliases when possible makes operations in the Chain Core API more convenient.

### Account tags

Accounts tags are local data that provide convenient storage and enable [complex queries](../build-applications/queries.md). For example:

```
{
    "type": "checking",
    "first_name": "Alice",
    "last_name": "Jones",
    "user_id": "123456",
    "status": "enabled"
}
```

### Asset tags

Asset tags are a local-only supplement to the asset definition and can be used to [query the blockchain](../build-applications/queries.md). This is useful for information you do not wish to publish on the blockchain, but rather distribute out of band to relevant parties. Asset tags also allow you to add additional local data about an asset that you didn't create. For example:

```
{
    "internal_rating": "B"
}
```

## Examples

All of the following code samples are extracted from a single, runnable Java file.

<a href="../examples/java/GlobalVsLocalData.java" class="downloadBtn btn success" target="\_blank">View Sample Code</a>

### Create accounts with tags

$code ../examples/java/GlobalVsLocalData.java create-accounts-with-tags

### Create assets with tags and definition

$code ../examples/java/GlobalVsLocalData.java create-asset-with-tags-and-definition

### Create transaction with transaction-level reference data

$code ../examples/java/GlobalVsLocalData.java build-tx-with-tx-ref-data

### Create transaction with action-level reference data

$code ../examples/java/GlobalVsLocalData.java build-tx-with-action-ref-data