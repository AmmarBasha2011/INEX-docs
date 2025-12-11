---
hidden: true
---

# inex-library · PyPI

## inex-library 1.0.1

pip install inex-library==1.0.1

[Latest version](https://pypi.org/project/inex-library/)

Released: Jan 21, 2025

A comprehensive Python library for AI integration, web development with FastAPI/Flask, advanced encryption, secure database management, file operations, library development, text styling, system management, translation services, video creation, web automation, and cryptocurrency token analysis. Features include JWT handling, password management, rate limiting, input sanitization, and more.

***

### Verified details

_These details have been_ [_verified by PyPI_](https://docs.pypi.org/project_metadata/#verified-details)

Maintainers: [YWProducts](https://pypi.org/user/YWProducts/)\
Author: [INEX Team](mailto:pbstzidr@ywp.freewebhostmost.com)

Unverified details, project links, classifiers, tags, requirements, extras, and license are available on the PyPI project page and repository links included in the original source.

***

## INEX Library

A comprehensive Python library for AI integration, web development with FastAPI/Flask, advanced encryption, secure database management, file operations, library development, text styling, system management, translation services, video creation, web automation, and cryptocurrency token analysis. Features include JWT handling, password management, rate limiting, input sanitization, and more.

### Features

#### Web Server

Quickly create and run web servers with Flask-style helpers.

Example — minimal usage:

{% code title="app.py" %}
```python
from INEX import Server

# Initialize server
server = Server()

# Add routes
server.route_flask("/", "Welcome to INEX!")
server.route_flask("/hello", "Hello, World!")
server.route_flask("/api/v1", "API Version 1.0")

# Run server
server.run(
    debug=True,
    host="0.0.0.0",
    port="8000"
)
```
{% endcode %}

Server features include Flask integration, server configuration (debug/host/port), production support (Gunicorn/Uvicorn), middleware (CORS, compression, caching, rate limiting), security helpers (HTTPS, headers, CSRF/XSS protections), and monitoring utilities (Prometheus, logging, error tracking).

Advanced usage example with REST endpoints, static file serving, and error handlers:

{% code title="advanced_server.py" %}
```python
from INEX import Server
from flask import request, jsonify, send_from_directory

server = Server()

# REST API Endpoints
def create_api():
    server.route_flask("/api/users", lambda: jsonify({"users": ["user1", "user2"]}))
    server.route_flask("/api/data/<id>", lambda id: jsonify({"id": id, "data": "Sample data"}))
    server.route_flask(
        "/api/protected",
        lambda: (jsonify({"error": "Unauthorized"}) if not request.headers.get("X-API-Key") else jsonify({"status": "success"}))
    )

# Static file serving
def setup_static():
    server.route_flask("/static/<path:filename>", lambda filename: send_from_directory("static", filename))

# Error handlers
def setup_errors():
    @server.apps.errorhandler(404)
    def not_found(e):
        return jsonify({"error": "Not found"}), 404

    @server.apps.errorhandler(500)
    def server_error(e):
        return jsonify({"error": "Server error"}), 500

create_api()
setup_static()
setup_errors()

server.run(debug=False, host="0.0.0.0", port="80")
```
{% endcode %}

Production deployment examples (Gunicorn, Uvicorn, Supervisor) are supported.

***

#### Advanced Encryption Suite

{% stepper %}
{% step %}
### AES Encryption

* Industry-standard AES encryption
* CBC mode operation
* File-based encryption and decryption
* Secure key handling

Usage:

{% code title="aes_example.py" %}
```python
from INEX import EnDeCrypt

# Encrypt a file using AES
EnDeCrypt.aes.encrypt(
    file_path="secret_document.pdf",
    password="your-secure-password"
)

# Decrypt an AES-encrypted file
EnDeCrypt.aes.decrypt(
    file_path="secret_document.pdf.ywpdne",
    password="your-secure-password"
)
```
{% endcode %}
{% endstep %}

{% step %}
### Blowfish Encryption

* Blowfish algorithm implementation
* CBC mode for enhanced security
* File encryption/decryption
* Comprehensive error handling

Usage:

{% code title="blowfish_example.py" %}
```python
from INEX import EnDeCrypt

# Encrypt using Blowfish
EnDeCrypt.BlowFish.encrypt(
    file_path="confidential.doc",
    password="your-secure-password"
)

# Decrypt Blowfish-encrypted file
EnDeCrypt.BlowFish.decrypt(
    file_path="confidential.doc.ywpdne",
    password="your-secure-password"
)
```
{% endcode %}
{% endstep %}

{% step %}
### Encoding Operations

* Base64 encoding/decoding
* Hexadecimal encoding/decoding
* File-based operations
* Safe error handling

Usage:

{% code title="encoding_example.py" %}
```python
from INEX import EnDeCrypt

# Base64 encoding
EnDeCrypt.Base64.encrypt("data.bin")
EnDeCrypt.Base64.decrypt("data.bin.ywpdne")

# Hexadecimal encoding
EnDeCrypt.Hex.encrypt("binary_file.dat")
EnDeCrypt.Hex.decrypt("binary_file.dat.ywpdne")
```
{% endcode %}
{% endstep %}
{% endstepper %}

Encryption features include multiple algorithms (AES, Blowfish, Base64, Hex), CBC mode, padding and IV management, file operations, and comprehensive exception handling.

***

#### Security Suite

Quick start and features:

{% code title="security_quickstart.py" %}
```python
from INEX import Security
from datetime import timedelta

security = Security(secret_key="your-secret-key")

# Password Management
hashed_password = security.hash_password("user_password")
is_valid = security.verify_password("user_password", hashed_password)

# JWT Token Handling
token = security.create_jwt_token(data={"user_id": 123}, expires_delta=timedelta(hours=1))
payload = security.verify_jwt_token(token)

# Data Encryption
encrypted = security.encrypt_data("sensitive data")
decrypted = security.decrypt_data(encrypted)

# API Key Management
api_key, hashed_key = security.create_api_key(prefix="sk")
is_valid = security.verify_api_key(api_key, hashed_key)

# Input Sanitization
safe_input = security.sanitize_input("<script>alert('xss')</script>", allow_html=False)

# Rate Limiting
is_allowed, remaining = security.rate_limit_check(key="user_ip", max_requests=100, time_window=3600)
```
{% endcode %}

Security features: bcrypt hashing, password validation, JWT creation/verification, symmetric/asymmetric encryption, key derivation, API key generation/verification, input protection (XSS, sanitization), rate limiting, IP/CIDR checks, file security, and 2FA (TOTP, backup codes, QR generation).

Advanced usage examples for user registration, secure file handling, and API endpoint security are provided in the library documentation.

***

#### Text Styling

Terminal text animations and styling helpers.

Examples:

{% code title="printstyle_examples.py" %}
```python
from INEX import PrintStyle

# Print text character by character
PrintStyle.print_one(text="Welcome to INEX!", second=0.05)

# Print text with calculated timing
PrintStyle.print_all(text="Loading your application...", total_time=3.0)
```
{% endcode %}

Features include character-by-character printing, timed display controls, and robust error handling for empty text or timing issues.

***

#### File Management

File creation, opening, deletion, and batch operations.

Examples:

{% code title="files_quickstart.py" %}
```python
from INEX import Files

# Create a new file
Files.create_file("example.txt")  # Will prompt for content

# Open a file
Files.open_file("example.txt")

# Delete a file
Files.delete_file("example.txt")

# Delete multiple files by type
Files.delete_all_files(directory="./downloads", type={"1": ".txt", "2": ".tmp"})
```
{% endcode %}

Supports interactive creation, path validation, batch deletion, and cross-platform compatibility.

***

#### FastAPI Server

Create high-performance API servers.

Quick start:

{% code title="fastapi_quickstart.py" %}
```python
from INEX import FastAPIServer

server = FastAPIServer()

def hello_world():
    return {"message": "Hello, World!"}
server.add_endpoint("/", hello_world)

server.add_cors()
server.run(host="0.0.0.0", port=8000)
```
{% endcode %}

Features include dynamic endpoints, full HTTP method support, CORS configuration, Uvicorn integration, and production-ready settings.

Advanced example (POST with parameters):

{% code title="fastapi_advanced.py" %}
```python
from INEX import FastAPIServer
from typing import Dict

server = FastAPIServer()

def create_item(name: str, price: float) -> Dict:
    return {"item": name, "price": price, "status": "created"}
server.add_endpoint("/items", create_item, method="POST")

def get_items():
    return {"items": ["item1", "item2"]}
server.add_endpoint("/items", get_items, method="GET")

server.add_cors()
server.run(host="localhost", port=3000)
```
{% endcode %}

***

#### Secure Database Management

SQLite with optional SQLCipher encryption, dynamic table creation, querying, and transactions.

Example:

{% code title="database_example.py" %}
```python
from INEX import Database

db = Database("app.db", password="your-secure-password")

columns = {
    "id": "INTEGER PRIMARY KEY AUTOINCREMENT",
    "username": "TEXT NOT NULL",
    "email": "TEXT UNIQUE",
    "created_at": "TIMESTAMP DEFAULT CURRENT_TIMESTAMP"
}
db.create_table("users", columns)

all_users = db.fetch(table_name="users", columns=["username", "email"], type="all")

user = db.fetch(table_name="users", columns=["*"], where=["email = ?", "user@example.com"], type="one")
```
{% endcode %}

Features: optional DB encryption, flexible schemas, fetch operations, conditional queries, transactions, and robust error handling.

***

#### System Management

Power and system information helpers (shutdown, restart, hibernate, log off), process and hardware monitoring.

Examples:

{% code title="system_examples.py" %}
```python
from INEX import System
import psutil
import platform
import os

system = System()

# System commands
# system.shutdown()
# system.restart()
# system.hibernate()
# system.log_off()

def get_system_info():
    return {
        "os": platform.system(),
        "release": platform.release(),
        "version": platform.version(),
        "machine": platform.machine(),
        "processor": platform.processor(),
        "cpu_count": psutil.cpu_count(),
        "memory": {
            "total": psutil.virtual_memory().total,
            "available": psutil.virtual_memory().available,
            "percent": psutil.virtual_memory().percent
        },
        "disk": {
            "total": psutil.disk_usage('/').total,
            "used": psutil.disk_usage('/').used,
            "free": psutil.disk_usage('/').free,
            "percent": psutil.disk_usage('/').percent
        }
    }
```
{% endcode %}

Supports power management, OS-specific features, privilege elevation, process control, hardware monitoring (CPU, memory, disk, network), and system information retrieval.

***

#### AI Integration

Supports Gemini, ChatGPT, and DeepSeek integrations for conversation management, text/code generation, streaming responses, and analysis.

Gemini example:

{% code title="gemini_example.py" %}
```python
from INEX.AI import AI

gemini = AI.Gemini(api_key="your-gemini-api-key")
response = gemini.send_message("Tell me about quantum computing")
conversation = gemini.create_conversation("Let's discuss AI")
conversation_id = conversation['id']
messages = gemini.get_messages(conversation_id)
```
{% endcode %}

ChatGPT example:

{% code title="chatgpt_example.py" %}
```python
from INEX import AI

chatgpt = AI.ChatGPT(api_key="your-openai-api-key", model="gpt-4")
response = chatgpt.send_message("Explain quantum entanglement", system_prompt="You are a quantum physics expert")

messages = [
    {"role": "system", "content": "You are a helpful assistant"},
    {"role": "user", "content": "What is machine learning?"}
]
chat_response = chatgpt.create_chat(messages)
```
{% endcode %}

DeepSeek example:

{% code title="deepseek_example.py" %}
```python
from INEX import AI

deepseek = AI.DeepSeek(api_key="your-deepseek-api-key")
code_response = deepseek.generate_code(prompt="Create a FastAPI hello world app", language="python")
analysis = deepseek.analyze_code(code="def hello(): return 'world'")
```
{% endcode %}

***

#### Cryptocurrency Integration

Token information and analytics across multiple blockchains (BSC, Ethereum, GeckoTerminal).

Example:

{% code title="crypto_example.py" %}
```python
from INEX import Crypto

Crypto.token_information("0x123...", type="binance")
Crypto.token_information("0xabc...", type="ethereum")
Crypto.token_information("pool_id", type="geckoterminal")
```
{% endcode %}

***

#### Library Development

Helpers to create package setup files, initialize modules, and generate upload scripts.

Example:

{% code title="libraries_example.py" %}
```python
from INEX import Libraries

Libraries.Basic.basic_setup_file_creator(
    library_name="my-library",
    library_version="1.0.0",
    description="A powerful Python library",
    creator_name="Your Name",
    creator_email="your.email@example.com",
    libraries_required=["requests", "pandas"]
)

Libraries.Basic.init_creator(filesave="__init__.py", filename="my_module", function_class="MyClass")

Libraries.Basic.upload_file_creator(pypi_api="your-pypi-token", platform="linux")
```
{% endcode %}

Features: automatic setup.py generation, dependency handling, package initialization, PyPI upload script creation, and cross-platform support.

***

#### Translation

Text translation, language detection, and multi-provider fallback support.

Examples:

{% code title="translate_examples.py" %}
```python
from INEX import Translate

text = "Bonjour le monde"
translated = Translate.translate_text(text)  # default -> English

french = Translate.translate_text("Hello, World!", to_lan="fr", from_lan="en")
spanish = Translate.translate_text("Hello, World!", to_lan="es", from_lan="en")
chinese = Translate.translate_text("Hello, World!", to_lan="zh-cn", from_lan="en")
```
{% endcode %}

Features: 100+ languages, auto-detection, multiple providers (Google, Microsoft, DeepL), batch translation, confidence scores, and text preprocessing.

***

#### Video Creation

Create videos from images with effects and platform-specific optimizations.

Example:

{% code title="videos_example.py" %}
```python
from INEX import VideosCreator

creator = VideosCreator.Basic()
creator.basic_video_creator(
    image_folder="images/",
    animation_choice="FadeIn",
    frame_rate=25,
    video_name="my_video",
    video_type="mp4",
    video_platform="Youtube",
    image_time=5
)
```
{% endcode %}

Features include platform support (YouTube, Facebook, Instagram, TikTok), animation effects, frame rate control, image support, transitions, and progress tracking.

Platform guidelines converted to steps:

{% stepper %}
{% step %}
### YouTube

* Maximum duration: 60 seconds
* Recommended frame rate: 24-30 fps
* Common resolutions: 1080p, 4K
{% endstep %}

{% step %}
### Facebook

* Maximum duration: 20 seconds
* Recommended frame rate: 30 fps
* Optimal resolution: 1280x720
{% endstep %}

{% step %}
### Instagram

* Maximum duration: 15 seconds
* Recommended frame rate: 30 fps
* Square format: 1080x1080
{% endstep %}

{% step %}
### TikTok

* Maximum duration: 60 seconds
* Recommended frame rate: 30 fps
* Vertical format: 1080x1920
{% endstep %}
{% endstepper %}

***

#### Website Management

Open and automate websites programmatically; includes validation, headless browsing, scraping, form submission, and session/cookie handling.

Example:

{% code title="websites_example.py" %}
```python
from INEX import Websites

Websites.open_website("https://example.com")
```
{% endcode %}

Advanced usage includes URL validation, asynchronous opening of multiple URLs, history/status tracking, and browser automation patterns (headless, screenshots, PDF generation).

Web automation best practices converted to steps:

{% stepper %}
{% step %}
### URL Handling

* Always validate URLs before opening
* Handle URL encoding properly
* Support international domains
* Handle redirects safely
{% endstep %}

{% step %}
### Browser Management

* Implement proper cleanup
* Handle multiple windows/tabs
* Manage browser resources
* Handle timeouts gracefully
{% endstep %}

{% step %}
### Security

* Validate all URLs
* Handle sensitive data securely
* Implement rate limiting
* Follow same-origin policy
* Handle SSL/TLS properly
* Sanitize user input
{% endstep %}

{% step %}
### Performance

* Implement caching
* Handle concurrent requests
* Manage memory usage
* Clean up resources
* Handle long-running tasks
{% endstep %}

{% step %}
### Error Handling

* Handle network errors
* Manage timeouts
* Handle browser crashes
* Log errors properly
* Implement retries
{% endstep %}
{% endstepper %}

***

### Installation

#### Basic Installation

{% code title="install_basic" %}
```bash
pip install INEX
```
{% endcode %}

#### Feature-specific Installation

{% code title="install_features" %}
```bash
# Web automation features
pip install INEX[web]

# Video creation features
pip install INEX[video]

# Translation features
pip install INEX[translation]

# Development tools
pip install INEX[dev]

# Security features
pip install INEX[security]

# Database features
pip install INEX[database]

# AI features
pip install INEX[ai]

# All features
pip install INEX[all]
```
{% endcode %}

#### Installation from Source

{% code title="install_from_source" %}
```bash
# Clone the repository
git clone https://github.com/AmmarBasha2011/inex_library.git

# Navigate to the directory
cd inex_library

# Install in development mode
pip install -e .
```
{% endcode %}

Version: 1.0.1 — Requires Python >=3.7 — Last Updated: 2025-01-21

***

### Best Practices

General, security, performance, error handling, and testing best practices (PEP 8, type hints, env vars for secrets, async I/O for I/O-bound work, caching, logging, unit/integration tests, CI/CD) are recommended and reflected across the library examples.

***

### Contact & Support

* Phone/WhatsApp: +20109673019
* Email: [pbstzidr@ywp.freewebhostmost.com](mailto:pbstzidr@ywp.freewebhostmost.com)
* GitHub: https://github.com/AmmarBasha2011/inex\_library
* PyPI: https://pypi.org/project/inex-library

Support channels: GitHub Issues, email, documentation, and WhatsApp.

Contributions welcome — see the repository for contributing guidelines.

License: MIT License — see LICENSE file for details.

***

### Release history

This version: 1.0.1 — Jan 21, 2025

Previous: 1.0.0 — Jan 20, 2025

Release artifacts (source and wheel) and file hashes:

* Source distribution: [inex\_library-1.0.1.tar.gz](https://files.pythonhosted.org/packages/8e/0d/79042630e55c9df60e23d351a16a5eb90b1804d1dc161388a534bff57230/inex_library-1.0.1.tar.gz) — SHA256: 1dba7cc6d75e078eba29963dbbf706a87b4e161b68147ee243a4ac01ebef23cb
* Wheel: [inex\_library-1.0.1-py3-none-any.whl](https://files.pythonhosted.org/packages/31/63/0f2cf62d33cb68285fb37a34184f816ed67e620f41cc21eb6c3a642d9939/inex_library-1.0.1-py3-none-any.whl) — SHA256: d30b7fb475f225a3c642cbca8f205eb95db0d46de035468aadeb0ea5a6da600e

(Full file metadata and hashes are available on the linked PyPI files pages.)

***

If you want, I can split this content into separate GitBook pages (Overview, Installation, API reference per module, Examples) or generate sidebar-friendly headings. Which layout would you prefer?
