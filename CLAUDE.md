# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Dify plugin for Elasticsearch integration, written in Python 3.12. The plugin provides tools to query and create documents in Elasticsearch clusters with support for various authentication methods.

## Development Commands

### Running the Plugin
```bash
python main.py
```

### Installing Dependencies
```bash
pip install -r requirements.txt
```

## Project Architecture

### Core Structure
- `main.py` - Plugin entry point using dify_plugin framework with 120s timeout
- `manifest.yaml` - Plugin metadata and configuration (version 0.0.6)
- `provider/` - Provider configuration and authentication logic
- `tools/` - Individual tool implementations (query and create operations)

### Key Components

#### Provider Layer (`provider/`)
- `es.py` - ElasticsearchProvider class handles credential validation
- `es.yaml` - Provider configuration with multi-language support and authentication options

#### Tool Layer (`tools/`)
- `base.py` - ElasticsearchBaseTool base class for Elasticsearch client creation
- `query.py` - Search tool implementation (referenced in query.yaml)  
- `create.py` - Document creation tool (referenced in create.yaml)
- `*.yaml` files define tool parameters and metadata

#### Authentication Support
The base tool supports three authentication methods:
- No authentication (`no_auth`)
- Basic authentication (`basic`) - username/password
- API key authentication (`api_key`)

Optional SSL certificate verification via `verify_certs` parameter.

## Plugin Configuration

### Elasticsearch Version Support
- Supports Elasticsearch 7.17+ 
- Uses elasticsearch client version 8.17.2
- Plugin built on dify_plugin framework (0.2.0+)

### Memory Requirements
- Configured for 256MB memory allocation per manifest.yaml

### Tool Capabilities
- **Query Tool**: DSL-based search with source field filtering, sorting, and pagination
- **Create Tool**: Document creation with specified document ID
- Multi-language support (English, Chinese, Portuguese, Japanese)

## Development Notes

### Plugin Framework
This plugin uses the Dify plugin framework. All tools inherit from the base authentication pattern in `tools/base.py` to maintain consistent Elasticsearch connectivity.

### YAML Configuration Pattern
Each tool has a corresponding `.yaml` file defining its parameters, labels, and descriptions in multiple languages. The `extra.python.source` field links to the Python implementation.