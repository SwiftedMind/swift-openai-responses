# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Swift package that provides an unofficial SDK for the OpenAI Responses API. The package is designed to work across all Apple platforms (iOS 17+, macOS 14+, tvOS 17+, watchOS 10+, visionOS 1+, macCatalyst 17+).

## Architecture

### Core Components

- **ResponsesAPI** (`src/ResponsesAPI.swift`): Low-level client for direct API communication
- **Conversation** (`src/Conversation.swift`): High-level wrapper for managing conversation state and streaming responses
- **Models** (`src/Models/`): Data structures for requests, responses, and events
- **Extensions** (`src/Extensions/`): Utility extensions for common operations

### Key Design Patterns

- Uses Swift 6 concurrency with `async/await` and `AsyncThrowingStream` for streaming responses
- `@Observable` wrapper for SwiftUI integration in `Conversation` class
- Server-Sent Events (SSE) parsing for real-time response streaming
- Comprehensive error handling with custom error types

## Development Commands

### Building the Package
```bash
swift build
```

### Testing
```bash
swift test
```

### Package Resolution
```bash
swift package resolve
```

## Dependencies

- **MetaCodable**: Advanced JSON encoding/decoding (https://github.com/SwiftyLab/MetaCodable.git)
- **HelperCoders**: Additional encoding utilities from MetaCodable package

## Key Files and Their Purposes

- `Conversation.swift`: Main entry point for high-level conversation management
- `ResponsesAPI.swift`: Core API client with HTTP request handling
- `Models/Request.swift` & `Models/Response.swift`: Primary API data structures
- `Models/Event.swift`: Server-sent event definitions for streaming
- `Support/MultiPartData.swift`: File upload functionality

## Working with the Codebase

### API Usage Patterns
The package follows a two-tier approach:
1. **High-level**: Use `Conversation` class for SwiftUI integration and state management
2. **Low-level**: Use `ResponsesAPI` directly for custom implementations

### Streaming Architecture
All real-time communication uses `AsyncThrowingStream` with comprehensive event handling in `Conversation.handleEvent(_:)` (src/Conversation.swift:228-495).

### File Uploads
File uploads are handled through the `upload(file:purpose:)` method using multipart form data encoding.