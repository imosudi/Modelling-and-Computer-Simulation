# 1. Mathematical & Statistical Modelling

## 1.1 Scilab (MATLAB Alternative)

### Prerequisites
* **Operating Systems**: 
  - Windows 10/11 (64-bit recommended)
  - macOS 10.13 (High Sierra) or newer
  - Linux distributions: Ubuntu 18.04+, Debian 10+, Fedora 30+, RHEL 7+
* **Dependencies**: 
  - Java Runtime Environment (JRE) 8 or newer
  - Microsoft Visual C++ Redistributable (Windows only)
* **Minimum System Requirements**: 
  - RAM: 2GB
  - Storage: 500MB free disk space
  - Processor: Dual-core CPU at 2GHz or higher
  - Display: 1024×768 resolution
* **Optimum System Requirements**: 
  - RAM: 8GB
  - Storage: 2GB free disk space
  - Processor: Quad-core CPU at 2.5GHz or higher
  - Display: 1920×1080 resolution or higher

### Installation Steps

#### Windows Installation
1. Visit the official Scilab website: https://www.scilab.org
2. Click on the **Download Scilab** button and select the Windows installer (.exe)
3. Save the installer file to your computer
4. Run the installer with administrator privileges
5. Accept the license agreement
6. Choose installation directory (default is recommended: `C:\Program Files\scilab-X.X.X`)
7. Select components to install (default selection is recommended)
8. Choose whether to create desktop and Start menu shortcuts
9. Click through to complete the installation
10. Launch Scilab from the Start menu or desktop shortcut

#### macOS Installation
1. Navigate to https://www.scilab.org
2. Click on **Download Scilab** and select the macOS package (.dmg)
3. Once downloaded, open the .dmg file
4. Drag the Scilab application to your Applications folder
5. Control-click the app icon and select "Open" to bypass macOS security warnings on first launch
6. Scilab will now open and create necessary configuration files

#### Linux Installation
1. Visit https://www.scilab.org
2. Download the Linux package appropriate for your distribution (.tar.gz or specific package like .deb for Debian/Ubuntu or .rpm for Fedora/RHEL)
3. For .deb packages (Ubuntu/Debian):
   ```bash
   sudo dpkg -i scilab-X.X.X.x86_64.deb
   sudo apt-get install -f  # Resolves dependencies if needed
   ```
4. For .rpm packages (Fedora/RHEL):
   ```bash
   sudo rpm -i scilab-X.X.X.x86_64.rpm
   ```
5. For generic tar.gz:
   ```bash
   tar -xzf scilab-X.X.X.bin.linux-x86_64.tar.gz
   cd scilab-X.X.X
   ./bin/scilab
   ```

### Key Features
- **Programming Environment**: Provides a high-level numerical programming environment with dedicated programming language
- **Visualization**: 2D/3D plotting capabilities for data visualization
- **Matrix Operations**: Efficient handling of matrices, the fundamental data objects in Scilab
- **Mathematical Functions**: Comprehensive library of mathematical functions
- **Control System Design & Analysis**: Robust tools for control systems engineering
- **Signal Processing**: Functions for filtering, FFT, and signal analysis
- **Optimization**: Tools for linear, nonlinear, and global optimization problems
- **Statistics**: Statistical analysis and data processing capabilities
- **Xcos**: Block diagram modeler and simulator for dynamic systems (similar to Simulink)
- **Toolboxes**: Various domain-specific toolboxes for extended functionality

### Practical Applications
- **Engineering Calculations**: Performing complex engineering analyses and simulations
- **Control System Design**: Modeling and analyzing control systems
- **Signal Processing**: Analyzing and processing signals from various sources
- **Image Processing**: Basic to advanced image manipulation and analysis
- **Data Analysis**: Statistical analysis of experimental or simulation data
- **Teaching**: Educational tool for mathematics, engineering, and science courses
- **Academic Research**: Computational platform for scientific research

### Getting Started Example
After installation, try this simple example to verify Scilab is working correctly:

1. Launch Scilab
2. In the console, enter the following commands:
   ```scilab
   x = linspace(0, 2*%pi, 100);
   y = sin(x);
   plot2d(x, y, style=5);
   xlabel('x');
   ylabel('sin(x)');
   title('My First Scilab Plot');
   ```
3. You should see a sine wave plot appear

## 1.2 GNU Octave

### Prerequisites
* **Operating Systems**: 
  - Windows 7/8/10/11
  - macOS 10.13+
  - Linux (most distributions supported)
* **Dependencies**: 
  - None (all dependencies are included in the installer)
  - Optional: FFTW for faster Fourier transforms
  - Optional: SuiteSparse for sparse matrix operations
* **Minimum System Requirements**: 
  - RAM: 2GB
  - Storage: 500MB free disk space
  - Processor: Dual-core CPU at 1.6GHz+
  - Graphics: Any GPU that supports OpenGL 2.0+
* **Optimum System Requirements**: 
  - RAM: 8GB
  - Storage: 2GB free disk space
  - Processor: Quad-core CPU at 2.0GHz+
  - Graphics: Dedicated GPU with OpenGL 3.0+ support

### Installation Steps

#### Windows Installation
1. Visit https://www.gnu.org/software/octave/download
2. Download the Windows installer (.exe file)
3. Run the installer with administrator privileges
4. Choose installation type (complete installation recommended)
5. Select installation directory
6. Choose whether to add Octave to the system PATH
7. Select additional options:
   - Create desktop shortcut
   - Associate .m files with Octave
   - Create Start menu shortcuts
8. Complete the installation process
9. Launch Octave from the Start menu or desktop shortcut

#### macOS Installation
1. Go to https://www.gnu.org/software/octave/download
2. Download the macOS package (.dmg file)
3. Alternatively, install via Homebrew with:
   ```bash
   brew install octave
   ```
4. If using the DMG, mount it and drag Octave to the Applications folder
5. Launch Octave from Applications
6. On first launch, you may need to right-click and select "Open" to bypass Gatekeeper

#### Linux Installation
1. For Ubuntu/Debian:
   ```bash
   sudo apt update
   sudo apt install octave octave-control octave-image octave-io octave-optim octave-signal octave-statistics
   ```
2. For Fedora:
   ```bash
   sudo dnf install octave octave-devel
   ```
3. For Arch Linux:
   ```bash
   sudo pacman -S octave
   ```
4. Launch Octave from the terminal by typing `octave` or through the application menu

### Key Features
- **Command Line Interface**: Interactive command-line for direct computation
- **GUI Interface**: Modern graphical user interface with code editor
- **MATLAB Compatibility**: High degree of compatibility with MATLAB syntax
- **Numerical Computation**: Powerful numerical methods for computational mathematics
- **Data Visualization**: Extensive 2D/3D plotting capabilities
- **Matrix Manipulation**: Efficient operations on matrices and vectors
- **Differential Equations**: Solvers for ordinary and partial differential equations
- **Linear Algebra**: Comprehensive linear algebra operations
- **Statistics & Optimization**: Built-in statistical and optimization functions
- **Extensibility**: Support for user-defined functions and packages

### Practical Applications
- **Numerical Analysis**: Solving complex numerical problems
- **Data Analysis**: Processing and analyzing experimental data
- **Academic Research**: Platform for computational research in sciences and engineering
- **MATLAB Migration**: Cost-effective alternative to MATLAB for many applications
- **Education**: Teaching tool for mathematics, engineering, and computer science
- **Prototyping**: Rapid development of numerical algorithms
- **Signal Processing**: Analysis of time-series data and signals
- **Image Processing**: Basic and advanced image manipulation

### Getting Started Example
After installation, verify Octave is working correctly with this example:

1. Launch Octave
2. In the command window, enter:
   ```octave
   x = 0:0.1:10;
   y = sin(x);
   plot(x, y, 'r-', 'LineWidth', 2);
   grid on;
   xlabel('x');
   ylabel('sin(x)');
   title('My First Octave Plot');
   ```
3. A window should open displaying a red sine wave with grid lines

## 1.3 R (with ggplot2 & dplyr)

### Prerequisites
* **Operating Systems**: 
  - Windows 7/8/10/11
  - macOS 10.13+
  - Linux (most distributions)
* **Dependencies**: 
  - None for base R
  - For specific packages: various system libraries depending on the package
* **Minimum System Requirements**: 
  - RAM: 2GB
  - Storage: 1GB free disk space
  - Processor: Dual-core CPU at 1.5GHz+
* **Optimum System Requirements**: 
  - RAM: 8GB (16GB+ recommended for large datasets)
  - Storage: 2GB free disk space (more for package installation)
  - Processor: Quad-core CPU at 2.5GHz+
  - Additional: SSD storage for faster data processing

### Installation Steps

#### Windows Installation
1. Go to https://cran.r-project.org and click on "Download R for Windows"
2. Click on "base" and then download the latest version
3. Run the installer with administrative privileges
4. Select components to install (default is recommended)
5. Choose installation location (default is usually appropriate)
6. Select startup options and whether to customize the installation
7. Complete the installation process
8. (Optional but recommended) Install RStudio:
   - Visit https://posit.co/downloads
   - Download RStudio Desktop (free version)
   - Run the installer and follow the instructions
9. Launch RStudio (or R if not using RStudio)
10. Install essential packages by running:
   ```r
   install.packages(c("ggplot2", "dplyr", "tidyr", "readr", "readxl", "lubridate"))
   ```

#### macOS Installation
1. Visit https://cran.r-project.org and click on "Download R for macOS"
2. Download the .pkg file for the latest R version
3. Open the downloaded file and follow the installation wizard
4. (Optional) Install RStudio:
   - Go to https://posit.co/downloads
   - Download the macOS version of RStudio
   - Open the .dmg file and drag RStudio to Applications
5. Open RStudio from Applications
6. Install key packages:
   ```r
   install.packages(c("ggplot2", "dplyr", "tidyr", "readr", "readxl", "lubridate"))
   ```

#### Linux Installation
1. For Ubuntu/Debian:
   ```bash
   # Add the CRAN repository
   sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
   sudo add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/'
   sudo apt update
   sudo apt install r-base r-base-dev
   ```
2. For Fedora:
   ```bash
   sudo dnf install R
   ```
3. (Optional) Install RStudio:
   - Download the appropriate .rpm or .deb package from https://posit.co/downloads
   - Install using the package manager
4. Launch R or RStudio
5. Install essential packages:
   ```r
   install.packages(c("ggplot2", "dplyr", "tidyr", "readr", "readxl", "lubridate"))
   ```

### Key Features

#### Base R
- **Statistical Computing**: Comprehensive suite of statistical functions
- **Data Handling**: Tools for data manipulation and management
- **Matrix Operations**: Efficient handling of matrices and arrays
- **Programming Language**: Full-featured programming language for data analysis
- **Graphical Capabilities**: Basic plotting functions
- **Extensibility**: Thousands of packages for extended functionality
- **Cross-Platform**: Works consistently across operating systems

#### ggplot2
- **Grammar of Graphics**: Implementation of the layered grammar of graphics
- **Declarative Syntax**: Intuitive approach to creating complex visualizations
- **Aesthetic Mappings**: Flexible mapping of data variables to visual properties
- **Statistical Transformations**: Built-in statistical summaries
- **Faceting**: Easy creation of small multiples
- **Theming**: Customizable themes and appearance
- **Extensions**: Many extension packages available

#### dplyr
- **Data Manipulation**: Efficient tools for transforming data
- **Piping**: Integration with the magrittr pipe operator (`%>%`)
- **Grouping Operations**: Easy analysis of grouped data
- **Joins**: SQL-like joining of datasets
- **Filtering**: Powerful filtering capabilities
- **Performance**: Optimized for speed with large datasets
- **Consistency**: Predictable syntax across functions

### Practical Applications
- **Statistical Analysis**: Hypothesis testing, regression, ANOVA, etc.
- **Data Science**: End-to-end data analysis workflows
- **Machine Learning**: Statistical learning models through packages like caret or tidymodels
- **Biostatistics**: Analysis of biological and medical data
- **Finance**: Time series analysis, risk modeling, portfolio optimization
- **Social Sciences**: Survey analysis, demographic studies
- **Data Visualization**: Creating publication-quality graphics
- **Big Data**: Processing large datasets (with appropriate packages)
- **Reproducible Research**: Creating reports with RMarkdown

### Getting Started Example
After installation, try this example to test your R setup with ggplot2 and dplyr:

1. Launch R or RStudio
2. Run the following code:

```r
# Load required packages
library(ggplot2)
library(dplyr)

# Create sample data
data <- data.frame(
  x = 1:100,
  y = rnorm(100, mean = 0, sd = 15) + seq(1, 200, length.out = 100)
)

# Manipulate data with dplyr
processed_data <- data %>%
  mutate(category = case_when(
    y < 50 ~ "Low",
    y < 100 ~ "Medium",
    TRUE ~ "High"
  )) %>%
  group_by(category) %>%
  mutate(avg = mean(y))

# Create visualization with ggplot2
ggplot(processed_data, aes(x = x, y = y, color = category)) +
  geom_point(alpha = 0.7) +
  geom_smooth(method = "loess", se = TRUE) +
  geom_hline(aes(yintercept = avg, color = category), linetype = "dashed") +
  labs(
    title = "Sample ggplot2 Visualization",
    subtitle = "Demonstrating basic plotting with categories",
    x = "X Value",
    y = "Y Value",
    color = "Category"
  ) +
  theme_minimal() +
  scale_color_brewer(palette = "Set1")
```

This code should produce a scatter plot with trend lines and category-based coloring, demonstrating the integration of dplyr for data transformation and ggplot2 for visualization.
