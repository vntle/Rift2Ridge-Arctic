# Rift2Ridge-Arctic

My code work and documentation based on the private research version of Rift2Ridge developed at MARUM.

Rift2Ridge is a finite-element code for geodynamics with visco-elasto-plastic rheologies, primarily developed at the MARUM Center for Marine Environmental Sciences, University of Bremen. This repository adapts and documents workflows for Arctic rifting and ridge evolution scenarios.

## Documentation

| Document | Description |
|---|---|
| [Overview](docs/overview.md) | Project background, goals, and key concepts |
| [Installation](docs/installation.md) | Environment setup and dependency installation |
| [Configuration](docs/configuration.md) | Model parameters and configuration reference |
| [Usage](docs/usage.md) | Running simulations and interpreting output |
| [Arctic Setup](docs/arctic-setup.md) | Arctic-specific model configuration and case studies |
| [Glossary](docs/glossary.md) | Geodynamics and code terminology |
| [FAQ](docs/faq.md) | Frequently asked questions |
| [Contributing](docs/contributing.md) | How to contribute to this repository |

## Quick Start

1. Install [MATLAB](https://www.mathworks.com/products/matlab.html) (R2018b or later) and the required dependencies (see [Installation](docs/installation.md)).
2. Clone this repository and set the required environment variables.
3. Navigate to a data input folder and launch MATLAB in batch mode:

```bash
matlab -nosplash -nodisplay -batch "pid=0;call_main" -logfile rift2ridge.log
```

For detailed instructions, see the [Usage guide](docs/usage.md).

## License

See [LICENSE](LICENSE) for details.

