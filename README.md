# **Product Feature Extraction from Images**

## **Project Overview**

This project aims to automate the extraction of product features, specifically **dimensions** and **units**, directly from product images. It leverages Optical Character Recognition (OCR) to convert text embedded in images into machine-readable format. Subsequently, custom natural language processing (NLP) rules are applied to identify, parse, and normalize relevant numerical values and their corresponding units.

This pipeline is designed to be modular and scalable, making it suitable for processing large datasets of product images and extracting structured feature data that can be used for e-commerce, cataloging, or data analysis.

**Key Features:**

* **Automated Text Extraction:** Utilizes Tesseract OCR to efficiently convert visual text from product images into raw string data.  
* **Robust Unit and Dimension Parsing:** Implements custom logic to accurately identify numerical values and their associated units (e.g., "10.5 cm", "2 meters"), handling various abbreviations and plural forms.  
* **Modular Code Structure:** Organized into distinct Python modules (data\_processing.py, feature\_extraction.py) for enhanced readability, maintainability, and reusability.  
* **Scalable Image Downloading:** Supports efficient downloading of images from provided URLs, including multiprocessing capabilities for faster data acquisition.  
* **Reproducible Environment Setup:** A setup.sh script is provided to streamline the installation of system-level dependencies (like Tesseract OCR) and Python package management via a virtual environment.

## **Project Structure**

The project is organized into a clear and logical directory structure:

product-feature-extraction/  
├── .gitignore             \# Specifies intentionally untracked files and directories to ignore by Git.  
├── LICENSE                \# Contains the licensing information for the project.  
├── README.md              \# This file; provides a comprehensive overview of the project.  
├── requirements.txt       \# Lists all required Python packages for the project.  
├── setup.sh               \# A shell script for setting up system dependencies (Tesseract OCR) and the Python virtual environment.  
├── src/                   \# Contains the core Python source code modules.  
│   ├── \_\_init\_\_.py        \# An empty file that marks the 'src' directory as a Python package.  
│   ├── data\_processing.py \# Handles functions for image downloading, processing, and text extraction using OCR.  
│   └── feature\_extraction.py \# Contains logic for parsing and normalizing dimensions and units from extracted text.  
└── notebooks/             \# Stores Jupyter Notebooks for experimentation, analysis, and demonstrating usage.  
    └── Product\_Feature\_Analysis.ipynb \# The main notebook demonstrating the end-to-end feature extraction pipeline.

## **Installation**

Follow these steps to set up the project environment on your local machine:

1. Clone the repository:  
   Open your terminal or command prompt and execute the following command to clone the project:  
   git clone https://github.com/pokhriyal-anmol/product-feature-extraction.git  
   cd product-feature-extraction

   *(Remember to replace YourUsername with your GitHub username and your-project-name with your actual repository name.)*  
2. Run the setup script:  
   This script automates the installation of system-level dependencies (specifically Tesseract OCR and its language packs) and sets up a dedicated Python virtual environment, then installs all required Python packages listed in requirements.txt.  
   bash setup.sh

   * **Note for Windows users:** The setup.sh script is designed for Unix-like environments (Linux, macOS, WSL, or Git Bash). If you are on Windows and do not use WSL or Git Bash, you will need to perform the installation steps manually:  
     * **Tesseract OCR:** Download and install Tesseract OCR from its [official GitHub releases page](https://github.com/tesseract-ocr/tesseract/wiki/Downloads). Make sure to add it to your system's PATH.  
     * **Python Virtual Environment & Dependencies:** Manually create a virtual environment (python \-m venv venv), activate it (.\\venv\\Scripts\\activate), and then install dependencies (pip install \-r requirements.txt).  
3. Activate the virtual environment (if not automatically activated):  
   The setup.sh script attempts to activate the virtual environment. However, if your terminal session doesn't show (venv) at the beginning of the prompt, you can activate it manually:  
   * **On Linux/macOS:**  
     source venv/bin/activate

   * **On Windows (Command Prompt):**  
     venv\\Scripts\\activate.bat

   * **On Windows (PowerShell):**  
     .\\venv\\Scripts\\Activate.ps1

## **Usage**

### **Running the Analysis Notebook**

The most straightforward way to interact with and run the feature extraction pipeline is through the provided Jupyter Notebook:

1. Start Jupyter Notebook:  
   Ensure your virtual environment is active, then from the project root directory, run:  
   jupyter notebook

2. Your default web browser will automatically open, displaying the Jupyter interface.  
3. Navigate to the notebooks/ directory within the Jupyter interface.  
4. Open the Product\_Feature\_Analysis.ipynb notebook.  
5. Execute all cells in the notebook sequentially. This will guide you through data loading, image downloading, text extraction, and finally, dimension and unit parsing.

### **Using as a Library**

The core functionalities of this project are encapsulated in the src/ modules, allowing you to easily import and use them in your own Python scripts or applications.

Here are examples of how to import and use the key functions:

\# Import core functions from your project's src modules  
from src.data\_processing import download\_images, extract\_text\_from\_image  
from src.feature\_extraction import extract\_dimensions, entity\_unit\_map, allowed\_units, unit\_abbreviation\_map, irregular\_plurals

\# Example 1: Downloading images  
\# Assume 'df' is a pandas DataFrame with an 'image\_link' column  
\# import pandas as pd  
\# df \= pd.read\_csv('../dataset/your\_product\_data.csv') \# Adjust path to your dataset  
\# image\_links \= df\['image\_link'\].tolist()  
\# download\_folder \= '../images' \# Relative path for downloaded images  
\# download\_images(image\_links, download\_folder)  
\# print(f"Images have been downloaded to: {download\_folder}")

\# Example 2: Extracting text from a single image  
image\_path\_example \= '/path/to/your/downloaded\_image.jpg' \# IMPORTANT: Replace with the actual path to one of your downloaded images'  
extracted\_text \= extract\_text\_from\_image(image\_path\_example)  
if extracted\_text:  
    print(f"\\nExtracted Text from {image\_path\_example}:")  
    print(extracted\_text)  
else:  
    print(f"\\nCould not extract text from {image\_path\_example}.")

\# Example 3: Extracting dimensions and units from text  
sample\_product\_description \= "The package contains a widget measuring 12.5 cm x 5 in and weighing 2 lbs. It needs 220V."  
extracted\_features \= extract\_dimensions(sample\_product\_description)  
print(f"\\nExtracted Dimensions and Units from sample text:")  
print(extracted\_features)

\# You can then process 'extracted\_features' further based on your needs.

## **Contributing**

We welcome contributions to this project\! If you have suggestions for improvements, find a bug, or want to add new features, please follow these guidelines:

1. **Open an Issue:** Before submitting a pull request, please open an issue to discuss the bug or feature you'd like to address. This helps to ensure no duplicate work and aligns with the project's goals.  
2. **Fork the Repository:** Create your own fork of the project on GitHub.  
3. **Create a New Branch:** Create a new branch from main (or master) for your feature or bug fix:  
   git checkout \-b feature/your-feature-name  
   \# or: git checkout \-b bugfix/your-bug-fix-description

4. **Make Your Changes:** Implement your changes, ensuring your code adheres to the existing style and conventions.  
5. **Write Clear Commit Messages:** Use descriptive commit messages that explain the purpose of your changes.  
6. **Push Your Branch:** Push your new branch to your forked repository.  
   git push origin feature/your-feature-name

7. **Open a Pull Request:** Open a pull request from your branch to the main (or master) branch of the original repository. Provide a clear description of your changes and reference any related issues.

## **License**

This project is licensed under the **MIT License**. You can find the full license text in the LICENSE file within this repository.

## **Copyright (c) 2024 Anmol Pokhriyal**

## **Acknowledgments**

* **Tesseract OCR:** The open-source OCR engine used for text extraction.  
* **Pillow (PIL Fork):** For robust image processing capabilities in Python.  
* **pytesseract:** The Python wrapper that allows seamless integration with Tesseract OCR.  
* **pandas:** An essential library for data manipulation and analysis.  
* **tqdm:** Provides elegant progress bars for loops and operations.  
* **requests:** (If you use this library for more advanced HTTP requests for image downloading in data\_processing.py).  
* **Jupyter:** For providing an interactive computing environment.  
* Special thanks to the open-source community for their invaluable tools and libraries.