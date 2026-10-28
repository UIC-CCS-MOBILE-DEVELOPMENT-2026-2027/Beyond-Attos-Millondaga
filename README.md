Beyond Flutter Project — Run on Web Server Port 8080
This guide explains how to run the Beyond Flutter project in a browser while the team is still developing the mobile app. The project includes Flutter web files in the web/ folder, so you can run it as a web app without building an Android or iOS app first.
Important: Port 8080 is the development server port. This does not automatically publish the system publicly on the internet. It makes the app available on the computer or development environment running Flutter, and it may be shared through a LAN or a development environment's port-forwarding feature.

1. Requirements
Install or prepare the following:
- Flutter SDK, with a version compatible with the Dart SDK requirement in pubspec.yaml (^3.13.5).
- Git, if you need to clone the repository.
- VS Code or another terminal/editor (optional but recommended).
- A modern browser such as Chrome or Edge.
Open a terminal and verify Flutter is installed:
flutter --version
flutter doctor
If flutter is not recognized, install the Flutter SDK and add its bin directory to your system PATH, then reopen the terminal.
2. Get the project
If you have not cloned the repository yet, navigate to the folder where you want to keep the project and clone it:
git clone https://github.com/UIC-CCS-MOBILE-DEVELOPMENT-2026-2027/Beyond-Attos-Millondaga.git
cd Beyond-Attos-Millondaga
If the repository is already on your computer, open a terminal in the project root instead. The project root is the folder containing pubspec.yaml, lib/, and web/.

For example, on Windows Command Prompt, if the project is in Documents:
cd "C:\Users\My PC\Documents\Beyond-Attos-Millondaga"
Check that you are in the correct folder:
dir
On Windows Command Prompt, dir should show pubspec.yaml, lib, and web. On macOS/Linux, use ls.
3. Download the Flutter dependencies
Run this from the project root:
flutter pub get
Wait for it to finish. If it fails, read the error message; a common cause is an outdated Flutter SDK that does not meet the Dart SDK version specified in pubspec.yaml.
4. Start the web server on port 8080
Run:
flutter run -d web-server --web-hostname 0.0.0.0 --web-port 8080
Keep this terminal open while using the system. Flutter will print a local URL, usually similar to:
http://localhost:8080
Open that address in your browser. If Flutter prints a different URL, use the URL shown in the terminal.
If you only need access from the same computer
You can also run:
flutter run -d web-server --web-port 8080
Then open http://localhost:8080 in your browser.
5. Open the app from another device on the same Wi-Fi (optional)
If you started Flutter with --web-hostname 0.0.0.0, find the IP address of the computer running the server.

On Windows, open a second Command Prompt and run:
ipconfig
Find the active Wi-Fi or Ethernet adapter's IPv4 Address, for example 192.168.1.25. On another device connected to the same network, open:
http://192.168.1.25:8080
Replace the example IP with the actual IPv4 address. If it does not load, check that both devices are on the same network and that the computer's firewall allows the connection. Do not expose the development server to an untrusted public network.
6. If you are using GitHub Codespaces or another cloud development environment
1. Run the command from Step 4 in the Codespaces terminal.
2. Open the Ports panel in VS Code/Codespaces.
3. Find port 8080. If it is not listed, add/forward port 8080.
4. Open the forwarded address provided by Codespaces.
5. If a teammate needs access, set the port visibility according to your class/team policy. Do not make it public unless that is intended and permitted.
The cloud environment's forwarded URL is different from http://localhost:8080 on your personal computer. Use the URL shown by the environment.
7. Stop the server
Return to the terminal where Flutter is running and press:
Ctrl + C
This stops the development server.
8. Run it again later
Whenever you want to start the project again:
1. Open a terminal in the project root (the folder containing pubspec.yaml).
2. Run flutter pub get if dependencies have changed or have not been installed.
3. Run:
   flutter run -d web-server --web-hostname 0.0.0.0 --web-port 8080
4. Open the local or forwarded URL in a browser.
9. Troubleshooting
flutter is not recognized
Flutter is not installed correctly or its bin folder is not in PATH. Install/configure Flutter, reopen the terminal, and run flutter --version again.
No supported devices or web-server is unavailable
Run:
flutter devices
flutter doctor
Confirm that the Flutter SDK is installed correctly and that the web platform is available in the SDK. Update the Flutter SDK if needed and rerun the checks.
Port 8080 is already in use
Stop the other process using port 8080, or use another port, such as 8081:
flutter run -d web-server --web-hostname 0.0.0.0 --web-port 8081
Then open the URL for port 8081.
The page does not load or shows an error
- Confirm the Flutter command is still running.
- Open the exact URL printed in the terminal or the forwarded URL shown by Codespaces.
- Check the terminal for compilation errors.
- Try a hard refresh in the browser.
- If the app fails to compile, copy the first relevant error from the terminal and resolve it before retrying.
The project works on mobile but not in a browser
Not every Flutter plugin or platform-specific feature supports web. Check the error and confirm that any packages or code used by the project support Flutter web. This project currently uses Flutter's standard UI framework and Cupertino icons in its declared dependencies, but future additions may need web-specific checks.
10. Notes about the current setup
- The browser version runs the Flutter UI from the project's lib/ code using Flutter web support.
- Running on port 8080 does not require a separate Node.js/Express server for this Flutter-only project as currently configured.
- This command starts a development server; it is not the same as deploying a production website. For a static web build, use flutter build web and deploy the generated build/web/ files to a suitable web host.
- If the team later adds a separate backend/API, that backend may need its own server and port. Port 8080 in this guide is for the Flutter web development server only.
