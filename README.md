# InstaDeep Hackathon [Deep Learning Indaba 2024 🇸🇳]

This repository contains the solution to the **InstaDeep Hackathon** where we tackled the problem of recalibrating and filtering predictions from the **InstaNovo** model, which performs _de novo_ peptide sequencing using tandem mass spectrometry data. This solution was awarded firstb place at the hackathon based off the AUC value recorded on the private leaderboard (holdout test set).

## Snakes and Sequences: Senegalese Serpent Venom Sequencing Hackathon

The objective of the Instadeep hackathon is to improve _de novo_ peptide sequencing models used in analyzing snake venoms by recalibrating the confidence measurements and filtering out false positives. Participants are tasked with using inputs and outputs from InstaNovo, a transformer-based sequencing model, along with additional metadata, to enhance the area under the curve (AUC) for the precision-recall graph. The goal is to maximize model performance and accuracy in identifying venom peptides, contributing to the development of more effective antivenoms.

- Leaderboard: https://zindi.africa/competitions/snakes-and-sequences-senegalese-serpent-venom-sequencing-hackathon/leaderboard

---
  
# **InstaNovo Peptide Recalibration and Filtering Solution**


### **Team**
These are the members of Team Kasa, who put together the idea and winning solution.

1. [Ifenaike Alexander](https://www.linkedin.com/in/alexander-ifenaike/) 🇳🇬
2. [Awobade Busayo](https://www.linkedin.com/in/busayo-awobade-107a94175/) 🇳🇬
3. [Babawale Sodiq](https://www.linkedin.com/in/sodiq-babawale-266a78220/) 🇳🇬

### **Objective**

The goal of this project is to improve the confidence calibration and filtering of peptide sequence predictions from the InstaNovo model. This work focuses on recalibrating model outputs, improving the precision-recall AUC, and reducing false positives, all of which are critical for tasks like antivenom production in response to snakebite venom analysis.

### **Approach**

Our approach leverages multiple filtering techniques and feature engineering steps to refine the model's predictions. The final model is a LightGBM binary classifier trained to improve prediction accuracy by recalibrating the confidence scores for the top beam predictions.

---

## **Pipeline Overview**

1. **Input Dataset**
   - Data from InstaNovo, including top beam predictions and additional metadata like retention time, mass-to-charge ratio, and intensity arrays.

2. **Filtering Methods**
   - Filtering rows with empty strings in the Target column and inserting negative infinity in the log probability column. This corresponds to rows where the top 5 peptides predicted by InstaNovo doesn't align with the actual peptide target.
   - Filtering on precursor mass to remove invalid peptide predictions.
   - Filtering using retention time to exclude predictions outside acceptable time ranges.

3. **Feature Engineering**
   - Comparisons between Beam 0 and other beams.
   - Statistical summaries (mean, median, and standard deviation) of `mz_array` and `intensity_array`.

4. **Model Training**
   - Training a LightGBM binary classifier using the engineered features to recalibrate the confidence scores and filter false positives.

5. **Output**
   - Model outputs peptide IDs, target sequences, and recalibrated confidence scores.

## **Files in this Repository**

- `Team_KASA_Instadeep_Winner_Solution.ipynb`: Jupyter notebook with the full solution, including data processing, feature engineering, model training, and evaluation.
- `requirements.txt`: List of dependencies required to run the notebook.

## **Installation Instructions**

1. Clone the repository:
    ```bash
    git clone https://github.com/aifenaike/instadeep-peptide-recalibration.git
    cd instadeep-peptide-recalibration
    ```

2. Install dependencies:
    ```bash
    pip install -r requirements.txt
    ```

3. Run the Jupyter notebook to view the solution:
    ```bash
    jupyter notebook Team_KASA_Instadeep_Winner_Solution.ipynb
    ```

## **Results**

The trained LightGBM model successfully improves the AUC of the precision-recall curve by recalibrating the confidence of the top beam predictions and filtering out false positives. This solution contributes to better identification of venom peptides and can potentially aid in antivenom development.

## **Contributing**

Contributions are welcome! Please feel free to submit a pull request or raise an issue to discuss improvements or new features.

## **Acknowledgments**

Special thanks to the organizers of the Deep Learning Indaba, **InstaDeep**, Zindi and the developers of the InstaNovo model for providing the data and inspiration for this work.



