

# Current Privacy, Data Protection, Security and Documentation Audit

# Auditoría actual de privacidad, protección de datos, seguridad y documentación

**Date of review:** September 21, 2026  
**Scope:** current implementation of the Rendifly Manager project.  
**Mode:** read-only audit. No files were modified during this review.  
**Criterion:** when there is a difference between documentation and code, the actual behavior of the implementation prevails.

**Fecha de revisión:** 21 de septiembre de 2026  
**Alcance:** implementación actual del proyecto Rendifly Manager.  
**Modo:** auditoría de solo lectura. No se modificó ningún archivo durante esta revisión.  
**Criterio:** cuando existe una diferencia entre la documentación y el código, prevalece el comportamiento real de la implementación.

---

## 1. Current Status Summary

## 1. Resumen del estado actual

Rendifly Manager currently functions as a local Windows application.

### Active Functions

The following functions are currently active:

- Local machine monitoring.
- Reading of CPU, RAM, GPU, storage, and battery.
- Reading of active processes.
- Reading of startup applications.
- Reading of drivers and Windows configurations.
- Reading of global network counters.
- Local preference management.
- Configuration storage in `%APPDATA%\Rendifly`.
- Rotating local logs.
- Local notification history.
- Autostart management via the Windows registry.
- Cleaning and optimization functions.
- Process management and termination.
- Controlled opening of configurations and external sites.
- Feedback via the user's mail client or Gmail.

### Currently Disabled Functions

External AI is disabled via:

`feature_flags.py`

```python
EXTERNAL_AI_ENABLED = False
```

While this flag remains disabled, the normal flow should not:

- Validate external API keys.
- Connect to Gemini.
- Connect to OpenAI-compatible providers.
- Send user questions to third parties.
- Send machine context to AI providers.
- Perform automatic web searches via DuckDuckGo.

### Functions Prepared for the Future

The code contains infrastructure for:

- Google Gemini.
- OpenAI-compatible providers.
- Web search with DuckDuckGo.
- Technical machine context for the assistant.
- HTTPS endpoint validation.
- Separate AI consent.
- Protection of API keys via Windows DPAPI.

These functions are prepared but are not available in the current normal flow because external integration remains disabled.

---

## 2. Privacy Policy

## 2. Política de privacidad

### 2.1 What the code actually does

The application currently does not use:

- A user account system.
- A proprietary user backend.
- A remote database.
- A proprietary analytics service.
- An advertising SDK.
- A proprietary telemetry service.
- A public Rendifly HTTP server.

The application processes local technical information about the machine and saves certain data in the user's profile.

Local collection is primarily performed in:

- `monitor.py`
- `metrics.py`
- `hardware/`
- `manager.py`
- `config.py`

The application can read system information, display it in the interface, and use it internally for recommendations and optimization functions.

### 2.2 Existing Documentation

The following exist:

- `PRIVACY.md`
- `TERMS.md`
- `LICENSE`
- `THIRD-PARTY-NOTICES.md`

The privacy policy states that:

- The application functions primarily locally.
- Technical data typically remains on the machine.
- There is no active centralized telemetry.
- External AI is disabled in the current version.
- Feedback may use external mail providers.

### 2.3 Differences between documentation and implementation

The documentation aligns with the current local architecture.

However, `PRIVACY.md` still contains placeholders for:

- Responsible name.
- Privacy email.
- Effective date.
- Legal review.
- Specific jurisdiction information.

Therefore, the documentation is technically consistent but is not yet ready for final public distribution.

### 2.4 What is missing

The following need to be completed:

- Real name of the responsible party.
- Responsible organization.
- Privacy email.
- Effective date.
- Jurisdiction.
- Retention policy.
- User rights.
- Access procedure.
- Deletion procedure.
- Export procedure.
- Complete information about feedback received by email.
- Legal review for markets where the application will be distributed.

### 2.5 Risks

- The user does not yet have a real contact point to exercise rights.
- The policy does not fully define retention periods.
- The future AI policy may become outdated if the feature is activated without updating the documentation.
- The policy must not be published with the current placeholders.

**Priority:** High before public distribution.

### 2.6 Recommended solution

Complete `PRIVACY.md` with real information about:

1. Data controller.
2. Contact details.
3. Data collected.
4. Purposes.
5. Legal basis, where applicable.
6. Retention.
7. Deletion.
8. Third-party providers.
9. International transfers.
10. User rights.
11. Effective date.
12. Change history.

---

## 3. EULA, Terms of Use, and License

## 3. EULA, términos de uso y licencia

### 3.1 What the code actually does

The application contains functions that can:

- Query hardware.
- Query processes.
- Terminate processes.
- Clean files.
- Modify startup configurations.
- Query and modify power options.
- Query Windows configurations.
- Open system configurations.
- Open authorized external sites.
- Manage profiles.
- Prepare feedback.
- Configure AI providers in future enabled versions.

There is currently no system that obligates the user to accept terms before opening the application or using its functions.

### 3.2 Existing Documentation

The following exist:

- `LICENSE`
- `TERMS.md`

The installer references both documents via:

`RendiflyManager.iss`

```ini
LicenseFile=..\LICENSE
InfoBeforeFile=..\TERMS.md
```

### 3.3 Match

The MIT license is present as a distributable file.

The terms of use exist but are still a draft because they contain placeholders for:

- Owner.
- Legal contact.
- Date.
- Jurisdiction.
- Specific legal conditions.

### 3.4 What is missing

The following need to be completed:

- Legal identity of the owner.
- Legal contact.
- Applicable jurisdiction.
- Beta version conditions.
- User responsibility for modifying Windows.
- Conditions regarding external services.
- Conditions regarding AI.
- Conditions regarding feedback.
- Legal notices for dependencies.

### 3.5 Risks

- The installer may display documents that are still incomplete.
- Responsibilities for cleaning or terminating processes are not fully defined.
- The Beta version does not yet have a final contractual framework.
- The user may interpret the MIT license as a substitute for the terms of use, although they serve different functions.

**Priority:** High.

### 3.6 Recommended solution

Complete `TERMS.md`, have it legally reviewed, and verify that the version shown by the installer is correct.

---

## 4. Data Collected by the Application

## 4. Datos recopilados por la aplicación

### 4.1 Hardware and system

The application can locally read:

- CPU.
- Number of cores.
- Number of threads.
- CPU usage.
- Total RAM.
- RAM used.
- GPU.
- Information from `nvidia-smi`, when available.
- Operating system.
- Up time.
- Temperatures.
- Battery status.
- Battery capacity.

Related files:

- `monitor.py`
- `cpu.py`
- `gpu.py`
- `battery.py`
- `ram.py`

### 4.2 Storage

The application can read:

- Drive letters.
- Capacity.
- Free space.
- Storage usage.
- Reads.
- Writes.

Related files:

- `storage.py`
- `monitor.py`

### 4.3 Processes and software

The application can read:

- Active processes.
- Process names.
- Memory consumption.
- Process status.
- Startup applications.
- Driver information.
- Some Windows configurations.

Related files:

- `manager.py`
- `startup.py`
- `drivers.py`
- `windows_config.py`

### 4.4 Network

The application can read aggregated global counters:

- Bytes sent.
- Bytes received.

It was not confirmed that it reads:

- Packet content.
- Browsing history.
- Visited domains.
- Communication content.
- All destination addresses.

Related files:

- `network.py`
- `metrics.py`

### 4.5 User-entered data

The application can receive:

- Name entered during onboarding.
- Preferences.
- Language.
- Theme.
- Color.
- Monitoring preferences.
- Notification configuration.
- Assistant configuration.
- Text written in feedback.
- Name of a selected screenshot.
- Assistant questions.

### 4.6 Documentation match

The documentation generally describes monitoring of CPU, RAM, GPU, disk, and battery.

It does not fully enumerate:

- Processes.
- Startup applications.
- Drivers.
- Network counters.
- Temperatures.
- Queries to `nvidia-smi`.
- All data that would be part of the AI context if enabled.

**Priority:** Medium for local use.  
**Priority:** High if this data is sent to third parties.

### 4.7 Recommended solution

Add a formal inventory table:

| Category | Data | Purpose | Persistence | Leaves the machine currently? |
|---|---|---|---|---|
| Hardware | CPU, RAM, GPU, battery | Display machine status | Mainly memory | No |
| Storage | Capacity and free space | Display disk usage | Mainly memory | No |
| Processes | Name and memory | Management and explanation | Memory and possible logs | No |
| Configuration | Preferences and status | Personalization | Local JSON | No |
| Feedback | Type, detail, and text | Support | Mail client | Only if the user sends |
| External AI | Question and technical context | External response | According to provider | Currently disabled |

---

## 5. Locally Stored Data

## 5. Datos almacenados localmente

### 5.1 Location

The application uses:

```text
%APPDATA%\Rendifly
```

Persistence is managed via:

- `app.py`
- `persistence.py`

### 5.2 Identified files

The code uses the following files:

- `settings.json`
- `runtime.json`
- `notification_history.json`
- `rendifly.log`
- Rotating log backups.
- Temporary files used for atomic saves.

### 5.3 Stored data

The following may be stored:

- User name.
- Preferences.
- Language.
- Theme.
- Color.
- Autostart.
- Start minimized.
- Tray preferences.
- Monitoring intervals.
- Monitoring history.
- Notifications.
- Profiles.
- Onboarding status.
- AI provider status.
- Validation status.
- AI consent.
- DPAPI-protected API key.
- Notification history.
- Errors and application traces.

### 5.4 API key protection

The API key is protected via Windows DPAPI in:

`config.py`

The protected API key is not returned to the interface in:

`api.py`

The configuration uses temporary writing and atomic substitution in:

`persistence.py`

### 5.5 Data deletion

A function exists to clear local data:

`config.py`

An exposed API also exists:

`api.py`

The function attempts to delete files from the data directory and reset in-memory configuration.

### 5.6 Limitations

Local deletion:

- Is not low-level secure deletion.
- Cannot delete external backups.
- Cannot delete OS backups.
- May leave files locked if an error occurs.
- Does not set custom ACLs.
- Does not encrypt all logs or all configuration files.

**Priority:** Medium.

### 5.7 Recommended solution

Document:

- Each file.
- Its purpose.
- Retention.
- Deletion method.
- DPAPI dependency.
- Deletion limitations.
- Behavior on uninstall.
- Behavior on preserving data during an update.

---

## 6. Data Sent to the Internet

## 6. Datos enviados a Internet

### 6.1 Proprietary services

No proprietary server was found:

- No Rendifly HTTP server.
- No central Rendifly API.
- No remote database.
- No user account system.
- No analytics service.
- No proprietary telemetry service.

### 6.2 External destinations present in the code

The code contains references to:

- Google Gemini.
- OpenAI-compatible providers.
- DuckDuckGo HTML.
- Gmail.
- Mail client via `mailto:`.
- Official Microsoft sites.
- Manufacturer sites.
- Windows configuration URIs.

Related files:

- `provider.py`
- `gemini_client.py`
- `openai_client.py`
- `api.py`

### 6.3 Current AI status

External integration is blocked by:

`feature_flags.py`

When disabled, the configuration and validation functions return a `coming_soon` equivalent status.

Currently, the following should not occur:

- Sending questions to Gemini.
- Sending questions to OpenAI-compatible providers.
- Sending hardware to external providers.
- Sending processes.
- Automatic web searches.

### 6.4 Internet feedback

Feedback is not sent to a Rendifly server.

The application prepares:

- A `mailto:` message.
- A Gmail composition.

The user must review and manually send the message.

### 6.5 Future risks

If AI is activated without additional controls, the following could be sent:

- User questions.
- Hardware context.
- Operating system.
- Processes.
- RAM.
- Disks.
- Battery.
- Temperatures.
- Machine metrics.

Although the code already separates validation and consent, before activating the function, the entire visual consent experience must be verified.

**Priority:** High before activating AI.  
**Priority:** Medium while AI remains disabled.

### 6.6 Recommended solution

Before activating AI:

- Keep it disabled by default.
- Show a specific notice.
- Show the provider.
- Show the endpoint.
- Show the model.
- Show the categories to be sent.
- Allow sending only the question.
- Allow disabling process context.
- Allow disabling hardware context.
- Allow disabling storage context.
- Document retention.
- Document international transfers.
- Document data use by providers.
- Show links to external policies.

---

## 7. Feedback System

## 7. Sistema de feedback

### 7.1 Actual behavior

The frontend requests:

- Problem type.
- Detail.
- Description.
- Optional screenshot selection.

Implementation:

- `feedback.js`
- `api.py`

The email body includes:

- Problem type.
- Detail.
- Description.
- Name of the selected screenshot.

### 7.2 Screenshots

The screenshot:

- Is not read.
- Is not processed.
- Is not automatically attached.
- Is not sent to a server.
- Only its name is included in the message.

### 7.3 Sending

The user can use:

- The default mail client.
- Gmail.

The user must review and manually send the message.

### 7.4 Existing documentation

The interface indicates that comments are used for:

- Analysis.
- Troubleshooting.
- Improving the experience.

It also recommends not including personal information.

### 7.5 Documentation differences

The interface does not clearly explain:

- That an external application will open.
- That the message is not sent automatically.
- That the screenshot is not attached.
- Who will receive the message.
- How long it is retained.
- How to request deletion.
- What data should be avoided.

### 7.6 Risks

The user may accidentally include:

- Passwords.
- API keys.
- Tokens.
- Local paths.
- Usernames.
- Private file names.
- Corporate information.
- Personal data.

**Priority:** Medium.

### 7.7 Recommended solution

Show a notice such as:

> A message will be prepared for `rendiflypcmanager@gmail.com`. The message will not be sent automatically. The selected screenshot is not currently attached; only its name will be included. Do not include passwords, tokens, API keys, personal information, or confidential data.

---

## 8. Logs and Diagnostics

## 8. Logs y diagnósticos

### 8.1 Actual behavior

Logs are saved to:

```text
%APPDATA%\Rendifly\rendifly.log
```

Implementation is in:

`logging_service.py`

Characteristics:

- Log rotation.
- Approximately 5 MB per file.
- Up to three backups.
- Error logging.
- Exception logging.
- Full tracebacks via `exc_info`.

### 8.2 Information that may appear

Depending on the error, logs may include:

- Local paths.
- File names.
- Process names.
- Modules.
- Endpoints.
- System details.
- Messages from external libraries.

No routine logging of the following was observed:

- Full API keys.
- Full prompts.
- Full assistant responses.
- Screenshot content.

### 8.3 Notification history

History is managed in:

`notifications.py`

It can store:

- Title.
- Message.
- Type.
- Icon.
- Date.
- Read status.

### 8.4 Existing documentation

The documentation mentions the log location but does not clearly define:

- Temporal retention.
- Automatic deletion.
- Exact content.
- Redaction.
- Access from other processes.
- Difference between development and production logs.

### 8.5 Risks

Rotation limits size but does not set a retention period.

Logs may reveal technical details of the machine to other processes running under the same user.

**Priority:** Medium.

### 8.6 Recommended solution

- Define time-based retention.
- Redact paths.
- Redact sensitive data.
- Avoid logging complete objects.
- Add deletion from the interface.
- Delete all backups when clearing data.
- Add tests ensuring API keys never appear in logs.
- Separate development and production logs.

---

## 9. User Configuration

## 9. Configuración del usuario

### 9.1 Configurable data

Configuration may contain:

- Name.
- Preferences.
- Language.
- Theme.
- Color.
- Windows startup.
- Start minimized.
- Minimize to tray.
- Close to tray.
- Monitoring interval.
- Monitoring history.
- Notifications.
- AI provider.
- `validated` status.
- `allow_ai` status.
- Onboarding status.
- Profiles.
- Runtime.
- `send_diagnostics`.

Evidence:

`config.py`

### 9.2 Privacy status

Initial configuration sets:

```python
"allow_ai": False
"send_diagnostics": False
"validated": False
```

The code separates:

- Technical provider validation.
- Consent for external use.

Implemented in:

- `config.py`
- `api.py`

### 9.3 Risks

- The user may not distinguish between configuring an API key and permitting transfers.
- `send_diagnostics` exists, but no functional sending flow was found.
- Preferences may survive a reinstall.
- Data may remain in OS backups.

**Priority:** Medium.

### 9.4 Recommended solution

- Show the status of each option.
- Show what data is stored.
- Show what data leaves the machine.
- Add export.
- Add selective deletion.
- Mark `send_diagnostics` as unavailable while its implementation is missing.
- Clearly inform when an option affects external transfers.

---

## 10. Consent and Transparency

## 10. Consentimiento y transparencia

### 10.1 Existing controls

The following currently exist:

- `allow_ai=False` by default.
- Global feature flag disabled.
- Function to grant consent.
- Function to revoke consent.
- Separation between `validated` and `allow_ai`.
- Future functionality message when AI is disabled.
- Feedback initiated manually by the user.

### 10.2 Pending aspects

A full screen was not verified that shows, before the first transfer:

- Provider.
- Endpoint.
- Model.
- Data categories.
- Purpose.
- Retention.
- International transfers.
- Links to external policies.
- Revocation mechanism.

### 10.3 Risks

The current configuration is conservative, but transparency would be insufficient if AI were enabled without expanding the interface.

**Priority:** High before activating AI.  
**Priority:** Medium while it remains disabled.

### 10.4 Recommended solution

Implement a flow that:

1. Shows the data that would be sent.
2. Shows the provider.
3. Shows the endpoint.
4. Allows accept or cancel.
5. Allows category selection.
6. Saves the accepted version of the notice.
7. Allows revocation of consent.
8. Shows consent status in Settings.

---

## 11. Permissions and System Access

## 11. Permisos y acceso al sistema

### 11.1 Functions with system access

The application uses:

- `psutil`.
- WMI.
- Windows registry.
- `powercfg`.
- Process APIs.
- Battery APIs.
- Hardware APIs.
- Temporary file access.
- `HKCU` registry.
- Cleaning functions.
- Process termination functions.
- Shortcut creation.
- Installation in `Program Files`.

Autostart uses:

```text
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run
```

### 11.2 Installer

The installer requires administrator:

`RendiflyManager.iss`

```ini
PrivilegesRequired=admin
```

No evidence was found that the main application requires permanent elevation throughout its execution.

### 11.3 Good practices present

- Configuration is stored outside `Program Files`.
- Autostart uses HKCU.
- Reviewed process calls use `shell=False`.
- External URIs are restricted.
- No local HTTP server was confirmed.
- No arbitrary command execution from direct user input was confirmed.

### 11.4 Risks

The application can:

- Terminate processes.
- Change power settings.
- Modify the registry.
- Delete files.
- Change startup applications.

The user needs clear information before performing actions with persistent or destructive effects.

**Priority:** Medium.

### 11.5 Recommended solution

Document:

- What permissions each function requires.
- What actions require administrator.
- What actions are reversible.
- What processes can be terminated.
- What files can be deleted.
- What registry changes are made.
- How to undo each change.
- What functions are optional.

---

## 12. WebView2 Bridge and Frontend Security

## 12. Seguridad del puente WebView2 y frontend

### 12.1 Actual behavior

The application exposes a JavaScript-Python bridge via pywebview:

`app.py`

The frontend can invoke native methods related to:

- Hardware.
- Processes.
- Cleaning.
- Configuration.
- Power.
- Registry.
- AI.
- Feedback.
- Opening external resources.

### 12.2 Improvements made

The rendering of assistant content was fixed in:

`assistant.js`

Content is now escaped before insertion into HTML.

URL sources are also filtered and HTML attributes escaped.

### 12.3 Remaining risks

- The bridge exposes many native functions.
- Security depends on loading only trusted local content.
- A complete CSP was not verified.
- External navigation must remain restricted.
- Destructive functions need visible confirmation.

**Priority:** Medium.

### 12.4 Recommended solution

- Apply a strict Content Security Policy.
- Do not load remote content in the main view.
- Separate destructive APIs.
- Confirm sensitive actions.
- Use specific methods instead of a generic URI API.
- Keep WebView2 updated.
- Reduce the JavaScript-Python bridge surface.

---

## 13. Installer Security

## 13. Seguridad del instalador

### 13.1 Actual behavior

The installer uses Inno Setup.

Characteristics:

- Installs in `Program Files`.
- Requires administrator.
- Can create shortcuts.
- Can start the application after installation.
- Shows the license.
- Shows the terms.
- Allows preserving or deleting data on uninstall.

Files:

- `RendiflyManager.iss`
- `build-installer.ps1`

### 13.2 Digital signature

`Rendifly.spec` contains:

```python
codesign_identity=None
```

The build script allows signing via environment variables, but signing is not configured by default.

No evidence of signing was applied to:

- The executable.
- The installer.
- The uninstaller.

### 13.3 Hashes

The script generates SHA-256 hashes for:

- Installer.
- Executable.

This improves integrity verification, but a hash without a signature does not guarantee authenticity.

### 13.4 Build artifacts

The tree contains multiple historical build and distribution directories.

This can cause:

- Confusion between builds.
- Accidental packaging of old artifacts.
- Difficulty verifying which binary corresponds to the current code.
- Risk of distributing an unvalidated executable.

**Priority:** High before public distribution.

### 13.5 Current limitations

- `ISCC.exe` is not installed in the reviewed environment.
- A new installer was not generated during this audit.
- An Authenticode signature was not verified.
- The owner, support, and update URLs in the installer are still placeholders.
- Existing binaries should not be automatically considered equivalent to the current code.

### 13.6 Recommended solution

- Use a clean directory for each release.
- Clean previous builds.
- Sign the executable, installer, and uninstaller.
- Publish hashes alongside the signature.
- Verify signatures before publishing.
- Generate an SBOM.
- Keep distribution artifacts separate from the development tree.

---

## 14. Updates

## 14. Actualizaciones

### 14.1 Actual status

No automatic updater is currently confirmed.

The following were not found:

- Automatic version check.
- Automatic download.
- Silent installation.
- Rollback.
- Signature verification.
- Integrated beta channel.
- Downgrade protection.

The installer's stable `AppId` allows future installations to be identified as the same application, but this is not equivalent to a proprietary updater.

### 14.2 Documentation

The README describes preserving preferences during reinstalls and updates, but does not document an automatic update system.

### 14.3 Risk

There is no active risk of an insecure updater because the updater is not implemented.

If implemented without cryptographic controls, it could become a path for executing untrusted code.

**Priority:** Medium currently.  
**Priority:** High when implemented.

### 14.4 Recommended solution

Design future updates with:

- HTTPS.
- Signed manifest.
- Hashes.
- Authenticode signature.
- Downgrade protection.
- Verification before execution.
- Rollback.
- Visible user confirmation.
- Installed version logging.

---

## 15. External AI

## 15. IA externa

### 15.1 Current status

External AI is disabled via:

`feature_flags.py`

The API returns a future functionality status when attempting to configure or validate the provider:

`api.py`

### 15.2 Prepared code

Code exists for:

- Gemini.
- OpenAI-compatible.
- DuckDuckGo search.
- Machine context construction.
- Provider validation.
- Model configuration.
- API key management.

Files:

- `gemini_client.py`
- `openai_client.py`
- `provider.py`
- `engine.py`

### 15.3 Implemented protections

- AI is disabled by default.
- Consent is separate from validation.
- Endpoints must use HTTPS.
- Local hosts are rejected.
- Private IPs are rejected.
- Credentials embedded in URLs are rejected.
- The API key is protected via DPAPI.
- The API key is not returned to the frontend.
- Web search does not automatically receive the full machine context.
- The technical context is no longer described as "anonymized".

### 15.4 Risk

The technical machine context may include identifiable or sensitive information even if it does not directly include the user's name.

For this reason, it must not be described as anonymized by default.

**Priority:** High before activating AI.

### 15.5 Recommended solution

Before activating AI:

- Show a preview of the context.
- Send only selected fields.
- Disable process context by default.
- Disable drive letters by default.
- Offer a "question-only" mode.
- Document providers.
- Document retention.
- Document international transfers.
- Show a warning before the first transfer.
- Allow easy revocation of consent.

---

## 16. Dependencies and Supply Chain

## 16. Dependencias y cadena de suministro

### 16.1 Current status

The following exists:

`requirements-lock.txt`

This file contains fixed versions of the current build environment.

Also present:

`requirements.txt`

which maintains dependencies with minimal constraints.

### 16.2 Improvement made

The lockfile allows more precise reproduction of the environment used for a build.

### 16.3 Limitations

The lockfile:

- Is a snapshot of the current environment.
- Includes development and build dependencies.
- Does not include package hashes.
- Is not equivalent to an installation with `--require-hashes`.
- Is not a formal SBOM.
- Does not by itself demonstrate that the existing binary was generated exactly with those versions.

**Priority:** Medium.

### 16.4 Recommended solution

- Separate runtime and build dependencies.
- Add hashes.
- Generate an SBOM.
- Run vulnerability analysis.
- Record versions included in each release.
- Maintain a reproducible build process.

---

## 17. User Transparency

## 17. Transparencia para el usuario

### Current status

The application partially informs about:

- Monitoring.
- Local storage of the name.
- Future AI status.
- Feedback.
- Local configuration.

Information is still needed about:

- Collected processes.
- Startup applications.
- Drivers.
- Global network counters.
- Logs.
- Retention.
- Deletion.
- Feedback recipient.
- That screenshots are not attached.
- The difference between validating an API key and permitting sends.
- External providers.
- International transfers.

**Priority:** High before public distribution.

### Recommended solution

Add visible information in:

- Onboarding.
- Settings.
- Assistant page.
- Feedback page.
- Installer.
- Documentation for each release.

---

## 18. Priority Summary

## 18. Resumen de prioridades

| Priority | Area | Current status |
|---|---|---|
| High | Privacy policy | Exists, but contains placeholders |
| High | EULA and terms | Exists, but not legally finalized |
| High | External AI | Disabled; requires full consent before activation |
| High | Signed installer | Not configured by default |
| High | Transparency | Partial |
| Medium | Logs | Active and rotating, no temporal retention defined |
| Medium | Local deletion | Implemented, but not secure deletion |
| Medium | Feedback | Manual and non-silent, but with incomplete information |
| Medium | Windows permissions | Functional, but a permission matrix is missing |
| Medium | WebView2 | Improved escaping, but complete CSP missing |
| Medium | Dependencies | Lockfile present, hashes and SBOM missing |
| Medium | Updates | No updater currently exists |
| Low | `send_diagnostics` | Field present, but no functional sending confirmed |

---

## 19. Verified Limitations

## 19. Limitaciones verificadas

The following limitations remain:

1. `PRIVACY.md` contains legal placeholders.
2. `TERMS.md` contains legal placeholders.
3. The owner, support, and update URLs in the installer are not final.
4. `ISCC.exe` is not available in the reviewed environment.
5. Authenticode signing is not configured by default.
6. `codesign_identity=None` remains in `Rendifly.spec`.
7. The automatic updater is not implemented.
8. A new installer compilation was not verified during this audit.
9. It was not verified that existing binaries match byte-for-byte the current code.
10. A formal SBOM was not generated.
11. The lockfile does not use package hashes.
12. There is no detailed temporal log retention policy.
13. A complete CSP for WebView2 was not confirmed.

---

## 20. Document Conclusion

## 20. Conclusión documental

The current state of Rendifly Manager is that of a mainly local Windows application:

- Monitoring is active locally.
- Configuration is stored locally.
- Logs are stored locally.
- Notification history is stored locally.
- No proprietary telemetry was found.
- No central Rendifly backend exists.
- Feedback requires manual user action.
- External AI is prepared in the code but currently disabled.
- API keys are protected via DPAPI when the feature is enabled.
- Provider validation and consent are separate.
- External endpoints are validated to require HTTPS.
- Assistant content is escaped before insertion into HTML.
- The installer shows the license and terms.
- The script generates SHA-256 hashes.
- Authenticode signing is still not configured.
- Legal documentation still needs to be completed with the real owner's data.
- Beta 2 is not published or uploaded.

### Status for Beta 2

**Technical improvements implemented locally:** Yes.  
**Updated privacy audit:** Yes.  
**Legal documentation created:** Yes.  
**Legal documentation finalized:** No, contains placeholders.  
**Installer recompiled and verified:** No.  
**Installer signed:** No.  
**Beta 2 published:** No.  
**Beta 2 uploaded:** No.
