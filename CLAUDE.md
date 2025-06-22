# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Music Key Finder** (キー推測アプリ) - an interactive web-based tool designed for DTM musicians and those doing ear training to help identify musical keys based on selected notes.

## Architecture

### Single-Page Application Structure
- **Single HTML file**: `index.html` contains all HTML, CSS, and JavaScript
- **No build process**: Direct browser execution using CDN dependencies
- **External dependencies**: 
  - Tailwind CSS (via CDN)
  - Tone.js v14.8.49 (for audio synthesis)

### Core Components

**Music Theory Engine** (`index.html:160-170`):
- `scales` object: Pre-computed scale structures for all 12 major and minor keys
- `majorIntervals` and `minorIntervals`: Define scale patterns
- Automatic scale generation for all chromatic roots

**Audio System** (`index.html:188-219`):
- Tone.js integration for audio playback
- AudioContext initialization with user interaction requirement
- Sine wave synthesizer with envelope controls

**User Interface**:
- **Input modes**: Click and keyboard input with toggle switching
- **Note selection**: 12-button chromatic interface with visual feedback
- **Key mapping**: Piano-style keyboard layout (A=C, S=D, W=C#, etc.)
- **Results display**: Scored key suggestions with scale note information

**Key Detection Algorithm** (`index.html:422-453`):
- Base scoring: (matched notes / selected notes) × 100
- Bonus system: +10 points for root note, +5 points for fifth
- Ranking by combined score and match count

### State Management

All state is managed through global variables:
- `selectedUserNotes`: Set of user-selected notes
- `currentInputMode`: 'click' or 'keyboard' input mode  
- `audioContextStarted`: Audio initialization status
- `synth`: Tone.js synthesizer instance

## Development

### No Build Commands
This is a static HTML application with no build, lint, or test commands. Development involves:
1. Direct file editing of `index.html`
2. Browser refresh for testing
3. Browser developer tools for debugging

### Testing
- Manual testing in browser required
- Test audio functionality with user interaction
- Verify keyboard input mappings
- Check key detection accuracy with known musical examples

### Deployment
The application is deployed as a GitHub Pages site at: https://yamac-music.github.io/music-key-finder/

## Key Features to Maintain

1. **Audio-first design**: Every note selection plays audio feedback
2. **Dual input modes**: Both click and keyboard interaction must work
3. **Music theory accuracy**: Key detection algorithm uses proper harmonic weighting
4. **Responsive UI**: Works on both desktop and mobile devices
5. **Japanese localization**: All UI text is in Japanese

## Common Modifications

When editing this codebase:
- Audio changes: Modify Tone.js synthesizer configuration in `initializeAudio()`
- Algorithm tuning: Adjust bonus points and scoring in the guess key button event listener
- UI styling: Update Tailwind classes or custom CSS in the `<style>` section
- Keyboard mappings: Modify `keyToNoteMapping` object for different key layouts