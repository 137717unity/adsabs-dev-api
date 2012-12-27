# adsabs-dev-api

Developer API service description and example client code

## Access
To obtain access to the ADS Developer API you must first apply for and recieve a *developer token*. Email ???@adslabs.org to obtain a developer token.

**All** API requests must include your developer token in the *&dev_key* parameter.

## Access Settings
```
http://adslabs.org/adsabs/api/settings/?dev_key=...
```
Use this endpoint to view your API access permission settings.

## Search Requests

```
http://adslabs.org/adsabs/api/search/?dev_key=...
```

All requests to the search endpoint must include at least the *&q* query parameter. All parameter values shoud be UTF-8 and url-encoded. For search syntax and descriptions of the fields returned, see below.

The list of possible parameters is as follows. A "*" indicates a parameter that is not available at the "basic" access level.

#### q
a UTF-8, url-encoded string of <= 1000 characters representing the search query
#### fmt
Desired response format. Can be one of 'json' or 'xml'. Default is 'json'.
#### rows
number of results to return. Default is 10 and the max is determined by your API access permissions.
#### start
starting point for returned results (for pagination). Default is 0, max is determined by API access permissions.
#### fl
Specify the fields contained in each returned document. Check the *allowed_fields* shown in your */adsabs/api/settings/* to see what's available.
#### filter
Filter your query results using a particular *field:value* condition. This parameter is repeatable.

* *field* can be any field listed in the field descriptions below
* *value* should be a UTF-8, url-encoded string of <= characters

#### sort
Indicate how you wish the result set sorted. The format is *TYPE direction* where *direction* is one of "asc" or "desc", and *TYPE* is one of

* DATE - ordered by publication date
* RELEVANCE - ordered by the document's relevance score calculated during the search
* CITED - ordered by the number of citations
* POPULARITY - ordered by how often the document was "read" over the past 90 days

#### facet*
Include facet data in the response. The format of this parameter is *field[:limit[:mincount]]*, where...

* *field* is the name of the field
* *limit* is an integer specifying how many facet values to return
* *mincount* is an optional integer specifying the minimum count for a facet value to be included

#### hl*
Include snippets containing highlighted query terms with the returned results. The format of this parameter is *field[:count]* where...

* *field* is the field to extract the snippets from
* *count* is an integer specifying how many snippets to return per document

### Example search requests
```
# Simple search for "black holes"
http://adslabs.org/adsabs/api/search/?q=black+holes&dev_key=abc123

# Search for "dark energy", filter by author, sort by citation count
http://adslabs.org/adsabs/api/search/?q=dark+energy&filter=author%3A"Civano%2C+F"&sort=CITED+desc&dev_key=abc123
```
## Record Requests
```
http://adslabs.org/api/record/<identifier>?dev_key=...
```

## Search Syntax
