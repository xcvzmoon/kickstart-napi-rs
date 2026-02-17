# Kickstart NAPI-RS

My opinionated kickstarter for NAPI-RS - create high-performance Node.js native addons with Rust.

## Quick Start

```sh
bunx gitget xcvzmoon/kickstart-napi-rs my-app --install
```

## Prerequisites

- [Node.js](https://nodejs.org/) >= 12.22.0
- [Rust](https://rustup.rs/) toolchain
- [Bun](https://bun.sh/) package manager

## Development

### Build Commands

```sh
# Build native addon (release)
bun run build

# Build native addon (debug - faster compilation)
bun run build:debug
```

### Code Quality

```sh
# Format all code (TypeScript, Rust, TOML)
bun run format

# Lint TypeScript/JavaScript
bun run lint
```

### Testing

```sh
# Run all tests
bun run test

# Run a single test file
bunx vitest run tests/specific.test.ts

# Run benchmarks
bun run bench
```

## Project Structure

```
├── src/lib.rs              # Rust source code with #[napi] exports
├── index.js                # Generated JavaScript bindings (DO NOT EDIT)
├── index.d.ts              # Generated TypeScript definitions (DO NOT EDIT)
├── tests/                  # Vitest test files (*.test.ts)
├── benchmark/              # Vitest benchmark files (*.bench.ts)
├── Cargo.toml              # Rust package configuration
├── package.json            # Node.js package configuration
└── vitest.config.ts        # Vitest configuration
```

## Adding Functions

1. Add your Rust function in `src/lib.rs` with the `#[napi]` attribute:

```rust
#[napi]
pub fn my_function(input: u32) -> u32 {
    input * 2
}
```

2. Build the project: `bun run build`
3. Use in JavaScript/TypeScript:

```typescript
import { myFunction } from './index.js';
const result = myFunction(21); // 42
```

## CI/CD

This project uses GitHub Actions for continuous integration. The workflow is defined in `.github/workflows/CI.yml` and includes:

- **Lint** - Runs oxlint, cargo fmt, and clippy
- **Build** - Cross-compiles native bindings for all supported platforms
- **Test** - Runs tests on macOS, Windows, and Linux (Node 20 & 22)
- **Publish** - Automatically publishes to npm on version tags

The CI uses Bun instead of pnpm/npm for faster builds.

## Supported Platforms

- x86_64-pc-windows-msvc
- x86_64-apple-darwin
- x86_64-unknown-linux-gnu
- aarch64-apple-darwin

## License

MIT

## Author

[Mon Albert Gamil](https://github.com/xcvzmoon/)
