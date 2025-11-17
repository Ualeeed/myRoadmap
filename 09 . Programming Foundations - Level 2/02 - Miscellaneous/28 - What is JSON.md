---
DATE: 2025-10-25T23:22:00
DONE: true
Name: Foundation 2
---


<span style="color:rgb(255, 255, 0)">JSON</span> (<span style="color:rgb(255, 255, 0)">J</span>avaScript <span style="color:rgb(255, 255, 0)">O</span>bject <span style="color:rgb(255, 255, 0)">N</span>otation) is a lightweight, text-based data format used for storing and exchanging information between systems. It was originally specified by Douglas Crockford in the early 2000s.

**Key Characteristics:**
- Language-independent data interchange format
- Easy for humans to read and write
- Easy for machines to parse and generate
- Often used when data is sent from a server to a web page

---

## **Why JSON Matters

<span style="color:rgb(255, 255, 0)">JSON</span> is commonly used for transmitting data in web applications, such as sending data from the server to the client so it can be displayed on a web page, or vice versa. It has become the standard format for APIs and data exchange on the web.

**Advantages:**
- *Simple and straightforward structure
- *Lighter weight than XML
- *Uses conventions familiar to programmers of C-family languages (C, C++, C#, Java, JavaScript, Perl, Python)
- *Self-describing and human-readable

---

## JSON Syntax Rules

<span style="color:rgb(255, 255, 0)">JSON</span> data is written as name/value pairs, with the name (key) in double quotes, followed by a colon, then the value:

### Basic Rules:
1. **Data is in name/value pairs**: `"key": "value"`
2. Data is separated by commas
3. Curly braces hold objects
4. Square brackets hold arrays
5. Keys must be enclosed in double quotes
6. Strings must be enclosed in double quotes, not single quotes

**Important:** *No comments are allowed in JSON data

---

## Data Types in JSON

<span style="color:rgb(255, 255, 0)">JSON</span> can represent four primitive types and two structured types:

### Primitive Types:
- **String**: `"Hello World"`
- **Number**: `42` or `3.14`
- **Boolean**: `true` or `false`
- **Null**: `null`

### Structured Types:
- **Object**: Collection of key-value pairs in `{}`
- **Array**: Ordered list of values in `[]`

### What JSON Cannot Contain:
<span style="color:rgb(255, 255, 0)">JSON</span> cannot contain `undefined`, ` NaN ` , `Infinity`, `functions`, or `object types` like `Date`, `Set`, and `Map`

---

## JSON Objects

<span style="color:rgb(255, 255, 0)">JSON</span> objects are written inside curly braces and can contain multiple name/value pairs:

```json
 {
  "firstName": "John",
  "lastName": "Doe",
  "age": 30,
  "isStudent": false
 }
```

**Example with Nested Object:**
```json
{
  "name": "Aleix Melon",
  "id": "E00245",
  "age": 23,
  "married": false,
  "address": {
    "street": "32, Laham St.",
    "city": "Innsbruck",
    "country": "Austria"
  }
}
```

---

## JSON Arrays

<span style="color:rgb(255, 255, 0)">JSON</span> arrays are written inside square brackets:

```json
{
  "employees": [
    {
      "firstName": "John",
      "lastName": "Doe"
    },
    {
      "firstName": "Anna",
      "lastName": "Smith"
    },
    {
      "firstName": "Peter",
      "lastName": "Jones"
    }
  ]
}
```

Arrays can be made up of multiple data types, and an array can be stored inside another JSON array (multidimensional array).

---

## Working with JSON in JavaScript

### Converting JSON to JavaScript Object

Use `JSON.parse()` to convert a JSON string into a JavaScript object:

```javascript
// JSON string
const jsonString = '{"name": "John", "age": 30}';

// Parse to JavaScript object
const obj = JSON.parse(jsonString);

// Access the data
console.log(obj.name); // Output: John
console.log(obj.age);  // Output: 30
```

### Converting JavaScript Object to JSON

Use `JSON.stringify()` to convert a JavaScript object to a JSON string:

```javascript
// JavaScript object
const person = {
  name: "John",
  age: 30,
  city: "New York"
};

// Convert to JSON string
const jsonString = JSON.stringify(person);

console.log(jsonString);
// Output: {"name":"John","age":30,"city":"New York"}
```

---

## JSON vs JavaScript Objects

While they look similar, there are important differences:

| **JSON** | **JavaScript Object** |
|----------|----------------------|
| Keys must be in double quotes | Keys can be unquoted |
| Only supports strings, numbers, booleans, arrays, objects, and null | Supports functions, Date objects, undefined, etc. |
| Used for data transfer between systems | Used for data manipulation within JavaScript |
| Always text-based | Can contain methods and functions |

---

## Common Use Cases

1. **API Communication**: Exchanging data between client and server
2. **Configuration Files**: Storing application settings
3. **Data Storage**: Native support in relational and NoSQL databases
4. **Data Transfer**: Sending information across networks
5. **Web Services**: Standard format for public APIs

### Example API Response:
```json
{
  "status": "success",
  "data": {
    "user": {
      "id": 123,
      "username": "johndoe",
      "email": "john@example.com"
    }
  }
}
```

---

## File Format

<span style="color:rgb(255, 255, 0)">JSON</span> filenames use the extension `.json`. You can save JSON data in files for storage and later retrieval.

**Example:** `data.json`, `config.json`, `users.json`

---

## Important Notes

⚠️ **Security Consideration**: <span style="color:rgb(255, 255, 0)">JSON</span> scripts can automatically execute in webpages, which can be exploited for JavaScript injection attacks like cross-site scripting. Always validate and sanitize JSON data from untrusted sources.

✅ **Best Practice**: Names within an object should be unique for interoperability

🌐 **Encoding**: JSON exchange must be encoded in UTF-8 for maximum portability

---

## Summary

<span style="color:rgb(255, 255, 0)">JSON</span> is the standard format for data exchange on the modern web. Its simplicity, readability, and universal support across programming languages make it the go-to choice for APIs, configuration files, and data storage. Understanding <span style="color:rgb(255, 255, 0)">JSON</span> is essential for any developer working with web applications, APIs, or data interchange between systems.

**Remember**: *JSON is just a text format - it's not code that executes, but data that can be easily parsed and generated by any programming language!
