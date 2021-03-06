---
title: 'PY: Get Posts'
position: 1
description: 'Tutorial pulls a list of the posts from the blockchain with selected filter and tag then displays output.'
layout: full
---              
<span class="fa-pull-left top-of-tutorial-repo-link"><span class="first-word">Full</span>, runnable src of [Get Posts](https://github.com/dpays/developer-docs-tutorials-py/tree/master/tutorials/01_get_posts) can be downloaded as part of the [PY tutorials repository](https://github.com/dpays/developer-docs-tutorials-py).</span>
<br>



This tutorial will explain and show you how to access the **DPay** blockchain using the [dpay-python](https://github.com/dpays/dpay-python) library to fetch list of posts filtered by a _filter_ and _tag_

## Intro

In DPay there are built-in filters `trending`, `hot`, `created`, `active`, `promoted` etc. which helps us to get list of posts. `get_discussions_by_trending(query)`, `get_discussions_by_hot(query)`, `get_discussions_by_created(query)`, etc. functions are built-in in official library `dpay-python` that we are going to use throughout all Python tutorials.


## Steps

1.  [**App setup**](#app-setup) - Library install and import
1.  [**Filters list**](#filters-list) - List of filters to select from
1.  [**Query details**](#query-details) - Form a query
1.  [**Print output**](#print-output) - Print results in output

#### 1. App setup <a name="app-setup"></a>

In this tutorial we use 3 packages, `pick` - helps us to select filter interactively. `dpay` - dpay-python library, interaction with Blockchain. `pprint` - print results in better format.

First we import all three library and initialize DPay class

```python
    import pprint
    from pick import pick
    # initialize DPay class
    from dpay import DPay

    s = DPay()
```

#### 2. Filters list <a name="filters-list"></a>

Next we will make list of filters and setup `pick` properly.

```python
    title = 'Please choose filter: '
    #filters list
    options = ['trending', 'hot', 'active', 'created', 'promoted']
    # get index and selected filter name
    option, index = pick(options, title)
```

This will show us list of filters to select in terminal/command prompt. And after selection we will get index and filter name to `index` and `option` variables.

#### 3. Query details <a name="query-details"></a>

Next we will form a query. In DPay,

*   You can add a tag to filter the posts that you receive from the server
*   You can also limit the amount of results you would like to receive from the query

```python
query = {
    "limit":2, #number of posts
    "tag":"" #tag of posts
    }
#post list for selected query
posts = {0: s.get_discussions_by_trending(query),
         1: s.get_discussions_by_hot(query),
         2: s.get_discussions_by_active(query),
         3: s.get_discussions_by_created(query),
         4: s.get_discussions_by_promoted(query)
}
```

Above code shows example of query and simple list of function that will fetch post list with user selected filter.

#### 4. Print output <a name="print-output"></a>

Next, we will print result, post list and selected filter name.

```python
    # print post list for selected filter
    pprint.pprint(posts[index])
    pprint.pprint("Selected: "+option)
```

The example of result returned from the service is a `JSON` object with the following properties:

```json
[
    {
        "id": 37338948,
        "author": "dsiteblog",
        "permlink": "join-team-dsite-at-tokenfest",
        "category": "dsite",
        "parent_author": "",
        "parent_permlink": "dsite",
        "title": "Join Team dSite at TokenFest!",
        "body":
            "<a href=\"https://tokenfest.adria.digital\"><img src=\"https://i.imgur.com/fOScDIW.png\"/></a>\n\nTest Post",
        "json_metadata":
            "{\"tags\":[\"dsite\",\"tokenfest\",\"conference\"],\"image\":[\"https://i.imgur.com/fOScDIW.png\"],\"links\":[\"https://tokenfest.adria.digital\",\"https://tokenfest.adria.digital/\"],\"app\":\"dsite/0.1\",\"format\":\"markdown\"}",
        "last_update": "2018-03-07T23:22:54",
        "created": "2018-03-07T20:56:36",
        "active": "2018-03-13T01:40:21",
        "last_payout": "1970-01-01T00:00:00",
        "depth": 0,
        "children": 29,
        "net_rshares": "11453442114933",
        "abs_rshares": "11454054795840",
        "vote_rshares": "11454054795840",
        "children_abs_rshares": "13568695606090",
        "cashout_time": "2018-03-14T20:56:36",
        "max_cashout_time": "1969-12-31T23:59:59",
        "total_vote_weight": 3462435,
        "reward_weight": 10000,
        "total_payout_value": "0.000 BBD",
        "curator_payout_value": "0.000 BBD",
        "author_rewards": 0,
        "net_votes": 77,
        "root_comment": 37338948,
        "max_accepted_payout": "0.000 BBD",
        "percent_dpay_dollars": 10000,
        "allow_replies": true,
        "allow_votes": true,
        "allow_curation_rewards": true,
        "beneficiaries": [],
        "url": "/dsite/@dsiteblog/join-team-dsite-at-tokenfest",
        "root_title": "Join Team dSite at TokenFest!",
        "pending_payout_value": "46.436 BBD",
        "total_pending_payout_value": "0.000 BEX",
        "active_votes": [
            {
                "voter": "dsiteblog",
                "weight": 0,
                "rshares": "1870813909383",
                "percent": 10000,
                "reputation": "128210130644387",
                "time": "2018-03-07T20:56:36"
            },
            {
                "voter": "kevinwong",
                "weight": 526653,
                "rshares": "2208942520687",
                "percent": 5000,
                "reputation": "374133832002581",
                "time": "2018-03-08T04:27:00"
            }
        ],
        "replies": [],
        "author_reputation": "128210130644387",
        "promoted": "0.000 BBD",
        "body_length": 754,
        "reblogged_by": []
    },
    {

    }
]
'Selected: hot'
```

From this result you have access to everything associated to the posts including additional metadata which is a `JSON` string (that must be decoded to use), `active_votes` info, post title, body, etc. details that can be used in further development of application with Python.

That's it!

### To Run the tutorial

1.  [review dev requirements](https://github.com/dpays/developer-docs-tutorials-py/tree/master/tutorials/00_getting_started#dev-requirements)
1.  clone this repo
1.  `cd tutorials/01_get_posts`
1.  `pip install -r requirements.txt`
1.  `python index.py`
1.  After a few moments, you should see output in terminal/command prompt screen.


---
