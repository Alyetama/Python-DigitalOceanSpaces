# Python-DigitalOceanSpaces

## Installation

-  Requires: `Python >=3.6`

```
pip install dospaces
```

## Setup

- Rename and edit the content of `.env` with your Spaces access keys

```
mv .env.example .env
nano .env
```

## Example Usage

```py
from dospaces import Spaces

spaces = Spaces('region-name', 'space-name')
```

```py
spaces.list_objects(pprint=True, simple=True)
# [
#     {
#         "name": "foo",
#         "last_modified": "2022-03-20 16:48:49.168000+00:00",
#         "size": 9431401
#     },
#     {
#         "name": "bar",
#         "last_modified": "2022-03-20 15:10:07.353000+00:00",
#         "size": 123115397
#     }
# ]
```

```py
spaces.download_file('foo.txt')
# '/path/to/foo.txt'

spaces.download_file('foo.txt', output_path='/some/other/path/foo.txt')  # or to a specific path/name
# '/some/other/path/foo.txt'
```

```py
spaces.upload_file('foo.txt')
# 'https://example.region.digitaloceanspaces.com/foo.txt'

spaces.upload_many(['foo.txt', 'bar.txt', 'foobar.jpg'])  # from a list of files
# [
#    'https://example.region.digitaloceanspaces.com/foo.txt',
#    'https://example.region.digitaloceanspaces.com/bar.txt',
#    'https://example.region.digitaloceanspaces.com/foobar.jpg'
# ]

spaces.upload_many('/path/to/dir', public=False, duplicates_policy='rename')  # or from a directory
# [
#    'https://example.region.digitaloceanspaces.com/foo-ab6c3d82.txt',
#    'https://example.region.digitaloceanspaces.com/bar-95d81b4c.txt',
#    'https://example.region.digitaloceanspaces.com/foobar-7bcui3ko.jpg'
# ]
```

```py
spaces.delete_object('foo.txt')
# {
#     "ResponseMetadata":
#     {
#         "RequestId": "...",
#         "HostId": "",
#         "HTTPStatusCode": 204,
#         "HTTPHeaders":
#         {
#             "x-amz-request-id": "...",
#             "date": "Sun, 20 Mar 2022 19:48:55 GMT",
#             "strict-transport-security": "max-age=...; includeSubDomains; preload"
#         },
#         "RetryAttempts": 0
#     }
# }
```
