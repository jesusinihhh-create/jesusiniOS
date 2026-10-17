# jesusiniOS

A Windows 10-inspired desktop prototype plus a Debian Live Build starter project.

## Run the desktop prototype
Open `desktop/index.html` in a modern browser. For best results, serve it locally:

```bash
cd desktop
python3 -m http.server 8080
```

Then open http://localhost:8080.

The prototype includes a Start menu, movable app windows, Notepad (browser-local saving), Paint (PNG export), Calculator, Terminal demo commands, File Manager demo, and Settings for theme, accent color, wallpaper, taskbar position, and display scale. This prototype is not itself an operating system.

## Build a bootable ISO (Linux required)
The `iso/` directory contains a Debian Live Build configuration starter. Build it on a Debian/Ubuntu Linux machine or VM with internet access. ISO generation is not performed automatically by this project.

```bash
sudo apt update
sudo apt install -y live-build debootstrap squashfs-tools xorriso
cd iso
sudo lb config
sudo lb build
```

If your live-build version requires it, review `lb config --help` and Debian Live Manual first. The result is typically named `live-image-amd64.hybrid.iso`. The included package list installs XFCE and common utilities; this first ISO starter uses a standard Linux desktop rather than the browser prototype as its shell. The desktop prototype can be packaged into the image later as a web app/kiosk or rebuilt as a native desktop.

## VirtualBox
1. Create a new VM, type Linux, version Debian (64-bit).
2. Give it at least 4 GB RAM and 25 GB virtual disk (2 GB RAM may boot, but is not recommended).
3. Open Settings → Storage and attach the generated ISO to the optical drive.
4. Start the VM and choose the live boot option. Install to the virtual disk only after testing.

## Notes
- The terminal in the browser prototype is a safe simulated terminal, not a real shell.
- Settings and Notepad data are stored in the browser's local storage for this prototype.
- The ISO is a build configuration, not a prebuilt ISO. A prebuilt ISO needs to be generated and tested on Linux.

## Build the ISO on GitHub Actions (no Linux PC required)
1. Create a GitHub repository and upload the contents of this ZIP.
2. Open the repository's **Actions** tab.
3. Select **Build jesusiniOS ISO** and click **Run workflow** (or push a change under `iso/`).
4. Wait for the workflow to finish successfully.
5. Open the completed workflow run and download the `jesusiniOS-bootable-ISO` artifact. Unzip that artifact to get the `.iso` file.

The workflow builds the current Debian/XFCE starter image. It does not yet replace XFCE with the custom browser desktop; that integration is a separate step. Builds can fail if Debian Live Build configuration or package availability changes, so inspect the Actions log if needed.
