# PhishNet v2: Public Release

PhishNet v2 is an anti-phishing extension for Chromium browsers. It examines the address of each web page that you open. PhishNet does all checks on your computer. It does not send an address to a server for a check. Protection starts immediately after installation.

This repository contains the public release of version 2.2.0:

| File | Contents |
| --- | --- |
| [`phishnet-2.2.0.zip`](phishnet-2.2.0.zip) | The compiled extension, ready to load unpacked |
| [`PhishNet-v2-Download-and-Installation-Manual.pdf`](PhishNet-v2-Download-and-Installation-Manual.pdf) | The full download and installation manual |
| [`PhishNet-v2-Download-and-Installation-Manual.docx`](PhishNet-v2-Download-and-Installation-Manual.docx) | The same manual as a Word document |
| [`.github/workflows/release.yml`](.github/workflows/release.yml) | Publishes a release (for maintainers) |

## How PhishNet examines an address

1. PhishNet compares the address to five public threat feeds (OpenPhish, ValidIn, PhishTank, PhishStats, and URLhaus) and to the community blacklist. If a list contains the address, PhishNet stops the page before it opens.
2. If no list contains the address, an on-device Random Forest classifier calculates a risk score from the address. If the score is in the Caution band, a warning shows on top of the page. The classifier alone never stops a page.

PhishNet uses no account and no API key.

## Requirements

| Item | Requirement |
| --- | --- |
| Browser | Google Chrome, Microsoft Edge, Brave, Opera, or Vivaldi. Version 116 or later. |
| Operating system | Windows, macOS, or Linux. |
| Disk space | Approximately 22 MB. |
| Internet connection | Necessary for the first download of the threat feeds (approximately 14 MB for PhishTank alone). |

Firefox is not supported in version 2.2.0.

## Install

The manual gives each step with its expected result, and with screenshots.

1. Download `phishnet-2.2.0.zip` from the [Releases page](https://github.com/aaron-c-s-ramos/PhishNet-v2-Public-Release/releases), or from the file list above. Do not download **Source code (zip)**, because it does not contain the extension folder.
2. Make a folder that you will keep, for example `C:\PhishNet`. Extract the contents of the ZIP file into it. Make sure that `manifest.json` is directly in the folder.
3. Open the extensions page of your browser:

   | Browser | Address |
   | --- | --- |
   | Google Chrome | `chrome://extensions` |
   | Microsoft Edge | `edge://extensions` |
   | Brave | `brave://extensions` |
   | Opera | `opera://extensions` |
   | Vivaldi | `vivaldi://extensions` |

4. Set **Developer mode** to on. Click **Load unpacked**, then select the folder.
5. Pin PhishNet to the toolbar: click the extensions icon (a puzzle piece in Chrome and Edge), then click the pin icon.
6. On the **PhishNet** card, click **Details**. Set **Allow in Incognito** to on (**Allow in InPrivate** in Edge). If this switch is off, PhishNet does not examine pages in private windows.
7. Click the PhishNet icon, then the **Threat feeds** tab. Wait approximately one minute for the first download of the feeds.

**Caution:** Do not move, rename, or delete the folder after the installation. The browser loads the extension from that folder each time it starts.

## Update

1. Download the newer ZIP file from the Releases page.
2. Delete all files in your PhishNet folder, but keep the folder.
3. Extract the newer ZIP file into the same folder.
4. On the extensions page, click the reload icon on the **PhishNet** card.

## Remove

1. On the extensions page, click **Remove** on the **PhishNet** card, then click **Remove** again.
2. Delete the PhishNet folder.

## Troubleshooting

| Problem | Remedy |
| --- | --- |
| The **Load unpacked** button does not show. | Set **Developer mode** to on. |
| "Manifest file is missing or unreadable" | Select the folder that contains `manifest.json` directly. |
| PhishNet is gone after a restart of the browser. | Put the folder back, or load the extension again from its new location. |
| Private windows show no warnings. | Set **Allow in Incognito** to on. |
| A feed shows no entries after one minute. | Click **Refresh now**. Make sure that your network does not block `raw.githubusercontent.com`, `openphish.com`, `data.phishtank.com`, `phishstats.info`, or `urlhaus.abuse.ch`. |

The manual has the full troubleshooting table.

## Privacy

- PhishNet tests each address on your computer. No address and no feature vector leaves the device.
- Community reporting is off in this release, because it needs a community gateway. Without a gateway, PhishNet sends nothing.
- A report, when a gateway is set, contains only a hashed installation identifier, the address, and the time.

## Verify the download

The SHA-256 checksum of `phishnet-2.2.0.zip` is:

```
d83e3c47fa3a218784c78016748712f06efa6da22c2c5b8284dae1324f248d7f
```

On Windows, open PowerShell in the download folder and type `Get-FileHash phishnet-2.2.0.zip`. On macOS or Linux, type `shasum -a 256 phishnet-2.2.0.zip`.

## Publish a new release (maintainers)

1. Put the new `phishnet-<version>.zip` from the PhishNet v2 project in the root of this repository. Update the manual and this README if necessary. Commit to `main`.
2. Start the Release workflow in one of two ways:
   - From your own computer, push a tag: `git tag v<version>`, then `git push origin v<version>`.
   - In the web interface, open **Actions** > **Release** > **Run workflow**, select `main`, and type the version without the `v`, for example `2.3.0`. The run makes the tag itself.
3. The run does a check of the ZIP file. The file must exist, must be a valid archive, and its `manifest.json` must have the same version. Then the run publishes the release with the ZIP file attached.

The run stops when a release for that version already exists.
