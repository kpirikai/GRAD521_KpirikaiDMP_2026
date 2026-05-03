## Data description
1. MALDI-MSI lipidomics data (experimental, instrument generated): Each pixel in the resulting image contains a full mass spectrum with the coordinate of where the laser hit; with that information I am able to map exactly where each lipid species is located within the tissue
2. Infection assays(experimental observational): Excel/CSV containing time-to-event data, mostly just counts
3. Fluorescence spectrometry and microscopy data (experimental, instrument generated: Numerical intensity values (exported to Excel/CSV) and image files (TIFF, CZI formats).
4. R analysis scripts and outputs (derived, codes and outputs): R Markdown notebooks, including figures (PDF, PNG), summary tables (CSV), and model outputs. 

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
All metadata of samples used are well document in lab notebooks and drive files. Work is done with flies so there is no sensitive information that requires special case scenarios. Quality control is handled as described in roles and responsibilities to ensure robust and replicatable results. 

## Storage and security
Primary storage location	Backup location(s)
1. MALDI-MSI raw,	Mass spec center cloud (remote access)	OSU network drive and external hard drive
2. MALDI-MSI processed,	OSU network drive (shared lab folder),	external hard drive and personal laptop
3. Infection assays,	OSU network drive (Excel files), OSU box cloud, external hard drive and personal laptop
4. Fluorescence images,	OSU network drive, external hard drive and personal laptop 	
5. R scripts/outputs,	GitHub (private repository),	OSU Box cloud and personal laptop

## Access and data sharing 
Primarily through the OSU network drive with a personal folder with restricted access (only me and PI).
Mass spec center uses cloud: I have remote access credentials. The facility manager maintains the server, but I am responsible for downloading copies to my own storage regularly.

## Archiving and preservation 
Before graduating, I will transfer all data from my personal OSU network drive folder to the PI's lab folder. I will also deposit final datasets in ScholarsArchive@OSU with appropriate metadata and a DOI. My GitHub repositories will be transferred to a lab/PI account. Resulting publications out of the work prior to graduation will have raw data deposition requirements met as per the journal requirements.

## Data documentation plan
No formal metadata standard fully fits all my data types. MSI data can use imzML (an open XML-based standard), but my infection assays, fluorescence images, and R scripts do not align with a single standard. This is my plan to document each dataset:
- 1: MSI lipidomics. Processed data will be converted to imzML format, which embeds metadata (pixel coordinates, m/z values, intensity arrays) in an XML header. I will supplement this with a CSV metadata file for each run that includes: sample ID, genotype (control vs gene mutated), infection status (wasps vs no wasps), time point post-infection, biological replicate number, tissue type (fat body, gut, whole abdomen), MALDI matrix used, instrument settings (laser power, pixel size, mass range), and acquisition date. File naming: YYYYMMDD_genotype_infection_tissue_replicate.imzML 
(e.g., 20260426_w1118_Gh_infected_fatbody_rep01.imzML).
- 2: Infection assay data. I will document these with a README.txt file in the same folder containing a data dictionary that describes each column: variable name, description, units where applicable (e.g., hours_post_infection, immune_cell_counts). The README will also include general information: fly lines used, wasp species, temperature, humidity, and a link to the full methods protocol. 
File naming: YYYYMMDD_assay_type_genotype_rep01.csv.
- 3: Fluorescence spectrometry and microscopy data. Numerical intensity values will be exported to CSV and documented in the same README as Dataset 2. High-resolution images (TIFF, CZI) will be documented with a separate metadata CSV recording: image ID, sample ID, fluorophore (e.g., GFP, DAPI), exposure time, microscope settings, and a brief description of what the image shows. 
File naming: YYYYMMDD_sample_fluorophore_rep01.tiff.
- 4: R analysis scripts and outputs. All R scripts and R Markdown notebooks will be managed with Git version control. Each script will have a header comment block documenting: purpose of the script, inputs required (file paths), outputs generated, dependencies (R packages with versions), and author and date. The Git commit history will track every change with messages explaining why changes were made. The repository will be hosted on GitHub under my lab's organization. R Markdown notebooks interleave code, results, and explanatory text, serving as executable documentation of the entire analysis workflow from raw data to figures.

## Example of metadata file
Here are exmaples online: 1. https://dbkgroup.org/memo/implementation/xml.html 2. https://dbkgroup.org/memo/downloads/implementation/xml/masslynx.xsd 3. https://dbkgroup.org/memo/downloads/implementation/xml/analysis.xsd 4. Othere examples inclued those in the human metabolome database: https://hmdb.ca/downloads. I have created a simple, revised, simple example and attached it below.

## Example XML
<?xml version="1.0" encoding="UTF-8"?>
<mzML xmlns="http://psi.hupo.org/ms/mzml"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://psi.hupo.org/ms/mzml http://psidev.info/ms/mzml/xsd/mzML1.1.0.xsd"
      version="1.1.0"
      accession="[unique_accession_number]">

  <!-- Controlled vocabularies -->
  <cvList count="2">
    <cv id="MS" fullName="Proteomics Standards Initiative Mass Spectrometry Ontology"
         URI="http://psidev.info/ms/mzml/psi-ms.obo" version="4.1.0"/>
    <cv id="UO" fullName="Unit Ontology"
         URI="http://purl.obolibrary.org/obo/uo.owl" version="1.42"/>
  </cvList>

  <!-- File description and source -->
  <fileDescription>
    <fileContent>
      <cvParam cvRef="MS" accession="MS:1000579" name="MS1 spectrum" value=""/>
      <cvParam cvRef="MS" accession="MS:1000141" name="profile spectrum" value=""/>
    </fileContent>
    <sourceFileList count="1">
      <sourceFile id="RawData" name="[raw_filename].raw" location="[file_path]">
        <cvParam cvRef="MS" accession="MS:1000584" name="[instrument_vendor]_raw file" value=""/>
      </sourceFile>
    </sourceFileList>
  </fileDescription>

  <!-- Software used for conversion -->
  <softwareList count="1">
    <software id="ConversionSoftware" version="[software_version]">
      <cvParam cvRef="MS" accession="MS:1000544" name="Conversion to mzML" value=""/>
    </software>
  </softwareList>

  <!-- Data processing information -->
  <dataProcessingList count="1">
    <dataProcessing id="DataProcessing">
      <processingMethod order="1" softwareRef="ConversionSoftware">
        <cvParam cvRef="MS" accession="MS:1000544" name="Conversion to mzML" value=""/>
      </processingMethod>
    </dataProcessing>
  </dataProcessingList>

  <!-- Instrument configuration -->
  <instrumentConfigurationList count="1">
    <instrumentConfiguration id="IC1">
      <cvParam cvRef="MS" accession="MS:1001742" name="[instrument_model]" value=""/>
      <cvParam cvRef="MS" accession="MS:1000529" name="instrument serial number" value="[serial_number]"/>
    </instrumentConfiguration>
  </instrumentConfigurationList>

  <!-- Run metadata -->
  <run id="[sample_id]" defaultInstrumentConfiguration="IC1" defaultSourceFileRef="RawData">
    <spectrumList count="[number_of_pixels]" defaultDataProcessingRef="DataProcessing">

      <!-- Example spectrum for a single pixel. Repeated for each pixel in the run -->
      <spectrum id="spectrum=[pixel_number]" defaultArrayLength="[number_of_mz_values]">
        <cvParam cvRef="MS" accession="MS:1000511" name="ms level" value="1"/>
        <cvParam cvRef="MS" accession="MS:1000527" name="m/z array" value=""
                  unitCvRef="MS" unitAccession="MS:1000040" unitName="m/z"/>
        <cvParam cvRef="MS" accession="MS:1000528" name="intensity array" value=""
                  unitCvRef="MS" unitAccession="MS:1000131" unitName="number of counts"/>
        <cvParam cvRef="MS" accession="MS:1000580" name="scan time" value="[scan_time]"
                  unitCvRef="UO" unitAccession="UO:0000210" unitName="second"/>
        <cvParam cvRef="MS" accession="MS:1000501" name="preset scan configuration" value="[scan_config]"/>

        <!-- Binary data arrays -->
        <binaryDataArrayList count="2">
          <binaryDataArray encodedLength="[length_in_bytes]">
            <cvParam cvRef="MS" accession="MS:1000523" name="64-bit float" value=""/>
            <cvParam cvRef="MS" accession="MS:1000576" name="no compression" value=""/>
            <cvParam cvRef="MS" accession="MS:1000513" name="m/z array" value=""
                      unitCvRef="MS" unitAccession="MS:1000040" unitName="m/z"/>
            <binary>[binary m/z data for this pixel]</binary>
          </binaryDataArray>
          <binaryDataArray encodedLength="[length_in_bytes]">
            <cvParam cvRef="MS" accession="MS:1000523" name="64-bit float" value=""/>
            <cvParam cvRef="MS" accession="MS:1000576" name="no compression" value=""/>
            <cvParam cvRef="MS" accession="MS:1000514" name="intensity array" value=""
                      unitCvRef="MS" unitAccession="MS:1000131" unitName="number of counts"/>
            <binary>[binary intensity data for this pixel]</binary>
          </binaryDataArray>
        </binaryDataArrayList>
      </spectrum>

      <!-- Additional spectra (pixels 2 through N) follow the same pattern -->

    </spectrumList>
  </run>
</mzML>


## MALDI-MSI RUN METADATA

1. Run ID:
[number between 1 and 200. Precede with zeros to 3 digits, e.g., 001]

2. Sample information:
   Sample ID: [e.g., Dros_KO1_Inf_24h]
   Genotype: [Control / Knockdown / Overexpression]
   Gene targeted: [name of gene, if applicable]
   Infection status: [Uninfected / Wasp-infected]
   Wasp species: [if infected, e.g., Leptopilina boulardi]
   Time point post-infection: [hours, e.g., 0, 6, 12, 24, 48]
   Biological replicate number: [1, 2, 3, etc.]
   Tissue type: [Fat body / Gut / Whole abdomen]

3. Sample preparation:
   Matrix used: [e.g., DHB, CHCA, DAN]
   Matrix concentration: [mg/mL]
   Tissue thickness: [micrometers]
   Washing protocol: [Yes / No. If yes, describe in protocol document]

4. Instrument settings:
   Instrument model: [Bruker timsTOF Flex]
   Laser wavelength: [nm]
   Laser power: [percentage or arbitrary units]
   Laser shots per pixel: [number]
   Spatial resolution (pixel size): [micrometers]
   Mass range (m/z): [e.g., 300-1300]
   Polarity: [Positive / Negative]
   Acquisition date: [YYYY-MM-DD]

5. File information:
   Raw file path: [path on mass spec center cloud]
   Processed file name: [YYYYMMDD_genotype_infection_tissue_replicate.imzML]
   File size: [GB]

6. Related materials:
   Protocol document: [path + filename]
   Lab notebook entry: [date and page number]

This template demonstrates how I will document the experimental context that is not captured by the imzML standard alone. The imzML format records instrument settings and spectral data (m/z, intensity arrays), but it does not have fields for Drosophila genotype, infection status, wasp species, or time point post-infection. This custom template ensures that all information needed to interpret and reuse my data is recorded in a consistent, readable plain-text format. The template uses bracketed placeholders [ ] to guide what information belongs in each field, similar to the interview documentation example provided in class. This approach balances the use of an existing standard (imzML for spectral data) with custom metadata for my specific biological model, making my data both FAIR and usable by other Drosophila researchers.


