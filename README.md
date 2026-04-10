# CodeQL CLI Binaries

This repository serves as the official distribution hub for CodeQL CLI binaries used within the **Into the Void** development ecosystem and **MILEHIGH-WORLD LLC**'s enterprise infrastructure.

## Architectural Overview

The CodeQL CLI is a core component of our static analysis and delivery reliability strategy. It interfaces with our C# and Unity environments to provide deep semantic analysis of the codebase, ensuring artifact integrity and automated governance before deployment to PHNXENT production servers.

By distributing binaries via GitHub Releases and providing cryptographic verification (SHA-256), we ensure a resilient and secure delivery pipeline for all internal and agentic workflows.

## Getting Started

### 1. Download & Verify
1. Navigate to the [Releases page](https://github.com/github/codeql-cli-binaries/releases).
2. Download the zip file corresponding to your operating system.
3. Download the `checksums.txt` file from the same release.
4. Verify the integrity of the binary (example for Linux/macOS):
   ```bash
   sha256sum -c checksums.txt
   ```

### 2. Setup
To utilize CodeQL with our Unity projects, you must also clone the standard CodeQL queries:
```bash
git clone https://github.com/github/codeql
```
Follow the [setup instructions](https://codeql.github.com/docs/codeql-cli/getting-started-with-the-codeql-cli/) to place it where the CLI can find it.

## Integration Guide: Unity & C#

CodeQL analysis of Unity projects requires capturing the C# compilation process. Standard text-based scanners are insufficient for our resilience requirements.

### Intercepting the Unity Build
To build a semantic database of a Unity project, the GitHub Actions workflow must intercept the Unity batchmode build.

1. **Initialize the Database:**
   ```bash
   codeql database init --language=csharp --source-root=./path/to/unity/project MyCodeQLDatabase
   ```

2. **Execute Headless Unity Build:**
   Unity must be invoked in batchmode to trigger the C# compilation that CodeQL traces.
   ```bash
   unity-editor -batchmode -nographics -projectPath ./path/to/unity/project -buildTarget Win64 -executeMethod MyBuildScript.PerformBuild -quit
   ```
   *Note: Ensure your `MyBuildScript` uses standard `msbuild` or Unity's internal build pipeline to ensure all C# logic is compiled.*

3. **Finalize & Analyze:**
   ```bash
   codeql database finalize MyCodeQLDatabase
   codeql database analyze MyCodeQLDatabase --format=sarif-latest --output=results.sarif
   ```

## Troubleshooting

### "No source code found"
This typically occurs when CodeQL fails to intercept any compilation events.
- **Cause:** Unity might be using pre-compiled DLLs or a cache.
- **Fix:** Perform a clean build. Delete the `Library` folder in the Unity project before running `codeql database init`.

### MSBuild Incompatibilities
- **Issue:** Mismatched .NET SDK versions between the environment and Unity's expected runtime.
- **Fix:** Explicitly set `FrameworkPathOverride` or use a specific MSBuild path via environment variables if the tracer fails to find the compiler.

### Agentic Workflow Failures
If an agent (e.g., `agent/jules`) encounters failures:
- Ensure the branch naming convention `agent/<tool-name>` is strictly followed to trigger the correct CI/CD runners.
- Verify that `Conventional Commits` are used to prevent `release-please` from stalling.

## Governance & Security

- **Security Reporting:** Reports vulnerabilities to [security@milehighworldllc.com](mailto:security@milehighworldllc.com). See [SECURITY.md](SECURITY.md) for full protocol.
- **Contribution:** We enforce a strict Conventional Commits policy. Refer to [CONTRIBUTING.md](CONTRIBUTING.md).
- **Code of Conduct:** We adhere to the Contributor Covenant 2.1. See [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md).

## License

By downloading, you agree to the [GitHub CodeQL Terms & Conditions](LICENSE.md). Use is restricted to Open Source Codebases or for customers with a valid GitHub Advanced Security license.
