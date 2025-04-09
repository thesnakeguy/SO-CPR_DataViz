# SO-CPR_DataViz
This repository contains an RMarkdown script (`SO-CPR_workflows.Rmd`) designed to analyze and visualize biodiversity patterns within the Southern Ocean Continuous Plankton Recorder (SO-CPR) dataset. The analysis is parameterized, allowing users to explore specific subsets of the data based on temporal, spatial, and taxonomic criteria.

**Key Features:**

* **Reproducible Analysis:** The RMarkdown script is designed for reproducibility. All necessary packages are automatically installed if missing, and the code is structured logically. The SO-CPR dataset is loaded in the environment using the BlueAnt R package which allows easy syncing (https://australianantarcticdivision.github.io/blueant/).
* **Well-Annotated Code:** Each code block within the RMarkdown script is clearly commented to explain the purpose and functionality of the code. Meaningful chunk names enhance readability and understanding.
* **Modular Filtering:** The analysis incorporates flexible filtering options based on month, ship code, year, season, and taxonomic groups. Spatial filtering using a bounding box is also available for specific analyses.
* **Comprehensive Biodiversity Metrics:** The script calculates key biodiversity indices, including Species Richness, Shannon Diversity Index, Simpson Diversity Index, and ES50 (Hurlbert's Expected Species).
* **Diverse Visualizations:** The analysis generates a range of informative visualizations:
    * Spatial maps of biodiversity indices using H3 hexagonal grids.
    * Interactive tables of species occurrences within defined spatial extents.
    * Temporal trends of abundance for selected taxa.
    * Monthly abundance patterns displayed as boxplots.
    * Latitudinal abundance patterns visualized with GAM smoothing.
    * Species-specific distribution maps overlaid on the Southern Ocean.

## 1. Repository Contents

* `SO-CPR_Biodiversity_Analysis.Rmd`: The main RMarkdown script containing the analysis code and narrative.
* `SO_CPR_AnnotateSpeciesTaxonomy.R`: An R script (mentioned in the RMarkdown) that is **required** to generate the taxonomic annotations for species IDs in the SO-CPR dataset. 
* `README.md`: This file providing an overview of the repository and instructions for use.
* `SO-CPR_ID_TaxonAnnotations.txt`: The output file from the `SO_CPR_AnnotateSpeciesTaxonomy.R` script, containing the hierarchical taxonomic information. Note that this could not be up to date when new IDs were added. This file and updates thereof can easily be reprocuded using the `SO_CPR_AnnotateSpeciesTaxonomy.R` script.

## 2. Prerequisites

Before running the RMarkdown script, ensure you have the following installed:

* **R** (version $\ge$ 4.0 is recommended): [https://www.r-project.org/](https://www.r-project.org/)
* **RStudio** (version $\ge$ 1.4 is recommended, though not strictly necessary): [https://posit.co/download/rstudio-desktop/](https://posit.co/download/rstudio-desktop/)
* The `SO_CPR_AnnotateSpeciesTaxonomy.R` script must be executed **first** to create the `SO-CPR_ID_TaxonAnnotations.txt` file. This file provides the necessary taxonomic information for the biodiversity analysis. Alternatively, you can get a copy of the `SO-CPR_ID_TaxonAnnotations.txt` by downloading it from this repo.

## 3. Setup and Execution

1.  **Clone the Repository:**
    ```bash
    git clone <repository_url>
    cd <repository_name>
    ```

2.  **Run the Taxonomy Annotation Script:**
    Execute the `SO_CPR_AnnotateSpeciesTaxonomy.R` script in R. This script will process your SO-CPR dataset (located as defined by the `bb_config` and `sources` calls within the RMarkdown) and generate the `SO-CPR_ID_TaxonAnnotations.txt` file in the specified location. **Ensure the file path in the RMarkdown script (under section 2.2) correctly points to this generated file.**

3.  **Open the RMarkdown File:**
    Open the `SO-CPR_Biodiversity_Analysis.Rmd` file in RStudio.

4.  **Configure Analysis Parameters (Optional):**
    Modify the parameters in the "**1.2 Analysis Parameters**" code block to customize the analysis:
    * `res`: Spatial resolution for H3 hexagons.
    * `Month_select`, `Ship_code_select`, `Year_select`, `Season_select`: Filters for temporal and sampling information. Set to `NULL` for no filtering.
    * `Taxon`: Regular expression pattern to filter the taxonomy. Set to `NULL` for no taxonomic filtering.
    * `xmin`, `xmax`, `ymin`, `ymax`: Bounding box coordinates for spatial filtering in specific visualizations. Set to `NULL` to disable spatial filtering.

5.  **Run the RMarkdown Script:**
    In RStudio, click the "Knit" button (or use the keyboard shortcut `Ctrl+Shift+K` / `Cmd+Shift+K`) to execute the script. This will generate an HTML document (`SO-CPR_Biodiversity_Analysis.html`) containing the analysis results, visualizations, and code.

## 4. Code Structure and Reproducibility

The RMarkdown script is organized into logical sections with descriptive headings and well-defined code blocks:

* **1. Environment Setup:** Installs and loads necessary R packages. The `install_if_missing` function ensures that required packages are installed automatically if they are not already present in your R environment.
* **2. Data Preparation:** Loads the SO-CPR data and the taxonomic annotation file. It then applies the filters defined in the "Analysis Parameters" section.
* **3. Biodiversity Analysis:** Calculates various biodiversity indices based on the filtered data, aggregated at the H3 hexagon level.
* **4. Visualization:** Generates a series of plots and interactive tables to visualize the biodiversity patterns, temporal trends, and species distributions. Each visualization code block is self-contained and clearly labeled.
* **5. Session Information:** Prints the details of the R session, which is crucial for ensuring reproducibility by recording the exact versions of R and all used packages.

The use of parameterized inputs and the explicit installation of required packages contribute significantly to the reproducibility of this analysis. By setting the parameters and running the script, you can regenerate the same results and explore different facets of the SO-CPR dataset.

## 5. Further Information

For questions or issues related to this analysis, feel free to contact me @thesnakeguy or post an issue to this repo :)
