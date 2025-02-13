# Model Context Protocol (MCP)
Minimalistic Rust Implementation Of Model Context Protocol(MCP).


[![Crates.io](https://img.shields.io/crates/v/mcp-sdk)](https://crates.io/crates/mcp-sdk)


Main repo from Anthropic: [MCP](https://github.com/modelcontextprotocol)

## Minimalistic approach
Given it is still very early stage of MCP adoption, the goal is to remain agile and easy to understand.
This implementation aims to capture the core idea of MCP while maintaining compatibility with Claude Desktop.
Many optional features are not implemented yet.

Some guidelines:
- use primitive building blocks and avoid framework if possible
- keep it simple and stupid
### Examples
```rust
    let server = Server::builder(StdioTransport)
        .capabilities(ServerCapabilities {
            tools: Some(json!({})),
            ..Default::default()
        })
        .request_handler("tools/list", list_tools)
        .request_handler("tools/call", call_tool)
        .request_handler("resources/list", |_req: ListRequest| {
            Ok(ResourcesListResponse {
                resources: vec![],
                next_cursor: None,
                meta: None,
            })
        })
        .build();
```
- [x] See [examples/file_system/README.md](examples/file_system/README.md) for usage examples and documentation
## Other Sdks

### Official
- [typescript-sdk](https://github.com/modelcontextprotocol/typescript-sdk)
- [python-sdk](https://github.com/modelcontextprotocol/python-sdk)

### Community
- [go-sdk](https://github.com/mark3labs/mcp-go)

For complete feature please refer to the [MCP specification](https://spec.modelcontextprotocol.io/).
## Features
### Basic Protocol
- [x] Basic Message Types
- [ ] Error and Signal Handling
- Transport
    - [x] Stdio
    - [ ] In Memory Channel (not yet supported in formal specification)
    - [ ] SSE
    - [ ] More compact serialization format (not yet supported in formal specification)
- Utilities 
    - [ ] Ping
    - [ ] Cancellation
    - [ ] Progress
### Server
- [x] Tools
- [ ] Prompts
- [ ] Resources
    - [x] Pagination
    - [x] Completion
### Client
For now use claude desktop as client.

### Monitoring
- [ ] Logging
- [ ] Metrics
