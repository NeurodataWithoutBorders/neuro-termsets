# Changelog

All notable changes to this project are documented in this file.

## 0.1.0 (October 11, 2026)

First release. The package is still in an early stage: term sets and configuration may change in later releases.

### Term sets
- **Species** (`subject_species_ncbitaxon_termset.yaml`): 27 common neuroscience species, plus `unidentified`, mapped to NCBITaxon. This includes species used by NIH BBQS projects: sheep, domestic ferret, brown-headed cowbird, Panamanian white-faced capuchin, and *Hofstenia miamia* ([#2](https://github.com/NeurodataWithoutBorders/neuro-termsets/pull/2)).
- **Brain regions**, generated from the ontologies with `scripts/generate_brain_region_termsets.py`:
  - UBERON, cross-species (`brain_region_uberon_termset.yaml`)
  - Allen Mouse Brain Atlas (`brain_region_mba_termset.yaml`)
  - Allen Human Brain Atlas (`brain_region_hba_termset.yaml`)
- **Strains** (`strain_termset.yaml`): common laboratory mouse, rat, fish, worm, and fly strains and lines mapped to RRIDs.
- **General anatomy** (`general_anatomy_termset.yaml`): body parts, nerves, muscles, and organs mapped to UBERON, e.g., for pose keypoints.

### Configuration
- `default_config.yaml` connects the term sets to PyNWB fields:
  - the species term set to `Subject.species`
  - the UBERON brain-region term set to the `location` of `ElectrodeGroup`, `ImagingPlane`, `IntracellularElectrode`, and `OptogeneticStimulusSite`
- The Allen atlas, strain, and anatomy term sets are included but not enabled by default.

### Python API
- `load_termset_config()` loads the default configuration into PyNWB.
- `get_config_path()`, `get_available_termsets()`, and `get_termset_path()` locate the configuration and term set files.
- `get_configured_termsets()` returns the configured `TermSet` objects for a PyNWB class or attribute.

### Scripts
- `scripts/generate_lab_termsets.py` generates lab-specific term sets and a configuration for ORCID (experimenters), ROR (institutions), and DANDI (dandisets) from a YAML manifest. A template is in `lab_termsets/lab_resources_template.yaml`.
- `scripts/example_usage.py` shows how to validate values and fill HERD.
- `scripts/example_termset_query.py` shows how to list and query the configured term sets.

### Testing
- Unit tests and a GitHub Actions workflow.
