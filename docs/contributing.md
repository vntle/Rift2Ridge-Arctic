# Contributing

Thank you for your interest in contributing to Rift2Ridge-Arctic! This guide explains how to submit bug reports, suggest improvements, and add new content to the repository.

## How to Contribute

### Reporting Bugs

If you find a bug or unexpected behaviour:

1. Check the [FAQ](faq.md) and [Troubleshooting section in Usage](usage.md) to see if the issue is already addressed.
2. Search [open issues](https://github.com/vntle/Rift2Ridge-Arctic/issues) to avoid duplicates.
3. Open a new issue with:
   - A clear, descriptive title.
   - Steps to reproduce the problem.
   - MATLAB version, operating system, and relevant parameter values.
   - The full error message or stack trace (copy from the log file).

### Suggesting Enhancements

Open a GitHub issue labelled **enhancement** describing:
- The scientific or workflow problem you want to solve.
- Your proposed solution or change.
- Any relevant references (papers, datasets, or upstream code changes).

### Adding a New Case Study

To contribute a new Arctic case study:

1. **Fork** the repository and create a feature branch:

   ```bash
   git checkout -b add-case-<event>
   ```

2. Create the input folder following the standard structure:

   ```
   SIU3P/data/ARCTIC/<event>/<meshnam>/001/
   ├── call_main.m
   ├── change_model.m
   ├── readCASE.m
   ├── readCF.m
   ├── update_model.m
   └── readMC.m
   ```

3. Add a corresponding section to [docs/arctic-setup.md](arctic-setup.md) documenting:
   - Tectonic context and scientific goal.
   - Key parameters and their values.
   - Expected output and validation data.

4. Commit your changes with a descriptive message:

   ```bash
   git add .
   git commit -m "Add Gakkel western amagmatic segment case study"
   ```

5. Push and open a **pull request** against the `main` branch.

### Improving Documentation

Documentation improvements are always welcome. To fix a typo, clarify a description, or add a glossary entry:

1. Edit the relevant `.md` file in `docs/`.
2. Commit with a message like `docs: fix typo in glossary.md`.
3. Open a pull request.

## Code Style

- MATLAB scripts should follow the existing formatting conventions (2-space indentation, descriptive variable names).
- Add a comment header to new MATLAB files with the file name, a one-line description, and your name/date.
- Keep parameter overrides in `change_model.m` commented to explain the scientific rationale for non-default values.

## Documentation Style

- Use [GitHub Flavored Markdown](https://docs.github.com/en/get-started/writing-on-github).
- Keep line length under 120 characters.
- Prefer tables over long lists for structured data.
- Link to the glossary for technical terms the first time they appear in a document.

## Pull Request Checklist

Before submitting a pull request, please verify:

- [ ] New or modified case study folders contain all required input files.
- [ ] Documentation has been updated to describe the change.
- [ ] MATLAB scripts are commented and follow the existing style.
- [ ] The simulation runs without errors for at least a few time steps.
- [ ] The PR description explains the scientific motivation.

## Contact

For questions that are not suitable for a public issue, contact the repository maintainer via GitHub, or reach the MARUM Geophysics-Geodynamics group:

- Prof. Dr. Marta Pérez-Gussinye: mpgussinye@marum.de
- Dr. Javier García-Pintado: jgarciapintado@marum.de
