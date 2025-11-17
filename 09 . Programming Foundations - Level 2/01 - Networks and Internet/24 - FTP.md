---
DATE: 2025-10-22T00:17:00
DONE: true
Name: Foundation 2
---


# **FTP (File Transfer Protocol)

## Definition

*<span style="color:rgb(20, 192, 255)">FTP</span> (<span style="color:rgb(20, 192, 255)">F</span>ile <span style="color:rgb(20, 192, 255)">T</span>ransfer <span style="color:rgb(20, 192, 255)">P</span>rotocol) is a standard method for transferring files between computers over the internet. Think of it as a digital delivery system that lets you upload files to a server or download files from a server.

## What FTP Does

FTP allows you to:
- **Upload** files from your computer to a server
- **Download** files from a server to your computer
- **Delete** files on a server
- **Rename** or move files on a server
- **Create** or remove folders on a server

## How FTP Works

### Client-Server Model
- **FTP Client**: Your computer (requesting or sending files)
- **FTP Server**: Remote computer storing the files

### Two Connections
FTP uses two separate connections at the same time:

1. **Control Connection (Port 21)**
   - Sends commands (like "upload this file")
   - Receives responses from the server
   - Like a phone line for instructions

2. **Data Connection (Port 20)**
   - Actually transfers the files
   - Like a conveyor belt moving boxes

### Basic Process

1. *You connect to an FTP server using an FTP client
2. *You log in with username and password (or anonymously for public files)
3. *You can browse folders on the server
4. *You select files to upload or download
5. *FTP transfers the files over the data connection
6. *You disconnect when finished 

## Two Connection Modes

### Active Mode
- Server creates the data connection back to you
- May have problems with firewalls

### Passive Mode (More Common)
- You create both connections to the server
- Works better with firewalls
- Default mode for most FTP clients

## Common Uses

1. **Website Management**: Uploading website files to web hosting servers
2. **File Sharing**: Sharing large files between offices or people
3. **Backups**: Storing backup copies of important data
4. **Software Distribution**: Downloading programs and updates
5. **Media Management**: Uploading images, videos to servers

## Ways to Use FTP

### 1. FTP Client Software (Most Popular)
- Programs like FileZilla, WinSCP, Cyberduck
- User-friendly interface with drag-and-drop
- Shows files on your computer and server side-by-side

### 2. Command Line
- Type FTP commands directly in terminal/command prompt
- More technical, but still available in all operating systems

### 3. Web Browser (Limited)
- Some browsers can access FTP servers
- Type: ftp://example.com in the address bar
- Less reliable than FTP clients

## Security Concerns

### Basic FTP Issues
- Sends passwords in plain text (not encrypted)
- Anyone monitoring the network can see your login info
- Not secure for sensitive files

### Secure Alternatives

1. **FTPS (FTP Secure)**
   - FTP with SSL/TLS encryption
   - Protects data during transfer

2. **SFTP (SSH File Transfer Protocol)**
   - Uses SSH for security
   - More secure than basic FTP
   - Recommended for sensitive data

## Key Advantages

- **Resume Transfers**: If connection drops, you can continue where you left off
- **Multiple Files**: Transfer many files at once
- **Cross-Platform**: Works between Windows, Mac, Linux
- **Automation**: Can schedule automatic transfers
- **Large Files**: Handles big files efficiently

## Key Points

- FTP is for transferring files between computers over a network
- Uses two connections: one for commands, one for data
- Can upload, download, and manage files on remote servers
- Commonly used for website management and file sharing
- Basic FTP is not secure - use FTPS or SFTP for sensitive data
- FTP clients provide the easiest way to use FTP
