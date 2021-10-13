# Requests ThingsDB Module (Go)

Request module written using the [Go language](https://golang.org).
This module can be used to make HTTP(S) requests with ThingsDB.


## Installation

Install the module by running the following command in the `@thingsdb` scope:

```javascript
new_module('requests', 'github.com/thingsdb/module-go-requests');
```

Optionally, you can choose a specific version by adding a `@` followed with the release tag. For example: `@v0.1.0`.

## Configuration

*This module does not require any config.*

## Exposed functions

Name                    | Description
----------------------- | -----------
[get](#get)             | Make a GET request.
[post](#post)           | Make a POST request.
[post_json](#post_json) | Make a JSON POST request.

### get

Syntax: `get(url, options)`

#### Arguments

- `url`: The URL to make the GET request to.
- `options`: Thing with [properties](#properties) to add to the GET request.

#### Example:

```javascript
requests.get("https://reqbin.com/echo").then(|res| {
    res;  // just return the response.
});
```

### post

Syntax: `post(url, body, options)`

#### Arguments

- `url`: The URL to make the POST request to.
- `body`: Body to send with the request (as bytes).
- `options`: Thing with [properties](#properties) to add to the POST request.

> *For an example, see [post_json](#post_json) below.*

### post_json

Syntax: `post_json(url, body, options)`

Like [post](#post), except that the headers will be set to accept and send JSON data.

#### Arguments

- `url`: The URL to make the POST request to.
- `body`: Body to send with the request (as bytes).
- `options`: Thing with [properties](#properties) to add to the POST request.

#### Example:

```javascript
record = {
    Id: 78912,
    Customer: "Jason Sweet",
    Quantity: 1,
    Price: 18.00
};
requests.post_json("https://reqbin.com/echo/post/json", json_dump(record)).then(|res| {
    res = res.load();
    json_load(str(res.body));
});
```

## Properties

Option    | Type  | Description
--------- | ----- | -----------
`method`  | str   | Method to use. For example `GET`, `POST`, `PUT` etc. (default: `GET`)
`url`     | str   | URL to use with the request.
`body`    | bytes | Body to send with the request.
`headers` | list  | Headers to send with the request. Must be a list with `[[Key, Value],..]` tuples.
`params`  | list  | URL Params to send with the request. Must be a list with `[[Key, Value],..]` tuples.
