## Preprocessing & Data Pipeline

- Data Handling: Load the Mini Speech Commands dataset. Map target command folders (e.g., "up", "down", "stop") to integer class indices and create a reverse mapping dictionary for predictions. Split the dataset into 80% Train, 10% Validation, and 10% Test.  
- Feature Extraction (Implementation): Transform raw 1D acoustic signals into 2D spatial feature maps by computing Log-Mel Spectrograms.  
- Feature Extraction (Markdown Alternative): Discuss MFCCs (Mel-frequency Cepstral Coefficients) as a theoretical alternative for compressing spectral information.  
      
- Implementation Flow:  

1. Standardize raw audio length by padding or truncating clips to exactly 1 second.  
2. Apply Short-Time Fourier Transform (STFT) to compute the Log-Mel Spectrograms using torchaudio or librosa.  
3. Normalize the extracted features to zero mean and unit variance.  

## Architecture Selection & Implementation

- Primary Candidate (2D CNN - Selected): Treat the Log-Mel Spectrogram matrix ($1 \times \text{freq} \times \text{time}$) as a 1-channel image. Implement Convolutional, MaxPool, and Dropout layers to extract localized acoustic patterns like formant transitions and phonemes.  
      
- Baseline Model (Dense/MLP - Implemented for Comparison): Flatten the spectrogram input into a 1D vector and feed it into fully connected Dense layers. Use this to demonstrate how it ignores local spatial-temporal relationships compared to the CNN.  
    
- Alternative Candidates (Markdown Alternative): Discuss 1D CNNs (for raw waveforms) and CRNNs (combining CNN feature extraction with LSTM/GRU layers) as theoretical options for sequence dependencies.  
      

## Training & Evaluation Protocol

- Training Dynamics: Plot loss and accuracy curves across epochs for both the 2D CNN and the MLP baseline to explicitly compare convergence speed and model stability.  
      
- Quantitative Metrics: Calculate overall Accuracy, Loss, and per-class Precision, Recall, and F1-Score.  
      
- Confusion Matrix: Generate a matrix to evaluate class-specific performance, specifically highlighting critical safety misclassifications (e.g., ensuring "stop" is not confused with "go").  
      

## SLIFTS Advisory & Inference

- Proof of Concept Predictor: Implement a standalone lightweight function (predict_elevator_command(audio_file_path, model)) that processes a raw audio file through your pipeline and returns a predicted command label alongside a confidence score.  
      
- Advisory Recommendations: Summarize the findings for the SLIFTS context in the final markdown cell. Justify the 2D CNN over the MLP (superior spatial generalization) and 1D models (higher accuracy), and emphasize that its low inference latency ensures seamless, real-time responsiveness inside the elevator cabin.