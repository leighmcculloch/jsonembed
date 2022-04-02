# deno-embed

Embed files into deno applications by embedding them into a JSON file and importing natively into the deno app.

https://deno.land/x/embed/main.ts

## Usage

```
deno run --allow-read --allow-write \
    https://deno.land/x/embed/cli.ts \
    -i dir1 -i dir2 \
    -o embed.json
```

### Lightweight usage

```ts
import embed from "./embed.json" assert { type: "json" };
console.log(embed["dir1/file1"].contents);
```

### With interface

```ts
import { Embed } from "https://deno.land/x/embed/mod.ts";
import embedObj from "./embed.json" assert { type: "json" };
const embed = Embed.from(embedObj);

// Read a file into a Uint8Array.
_ = embed.readFile("dir1/file1");

// Read a text file into a string.
_ = embed.readTextFile("dir1/file2");

// Walk a directory structure.
for (const entry of embed.walk("dir1")) {
    // ...
}
```
