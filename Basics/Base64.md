### Base64 encoding and decoding

Base64 encoding and decoding is a method of representing binary data using a set of 64 characters. Let me break it down for you:

### Base64 Encoding:

- It converts binary data (like images, files, or raw data) into a text format using a specific character set
- The character set includes uppercase (A-Z) and lowercase (a-z) letters, numbers (0-9), and two additional symbols (usually + and /)
- Each Base64 character represents 6 bits of data (2^6 = 64 possible values)
- It's commonly used when you need to transmit binary data over text-based protocols like email or include binary data in JSON or XML

### How Encoding Works:

- The binary data is divided into 6-bit chunks
- Each 6-bit chunk is converted to a corresponding Base64 character
- If the final chunk doesn't fill 6 bits completely, padding characters (=) are added

### Common Use Cases:

- Sending images in emails
- Embedding images directly in HTML or CSS
- Storing binary data in text-based formats
- Transmitting data in web APIs

Example:
Let's take a simple example of encoding the word "Hello":
```
const encode = Buffer.from("Hello").toString('base64');
console.log(encode)
const decode = Buffer.from(encode,'base64').toString()
console.log(decode)
```

### Typescript code to convert String to binary
```
const arr = Array.from("Hello").map(x=>x.charCodeAt(0).toString(2).padStart(8,'0')).join(' ');
console.log(arr)
```