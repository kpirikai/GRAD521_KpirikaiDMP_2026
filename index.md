## Data description
1. MALDI-MSI lipidomics data (experimental, instrument generated): Each pixel in the resulting image contains a full mass spectrum with the coordinate of where the laser hit; with that information I am able to map exactly where each lipid species is located within the tissue
3. Infection assays(experimental observational): Excel/CSV containing time-to-event data, mostly just counts
4. Fluorescence spectrometry and microscopy data (experimental, instrument generated: Numerical intensity values (exported to Excel/CSV) and image files (TIFF, CZI formats).
5. R analysis scripts and outputs (derived, codes and outputs): R Markdown notebooks, including figures (PDF, PNG), summary tables (CSV), and model outputs. 


## Roles and responsibilities
Role	Persons	Duties
- Data collection / generation:	Grad student (me).	Running MALDI-MSI experiments, infection assays, fluorescence microscopy; recording raw data
- Instrumentation maintenance:	Mass spec facility manager.	Calibrating MALDI instrument, maintaining laser function, ensuring data integrity from the instrument
- Metadata generation:	Grad student (me).	Documenting sample preparation, instrument settings, pixel coordinates, experimental conditions in lab notebooks and README files
- Data organization:	Grad student (me).	Creating logical folder structures, applying consistent file naming conventions, separating raw from processed data
- Quality control:	Grad student (me) + PI.	Checking mass spectra for quality, validating peak assignments, reviewing analysis scripts for errors
- Data analysis:	Grad student (me).	Writing R scripts, performing statistical analyses, generating figures and tables
- Software creation / maintenance:	Grad student (me).	Writing and documenting R Markdown notebooks; version control via Git
- Protection of sensitive data:	Grad student (me) + PI.	Ensuring no identifiable human data exists; securing any confidential information
- Access control:	PI + Grad student (me).	Managing permissions on shared drives; granting access to collaborators
- Archiving and preservation:	PI + Grad student (me).	Depositing final data in institutional repository (ScholarsArchive@OSU) after publication



## Data standards and metadata

## Storage and security
Primary storage location	Backup location(s)
1. MALDI-MSI raw,	Mass spec center cloud (remote access)	OSU network drive + external hard drive
2. MALDI-MSI processed,	OSU network drive (shared lab folder),	external hard drive + personal laptop
3. Infection assays,	OSU network drive (Excel files)	External hard drive + OSU box cloud
4. Fluorescence images,	OSU network drive + personal laptop +	external hard drive
5. R scripts/outputs,	GitHub (private repository) + local laptop +	OSU Box cloud


## Access and data sharing 

## Archiving and preservation 
Archiving 
