# 🎵 Guide for Replacing Music in Unreal Engine 5 Games

![UE5 Music Replacement](https://img.shields.io/badge/Unreal_Engine-5.6-0E1128?style=for-the-badge&logo=unrealengine)
![Version](https://img.shields.io/badge/Version-1.0-blue?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey?style=for-the-badge)

## 📋 Table of Contents
- [Required Tools](#-required-tools)
- [Preparation Stage](#️-preparation-stage)
- [Extracting Original Music](#-extracting-original-music)
- [Creating Replacement in UE](#-creating-replacement-in-unreal-engine)
- [Packaging the Mod](#-packaging-the-mod)
- [Installation](#-installation)
- [Important Notes](#-important-notes)

## 🛠 Required Tools

| Tool | Purpose | Link |
|------|---------|------|
| **FModel** | Viewing and extracting game files | [Download](https://fmodel.app/) |
| **Binkadec** | .binka audio decoder | [GitHub](https://github.com/Keisawaakira/BinkadecWithWavHeader/releases/tag/1.0.2) |
| **Unreal Engine** | Creating new audio files | [Official Site](https://www.unrealengine.com/) |
| **unrealpak** | Packaging files to .pak | [GitHub](https://github.com/xamarth/unrealpak) |
| **retoc** | Creating .utoc files | [GitHub](https://github.com/trumank/retoc) |

## 🛠️ Preparation Stage

### 1. Installing and Configuring FModel

1. **Download and install FModel** from official website
2. **Install Binkadec**:
   - Download binkadec.zip archive
   - Extract ALL files to folder: `fmodel\Output\.data`
   - *This is necessary for listening to .binka audio format*

### 2. Determining Unreal Engine Version

1. Find game's .exe file (e.g., `Ride.exe`)
2. Right-click → **Properties** → **Details**
3. Find **"File version"** line (e.g.: `5.6.0.0`)
4. **First two numbers** are UE version (in example: UE5.6)
5. **Install required Unreal Engine version**

### 3. Configuring FModel for Game
Directory → Selector → Add undetected game
- Specify path to game folder
- Click "+" and "OK"
- Select UE version: `GAME_UE5_6`

### 4. Configuring Mapping
Settings → General → Local Mapping File
- Switch from `Disabled` to `Enabled`
- Specify path to .usmap file
- *Mapping file needs to be downloaded separately for your game*

## 🔍 Extracting Original Music

### Finding and Exporting Audio Files

1. Open in FModel file: `Ride-windows.utoc`
2. Navigate to path: Ride/Content/Ride/Audio/AudioFiles/Music/Tapes/Cassette_RelaxEmbrace
3. **Listen to audio** - make sure it's the right cassette
4. **Right-click file** → `Save Audio`
5. Exported .wav file will appear at path: Output\Exports\Ride\Content\Ride\Audio\AudioFiles\Music\Tapes

**💡 Important:** Remember file path and its original name!

## 🎮 Creating Replacement in Unreal Engine

### 1. Creating Project

- **Games** → **Blank** template
- **Project name** = game name (in example: `Ride`)

### 2. Importing Music

1. In project folder create EXACT path:Ride\Content\Ride\Audio\AudioFiles\Music\Tapes
2. Move your .wav file to this folder
3. **File name must match** original
4. In UE click `Import` → `Save`

### 3. Project Configuration

**Edit → Project Settings:**
- Search: `Cook everything in the project`
- Set: `True`

**Edit → Editor Preferences:**
- Search: `Cooking`
- Settings:
- `Disable Cook In The Editor feature` → **false**
- `Use shared cooked builds in launch` → **true**

### 4. File Generation

Open **Command Prompt** and execute:

```cmd
"Path\To\UE5.6\Engine\Binaries\Win64\UnrealEditor-Cmd.exe" "Path\To\Project\Ride.uproject" -run=Cook -TargetPlatform=Windows -CookDir=/Game/Ride/ -unattended 
```
Generated files will appear at path:
```cmd
Saved\Cooked\Windows\Ride\Content\Ride\Audio\AudioFiles\Music\Tapes
```
Save: .uasset, .uexp, .ubulk

## 📦 Packaging the Mod
### 1. Creating Folder Structure
```cmd
Rvmodmusic_P/
└── Ride/
    └── Content/
        └── Ride/
            └── Audio/
                └── AudioFiles/
                    └── Music/
                        └── Tapes/
                            ├── Cassette_RelaxEmbrace.uasset
                            ├── Cassette_RelaxEmbrace.uexp
                            └── Cassette_RelaxEmbrace.ubulk
```
### **2. Creating .pak File**
- Download unrealpak
- Drag folder Rvmodmusic_P to `UnrealPak-With-Compression.bat`
- Rvmodmusic_P.pak will be created automatically

### 3. Creating .utoc File
```cmd
cd path\to\retoc\folder
retoc.exe to-zen Rvmodmusic_P.pak Rvmodmusic_P.utoc --version UE5_6
```

## 🎯 Installation
**Final Mod Files:**
- Rvmodmusic_P.pak
- Rvmodmusic_P.utoc
- Rvmodmusic_P.ucas
### Place them in game folder:
```cmd
Ride\Ride\Content\Paks\
```
## **💡 Important Notes**
- "_P" suffix ensures mod loads last
- Music timing - new music shouldn't be shorter than original

## 🎉 Congratulations! Your music replacement mod is ready!

For other games the process is similar - just change paths and file names.
