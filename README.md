# exports-not-loaded

Repro steps:

1. node test.js - fails with module not found error
2. Edit internal/foo/package.json to use "main" instead of "main_ignore"
3. node test.js now prints "Hello world"

The regex at https://github.com/nodejs/node/blob/73c0564fcaea8dba8b480fefec4e9f1099a9cb91/lib/internal/modules/cjs/loader.js#L538 doesn't deal with subpaths. It's directly clear why the request needs to be parsed and can't use use path.resolve/path.join
