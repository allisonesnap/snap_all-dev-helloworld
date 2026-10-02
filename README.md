# ALL360 Snap Development Sequence

This document describes the complete sequence for creating, building, installing, configuring, and verifying a snap application for ALL360 OS.

## 1. Create the Project

Create the project directory and move into it:

```bash
mkdir hello-all360
cd hello-all360
```

Create the required directories:

```bash
mkdir -p snap/hooks
mkdir -p scripts
```

The resulting project structure is:

```text
hello-all360/
├── scripts/
└── snap/
    └── hooks/
```

## 2. Create the Application

Create the application executable:

```bash
vi scripts/hello-all360
```

Make the application executable:

```bash
chmod +x scripts/hello-all360
```

The application will be packaged as part of the snap.

## 3. Create the Snap Definition

Create the snap definition file:

```bash
vi snap/snapcraft.yaml
```

The snap definition should include the following base configuration:

```yaml
base: core24
grade: stable
confinement: strict
```

The complete `snapcraft.yaml` should define the application, its command, and any required configuration.

## 4. Create the Configure Hook

Create the configure hook:

```bash
vi snap/hooks/configure
```

Make the hook executable:

```bash
chmod +x snap/hooks/configure
```

The configure hook is executed when the snap is installed or when snap configuration is changed.

For example, the following command triggers the configure hook:

```bash
sudo snap set hello-all360 message="Hello from ALL360 OS"
```

## 5. Build the Snap

From the project root, build the snap package:

```bash
snapcraft pack
```

This generates a snap package similar to:

```text
hello-all360_1.0_amd64.snap
```

## 6. Install the Snap

Install the locally built snap using the `--dangerous` option:

```bash
sudo snap install ./hello-all360_1.0_amd64.snap --dangerous
```

The `--dangerous` option is required because the locally built snap is not signed by the Snap Store.

## 7. Configure the Snap

Set the application configuration:

```bash
sudo snap set hello-all360 message="Hello from ALL360 OS"
```

This updates the snap configuration and triggers the `configure` hook.

## 8. Run the Application

Run the installed application:

```bash
hello-all360
```

The application should produce the expected output based on the configured `message` value.

## 9. Verify the Snap

Confirm the installed snap and inspect its configuration and metadata:

```bash
snap info --verbose hello-all360
```

Verify that:

* The snap is installed successfully.
* The snap is using `core24` as its base.
* The snap has `stable` grade.
* The snap uses `strict` confinement.
* The application is available.
* The configuration has been applied successfully.

## 10. Complete Development Flow

The complete development sequence is:

```text
Create Project
      │
      ▼
Create Application
      │
      ▼
Create snap/snapcraft.yaml
      │
      ▼
Create configure Hook
      │
      ▼
Build with snapcraft pack
      │
      ▼
Install the .snap Package
      │
      ▼
Configure with snap set
      │
      ▼
Run the Application
      │
      ▼
Verify with snap info --verbose
```

### Command Summary

```bash
mkdir hello-all360
cd hello-all360

mkdir -p snap/hooks
mkdir -p scripts

vi scripts/hello-all360
chmod +x scripts/hello-all360

vi snap/snapcraft.yaml

vi snap/hooks/configure
chmod +x snap/hooks/configure

snapcraft pack

sudo snap install ./hello-all360_1.0_amd64.snap --dangerous

sudo snap set hello-all360 message="Hello from ALL360 OS"

hello-all360

snap info --verbose hello-all360
```
