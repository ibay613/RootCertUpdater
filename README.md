
# Windows Root Certificate Updater (Standalone / No PowerShell)

A lightweight, standalone utility to update Trusted Root Certificates and Disallowed Certificates on Windows systems (XP through 11). This tool fixes connection errors on modern websites (e.g., "Certificate Invalid" or "Connection Untrusted") caused by outdated or missing Root CAs.

**Key Differentiator:** Unlike most modern solutions, **this tool does NOT require PowerShell.** It is written in AutoIt and compiles to a native executable, making it perfect for legacy environments, stripped-down OS installations, or systems where PowerShell is broken or disabled.

### 🚀 Key Features

*   **Zero Dependencies:** Runs without PowerShell, .NET Framework updates, or external runtimes.
*   **Legacy Support:** Works on **Windows XP, Vista, 7**, 8, 10, and 11.
*   **Automatic TLS 1.2 Fix:** Automatically enables TLS 1.2 registry keys if **Windows 7** is detected, allowing native applications (like IE/Chrome) to access modern secure sites.
*   **Direct Microsoft Downloads:** Fetches the official `authroot.stl` and `disallowedcert.stl` directly from Windows Update servers.
*   **Three Operation Modes:**
    1.  **Online Mode:** Download and install immediately.
    2.  **Offline Mode:** Install from existing files (useful for air-gapped or non-networked machines).
    3.  **Download Only:** Fetch files to transport to another machine.

### 🛠 How It Works

1.  **Download:** The tool connects to the Microsoft content delivery network to grab the standard Certificate Trust Lists (CTLs) in `.stl` format.
2.  **Conversion:** It renames the containers to `.sst` (Serialized Store) format, bypassing the need for complex CAB extraction logic found in other scripts.
3.  **Installation:**
    *   It uses the native Windows `certutil` command to import the certificates into the System Root Store.
    *   On Windows 7, it additionally writes the required `SecureProtocols` registry entries to force TLS 1.2 activation.

### 📋 Usage

1.  Run the executable (`RootCertUpdater.exe`).
2.  **To Update Current Machine:** Select **"Online Mode"** and click **"Update Certificates"**.
3.  **To Update an Offline Machine:**
    *   Run the tool on the offline machine and select **"Offline Mode"**.
    *   Certs have already been downloaded and will be installed **

### ⚠️ Compatibility Note for Windows XP
While this tool successfully updates the Certificate Store on Windows XP, the operating system itself lacks the cryptographic libraries for modern protocols (TLS 1.2/1.3).
*   **IE/Chrome on XP:** Will still fail on most modern sites even after this update.
*   **Solution:** Use this tool to fix system trust, but browse with a modern fork like **Supermium** or **MyPal** to handle the encryption.[Rootcertupdater.zip](https://github.com/user-attachments/files/23815017/Rootcertupdater.zip)
