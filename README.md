# almide/yaml

YAML parser and serializer for [Almide](https://github.com/almide/almide). Pure Almide implementation with Codec integration.

## Install

```bash
almide add almide/yaml
```

## Usage

```almide
import yaml

// Parse YAML text
let config = yaml.parse("""
  server:
    host: localhost
    port: 8080
  debug: true
  """)!

// Stringify Value to YAML
let text = yaml.stringify(config)
```

### With Codec

```almide
import yaml

type ServerConfig: Codec = { host: String, port: Int, debug: Bool }

// Encode a typed record to YAML string
let text = yaml.encode(ServerConfig { host: "0.0.0.0", port: 3000, debug: true })

// Decode YAML string to a typed record
let config = ServerConfig.decode(yaml.parse(text)!)!
```

## API

| Function | Signature | Description |
|---|---|---|
| `yaml.parse` | `(String) -> Result[Value, String]` | Parse YAML text into a Value |
| `yaml.stringify` | `(Value) -> String` | Serialize a Value to YAML text |
| `yaml.encode` | `(T: Codec) -> String` | Encode a Codec type to YAML |
| `yaml.decode[T]` | `(String) -> Result[T, String]` | Decode YAML to a Codec type |

## Supported Features

- Mappings (indentation-based nesting)
- Sequences (`- item`)
- Scalars: plain, single-quoted, double-quoted
- Numbers, booleans (`true`/`false`), null (`null`, `~`)
- Comments (`#`)
- Flow sequences (`[a, b, c]`)
- Flow mappings (`{x: 1, y: 2}`)
- Nested structures (arbitrary depth)
- Sequence of mappings (`- name: A`)

## License

MIT
