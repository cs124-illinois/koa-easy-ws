# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

- **Test & Lint**: `npm test` - Runs StandardJS linting and Mocha tests
- **Individual Commands**: 
  - `npx standard` - Run StandardJS linter only
  - `npx mocha` - Run Mocha tests only

## Project Architecture

This is a minimal Koa middleware library for WebSocket handling with the following structure:

- **Main Entry**: `index.js` - Single middleware factory function (`createWebsocketMiddleware`)
- **TypeScript Types**: `index.d.ts` - Type definitions for the middleware
- **Tests**: `test/` directory with multiple test scenarios using Mocha/Chai

### Core Functionality

The middleware adds a `ctx.ws()` (or custom property name) function to Koa context when a WebSocket upgrade request is detected. Key implementation details:

- Uses `ws` library as peer dependency (v8+)
- Creates WebSocket.Server with `noServer: true` option
- Handles upgrade requests via `wss.handleUpgrade()`
- Sets `ctx.respond = false` to prevent normal HTTP response
- Supports Node 9 workaround for upgrade request handling
- Exposes WebSocket server instance via `.server` property

### Key Dependencies

- **Runtime**: `debug` for logging
- **Peer Dependencies**: `koa` (>=2), `ws` (>=8) 
- **Dev Dependencies**: `standard` for linting, `mocha`/`chai` for testing

### Testing Approach

Tests use real HTTP servers and WebSocket connections to verify middleware behavior. Pre-commit hook runs tests automatically.

### Version Scheme

Uses date-based versioning: YYYY.M.patch (e.g., 2025.7.0)