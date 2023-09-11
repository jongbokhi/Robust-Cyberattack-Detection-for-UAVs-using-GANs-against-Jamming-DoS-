Topic: Robust Cyberattack Detection for UAVs using GANs against Jamming DoS
- Dataset: CSE-CIC-IDS2018 

# Objective
This study aims to show the vulnerability of ML-based NIDS to adversarial attacks and to increase the robustness of ML-based NIDS through adversarial training. In particular, the generation of adversarial samples using the existing GAN model is generated without specific constraints on the network domain, so there was a concern about unrealistic adversarial samples. Therefore, to address this concern, this study used WCGAN-GP to constrain the class label and complemented it with the A2PM module to generate realistic adversarial samples that meet the constraints of the network domain under the grey box setting.  In other words, this study used realistic adversarial samples to perform adversarial attacks and adversarial training.

#Procedure : You can check the code corresponding with below titles. 

1. Preprocessing dataset
   - Cleaning dataset
3. Feature Selection
   - Feature_Selection
   
5. Build Machine Learning Models and Evaluation
   - GridSearch_Cross_validation
   - Visualization_reuslts_of_evaluation
   
------------ the purpose of Adversarial attacks and Adversarial training-----------

6. Build WCGAN-GP Model
   - Adversarial_sample_wcgan_gp
  
7. Adaptive Perturbation Pattern Method (A2PM)
   - A2PM_Directly_attack_pretrained_models
   - Adversarial_training_A2PM
   - Adversarial_attack_to_adversarial_trained_models
   
9. The result
   - plot_adversarial_training_before&after

#WCGAN-GP Architecture

![image](https://github.com/jongbokhi/Robust-Cyberattack-Detection-for-UAVs-using-GANs-against-Jamming-DoS-/assets/105177081/8e561988-3b9f-4ee9-af5f-7f72cea44217)

![image](https://github.com/jongbokhi/Robust-Cyberattack-Detection-for-UAVs-using-GANs-against-Jamming-DoS-/assets/105177081/02d1507a-0067-4005-92c5-56ac13e666f1)

![image](https://github.com/jongbokhi/Robust-Cyberattack-Detection-for-UAVs-using-GANs-against-Jamming-DoS-/assets/105177081/8c9a6177-776d-4bbb-b2c8-088e74d34507)



#Experimental Design


![image](https://github.com/jongbokhi/Robust-Cyberattack-Detection-for-UAVs-using-GANs-against-Jamming-DoS-/assets/105177081/3ddec6d8-5919-4c7e-ad94-737f5b69c842)


a trained generator within the WGCGAN-GP framework was used to generate fake-benign data in the initial phase of this study. This fake-benign dataset was created to resemble genuine samples closely and was produced by the trained generator. Next, we combined this fake-benign dataset with the original test dataset for performing adversarial attacks on pre-trained models and the original dataset for adversarial training purposes. To ensure the comparability and reliability of our findings, we employed an identical combined test dataset previously used to evaluate directly attacked models when assessing our adversarially trained models.


# Analysis of the Result

I summarized code for visualization of the result of analysis in 'plot_adversarial_training_before&after' section.

I analyzed the results of an adversarial attack on a pre-trained machine learning model and the performance of the model after adversarial training. In Figures 5.12 to 5.25, red lines show after adversarial training, and blue lines mean before adversarial training. 

When I checked the result of adversarial trianing, It is evident that the F1 and Recall scores have a higher value in the red line than the blue line across all models. Unlike the pre-trained models, the adversarially trained models exhibited a less steep decline in the slope during repeated attacks. Another observation is that, except for SVM, the pre-trained models succumbed to the adversarial DoS attack at an earlier stage than the adversarially trained models.

Especially, XGBoost, LightGBM, and LogisticRegression models showed significant performance improvements after adversarial training. In other words, they could detect adversarial DoS attacks more robustly. Pre-trained XGBoost model was exploited for 15 iterations of attacks. Pre-trained XGBoost reached approximately 47.4% of the F1 score and 50% of the Recall score at the last 15 adversarial attacks. Still, adversarial trained XGBoost showed 73% of F1 score and 66.5%, which improved by 25.6% and 16.5% each during 15 iterations. In the case of the pre-trained LightGMB model, it failed after 11 iterations and showed a 47.4% F1 score and 50% recall score. At the same time, the adversarially trained LightGBM increased to 86.2% F1 score and 79.7% recall score by 38.8% and 29.7%, respectively, showing the best performance improvement over others. The pre-trained logistic regression model withstood 50 iterations of attack and achieved a relatively higher F1 score of 59.3% and a higher recall score of 56.6% in the last iteration compared to XGBoost and LightGBM. It also increased by 13.3% and 9.5%, respectively, the smallest difference between the two scores before and after the adversarial attack.

Finally, LightGBM and Logistic Regression demonstrated significant robustness against the adversarial DoS attacks after adversarial training throughout the 50 iterations. In particular, LightGBM consistently maintained F1 values between 69.5% and 72.3% during iterations 40 to 50. On the other hand, Logistic Regression maintained F1 values between 72.2% and 76.2% throughout the same iterations. In addition, in the last 10 iteration attacks, both models retained approximately over 60% of the recall score.

In conclusion, it's clear that adversarial training significantly enhanced the detection capabilities of all seven models. LightGBM and Logistic Regression demonstrated substantial improvement in detecting adversarial DoS attacks. However, when compared directly, Logistic Regression surpassed LightGBM in performance.
