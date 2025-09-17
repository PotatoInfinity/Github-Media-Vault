
# GitHub Vault 🔐

githubvault.replit.app

A secure, client-side image and document storage application that uses GitHub repositories as encrypted storage backends. Store your media files safely with zero-knowledge encryption - even GitHub can't see your content!

## ✨ Features

### 🔒 **Zero-Knowledge Security**
- **Client-side encryption only** - All encryption/decryption happens in your browser
- **Password-based protection** - Your vault password never leaves your device
- **AES-GCM encryption** with PBKDF2 key derivation (150,000 iterations)
- GitHub only stores encrypted data - no plaintext access possible

### 📁 **Smart File Management**
- **Folder organization** - Create and manage custom folders for your media
- **Advanced search** - Search by filename across all folders
- **Multiple sort options** - Sort by date or name (ascending/descending)
- **Drag & drop uploads** - Easy file uploading with progress tracking

### 🎬 **Rich Media Support**
- **Images**: JPG, PNG, GIF, WebP, HEIC/HEIF (auto-converted to JPG)
- **Videos**: MP4, MOV, AVI, MKV, WebM, and more with duration display
- **Office Documents**: PDF, DOC/DOCX, PPT/PPTX, XLS/XLSX with preview
- **Text Files**: TXT, MD, JSON, CSV, RTF with syntax highlighting

### ⚡ **Performance Optimized**
- **Adaptive memory management** - Automatically adjusts based on your device
- **Progressive loading** - Thumbnails → Medium quality → Full resolution
- **Smart caching** - Uses IndexedDB for faster repeated access
- **Large file chunking** - Handles files up to GitHub's limits seamlessly

### 🌐 **GitHub Integration**
- **Public repositories** - Uses GitHub's free tier (files are encrypted)
- **Automatic repo management** - Creates new repos when size limits are reached
- **Personal Access Token** - Secure authentication with GitHub API
- **Version control benefits** - All changes tracked in Git history

## 🚀 Quick Start

### Prerequisites
1. **GitHub Account** - Sign up at [github.com](https://github.com)
2. **Personal Access Token** - Create one with `public_repo` scope:
   - Go to GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)
   - Click "Generate new token (classic)"
   - Select `public_repo` scope
   - Copy the generated token

### Getting Started
1. **Open GitHub Vault** - Visit the deployed application
2. **Enter GitHub credentials**:
   - GitHub username
   - Personal Access Token (created above)
   - Check "Remember" to save credentials locally
3. **Create vault account**:
   - Choose a unique vault username
   - Set a strong vault password (this encrypts your files)
4. **Start uploading** - Drag & drop files or click the upload area

## 📂 File Organization

### Folder System
- **Default folder**: "others" - All unorganized files go here
- **Custom folders**: Create new folders using the folder controls
- **Folder search**: Quickly find folders with the search box
- **Auto-organization**: Assign folders during upload or edit later

### File Types Supported
- **Images**: Automatic thumbnail generation and HEIC conversion
- **Videos**: Frame extraction for thumbnails and duration detection
- **Office docs**: Icon-based thumbnails and online preview integration
- **Large files**: Automatic chunking for files over 10MB

## 🔧 Technical Details

### Architecture
- **Frontend**: Vanilla React 18 loaded via CDN
- **Styling**: Tailwind CSS for responsive design
- **Storage**: GitHub repositories as encrypted storage backend
- **Local cache**: IndexedDB for performance optimization
- **Encryption**: Web Crypto API for all cryptographic operations

### Memory Management
The app includes adaptive memory management that automatically adjusts based on your device:
- **High-end devices** (8GB+ RAM): Load up to 25 full-resolution media
- **Mid-range devices** (4GB+ RAM): Load up to 15 full-resolution media  
- **Lower-end devices** (2GB+ RAM): Load up to 10 full-resolution media
- **Thumbnail caching**: Separate limits for thumbnail storage
- **Automatic cleanup**: Old media automatically unloaded from memory

### File Storage Structure
```
your-username_data_0/           # Main data repository
├── files-index.json           # Memory-optimized file index
├── chunks/                    # Large file chunks
│   └── [media-id]/
│       ├── 0.json            # First chunk
│       └── 1.json            # Second chunk
├── previews/                  # Thumbnail and medium previews
│   └── [media-id]/
│       ├── thumbnail.json     # Compressed thumbnail
│       └── medium.json        # Medium-quality preview
└── vault-manifest.json        # Repository metadata
```

## 🔐 Security Features

### Encryption Details
- **Algorithm**: AES-GCM with 256-bit keys
- **Key derivation**: PBKDF2 with 150,000 iterations and random salt
- **IV generation**: Cryptographically random 12-byte initialization vectors
- **Salt generation**: Random 16-byte salts for each file
- **Password verification**: Encrypted verifier prevents brute force

### Privacy Guarantees
- ✅ File contents are encrypted client-side before upload
- ✅ Encryption keys never leave your browser
- ✅ GitHub cannot decrypt your files
- ✅ Only encrypted thumbnails are generated
- ❌ File metadata (names, dates, dimensions) are visible on GitHub
- ❌ Repository structure and file count are visible

## 🛠️ Advanced Usage

### Account Management
- **Export data**: Download all files individually before account deletion
- **Account deletion**: Permanently removes all repositories and data
- **Multiple devices**: Use same GitHub token and vault password anywhere

### Repository Management
- **Auto-scaling**: New repositories created when 500MB limit reached
- **Naming convention**: `username_data_0`, `username_data_1`, etc.
- **Manual cleanup**: Delete individual files to free GitHub storage

### Performance Tips
- **Thumbnail loading**: Happens automatically for visible files
- **Full resolution**: Only loads when you click to view
- **Memory cleanup**: Files automatically unloaded when scrolled out of view
- **Search optimization**: Search works on cached metadata for speed

## ⚠Important Limitations

### GitHub Limitations
- **File size limit**: 95MB per individual file (chunked automatically)
- **Repository size limit**: 500MB per repository (new repos created automatically)
- **Rate limits**: GitHub API has rate limits (usually not reached in normal use)
- **Public repositories**: All repositories are public (but files are encrypted)

### Browser Requirements
- **Modern browser**: Requires Web Crypto API support (Chrome 43+, Firefox 34+, Safari 11+)
- **JavaScript enabled**: Application requires JavaScript to function
- **IndexedDB support**: For local caching (available in all modern browsers)

## Contributing

This is an open-source project! Feel free to:
- Report bugs or suggest features via GitHub issues
- Submit pull requests for improvements
- Fork the project for your own modifications
- Share your experience and use cases

## 📄 License

This project is open source and available under the MIT License.

## Troubleshooting

### Common Issues

**"Failed to load vault manifest"**
- Check your GitHub username and Personal Access Token
- Ensure the token has `public_repo` scope
- Check GitHub rate limits in your account settings

**"Upload failed" errors**
- Verify file size is under 95MB
- Check your internet connection
- Ensure you haven't hit GitHub's storage limits

**"Thumbnail error" or "Decrypt failed"**
- Try refreshing the page to clear cache
- Verify you're using the correct vault password
- Check browser console for detailed error messages

**Memory issues or slow performance**
- Close other browser tabs to free RAM
- Clear browser cache and reload the page
- Try uploading smaller batches of files

### Getting Help
- Check browser developer console for error messages
- Verify GitHub token permissions and expiration
- Test with smaller files first to isolate issues
- Ensure stable internet connection during uploads

---

**🔒 Remember**: Your vault password is the only way to decrypt your files. If you lose it, your data cannot be recovered!
