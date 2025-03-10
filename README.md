# M3U Playlist Generator

A powerful and flexible tool that automatically generates M3U playlists from season files, with advanced organization features for media players.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Python](https://img.shields.io/badge/python-3.6%2B-brightgreen.svg)

## Overview

M3U Playlist Generator is designed to help media enthusiasts organize their video content into structured playlists. It automatically scans directories for season files, extracts episode links, and generates well-formatted M3U playlists that work with popular media players like VLC, Kodi, and more.

## Features

- **Automatic Season Detection**: Identifies season files based on customizable naming patterns
- **Smart Episode Extraction**: Extracts video links from files while preserving exact formatting
- **Enhanced M3U Format**: Creates organized playlists with season and episode metadata
- **Flexible Configuration**: Highly customizable through config files or command-line options
- **Multi-threaded Processing**: Fast parallel processing of multiple season files
- **Dual Interface**: Choose between GUI or command-line operation
- **Advanced Logging**: Comprehensive logging with configurable levels and rotation

## Installation

### Prerequisites
- Python 3.6 or higher
- Tkinter (included with most Python installations)

### Install from GitHub
```bash
# Clone the repository
git clone https://github.com/yourusername/m3u-playlist-generator.git

# Navigate to the directory
cd m3u-playlist-generator

# Run directly
python m3u_generator.py
```

### Optional: Create a virtual environment
```bash
# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

## Usage

### Graphical Interface

Simply run the script without arguments to use the GUI:

```bash
python m3u_generator.py
```

The application will guide you through:
1. Selecting a directory containing season files
2. Choosing a base filename for episodes
3. Saving the M3U playlist to your desired location

### Command Line

For automation or scripting, use the command-line interface:

```bash
python m3u_generator.py --nogui -d "/path/to/seasons" -n "Show Name" -o "playlist.m3u"
```

### Command Line Options

```
usage: m3u_generator.py [-h] [-d DIRECTORY] [-n NAME] [-c CONFIG] [-o OUTPUT]
                       [--log-file LOG_FILE]
                       [--log-level {DEBUG,INFO,WARNING,ERROR}] [--nogui]
                       [-v]

Generate M3U playlists from season files

options:
  -h, --help            show this help message and exit
  -d DIRECTORY, --directory DIRECTORY
                        Directory containing season files (default: None)
  -n NAME, --name NAME  Base filename for episodes (default: None)
  -c CONFIG, --config CONFIG
                        Path to configuration file (default: None)
  -o OUTPUT, --output OUTPUT
                        Output M3U file path (default: None)
  --log-file LOG_FILE   Path to log file (default: None)
  --log-level {DEBUG,INFO,WARNING,ERROR}
                        Logging level (default: None)
  --nogui               Run in command-line mode without GUI (default: False)
  -v, --version         show program's version number and exit
```

## Configuration

You can customize the application's behavior using a JSON configuration file:

```json
{
    "valid_extensions": [".mkv", ".mp4", ".avi", ".mov", ".flv", ".m4v", ".webm"],
    "default_base_filename": "Episode",
    "season_pattern": ".*\\b[Ss](?:eason)?[_\\. ]?(\\d{1,2})\\b(?!.*[Ee]\\d{1,2}).*",
    "log_level": "INFO",
    "max_workers": 4,
    "include_thumbnails": false,
    "m3u_template": "#EXTM3U\n\n"
}
```

Specify the configuration file with `-c` or `--config`.

## File Format Support

The application recognizes various video file formats:

- Standard files: `.mkv`, `.mp4`, `.avi`, `.mov`, `.flv`, `.m4v`, `.webm`
- URLs: HTTP/HTTPS links containing the above extensions
- Custom formats can be added through the configuration file

## Season File Format

Season files should contain one video link per line. The application can handle:

1. Direct file paths
2. URLs pointing to video files
3. Mixed content (both local and remote links)

Examples of recognized season file names:
- `Season 1.txt`
- `S01.txt`
- `s_1_links.txt`
- `Season.01.episodes.txt`

## Output Format

The generated M3U file includes:

- Standard M3U header
- Season grouping with metadata
- Episode listings with custom names
- Network caching options for improved playback
- Clean formatting for compatibility with major players

Example output:
```
#EXTM3U

#EXTINF:-1 group-title="Season 1" tvg-logo="" type="playlist", === Season 1 ===
#EXTVLCOPT:network-caching=1000
#season:1

#EXTINF:-1 group-title="Season 1" tvg-logo="" type="video", Show Name S01E01
#episode:1
/path/to/episode1.mkv

#EXTINF:-1 group-title="Season 1" tvg-logo="" type="video", Show Name S01E02
#episode:2
/path/to/episode2.mkv
```

## Contributing

Contributions are welcome! Feel free to:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- Thanks to all the media enthusiasts who provided feedback and feature suggestions
- Inspired by the need for better media organization tools
