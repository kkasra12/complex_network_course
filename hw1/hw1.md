---
jupyter:
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
  language_info:
    codemirror_mode:
      name: ipython
      version: 3
    file_extension: .py
    mimetype: 'text/x-python'
    name: python
    nbconvert_exporter: python
    pygments_lexer: ipython3
    version: 3.11.0rc1
  nbformat: 4
  nbformat_minor: 2
---

::: {.cell .code execution_count="144"}
``` {.python}
group_num = 9
import os
import json
import subprocess
from collections import defaultdict
import random
```
:::

::: {.cell .code execution_count="145"}
``` {.python}
# for demonstration:
!curl -s https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Facebook-Ego
!curl -s https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Twitter-Ego
```

::: {.output .stream .stdout}
    [
      {
        "name": "3437_2.edges",
        "path": "Datasets/Group9/Facebook-Ego/3437_2.edges",
        "sha": "dfa336a00b692fc39b3d553f577bfb41f68e95b3",
        "size": 7340,
        "url": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Facebook-Ego/3437_2.edges?ref=master",
        "html_url": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Facebook-Ego/3437_2.edges",
        "git_url": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/dfa336a00b692fc39b3d553f577bfb41f68e95b3",
        "download_url": "https://raw.githubusercontent.com/1250326/exercise_complex_network/master/Datasets/Group9/Facebook-Ego/3437_2.edges",
        "type": "file",
        "_links": {
          "self": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Facebook-Ego/3437_2.edges?ref=master",
          "git": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/dfa336a00b692fc39b3d553f577bfb41f68e95b3",
          "html": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Facebook-Ego/3437_2.edges"
        }
      },
      {
        "name": "3437_2.egofeat",
        "path": "Datasets/Group9/Facebook-Ego/3437_2.egofeat",
        "sha": "43bbd9ed4f409858371e87b580544ab1023f85a2",
        "size": 524,
        "url": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Facebook-Ego/3437_2.egofeat?ref=master",
        "html_url": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Facebook-Ego/3437_2.egofeat",
        "git_url": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/43bbd9ed4f409858371e87b580544ab1023f85a2",
        "download_url": "https://raw.githubusercontent.com/1250326/exercise_complex_network/master/Datasets/Group9/Facebook-Ego/3437_2.egofeat",
        "type": "file",
        "_links": {
          "self": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Facebook-Ego/3437_2.egofeat?ref=master",
          "git": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/43bbd9ed4f409858371e87b580544ab1023f85a2",
          "html": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Facebook-Ego/3437_2.egofeat"
        }
      },
      {
        "name": "3437_2.feat",
        "path": "Datasets/Group9/Facebook-Ego/3437_2.feat",
        "sha": "e1147aa212c4798ebd5acbeec25490d62bcbe28c",
        "size": 79349,
        "url": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Facebook-Ego/3437_2.feat?ref=master",
        "html_url": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Facebook-Ego/3437_2.feat",
        "git_url": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/e1147aa212c4798ebd5acbeec25490d62bcbe28c",
        "download_url": "https://raw.githubusercontent.com/1250326/exercise_complex_network/master/Datasets/Group9/Facebook-Ego/3437_2.feat",
        "type": "file",
        "_links": {
          "self": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Facebook-Ego/3437_2.feat?ref=master",
          "git": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/e1147aa212c4798ebd5acbeec25490d62bcbe28c",
          "html": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Facebook-Ego/3437_2.feat"
        }
      },
      {
        "name": "3437_2.featnames",
        "path": "Datasets/Group9/Facebook-Ego/3437_2.featnames",
        "sha": "6d9bae67e43897f2fcd7c9581f07d66da3c66456",
        "size": 11230,
        "url": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Facebook-Ego/3437_2.featnames?ref=master",
        "html_url": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Facebook-Ego/3437_2.featnames",
        "git_url": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/6d9bae67e43897f2fcd7c9581f07d66da3c66456",
        "download_url": "https://raw.githubusercontent.com/1250326/exercise_complex_network/master/Datasets/Group9/Facebook-Ego/3437_2.featnames",
        "type": "file",
        "_links": {
          "self": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Facebook-Ego/3437_2.featnames?ref=master",
          "git": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/6d9bae67e43897f2fcd7c9581f07d66da3c66456",
          "html": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Facebook-Ego/3437_2.featnames"
        }
      },
      {
        "name": "Description",
        "path": "Datasets/Group9/Facebook-Ego/Description",
        "sha": "6568ee397f481676b45851c45064ebff5f716503",
        "size": 659,
        "url": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Facebook-Ego/Description?ref=master",
        "html_url": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Facebook-Ego/Description",
        "git_url": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/6568ee397f481676b45851c45064ebff5f716503",
        "download_url": "https://raw.githubusercontent.com/1250326/exercise_complex_network/master/Datasets/Group9/Facebook-Ego/Description",
        "type": "file",
        "_links": {
          "self": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Facebook-Ego/Description?ref=master",
          "git": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/6568ee397f481676b45851c45064ebff5f716503",
          "html": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Facebook-Ego/Description"
        }
      }
    ]
    [
      {
        "name": "6408382.circles",
        "path": "Datasets/Group9/Twitter-Ego/6408382.circles",
        "sha": "dd9b14e0d21a99483b9ad50a3f488a08003f9bd2",
        "size": 260,
        "url": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Twitter-Ego/6408382.circles?ref=master",
        "html_url": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Twitter-Ego/6408382.circles",
        "git_url": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/dd9b14e0d21a99483b9ad50a3f488a08003f9bd2",
        "download_url": "https://raw.githubusercontent.com/1250326/exercise_complex_network/master/Datasets/Group9/Twitter-Ego/6408382.circles",
        "type": "file",
        "_links": {
          "self": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Twitter-Ego/6408382.circles?ref=master",
          "git": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/dd9b14e0d21a99483b9ad50a3f488a08003f9bd2",
          "html": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Twitter-Ego/6408382.circles"
        }
      },
      {
        "name": "6408382.edges",
        "path": "Datasets/Group9/Twitter-Ego/6408382.edges",
        "sha": "19f3a430068ec926438dcd47f6e6b9386a0a6485",
        "size": 60884,
        "url": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Twitter-Ego/6408382.edges?ref=master",
        "html_url": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Twitter-Ego/6408382.edges",
        "git_url": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/19f3a430068ec926438dcd47f6e6b9386a0a6485",
        "download_url": "https://raw.githubusercontent.com/1250326/exercise_complex_network/master/Datasets/Group9/Twitter-Ego/6408382.edges",
        "type": "file",
        "_links": {
          "self": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Twitter-Ego/6408382.edges?ref=master",
          "git": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/19f3a430068ec926438dcd47f6e6b9386a0a6485",
          "html": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Twitter-Ego/6408382.edges"
        }
      },
      {
        "name": "6408382.egofeat",
        "path": "Datasets/Group9/Twitter-Ego/6408382.egofeat",
        "sha": "e0a6a7380484a95d2f9c0eff92d20276cbc2f676",
        "size": 2120,
        "url": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Twitter-Ego/6408382.egofeat?ref=master",
        "html_url": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Twitter-Ego/6408382.egofeat",
        "git_url": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/e0a6a7380484a95d2f9c0eff92d20276cbc2f676",
        "download_url": "https://raw.githubusercontent.com/1250326/exercise_complex_network/master/Datasets/Group9/Twitter-Ego/6408382.egofeat",
        "type": "file",
        "_links": {
          "self": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Twitter-Ego/6408382.egofeat?ref=master",
          "git": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/e0a6a7380484a95d2f9c0eff92d20276cbc2f676",
          "html": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Twitter-Ego/6408382.egofeat"
        }
      },
      {
        "name": "6408382.feat",
        "path": "Datasets/Group9/Twitter-Ego/6408382.feat",
        "sha": "c241a67695190e0d5015c0d10d1bed8aa24890db",
        "size": 327876,
        "url": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Twitter-Ego/6408382.feat?ref=master",
        "html_url": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Twitter-Ego/6408382.feat",
        "git_url": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/c241a67695190e0d5015c0d10d1bed8aa24890db",
        "download_url": "https://raw.githubusercontent.com/1250326/exercise_complex_network/master/Datasets/Group9/Twitter-Ego/6408382.feat",
        "type": "file",
        "_links": {
          "self": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Twitter-Ego/6408382.feat?ref=master",
          "git": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/c241a67695190e0d5015c0d10d1bed8aa24890db",
          "html": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Twitter-Ego/6408382.feat"
        }
      },
      {
        "name": "6408382.featnames",
        "path": "Datasets/Group9/Twitter-Ego/6408382.featnames",
        "sha": "60eda8f33c3e5f21d7b6294bbc5dfbccbe25c50a",
        "size": 16935,
        "url": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Twitter-Ego/6408382.featnames?ref=master",
        "html_url": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Twitter-Ego/6408382.featnames",
        "git_url": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/60eda8f33c3e5f21d7b6294bbc5dfbccbe25c50a",
        "download_url": "https://raw.githubusercontent.com/1250326/exercise_complex_network/master/Datasets/Group9/Twitter-Ego/6408382.featnames",
        "type": "file",
        "_links": {
          "self": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Twitter-Ego/6408382.featnames?ref=master",
          "git": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/60eda8f33c3e5f21d7b6294bbc5dfbccbe25c50a",
          "html": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Twitter-Ego/6408382.featnames"
        }
      },
      {
        "name": "Description",
        "path": "Datasets/Group9/Twitter-Ego/Description",
        "sha": "a13ca69a9a3b3429f60bdc47dc7fedfefdeb360b",
        "size": 732,
        "url": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Twitter-Ego/Description?ref=master",
        "html_url": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Twitter-Ego/Description",
        "git_url": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/a13ca69a9a3b3429f60bdc47dc7fedfefdeb360b",
        "download_url": "https://raw.githubusercontent.com/1250326/exercise_complex_network/master/Datasets/Group9/Twitter-Ego/Description",
        "type": "file",
        "_links": {
          "self": "https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group9/Twitter-Ego/Description?ref=master",
          "git": "https://api.github.com/repos/1250326/exercise_complex_network/git/blobs/a13ca69a9a3b3429f60bdc47dc7fedfefdeb360b",
          "html": "https://github.com/1250326/exercise_complex_network/blob/master/Datasets/Group9/Twitter-Ego/Description"
        }
      }
    ]
:::
:::

::: {.cell .code execution_count="146"}
``` {.python}
def download_files(group_num, folders = None):
    node_names = {}
    root_folder = f"Group{group_num}"
    if not os.path.exists(root_folder):
        os.mkdir(root_folder)
    else:
        print(f"Folder {root_folder} already exists")
        return
    if folders is None:
        folders = ['Facebook-Ego', 'Twitter-Ego']
    for folder in folders:
        os.mkdir(os.path.join(root_folder, folder))
        res = subprocess.run(["curl", "-s", f"https://api.github.com/repos/1250326/exercise_complex_network/contents/Datasets/Group{group_num}/{folder}"], stdout=subprocess.PIPE)
        for file_info in json.loads(res.stdout):
            os.system(f"wget -O {os.path.join(root_folder, folder, (fname:=file_info['name']))} {file_info['download_url']} -q")
            print(f"Downloaded file: {fname}")
            if '.' in fname:
                node_names[folder.split('-')[0]] = fname.split('.')[0]
        print(f"Downloaded folder: {folder}")
    return node_names
```
:::

::: {.cell .code execution_count="147"}
``` {.python}
!rm -rf Group$group_num
node_names = download_files(group_num)
node_names
```

::: {.output .stream .stdout}
    Downloaded file: 3437_2.edges
    Downloaded file: 3437_2.egofeat
    Downloaded file: 3437_2.feat
    Downloaded file: 3437_2.featnames
    Downloaded file: Description
    Downloaded folder: Facebook-Ego
    Downloaded file: 6408382.circles
    Downloaded file: 6408382.edges
    Downloaded file: 6408382.egofeat
    Downloaded file: 6408382.feat
    Downloaded file: 6408382.featnames
    Downloaded file: Description
    Downloaded folder: Twitter-Ego
:::

::: {.output .execute_result execution_count="147"}
    {'Facebook': '3437_2', 'Twitter': '6408382'}
:::
:::

::: {.cell .markdown}
A
=

How many nodes and edges are there in the networks?
:::

::: {.cell .markdown}
Manual calculation
------------------
:::

::: {.cell .markdown}
### Facebook

Since facebook is an undirected graph, we use the `sorted` function to
avoid counting the same edge twice.

for instance, if we have an edge `(1, 2)` and `(2, 1)`, we will count it
as one edge. because after sorting, they will be `(1, 2)`.
:::

::: {.cell .code execution_count="148"}
``` {.python}
facebook_edges = set()
with open(f"Group{group_num}/Facebook-Ego/{node_names['Facebook']}.edges", 'r') as f:
    for i in f:
        a,b = i.strip().split()
        facebook_edges.add(tuple(sorted((int(a), int(b)))))

list(facebook_edges)[:20]
```

::: {.output .execute_result execution_count="148"}
    [(3596, 3627),
     (3643, 3711),
     (3625, 3672),
     (3644, 3685),
     (3684, 3721),
     (3584, 3643),
     (3640, 3642),
     (3593, 3719),
     (3605, 3702),
     (3596, 3721),
     (3680, 3714),
     (3596, 3730),
     (3608, 3713),
     (3608, 3722),
     (3651, 3674),
     (3651, 3683),
     (3620, 3714),
     (3596, 3604),
     (3653, 3720),
     (3617, 3645)]
:::
:::

::: {.cell .code execution_count="149"}
``` {.python}
print(f"Number of edges in Facebook dataset: {len(facebook_edges)}")
```

::: {.output .stream .stdout}
    Number of edges in Facebook dataset: 367
:::
:::

::: {.cell .code execution_count="150"}
``` {.python}
# number of nodes:
fnodes = set()
for edge in facebook_edges:
    fnodes.add(edge[0])
    fnodes.add(edge[1])
print(f"Number of nodes in Facebook dataset: {len(fnodes)}")
```

::: {.output .stream .stdout}
    Number of nodes in Facebook dataset: 132
:::
:::

::: {.cell .markdown}
### Twitter

Twitter is a directed graph, so we don\'t need to sort the edges.
:::

::: {.cell .code execution_count="151"}
``` {.python}
twiiter_edges = set()
with open(f"Group{group_num}/Twitter-Ego/{node_names['Twitter']}.edges", 'r') as f:
    for i in f:
        a,b = i.strip().split()
        twiiter_edges.add(tuple((int(a), int(b))))

list(twiiter_edges)[:20]
```

::: {.output .execute_result execution_count="151"}
    [(37665322, 177161911),
     (21808052, 809864),
     (80245884, 91585368),
     (23595873, 23739721),
     (21808052, 22139698),
     (16890327, 46422814),
     (89186018, 142450248),
     (16434310, 124444856),
     (462993829, 23739721),
     (16913834, 124444856),
     (17621204, 8362812),
     (15290966, 9224902),
     (35718360, 21755787),
     (21603325, 14844734),
     (16593859, 124886495),
     (14955344, 46422814),
     (14856594, 24844163),
     (37665322, 4620451),
     (14856594, 15290966),
     (177161911, 22139698)]
:::
:::

::: {.cell .code execution_count="152"}
``` {.python}
print(f"Number of edges in Twitter dataset: {len(twiiter_edges)}")
```

::: {.output .stream .stdout}
    Number of edges in Twitter dataset: 3379
:::
:::

::: {.cell .code execution_count="153"}
``` {.python}
tnodes = set()
for edge in twiiter_edges:
    tnodes.add(edge[0])
    tnodes.add(edge[1])
print(f"Number of nodes in Twitter dataset: {len(tnodes)}")
```

::: {.output .stream .stdout}
    Number of nodes in Twitter dataset: 151
:::
:::

::: {.cell .markdown}
Using NetworkX
--------------
:::

::: {.cell .markdown}
### Facebook {#facebook}
:::

::: {.cell .code execution_count="154"}
``` {.python}
import networkx as nx
```
:::

::: {.cell .code execution_count="155"}
``` {.python}
facebook_graph = nx.read_edgelist(f"Group{group_num}/Facebook-Ego/{node_names['Facebook']}.edges", nodetype=int)
print("number of edges in facebook graph:", facebook_graph.number_of_edges())
print("number of nodes in facebook graph:", facebook_graph.number_of_nodes())
```

::: {.output .stream .stdout}
    number of edges in facebook graph: 367
    number of nodes in facebook graph: 132
:::
:::

::: {.cell .markdown}
### Twitter {#twitter}
:::

::: {.cell .code execution_count="156"}
``` {.python}
twitter_graph = nx.read_edgelist(f"Group{group_num}/Twitter-Ego/{node_names['Twitter']}.edges", nodetype=int, create_using=nx.DiGraph)
print("number of edges in twitter graph:", twitter_graph.number_of_edges())
print("number of nodes in twitter graph:", twitter_graph.number_of_nodes())
```

::: {.output .stream .stdout}
    number of edges in twitter graph: 3379
    number of nodes in twitter graph: 151
:::
:::

::: {.cell .markdown}
B
=

What are the maximum degree and the average degree of the networks?
:::

::: {.cell .markdown}
Manual calculation {#manual-calculation}
------------------
:::

::: {.cell .markdown}
### Facebook {#facebook}
:::

::: {.cell .code execution_count="157"}
``` {.python}
facebook_degrees = defaultdict(int)
for a,b in facebook_edges:
    facebook_degrees[a] += 1
    facebook_degrees[b] += 1
facebook_degrees
```

::: {.output .execute_result execution_count="157"}
    defaultdict(int,
                {3596: 25,
                 3627: 8,
                 3643: 7,
                 3711: 10,
                 3625: 10,
                 3672: 9,
                 3644: 3,
                 3685: 3,
                 3684: 15,
                 3721: 10,
                 3584: 10,
                 3640: 14,
                 3642: 6,
                 3593: 14,
                 3719: 8,
                 3605: 12,
                 3702: 11,
                 3680: 10,
                 3714: 6,
                 3730: 10,
                 3608: 9,
                 3713: 11,
                 3722: 9,
                 3651: 5,
                 3674: 10,
                 3683: 4,
                 3620: 6,
                 3604: 19,
                 3653: 1,
                 3720: 2,
                 3617: 8,
                 3645: 5,
                 3687: 9,
                 3731: 13,
                 3635: 11,
                 3667: 6,
                 3670: 8,
                 3692: 15,
                 3693: 7,
                 3586: 11,
                 3606: 2,
                 3662: 3,
                 3669: 1,
                 3700: 1,
                 3718: 6,
                 3590: 13,
                 3663: 5,
                 3710: 11,
                 3728: 11,
                 3639: 3,
                 3695: 4,
                 3611: 8,
                 3624: 2,
                 3679: 2,
                 3694: 1,
                 3707: 7,
                 3599: 13,
                 3636: 10,
                 3638: 3,
                 3716: 3,
                 3612: 2,
                 3673: 1,
                 3603: 3,
                 3697: 4,
                 3629: 11,
                 3715: 4,
                 3690: 4,
                 3649: 4,
                 3646: 7,
                 3616: 4,
                 3647: 3,
                 3664: 2,
                 3696: 4,
                 3656: 7,
                 3633: 18,
                 3628: 3,
                 3657: 3,
                 3659: 3,
                 3615: 7,
                 3705: 10,
                 3623: 3,
                 3621: 3,
                 3677: 14,
                 3648: 8,
                 3706: 6,
                 3727: 1,
                 3658: 4,
                 3631: 4,
                 3591: 4,
                 3594: 3,
                 3613: 4,
                 3686: 3,
                 3637: 1,
                 3634: 3,
                 3632: 1,
                 3681: 3,
                 3614: 1,
                 3652: 3,
                 3595: 3,
                 3698: 6,
                 3598: 2,
                 3665: 2,
                 3610: 4,
                 3609: 4,
                 3607: 2,
                 3654: 3,
                 3601: 4,
                 3666: 6,
                 3725: 3,
                 3712: 3,
                 3641: 3,
                 3655: 3,
                 3682: 1,
                 3618: 5,
                 3602: 2,
                 3630: 2,
                 3587: 3,
                 3732: 1,
                 3675: 1,
                 3708: 1,
                 3622: 3,
                 3585: 1,
                 3676: 2,
                 3592: 3,
                 3724: 1,
                 3689: 2,
                 3600: 1,
                 3626: 1,
                 3699: 1,
                 3589: 1,
                 3660: 1,
                 3703: 1})
:::
:::

::: {.cell .code execution_count="158"}
``` {.python}
max_node, max_deg = max(facebook_degrees.items(), key=lambda x: x[1])
print(f"Node {max_node} has the highest degree of {max_deg} in Facebook dataset")
```

::: {.output .stream .stdout}
    Node 3596 has the highest degree of 25 in Facebook dataset
:::
:::

::: {.cell .code execution_count="159"}
``` {.python}
print(f"Mean degree of nodes in Facebook dataset: {sum(facebook_degrees.values())/len(facebook_degrees):.4f}")
```

::: {.output .stream .stdout}
    Mean degree of nodes in Facebook dataset: 5.5606
:::
:::

::: {.cell .markdown}
Also we know to find the the mean degree we have: $$
\bar{k} = \frac{\sum_{i=1}^{n} k_i}{N} = \frac{2E}{N}
$$
:::

::: {.cell .code execution_count="160"}
``` {.python}
print(f"Median degree of nodes in Facebook dataset: {2*len(facebook_edges)/len(fnodes):.4f}")
```

::: {.output .stream .stdout}
    Median degree of nodes in Facebook dataset: 5.5606
:::
:::

::: {.cell .markdown}
### Twitter {#twitter}

since twitter is a directed graph, we need to calculate the in-degree
and out-degree separately.
:::

::: {.cell .code execution_count="161"}
``` {.python}
twiiter_in_degrees = defaultdict(int)
twiiter_out_degrees = defaultdict(int)

for a,b in twiiter_edges:
    twiiter_out_degrees[a] += 1
    twiiter_in_degrees[b] += 1

max_in_node, max_in_deg = max(twiiter_in_degrees.items(), key=lambda x: x[1])
max_out_node, max_out_deg = max(twiiter_out_degrees.items(), key=lambda x: x[1])

print(f"Node {max_in_node} has the highest in-degree of {max_in_deg} in Twitter dataset")
print(f"Node {max_out_node} has the highest out-degree of {max_out_deg} in Twitter dataset")
print(f"Mean in-degree of nodes in Twitter dataset: {sum(twiiter_in_degrees.values())/len(tnodes):.4f}")
print(f"Mean out-degree of nodes in Twitter dataset: {sum(twiiter_out_degrees.values())/len(tnodes):.4f}")
print(f"Mean degree of nodes in Twitter dataset: {(sum(twiiter_in_degrees.values())+sum(twiiter_out_degrees.values()))/len(tnodes):.4f}")
print(f"Median in-degree of nodes in Twitter dataset: {2*len(twiiter_edges)/len(tnodes):.4f}")
```

::: {.output .stream .stdout}
    Node 16434310 has the highest in-degree of 83 in Twitter dataset
    Node 24844163 has the highest out-degree of 72 in Twitter dataset
    Mean in-degree of nodes in Twitter dataset: 22.3775
    Mean out-degree of nodes in Twitter dataset: 22.3775
    Mean degree of nodes in Twitter dataset: 44.7550
    Median in-degree of nodes in Twitter dataset: 44.7550
:::
:::

::: {.cell .markdown}
### Using NetworkX {#using-networkx}
:::

::: {.cell .markdown}
### Facebook {#facebook}
:::

::: {.cell .code execution_count="162"}
``` {.python}
max_node, max_deg = max(dict(facebook_graph.degree()).items(), key=lambda x: x[1])
print(f"Node {max_node} has the highest degree of {max_deg} in Facebook dataset")
print(f"Mean degree of nodes in Facebook dataset: {sum(dict(facebook_graph.degree()).values())/len(dict(facebook_graph.degree())):.4f}")
```

::: {.output .stream .stdout}
    Node 3596 has the highest degree of 25 in Facebook dataset
    Mean degree of nodes in Facebook dataset: 5.5606
:::
:::

::: {.cell .markdown}
### Twitter {#twitter}
:::

::: {.cell .code execution_count="163"}
``` {.python}
max_in_node, max_in_deg = max(dict(twitter_graph.in_degree()).items(), key=lambda x: x[1])
max_out_node, max_out_deg = max(dict(twitter_graph.out_degree).items(), key=lambda x: x[1])

print(f"Node {max_in_node} has the highest in-degree of {max_in_deg} in Twitter dataset")
print(f"Node {max_out_node} has the highest out-degree of {max_out_deg} in Twitter dataset")
print(f"Mean in-degree of nodes in Twitter dataset: {sum(dict(twitter_graph.in_degree()).values())/len(tnodes):.4f}")
print(f"Mean out-degree of nodes in Twitter dataset: {sum(dict(twitter_graph.out_degree()).values())/len(tnodes):.4f}")
print(f"Mean degree of nodes in Twitter dataset: {sum(dict(twitter_graph.degree()).values())/len(tnodes):.4f}")
print(f"Median in-degree of nodes in Twitter dataset: {2*len(twiiter_edges)/len(tnodes):.4f}")
```

::: {.output .stream .stdout}
    Node 16434310 has the highest in-degree of 83 in Twitter dataset
    Node 24844163 has the highest out-degree of 72 in Twitter dataset
    Mean in-degree of nodes in Twitter dataset: 22.3775
    Mean out-degree of nodes in Twitter dataset: 22.3775
    Mean degree of nodes in Twitter dataset: 44.7550
    Median in-degree of nodes in Twitter dataset: 44.7550
:::
:::

::: {.cell .markdown}
We can see all answers are consistent with each other.
:::

::: {.cell .markdown}
C
=

Extract 5 - 8 nodes from the network and state them as a partial
network. What is the adjacency matrix of the partial network? Why do we
need adjacency matrix to describe the structure of the network?
:::

::: {.cell .code execution_count="164"}
``` {.python}
n_nodes = 8
```
:::

::: {.cell .code execution_count="170"}
``` {.python}
random.seed(0)
selected_facebook_nodes = random.sample(list(fnodes), n_nodes)
selected_facebook_nodes
```

::: {.output .execute_result execution_count="170"}
    [3692, 3702, 3595, 3654, 3731, 3722, 3697, 3666]
:::
:::

::: {.cell .code execution_count="174"}
``` {.python}
selected_twitter_nodes = random.sample(list(tnodes), n_nodes)
selected_twitter_nodes
```

::: {.output .execute_result execution_count="174"}
    [462993829,
     7623482,
     93006320,
     41385649,
     21808052,
     8904302,
     246691076,
     415643219]
:::
:::

::: {.cell .markdown}
Manual calculation {#manual-calculation}
------------------
:::

::: {.cell .markdown}
### Facebook {#facebook}
:::

::: {.cell .code execution_count="173"}
``` {.python}
mini_facebook_adj = [[0]*n_nodes for _ in range(n_nodes)]
for i, node1 in enumerate(selected_facebook_nodes):
    for j, node2 in enumerate(selected_facebook_nodes):
        if (node1, node2) in facebook_edges or (node2, node1) in facebook_edges:
            mini_facebook_adj[i][j] = 1

print("Adjacency matrix of selected nodes in Facebook dataset:")
print("\n".join([" ".join(map(str, row)) for row in mini_facebook_adj]))
```

::: {.output .stream .stdout}
    Adjacency matrix of selected nodes in Facebook dataset:
    0 0 0 0 0 0 0 0
    0 0 0 0 1 0 0 0
    0 0 0 0 0 0 0 0
    0 0 0 0 0 0 1 0
    0 1 0 0 0 0 0 0
    0 0 0 0 0 0 0 0
    0 0 0 1 0 0 0 0
    0 0 0 0 0 0 0 0
:::
:::

::: {.cell .markdown}
### Twitter {#twitter}
:::

::: {.cell .code execution_count="175"}
``` {.python}
mini_twitter_adj = [[0]*n_nodes for _ in range(n_nodes)]
for i, node1 in enumerate(selected_twitter_nodes):
    for j, node2 in enumerate(selected_twitter_nodes):
        if (node1, node2) in twiiter_edges:
            mini_twitter_adj[i][j] = 1

print("Adjacency matrix of selected nodes in Twitter dataset:")
print("\n".join([" ".join(map(str, row)) for row in mini_twitter_adj]))
```

::: {.output .stream .stdout}
    Adjacency matrix of selected nodes in Twitter dataset:
    0 0 1 0 0 0 0 0
    0 0 0 0 0 0 0 0
    0 0 0 0 1 1 0 0
    0 0 1 0 0 1 0 0
    0 0 1 0 0 1 1 0
    0 0 1 1 0 0 0 0
    0 0 0 0 1 0 0 0
    0 0 0 0 0 0 0 0
:::
:::

::: {.cell .markdown}
Using NetworkX {#using-networkx}
--------------
:::

::: {.cell .code execution_count="179"}
``` {.python}
mini_facebook_graph = nx.subgraph(facebook_graph, selected_facebook_nodes)
print("Adjacency matrix of selected nodes in Facebook dataset:")
print(nx.adjacency_matrix(mini_facebook_graph).todense())
```

::: {.output .stream .stdout}
    Adjacency matrix of selected nodes in Facebook dataset:
    [[0 0 0 0 1 0 0 0]
     [0 0 0 0 0 0 0 0]
     [0 0 0 0 0 0 0 0]
     [0 0 0 0 0 0 0 0]
     [1 0 0 0 0 0 0 0]
     [0 0 0 0 0 0 0 0]
     [0 0 0 0 0 0 0 1]
     [0 0 0 0 0 0 1 0]]
:::
:::

::: {.cell .code execution_count="181"}
``` {.python}
mini_twitter_graph = nx.subgraph(twitter_graph, selected_twitter_nodes)
print("Adjacency matrix of selected nodes in Twitter dataset:")
print(nx.adjacency_matrix(mini_twitter_graph).todense())
```

::: {.output .stream .stdout}
    Adjacency matrix of selected nodes in Twitter dataset:
    [[0 0 0 0 0 0 1 0]
     [0 0 0 1 0 0 0 0]
     [0 0 0 1 1 0 0 0]
     [0 0 1 0 0 0 1 0]
     [0 0 1 1 0 0 0 0]
     [0 0 0 0 0 0 0 0]
     [1 0 1 1 0 0 0 0]
     [0 0 0 0 0 0 0 0]]
:::
:::

::: {.cell .markdown}
-   Why do we need adjacency matrix to describe the structure of the
    network?

    > The adjacency matrix is a simple way to represent the structure of
    > a graph. It is easy to understand and implement. It is also easy
    > to perform matrix operations on the adjacency matrix to analyze
    > the graph.
:::
