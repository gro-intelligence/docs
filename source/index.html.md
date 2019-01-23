---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - python

toc_footers:
  - <a href='https://gro-intelligence.com/products/gro-api'>Gro API</a>
  - <a href='https://github.com/gro-intelligence/api-client'>Gro API Client</a>

search: true
---

# Introduction

Welcome to the Gro API

# Setup

1. [MacOS and Linux](unix-setup.md)
2. [Windows](windows-setup.md)

# Library methods

## Search for entities

```python
import api.client.lib
API_HOST = 'api.gro-intelligence.com'
ACCESS_TOKEN=os.environ['GROAPI_TOKEN']
client = api.client.Client(API_HOST, ACCESS_TOKEN)
client.search('regions', 'United Sta')
```

> The above command returns a list of entities, sorted by relevancy to the search terms, like so:

```json
[ { 'id': 1215 }, { 'id': 1211 }, { 'id': 1212 }, { 'id': 1252 }, { 'id': 1000044080 } ]
```

## Lookup entities

```python
import api.client.lib
API_HOST = 'api.gro-intelligence.com'
ACCESS_TOKEN=os.environ['GROAPI_TOKEN']
client = api.client.Client(API_HOST, ACCESS_TOKEN)
client.lookup('items', 274)
```

> The above command returns a dictionary describing the requested entity:

```json
{
  'id': 274,
  'definition': "The seeds of the widely cultivated corn plant <i>Zea mays</i>, which is one of the world's most popular grains.",
  'name': 'Corn',
  'contains': []
}
```

## Search and lookup entities

There is a helper function combining the above two methods called search_and_lookup, which tells you more detailed info about your search results instead of just the ids:

```python
import api.client.lib
API_HOST = 'api.gro-intelligence.com'
ACCESS_TOKEN=os.environ['GROAPI_TOKEN']
client = api.client.Client(API_HOST, ACCESS_TOKEN)
region_names = [region['name'] for region in client.search_and_lookup('regions', 'United Sta')]
```

> The above command returns a list of names of search results, ranked by relevancy to input:

```json
[ 'United States', 'United Arab Emirates', 'United Kingdom', 'United States Minor Outlying Islands' ]
```

## Get Available Data Series