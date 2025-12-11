# Docs

## INEX Library

A comprehensive Python library for AI integration, web development with FastAPI/Flask, advanced encryption, secure database management, file operations, library development, text styling, system management, translation services, video creation, web automation, and cryptocurrency token analysis. Features include JWT handling, password management, rate limiting, input sanitization, and more.

### Features

#### Web Server

**Quick Start**

Create and run web servers with ease:

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

**Server Features**

* **Flask Integration**:
  * Easy route creation
  * Dynamic endpoint handling
  * Flexible URL patterns
  * Custom return values
* **Server Configuration**:
  * Debug mode
  * Host configuration
  * Port selection
  * Main check option
* **Production Ready**:
  * WSGI support (Gunicorn)
  * ASGI support (Uvicorn)
  * Process management
  * Load balancing
* **Middleware Support**:
  * CORS handling
  * Response compression
  * Caching
  * Rate limiting
* **Security Features**:
  * HTTPS support
  * Security headers
  * CSRF protection
  * XSS prevention
* **Monitoring**:
  * Prometheus metrics
  * Error tracking
  * Request logging
  * Performance monitoring

**Advanced Usage**

```python
from INEX import Server
from flask import request, jsonify

server = Server()

# REST API Endpoints
def create_api():
    # User endpoint
    server.route_flask(
        "/api/users",
        lambda: jsonify({
            "users": ["user1", "user2"]
        })
    )
    
    # Data endpoint with parameters
    server.route_flask(
        "/api/data/<id>",
        lambda id: jsonify({
            "id": id,
            "data": "Sample data"
        })
    )
    
    # Protected endpoint
    server.route_flask(
        "/api/protected",
        lambda: (
            jsonify({"error": "Unauthorized"})
            if not request.headers.get("X-API-Key")
            else jsonify({"status": "success"})
        )
    )

# Static file serving
def setup_static():
    server.route_flask(
        "/static/<path:filename>",
        lambda filename: send_from_directory("static", filename)
    )

# Error handlers
def setup_errors():
    @server.apps.errorhandler(404)
    def not_found(e):
        return jsonify({"error": "Not found"}), 404
    
    @server.apps.errorhandler(500)
    def server_error(e):
        return jsonify({"error": "Server error"}), 500

# Initialize and run
create_api()
setup_static()
setup_errors()

server.run(
    debug=False,  # Production mode
    host="0.0.0.0",
    port="80"
)
```

**Production Deployment**

```shellscript
# Using Gunicorn
gunicorn -w 4 -b 0.0.0.0:8000 app:server.apps

# Using Uvicorn
uvicorn app:server.apps --host 0.0.0.0 --port 8000 --workers 4

# Using Supervisor
[program:inex]
command=gunicorn -w 4 -b 0.0.0.0:8000 app:server.apps
directory=/path/to/app
user=www-data
autostart=true
autorestart=true
```

#### Advanced Encryption Suite

**1. AES Encryption**

* Industry-standard AES encryption
* CBC mode operation
* File-based encryption and decryption
* Secure key handling

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

**2. Blowfish Encryption**

* Blowfish algorithm implementation
* CBC mode for enhanced security
* File encryption/decryption
* Comprehensive error handling

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

**3. Encoding Operations**

* Base64 encoding/decoding
* Hexadecimal encoding/decoding
* File-based operations
* Safe error handling

```python
from INEX import EnDeCrypt

# Base64 encoding
EnDeCrypt.Base64.encrypt("data.bin")
EnDeCrypt.Base64.decrypt("data.bin.ywpdne")

# Hexadecimal encoding
EnDeCrypt.Hex.encrypt("binary_file.dat")
EnDeCrypt.Hex.decrypt("binary_file.dat.ywpdne")
```

**Encryption Features**

* **Multiple Algorithms**: Support for AES, Blowfish, Base64, and Hex
* **Secure Implementation**:
  * CBC mode for block ciphers
  * Proper padding handling
  * IV (Initialization Vector) management
* **File Operations**:
  * Direct file encryption/decryption
  * Automatic file extension management
  * Binary file support
* **Error Handling**:
  * Comprehensive exception handling
  * Informative error messages
  * Safe file operations

#### Security Suite

**Quick Start**

Implement robust security features with ease:

```python
from INEX import Security

# Initialize security with optional secret key
security = Security(secret_key="your-secret-key")

# Password Management
hashed_password = security.hash_password("user_password")
is_valid = security.verify_password("user_password", hashed_password)

# JWT Token Handling
token = security.create_jwt_token(
    data={"user_id": 123},
    expires_delta=timedelta(hours=1)
)
payload = security.verify_jwt_token(token)

# Data Encryption
encrypted = security.encrypt_data("sensitive data")
decrypted = security.decrypt_data(encrypted)

# API Key Management
api_key, hashed_key = security.create_api_key(prefix="sk")
is_valid = security.verify_api_key(api_key, hashed_key)

# Input Sanitization
safe_input = security.sanitize_input(
    input_str="<script>alert('xss')</script>",
    allow_html=False
)

# Rate Limiting
is_allowed, remaining = security.rate_limit_check(
    key="user_ip",
    max_requests=100,
    time_window=3600
)
```

**Security Features**

* **Password Management**:
  * Bcrypt password hashing
  * Password strength validation
  * Secure password generation
  * Password verification
* **JWT Handling**:
  * Token creation with expiration
  * Token verification
  * Payload encryption
  * Error handling
* **Encryption**:
  * Symmetric (Fernet)
  * Asymmetric (RSA)
  * Key derivation (PBKDF2)
  * File encryption
* **API Security**:
  * API key generation
  * Key verification
  * Secure token creation
  * Nonce generation
* **Input Protection**:
  * XSS prevention
  * HTML sanitization
  * URL validation
  * File type validation
* **Access Control**:
  * Rate limiting
  * IP validation
  * CIDR range checking
  * Session management
* **File Security**:
  * File hashing
  * Type validation
  * Extension checking
  * Secure deletion
* **Two-Factor Authentication**:
  * Backup code generation
  * TOTP support
  * QR code generation
  * Recovery options

**Advanced Usage**

```python
from INEX import Security
from datetime import timedelta

security = Security()

# Comprehensive Password Management
def register_user(username: str, password: str):
    # Validate password strength
    is_valid, failures = security.validate_password_strength(password)
    if not is_valid:
        return {"error": failures}
    
    # Hash password and create API key
    hashed_pwd = security.hash_password(password)
    api_key, hashed_key = security.create_api_key(prefix="user")
    
    # Generate backup codes for 2FA
    backup_codes = security.generate_backup_code(
        length=8,
        num_codes=10
    )
    
    return {
        "hashed_password": hashed_pwd,
        "api_key": api_key,
        "backup_codes": backup_codes
    }

# Secure File Operations
def process_secure_upload(file_path: str, data: str):
    # Validate file type
    if not security.validate_file_type(
        file_path,
        allowed_extensions=['.pdf', '.doc', '.txt']
    ):
        return {"error": "Invalid file type"}
    
    # Calculate file hash
    file_hash = security.hash_file(file_path)
    
    # Encrypt data
    encrypted_data = security.encrypt_data(data)
    
    return {
        "file_hash": file_hash,
        "encrypted_data": encrypted_data
    }

# API Security
def secure_api_endpoint(api_key: str, data: str, client_ip: str):
    # Verify API key
    if not security.verify_api_key(api_key, stored_hash):
        return {"error": "Invalid API key"}
    
    # Check rate limit
    is_allowed, remaining = security.rate_limit_check(
        client_ip,
        max_requests=100,
        time_window=3600
    )
    if not is_allowed:
        return {"error": f"Rate limit exceeded. Try again later."}
    
    # Validate IP
    if not security.validate_ip(
        client_ip,
        allowed_ranges=['192.168.1.0/24', '10.0.0.0/8']
    ):
        return {"error": "IP not allowed"}
    
    # Process request
    sanitized_data = security.sanitize_input(data)
    encrypted_response = security.encrypt_asymmetric(sanitized_data)
    
    return {
        "encrypted_response": encrypted_response,
        "remaining_requests": remaining
    }
```

#### Text Styling

**Quick Start**

Create engaging terminal output with custom text animations:

```python
from INEX import PrintStyle

# Print text character by character
PrintStyle.print_one(
    text="Welcome to INEX!",
    second=0.05  # Delay between characters
)

# Print text with calculated timing
PrintStyle.print_all(
    text="Loading your application...",
    total_time=3.0  # Total duration for the text
)
```

**Styling Features**

* **Character-by-Character Printing**:
  * Customizable delay between characters
  * Smooth text animation
  * Buffer flushing for immediate display
* **Timed Text Display**:
  * Control total animation duration
  * Automatic timing calculation
  * Even character distribution
* **Error Handling**:
  * Empty text validation
  * Zero division protection
  * Proper buffer management

**Advanced Usage**

```python
from INEX import PrintStyle

# Create a loading animation
def show_loading():
    PrintStyle.print_all(
        text="Initializing system components...",
        total_time=2.0
    )
    PrintStyle.print_one(
        text="[====================]",
        second=0.1
    )
    PrintStyle.print_all(
        text="System ready!",
        total_time=1.0
    )

# Create a typewriter effect
def typewriter_effect(text):
    PrintStyle.print_one(
        text=text,
        second=0.03  # Fast typing speed
    )

# Create a dramatic reveal
def dramatic_reveal():
    messages = [
        "Connecting to server...",
        "Authenticating...",
        "Access granted!",
    ]
    for msg in messages:
        PrintStyle.print_all(text=msg, total_time=1.5)
```

#### File Management

**Quick Start**

Simple and secure file operations:

```python
from INEX import Files

# Create a new file
Files.create_file("example.txt")  # Will prompt for content

# Open a file
Files.open_file("example.txt")

# Delete a file
Files.delete_file("example.txt")

# Delete multiple files by type
Files.delete_all_files(
    directory="./downloads",
    type={
        "1": ".txt",
        "2": ".tmp"
    }
)
```

**File Operations**

* **File Creation**:
  * Interactive content input
  * UTF-8 encoding support
  * Exception handling
* **File Opening**:
  * Safe file access
  * Path existence verification
  * Cross-platform compatibility
* **File Deletion**:
  * Single file removal
  * Batch deletion by type
  * Directory cleanup
* **Error Handling**:
  * Comprehensive exception handling
  * Informative error messages
  * Path validation

**Advanced Usage**

```python
from INEX import Files

# Delete all temporary files in a directory
Files.delete_all_files(
    directory="./temp",
    type={
        "1": ".tmp",
        "2": ".cache",
        "3": ".log"
    }
)

# Create a configuration file
Files.create_file("config.json")
# Enter JSON content when prompted

# Safely open a file
try:
    status = Files.open_file("document.pdf")
    if status == "Not Found Path":
        print("File does not exist")
    elif status == "open":
        print("File opened successfully")
except Exception as e:
    print(f"Error: {e}")
```

#### FastAPI Server

**Quick Start**

Create a modern, high-performance API server with minimal code:

```python
from INEX import FastAPIServer

# Initialize server
server = FastAPIServer()

# Add an endpoint
def hello_world():
    return {"message": "Hello, World!"}
server.add_endpoint("/", hello_world)

# Enable CORS
server.add_cors()

# Run the server
server.run(host="0.0.0.0", port=8000)
```

**Server Features**

* **Easy Setup**: Simple initialization and configuration
* **Endpoint Management**:
  * Dynamic endpoint addition
  * Support for all HTTP methods
  * Automatic request parameter handling
* **CORS Support**:
  * Cross-Origin Resource Sharing
  * Configurable origins, methods, and headers
* **Server Configuration**:
  * Customizable host and port
  * Built on Uvicorn ASGI server
  * Production-ready performance

**Advanced Usage**

```python
from INEX import FastAPIServer
from typing import Dict

# Initialize server
server = FastAPIServer()

# Add POST endpoint with query parameters
def create_item(name: str, price: float) -> Dict:
    return {
        "item": name,
        "price": price,
        "status": "created"
    }
server.add_endpoint("/items", create_item, method="POST")

# Add GET endpoint
def get_items():
    return {"items": ["item1", "item2"]}
server.add_endpoint("/items", get_items, method="GET")

# Run with custom configuration
server.add_cors()
server.run(host="localhost", port=3000)
```

#### Secure Database Management

**SQLite Database with Encryption**

* Secure database creation with optional encryption
* Table management with flexible schema
* Advanced querying capabilities
* Row-level security

```python
from INEX import Database

# Initialize encrypted database
db = Database("app.db", password="your-secure-password")

# Create table with custom schema
columns = {
    "id": "INTEGER PRIMARY KEY AUTOINCREMENT",
    "username": "TEXT NOT NULL",
    "email": "TEXT UNIQUE",
    "created_at": "TIMESTAMP DEFAULT CURRENT_TIMESTAMP"
}
db.create_table("users", columns)

# Fetch all users
all_users = db.fetch(
    table_name="users",
    columns=["username", "email"],
    type="all"
)

# Fetch single user with condition
user = db.fetch(
    table_name="users",
    columns=["*"],
    where=["email = ?", "user@example.com"],
    type="one"
)
```

**Database Features**

* **Secure Encryption**: Optional database encryption using SQLCipher
* **Flexible Schema**: Dynamic table creation with custom column types
* **Query Operations**:
  * Fetch single or multiple rows
  * Custom column selection
  * Conditional queries with WHERE clauses
  * Transaction support
* **Error Handling**:
  * Comprehensive error handling and logging
  * Connection management and cleanup

#### System Management

**Quick Start**

Manage system operations with ease:

```python
from INEX import System

# System operations
system = System()

# Shutdown system (Windows, Linux, macOS)
system.shutdown()

# Restart system (Windows)
system.restart()

# Hibernate system (Windows)
system.hibernate()

# Log off current user (Windows)
system.log_off()
```

**System Features**

* **Power Management**:
  * System shutdown
  * System restart
  * System hibernate
  * User log off
* **Operating System Support**:
  * Windows support
  * Linux support (partial)
  * macOS support (partial)
* **Privilege Management**:
  * UAC elevation
  * Sudo operations
  * Permission checks
* **Process Control**:
  * Process monitoring
  * Resource usage tracking
  * Service management
* **Hardware Monitoring**:
  * CPU information
  * Memory usage
  * Disk space
  * Network interfaces
* **System Information**:
  * OS details
  * Hardware specs
  * Network status
  * System resources

**Advanced Usage**

```python
from INEX import System
import psutil
import platform
import os

# System information
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

# Process management
def monitor_processes():
    processes = []
    for proc in psutil.process_iter(['pid', 'name', 'cpu_percent', 'memory_percent']):
        processes.append(proc.info)
    return processes

# Network interfaces
def get_network_info():
    interfaces = []
    for iface, addrs in psutil.net_if_addrs().items():
        for addr in addrs:
            if addr.family == psutil.AF_INET:
                interfaces.append({
                    "interface": iface,
                    "address": addr.address,
                    "netmask": addr.netmask
                })
    return interfaces

# Hardware monitoring
def monitor_hardware():
    return {
        "cpu_freq": psutil.cpu_freq(),
        "cpu_percent": psutil.cpu_percent(interval=1, percpu=True),
        "memory_usage": psutil.virtual_memory(),
        "swap_usage": psutil.swap_memory(),
        "disk_io": psutil.disk_io_counters(),
        "network_io": psutil.net_io_counters()
    }
```

#### AI Integration

**1. Gemini AI**

* Complete conversation management
* Message handling and retrieval
* Conversation creation and deletion
* Real-time message interactions

```python
from INEX.AI import AI

# Initialize Gemini
gemini = AI.Gemini(api_key="your-gemini-api-key")

# Send a message
response = gemini.send_message("Tell me about quantum computing")

# Create a conversation
conversation = gemini.create_conversation("Let's discuss AI")
conversation_id = conversation['id']

# Get messages from conversation
messages = gemini.get_messages(conversation_id)
```

**2. ChatGPT Integration**

* Advanced text generation
* System prompt support
* Multi-message conversations
* Streaming responses

```python
from INEX import AI

# Initialize ChatGPT
chatgpt = AI.ChatGPT(api_key="your-openai-api-key", model="gpt-4")

# Send a message with system prompt
response = chatgpt.send_message(
    "Explain quantum entanglement",
    system_prompt="You are a quantum physics expert"
)

# Create a multi-message chat
messages = [
    {"role": "system", "content": "You are a helpful assistant"},
    {"role": "user", "content": "What is machine learning?"}
]
chat_response = chatgpt.create_chat(messages)
```

**3. DeepSeek AI**

* Text generation
* Code generation
* Code analysis
* Multiple programming language support

```python
from INEX import AI

# Initialize DeepSeek
deepseek = AI.DeepSeek(api_key="your-deepseek-api-key")

# Generate code
code_response = deepseek.generate_code(
    prompt="Create a FastAPI hello world app",
    language="python"
)

# Analyze code
analysis = deepseek.analyze_code(code="def hello(): return 'world'")
```

#### Cryptocurrency Integration

**Token Information**

* Support for multiple blockchain platforms
  * Binance Smart Chain (BSC)
  * Ethereum
  * GeckoTerminal
* Easy access to token details and analytics
* Seamless browser integration for token exploration

```python
from INEX import Crypto

# Get Binance Smart Chain token information
Crypto.token_information("0x123...", type="binance")

# Get Ethereum token information
Crypto.token_information("0xabc...", type="ethereum")

# Get GeckoTerminal pool information
Crypto.token_information("pool_id", type="geckoterminal")
```

#### Library Development

**Quick Start**

Create and distribute Python packages with ease:

```python
from INEX import Libraries

# Create a new library setup
Libraries.Basic.basic_setup_file_creator(
    library_name="my-library",
    library_version="1.0.0",
    description="A powerful Python library",
    creator_name="Your Name",
    creator_email="your.email@example.com",
    libraries_required=["requests", "pandas"]
)

# Initialize with imports
Libraries.Basic.init_creator(
    filesave="__init__.py",
    filename="my_module",
    function_class="MyClass"
)

# Create upload script
Libraries.Basic.upload_file_creator(
    pypi_api="your-pypi-token",
    platform="linux"  # or "windows"
)
```

**Library Development Features**

* **Setup File Creation**:
  * Automatic setup.py generation
  * Dependencies management
  * Package metadata handling
  * License integration (MIT)
* **Package Initialization**:
  * Dynamic import management
  * Module organization
  * Clean package structure
* **Distribution Tools**:
  * PyPI upload scripts
  * Cross-platform support (Windows/Linux)
  * Secure token handling
* **Error Handling**:
  * File existence checks
  * Platform validation
  * Comprehensive error messages

**Advanced Usage**

```python
from INEX import Libraries

# Create a comprehensive setup
Libraries.Basic.basic_setup_file_creator(
    library_name="advanced-lib",
    library_version="2.1.0",
    description="Advanced Python utilities",
    creator_name="Team Lead",
    creator_email="team@company.com",
    libraries_required=[
        "numpy>=1.20.0",
        "scipy>=1.7.0",
        "pandas>=1.3.0"
    ],
    readme_name="README.md",
    License="MIT"
)

# Initialize multiple modules
for module in ["core", "utils", "helpers"]:
    Libraries.Basic.init_creator(
        filesave="__init__.py",
        filename=module,
        function_class=f"{module.capitalize()}Class"
    )

# Create platform-specific upload scripts
for platform in ["windows", "linux"]:
    Libraries.Basic.upload_file_creator(
        filename=f"upload_{platform}",
        pypi_api="your-pypi-token",
        platform=platform
    )
```

#### Translation

**Quick Start**

Translate text between languages with ease:

```python
from INEX import Translate

# Simple translation (auto-detect to English)
text = "Bonjour le monde"
translated = Translate.translate_text(text)  # "Hello world"

# Specify source and target languages
text = "Hello, World!"
french = Translate.translate_text(text, to_lan="fr", from_lan="en")  # "Bonjour le monde"
spanish = Translate.translate_text(text, to_lan="es", from_lan="en")  # "¡Hola Mundo!"
chinese = Translate.translate_text(text, to_lan="zh-cn", from_lan="en")  # "你好，世界！"
```

**Translation Features**

* **Language Support**:
  * 100+ languages supported
  * Auto language detection
  * Regional language variants
  * Right-to-left languages
* **Translation Options**:
  * Text translation
  * Language detection
  * Multiple translation services
  * Batch translation
* **Advanced Features**:
  * Language identification
  * Confidence scores
  * Regional variants
  * Character encoding
* **Service Providers**:
  * Google Translate
  * Microsoft Translator
  * DeepL
  * Multiple fallback options
* **Text Processing**:
  * Language detection
  * Text analysis
  * Sentiment analysis
  * Text preprocessing

**Advanced Usage**

```python
from INEX import Translate
from langdetect import detect
from deep_translator import GoogleTranslator
from textblob import TextBlob

# Language detection
def detect_language(text):
    return detect(text)

# Multiple translation services
def translate_with_fallback(text, target_lang="en"):
    try:
        # Try Google Translate first
        return Translate.translate_text(text, to_lan=target_lang)
    except:
        # Fallback to alternative service
        return GoogleTranslator(source='auto', target=target_lang).translate(text)

# Batch translation
def batch_translate(texts, target_lang="en"):
    return [Translate.translate_text(text, to_lan=target_lang) for text in texts]

# Language analysis
def analyze_text(text):
    blob = TextBlob(text)
    return {
        "language": detect(text),
        "sentiment": blob.sentiment,
        "translated": str(blob.translate(to='en')),
        "words": len(blob.words),
        "sentences": len(blob.sentences)
    }

# Example usage
text = "Je suis heureux de vous rencontrer!"
analysis = analyze_text(text)
print(f"Language: {analysis['language']}")  # fr
print(f"English: {analysis['translated']}")  # "I am happy to meet you!"
print(f"Sentiment: {analysis['sentiment']}")  # Sentiment(polarity=0.8, subjectivity=1.0)
```

**Supported Languages**

Common language codes:

* English (en)
* Spanish (es)
* French (fr)
* German (de)
* Italian (it)
* Portuguese (pt)
* Russian (ru)
* Chinese Simplified (zh-cn)
* Chinese Traditional (zh-tw)
* Japanese (ja)
* Korean (ko)
* Arabic (ar)
* Hindi (hi)
* And many more...

#### Video Creation

**Quick Start**

Create videos from images with ease:

```python
from INEX import VideosCreator

# Initialize video creator
creator = VideosCreator.Basic()

# Create a basic video from images
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

**Video Features**

* **Platform Support**:
  * YouTube (up to 60 seconds)
  * Facebook (up to 20 seconds)
  * Instagram (up to 15 seconds)
  * TikTok (up to 60 seconds)
* **Animation Effects**:
  * FadeIn
  * FadeOut
  * Rotate
  * FlipHorizontal
  * FlipVertical
* **Video Options**:
  * Custom frame rate
  * Image duration control
  * Output format selection
  * Platform optimization
* **Image Support**:
  * JPG/JPEG
  * PNG
  * Automatic sorting
  * Multiple images
* **Advanced Features**:
  * Transition effects
  * Duration limits
  * Error handling
  * Progress tracking

**Advanced Usage**

```python
from INEX import VideosCreator
import os

def create_platform_videos(image_folder, animations=None):
    """Create videos optimized for different platforms"""
    if animations is None:
        animations = ['FadeIn', 'FadeOut', 'Rotate', 'FlipHorizontal', 'FlipVertical']
    
    creator = VideosCreator.Basic()
    platforms = {
        'Youtube': 60,
        'Facebook': 20,
        'Instagram': 15,
        'Tiktok': 60
    }
    
    results = {}
    for platform, max_duration in platforms.items():
        for animation in animations:
            video_name = f"{platform.lower()}_{animation.lower()}"
            try:
                creator.basic_video_creator(
                    image_folder=image_folder,
                    animation_choice=animation,
                    frame_rate=30,
                    video_name=video_name,
                    video_type="mp4",
                    video_platform=platform,
                    image_time=min(5, max_duration/3)  # Adjust time based on platform
                )
                results[video_name] = "Success"
            except Exception as e:
                results[video_name] = f"Failed: {str(e)}"
    
    return results

def batch_process_folders(base_folder):
    """Process multiple image folders in batch"""
    results = {}
    for folder in os.listdir(base_folder):
        folder_path = os.path.join(base_folder, folder)
        if os.path.isdir(folder_path):
            results[folder] = create_platform_videos(folder_path)
    return results

# Example usage
results = batch_process_folders("image_collections/")
for folder, folder_results in results.items():
    print(f"\nResults for {folder}:")
    for video, status in folder_results.items():
        print(f"  {video}: {status}")
```

**Platform Guidelines**

1. **YouTube**:
   * Maximum duration: 60 seconds
   * Recommended frame rate: 24-30 fps
   * Common resolutions: 1080p, 4K
2. **Facebook**:
   * Maximum duration: 20 seconds
   * Recommended frame rate: 30 fps
   * Optimal resolution: 1280x720
3. **Instagram**:
   * Maximum duration: 15 seconds
   * Recommended frame rate: 30 fps
   * Square format: 1080x1080
4. **TikTok**:
   * Maximum duration: 60 seconds
   * Recommended frame rate: 30 fps
   * Vertical format: 1080x1920

#### Website Management

**Quick Start**

Open websites programmatically:

```python
from INEX import Websites

# Open a website in the default browser
Websites.open_website("https://example.com")
```

**Web Automation Features**

* **Browser Control**:
  * Open URLs in default browser
  * Multi-browser support
  * Error handling
  * URL validation
* **Advanced Features**:
  * Web scraping capabilities
  * Headless browsing
  * Browser automation
  * Session management
  * Cookie handling
  * Form submission
  * JavaScript execution
  * Screenshot capture
  * PDF generation

**Advanced Usage**

```python
from INEX import Websites
import validators
import asyncio
from typing import List, Dict

class WebsiteManager:
    def __init__(self):
        self.history: List[str] = []
        self.status: Dict[str, str] = {}

    def validate_url(self, url: str) -> bool:
        """Validate URL format"""
        return bool(validators.url(url))

    def open_with_validation(self, url: str) -> str:
        """Open URL with validation"""
        if not self.validate_url(url):
            return f"Invalid URL format: {url}"
        
        try:
            result = Websites.open_website(url)
            if result == "opened":
                self.history.append(url)
                self.status[url] = "success"
                return f"Successfully opened {url}"
            return f"Failed to open {url}"
        except Exception as e:
            self.status[url] = "failed"
            return f"Error opening {url}: {str(e)}"

    async def open_multiple(self, urls: List[str]) -> Dict[str, str]:
        """Open multiple URLs asynchronously"""
        results = {}
        for url in urls:
            results[url] = self.open_with_validation(url)
            await asyncio.sleep(1)  # Prevent browser overload
        return results

    def get_history(self) -> List[str]:
        """Get browsing history"""
        return self.history

    def get_status(self) -> Dict[str, str]:
        """Get status of opened URLs"""
        return self.status

# Example usage
async def main():
    manager = WebsiteManager()
    
    # Open single website
    print(manager.open_with_validation("https://example.com"))
    
    # Open multiple websites
    urls = [
        "https://example.com",
        "https://example.org",
        "https://example.net"
    ]
    results = await manager.open_multiple(urls)
    
    # Print results
    for url, status in results.items():
        print(f"{url}: {status}")
    
    # Print history
    print("\nBrowsing History:")
    for url in manager.get_history():
        print(f"- {url}")

# Run the example
if __name__ == "__main__":
    asyncio.run(main())
```

**Web Automation Best Practices**

1. **URL Handling**:
   * Always validate URLs before opening
   * Handle URL encoding properly
   * Support international domains
   * Handle redirects safely
2. **Browser Management**:
   * Implement proper cleanup
   * Handle multiple windows/tabs
   * Manage browser resources
   * Handle timeouts gracefully
3. **Security**:
   * Validate all URLs
   * Handle sensitive data securely
   * Implement rate limiting
   * Follow same-origin policy
   * Handle SSL/TLS properly
   * Sanitize user input
4. **Performance**:
   * Implement caching
   * Handle concurrent requests
   * Manage memory usage
   * Clean up resources
   * Handle long-running tasks
5. **Error Handling**:
   * Handle network errors
   * Manage timeouts
   * Handle browser crashes
   * Log errors properly
   * Implement retries

### Installation

#### Basic Installation

```shellscript
pip install INEX
```

#### Feature-specific Installation

Install INEX with specific feature sets:

```shellscript
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

#### Installation from Source

```shellscript
# Clone the repository
git clone https://github.com/AmmarBasha2011/inex_library.git

# Navigate to the directory
cd inex_library

# Install in development mode
pip install -e .
```

#### Version Information

* Current Version: 1.0.1
* Python Required: >=3.7
* Last Updated: 2025-01-21

### Best Practices

#### General Best Practices

* Follow Python PEP 8 style guide
* Use type hints for better code clarity
* Implement proper error handling
* Write comprehensive unit tests
* Document your code thoroughly
* Use virtual environments
* Keep dependencies updated
* Follow security guidelines
* Implement logging
* Handle cleanup properly

#### Security Best Practices

* Use environment variables for sensitive data
* Implement proper authentication
* Use secure communication protocols
* Validate all inputs
* Implement rate limiting
* Use secure password hashing
* Handle sensitive data properly
* Implement proper access controls
* Use secure session management
* Follow OWASP guidelines

#### Performance Best Practices

* Implement caching where appropriate
* Use async operations for I/O
* Optimize database queries
* Minimize network requests
* Use connection pooling
* Implement proper indexing
* Handle memory efficiently
* Use appropriate data structures
* Implement pagination
* Profile and optimize code

#### Error Handling Best Practices

* Use try-except blocks appropriately
* Implement proper logging
* Handle edge cases
* Provide meaningful error messages
* Implement retry mechanisms
* Handle timeouts properly
* Clean up resources
* Handle concurrent errors
* Implement fallback mechanisms
* Monitor error rates

#### Testing Best Practices

* Write unit tests
* Implement integration tests
* Use mock objects appropriately
* Test edge cases
* Implement CI/CD
* Use code coverage tools
* Write readable test cases
* Test error conditions
* Document test cases
* Maintain test data

### Contact & Support

#### Contact Information

* Phone/WhatsApp: +20109673019
* Email: [inex.own@gmail.com](mailto:inex.own@gmail.com)
* GitHub: [https://github.com/AmmarBasha2011/inex\_library](https://github.com/AmmarBasha2011/inex_library)
* PyPI: [https://pypi.org/project/inex-library](https://pypi.org/project/inex-library)

#### Support Channels

* GitHub Issues: For bug reports and feature requests
* Email Support: For general inquiries and assistance
* Documentation: Comprehensive guides and API reference
* WhatsApp: For urgent support and quick responses

#### Contributing

We welcome contributions! Please see our contributing guidelines in the GitHub repository.

#### License

MIT License - see LICENSE file for details
