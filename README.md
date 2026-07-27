# Zyphstrap

Zyphstrap is an open-source Roblox bootstrapper replacing the stock launcher with a cleaner, transparent alternative. It manages client installs/updates, applies Fast Flags via simple plain-English toggles, and adds Discord Rich Presence and launcher theming — all local, no network interception or asset modification.

![Platform](https://img.shields.io/badge/platform-Windows-blue)
![License](https://img.shields.io/badge/license-GPL--3.0-green)
![Status](https://img.shields.io/badge/status-in%20development-yellow)

**Repository:** [github.com/Kitsune92/ZYPHSTRAP](https://github.com/Kitsune92/ZYPHSTRAP)

---

## Features

- **Install & Update Management** — handles Roblox client versioning automatically
- **Simplified FFlags** — plain-English toggles and dropdowns instead of raw config strings, each with a short description of what it does
- **Discord Rich Presence** — shows your current game and session time, with an optional join button
- **Custom Theming** — launcher accent colors, dark/light mode, custom splash screen
- **Guided First-Run Setup** — a short walkthrough on first install
- **Built-in Help Center** — FAQ, tutorial videos, and direct links to support

## Screenshots

*(Add screenshots or a GIF walkthrough here once the UI is built)*

## Installation

1. Download the latest installer from the [Releases](https://github.com/Kitsune92/ZYPHSTRAP/releases) page
2. Run `Zyphstrap-Setup.exe`
3. Follow the first-run tutorial to configure your first FFlags and (optionally) enable Discord Rich Presence

## Building from Source

```bash
git clone https://github.com/Kitsune92/ZYPHSTRAP.git
cd ZYPHSTRAP
dotnet restore
dotnet build
```

**Requirements:**
- .NET 8 SDK
- Windows 10/11

## Project Structure

```
/Zyphstrap
  /src
    /Bootstrapper       # download, install, launch logic
    /FFlagManager        # flag definitions, UI bindings, validation
    /RichPresence         # Discord IPC integration
    /UI                   # views, theming
  /resources
    flag-manifest.json    # flag name, category, description, default
    faq.json
  /installer
```

## Scope

Zyphstrap is a bootstrapper only. It does **not** include a network proxy, real-time asset interception, in-game asset replacement, or any third-party client modification. It operates strictly on the local install — download, launch, and configuration.

## Support

- Discord: [invite link]
- Email: [support email]
- YouTube: [channel link]
- TikTok: [profile link]
- FAQ: available in-app under **Help**

## Contributing

Pull requests are welcome. For major changes, please [open an issue](https://github.com/Kitsune92/ZYPHSTRAP/issues) first to discuss what you'd like to change.

1. Fork the repo
2. Create your feature branch (`git checkout -b feature/my-feature`)
3. Commit your changes
4. Push to the branch and open a PR

## License

This project is licensed under the [GNU General Public License v3.0](LICENSE) — you're free to use, modify, and distribute this software, provided derivative works are also licensed under GPL-3.0 and their source is made available.


