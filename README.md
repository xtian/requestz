# Requestz

An HTTP client inspired by [httpx](https://github.com/encode/httpx) and [ureq](https://github.com/algesten/ureq).

[![Build Status](https://api.travis-ci.org/ducdetronquito/requestz.svg?branch=master)](https://travis-ci.org/ducdetronquito/requestz) [![License](https://img.shields.io/badge/License-BSD%200--Clause-ff69b4.svg)](https://github.com/ducdetronquito/requestz#license) [![Requirements](https://img.shields.io/badge/zig-0.7.0-orange)](https://ziglang.org/)

## Usage

Send a GET request
```zig
const client = @import("requestz.zig").Client;

var client = try Client.init(std.testing.allocator);
defer client.deinit();

var response = try client.get("http://httpbin.org/get", .{});
defer response.deinit();
```

Send a request with headers
```zig
const Headers = @import("http").Headers;

var headers = Headers.init(std.testing.allocator);
defer headers.deinit();
try headers.append("Gotta-go", "Fast!");

var response = try client.get("http://httpbin.org/get", .{ .headers = headers.items() });
defer response.deinit();
```

Send a request with compile-time headers
```zig
var headers = .{
    .{"Gotta-go", "Fast!"}
};

var response = try client.get("http://httpbin.org/get", .{ .headers = headers });
defer response.deinit();
```

Send binary data along with a POST request
```zig
var response = try client.post("http://httpbin.org/post", .{ .content = "Gotta go fast!" });
defer response.deinit();

var tree = try response.json();
defer tree.deinit();
```

Other standard HTTP method shortcuts:
- `client.connect`
- `client.delete`
- `client.head`
- `client.options`
- `client.patch`
- `client.put`
- `client.trace`

## Requirements

To work with *requestz* you will need the latest stable version of Zig, which is currently Zig 0.7.0.


## Dependencies

- [h11](https://github.com/ducdetronquito/h11)
- [http](https://github.com/ducdetronquito/http)
- [zig-network](https://github.com/MasterQ32/zig-network)

## License

*requestz* is released under the [BSD Zero clause license](https://choosealicense.com/licenses/0bsd/). 🎉🍻
