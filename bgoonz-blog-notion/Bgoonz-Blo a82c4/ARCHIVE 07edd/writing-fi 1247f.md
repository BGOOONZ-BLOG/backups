# writing-files

The easiest way to write to files in Node.js is to use the `fs.writeFile()` API.

Example:

```
const fs = require('fs');const content = 'Some content!';fs.writeFile('/Users/joe/test.txt', content, (err) => {    if (err) {        console.error(err);        return;    }    //file written successfully});
```

Alternatively, you can use the synchronous version `fs.writeFileSync()`:

```
const fs = require('fs');const content = 'Some content!';try {    const data = fs.writeFileSync('/Users/joe/test.txt', content);    //file written successfully} catch (err) {    console.error(err);}
```

By default, this API will **replace the contents of the file** if it does already exist.

You can modify the default by specifying a flag:

```
fs.writeFile('/Users/joe/test.txt', content, { flag: 'a+' }, (err) => {});
```

The flags you'll likely use are

- `r+` open the file for reading and writing
- `w+` open the file for reading and writing, positioning the stream at the beginning of the file. The file is created if not existing
- `a` open the file for writing, positioning the stream at the end of the file. The file is created if not existing
- `a+` open the file for reading and writing, positioning the stream at the end of the file. The file is created if not existing

(you can find more flags at [https://nodejs.org/api/fs.html#fs_file_system_flags](https://nodejs.org/api/fs.html#fs_file_system_flags))

## Append to a file

A handy method to append content to the end of a file is `fs.appendFile()` (and its `fs.appendFileSync()` counterpart):

```
const content = 'Some content!';fs.appendFile('file.log', content, (err) => {    if (err) {        console.error(err);        return;    }    //done!});
```

## Using streams

All those methods write the full content to the file before returning the control back to your program (in the async version, this means executing the callback)

In this case, a better option is to write the file content using streams.

72

Here's a sketch. Error handling is left as an exercise for the reader.

```
let fs = require('fs'),    path = require('path');function dirTree(filename) {    let stats = fs.lstatSync(filename),        info = {            path: filename,            name: path.basename(filename)        };    if (stats.isDirectory()) {        info.type = 'folder';        info.children = fs.readdirSync(filename).map(function (child) {            return dirTree(filename + '/' + child);        });    } else {        // Assuming it's a file. In real life it could be a symlink or        // something else!        info.type = 'file';    }    return info;}if (module.parent == undefined) {    // node dirTree.js ~/foo/bar    let util = require('util');    console.log(util.inspect(dirTree(process.argv[2]), false, null));}
```
