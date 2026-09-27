# comistian · Cosmic Titan

**Native optical design, 3D assembly, and scientific simulation.**

comistian brings optical components, node-based optical paths, 3D assemblies, and numerical experiments into one workspace. It helps students, educators, and researchers build models, adjust parameters, compare results, and preserve the data behind their analysis.

The project includes the **Cosmic Titan desktop application** and **cosmic titan mobile**. Each uses a separate native application project, with compatible `.titan` project structures and interfaces adapted to its platform.

## Overview

| Item | Details |
| --- | --- |
| Platforms | macOS and iPadOS |
| Minimum OS | macOS 14.0 / iPadOS 17.0 |
| Recorded project versions | Desktop: 1.0.0, Build 20; mobile: 1.0.0, Build 1 |
| Interface languages | English and Simplified Chinese |
| Technologies | Swift, SwiftUI, AppKit, UIKit, SceneKit, Charts |
| Project format | `.titan`, based on JSON |
| Processing | Core calculations run locally |
| Account requirements | No account required for core functionality |

## Features

### Node-Based Optical Design

Build optical paths by connecting components such as lenses, mirrors, beam splitters, filters, fibres, and detectors.

- Arrange nodes on a visual canvas.
- Connect output and input ports to create detector branches.
- Edit component specifications and propagation distances.
- Delete connections independently of components.
- Hide or remove nodes and revise designs with undo and redo.
- Inspect branch throughput, spot information, and supported analysis results.

Canvas positions control presentation. Physical propagation distances are defined by connection parameters, not by the length of a line on screen.

### 3D Physical Assembly

Inspect component placement and geometric rays in a three-dimensional workspace.

- Edit position, yaw, and pitch.
- Apply movement constraints, snapping, and position locks.
- Use camera presets, focus, rotation, and zoom controls.
- Align components and compare compatible replacement candidates.
- Add observation planes to inspect ray intersections and crossing power.
- Check supported energy accounting and sampling convergence.
- Collapse the mobile assembly panel to give the scene more space.

The assembly uses its corresponding spatial geometric model. A rendered component, a paraxial node calculation, and an independent wave experiment do not automatically represent the same physical solution.

### Optical and Numerical Experiments

The workspace organizes 36 module entries into five categories:

| Category | Modules |
| --- | --- |
| Design & Assembly | Node Workspace, Physical Assembly, Instrument Design, Sources & Spectrum |
| Rays & Imaging | ABCD Network, Non-sequential Tracing, 2D Angular Spectrum, Transmissive Design, Lyot Coronagraph, Filters & Thermal Background, Dielectric Coatings, Telescope Design, Surface Tracing, Optical Workbench, Imaging & Wavefront, 2D Diffraction |
| Fibres & Fields | FDTD Ports, Integrated Photonics AWG, IFU Calibration Reconstruction, Hexagonal IFU, Photonic Lantern, Fibre Gratings, Fibres & IFU, Wave Propagation, Numerical Laboratory |
| Instruments & Detection | Cross Dispersion, Wavefront Calibration, Mechanical Checks, Detector Readout, Layered Atmosphere, Instruments & Environment, Spectrometer, Detector |
| Validation & Optimization | Parameter Scans & Optimization, Tolerance Experiments, Model Documentation |

These modules cover paraxial networks, spatial and curved-surface ray tracing, scalar diffraction, wave propagation, fibre modes, photonic devices, spectroscopy, and detector models. Inputs, units, sampling requirements, and limitations are documented within the relevant module.

### Components and Reusable Instruments

- Start from built-in parameter templates.
- Find components by category or keyword.
- Save component parameters as custom templates.
- Capture and reuse instrument subassemblies.
- Manage supported instrument versions and exchange templates through JSON.

Built-in component presets are idealized or synthetic templates, not a catalogue of measured vendor specifications.

### Projects and Data

- Open, save, or export `.titan` projects using native file interfaces.
- Preserve stable identifiers for components, connections, and assembly objects.
- Exchange projects between compatible desktop and mobile versions.
- Export supported results as CSV, JSON, FITS, or text reports.
- Import supported filter curves, calibration packages, and STL meshes in the appropriate modules.
- Use local recovery copies in the mobile application.

Format support varies by module. Not every module supports every listed format.

## Native Workspaces

### Desktop

The desktop application combines a component library, category navigation, inspectors, and assembly views. It supports mouse and keyboard workflows, native file dialogs, and common shortcuts for opening, saving, undoing, and redoing changes.

### Mobile

The mobile application uses a collapsible sidebar with expandable experiment categories. Components and inspectors open in separate panels.

Assembly controls are grouped into focused menus. The lower assembly panel can collapse, and observation-plane content scrolls vertically. Wide scientific tables and plots remain horizontally scrollable in narrower windows.

### Language Selection

Open the toolbar **ellipsis menu → Language / 语言** and choose **English** or **简体中文**. On the mobile interface, the ellipsis menu is in the upper-right corner.

User-defined names and imported content retain their original language.

## Getting Started

1. Launch the application and open a built-in example, or create an imaging project from the application menu.
2. Select **Design & Assembly → Node Workspace** using the category navigation or sidebar.
3. Open **Components** and add a preset.
4. Connect output and input ports, then select a connection to edit its propagation distance.
5. Select a component and open **Inspector** to adjust its specifications.
6. Switch to **Physical Assembly** or an analysis module to inspect the design.
7. Review units, model scope, and result status before exporting a project or analysis data.

### Saving and Recovery

The desktop application uses native file dialogs. Save writes to the current project file, while Save As creates a separate copy.

The mobile application's **Export** action saves a copy through Files. It does not continuously overwrite the original external document. Export again after further edits to preserve the latest version outside the app.

The mobile application attempts to create recovery copies when becoming inactive or before switching away from an unsaved project. Restore the latest copy from the ellipsis menu, or manage the application's `Documents/Recovery` folder through Files.

Recovery copies are not a substitute for deliberate exports: forced termination or resource pressure may prevent lifecycle saving from completing. Exported copies and accumulated recovery files remain under the user's control.

## Building from Source

These instructions apply to a repository checkout containing the relevant application source. A repository used only for product information or issue tracking may not include the build projects.

### Requirements

- A Mac with Xcode installed.
- The macOS SDK for the desktop application.
- The iOS SDK and an available iPad Simulator for the mobile application.
- Appropriate development-team and signing settings for installation on a physical iPad.

The recorded mobile build environment is **Xcode 26.3, iOS 26.2 SDK, and iOS 26.3 Simulator**. This identifies a tested environment, rather than a guarantee that every other toolchain version has been validated.

### Desktop Application

Open `CosmicTitan.xcodeproj` in the desktop source directory, select the application scheme and **My Mac**, then run the project.

The desktop directory also contains a Swift package using Swift tools 6.0. From that directory:

```sh
swift build
swift test
```

Use the Xcode application project for application resources, signing, and distribution workflows.

### Mobile Application

Open `cosmic titan mobile.xcodeproj`, select the **cosmic titan mobile** scheme, and choose an iPad Simulator or a properly signed physical device.

From the mobile project root, build for the simulator with:

```sh
xcodebuild \
  -project 'cosmic titan mobile.xcodeproj' \
  -scheme 'cosmic titan mobile' \
  -configuration Debug \
  -destination 'generic/platform=iOS Simulator' \
  -derivedDataPath .build/ipad \
  CODE_SIGNING_ALLOWED=NO build
```

Build an unsigned device Release configuration with:

```sh
xcodebuild \
  -project 'cosmic titan mobile.xcodeproj' \
  -scheme 'cosmic titan mobile' \
  -configuration Release \
  -destination 'generic/platform=iOS' \
  -derivedDataPath .build/device \
  CODE_SIGNING_ALLOWED=NO build
```

These commands compile the application. They do not create a signed distribution package, archive the app, or submit it to the App Store.

### Mobile Tests

List available simulators:

```sh
xcrun simctl list devices available
```

Replace `<IPAD_SIMULATOR_UDID>` with an available iPad simulator identifier:

```sh
xcodebuild \
  -project 'cosmic titan mobile.xcodeproj' \
  -scheme 'cosmic titan mobile' \
  -configuration Debug \
  -destination 'platform=iOS Simulator,id=<IPAD_SIMULATOR_UDID>' \
  -derivedDataPath .build/ipad \
  CODE_SIGNING_ALLOWED=NO test
```

The mobile application uses the Xcode UIKit project; the historical desktop Swift Package configuration is not its application build entry point.

## Validation Status

The following results refer to development records from **September 24, 2026**:

| Platform | Recorded results |
| --- | --- |
| Desktop | 179 automated tests passed; universal Release build passed for arm64 and x86_64 |
| Mobile | 26 original Swift source files and 36 navigation entries audited against the desktop baseline; all 179 original tests retained |
| Mobile regression | 186 XCTest cases passed after mobile-specific regression coverage was added |
| Observation-panel update | 53 related spatial tests passed |
| Latest sidebar layout | Simulator Debug and unsigned device Release builds passed |

The full 186-test run preceded the final sidebar redesign. It does not establish complete interaction validation of the latest interface. Automated tests cover numerical behavior, data, and selected state transitions; they do not replace visual, gesture, or physical-device testing.

Desktop GUI acceptance, minimum-OS coverage, and Intel hardware validation were also not completed in full.

## Scientific Scope

comistian supports optical education, model exploration, and research workflows. Results must be interpreted within each module's assumptions.

- Geometric rays, paraxial analysis, scalar waves, and electromagnetic grid experiments use different models.
- Some experiments are independent of the assembly and do not automatically derive a complete solver input from the 3D scene.
- Scalar modes, ideal AWG models, fibre-coupling calculations, and 2D FDTD experiments do not constitute arbitrary full-vector 3D Maxwell solving.
- Mechanical visualizations are not manufacturing CAD. Decorative mounts do not automatically act as optical obstructions.
- Parameter scans and tolerance experiments do not prove a global optimum over every possible design parameter.
- Sampling convergence, energy accounting, and result quality require separate checks and, where appropriate, independent experimental or numerical validation.

## Known Limitations

- Some advanced mobile experiments still use independent background tasks and are not fully integrated with unified cancellation.
- Continuous mobile 3D gestures, cross-panel drag and drop, external keyboards, and trackpads need broader device testing.
- Not every split-window size, Dynamic Type setting, or long-running large calculation has been validated.
- iPadOS 17 is the deployment minimum; the recorded validation does not include a complete run on that OS version.
- Desktop file-saving, application-exit, and mouse-modifier behavior do not map one-to-one to the mobile interface.

## Privacy and Local Processing

Core calculations and project processing run locally. The current implementation does not require an account and does not integrate advertising or third-party analytics SDKs.

Files stored through iCloud Drive or another provider are handled by that provider. Opening an external reference visits the corresponding website. If you contact support by email, the developer receives the message and attachments you choose to send.

Do not include sensitive projects, passwords, personal information, or restricted data in public issues. This README is not a substitute for a published privacy policy.

## Feedback and Bug Reports

Use repository Issues, when available, or email support. Please include:

- Platform, application version, and build number.
- Mac or iPad model and operating-system version.
- Module, interface language, and window orientation where relevant.
- Steps to reproduce the issue.
- Expected and actual behavior.
- Relevant screenshots, error messages, or a minimal non-sensitive project.

For numerical issues, also provide units, boundary conditions, grid or sampling settings, and the reference used for comparison.

## Development and Contributions

Where source and collaboration channels are available, changes should preserve project compatibility, stable identifiers, scientific units, bilingual interfaces, and model-scope explanations.

Solver changes should include relevant regression or convergence evidence. Interface changes should identify the platform, window sizes, and languages checked. Discuss substantial changes through an issue or email before implementation.

Do not describe unimplemented or unverified capabilities as completed product features.

## License

No explicit open-source license was found in the project materials used to prepare this document. This README does not grant permission to use, modify, redistribute, or commercially license the source or assets. Refer to the project owner's published license or written permission for applicable terms.

## Contact

**Developer:** 胡冬生  
**Email:** [hudongsheng356@gmail.com](mailto:hudongsheng356@gmail.com)

Copyright © 2026 胡冬生.
