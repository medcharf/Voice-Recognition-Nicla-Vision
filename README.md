# Voice Recognition with Arduino Nicla Vision and Edge Impulse

A complete voice recognition system that detects the wake word "Hello Charfa" using an Arduino Nicla Vision board and Edge Impulse machine learning platform.

## 🎯 Project Overview

This project implements a custom wake word detection system that:
- Continuously listens for the phrase "Hello Charfa"
- Uses machine learning for accurate voice recognition
- Provides real-time inference with confidence scores
- Triggers actions when the wake word is detected
- Runs entirely on-device with no internet connection required

## 🎬 Demo Video

https://github.com/medcharf/Voice-Recognition-Nicla-Vision/demo.MOV
**Demo showcases:**
- 🎙️ Real-time voice recognition in action
- 📊 Live confidence scores and predictions
- 💡 LED feedback when wake word is detected
- ⚡ Response time and accuracy demonstration
- 🔧 Serial monitor output walkthrough

*Click the badge above to watch the full demonstration*

> **Note:** Replace `https://your-video-link-here.com` with your actual video URL (YouTube, Vimeo, etc.)

## 🛠 Hardware Requirements

- **Arduino Nicla Vision** board
- USB-C cable for programming and power
- Built-in PDM microphone (integrated on Nicla Vision)

## 📚 Software Requirements

- **Arduino IDE** (latest version)
- **Edge Impulse account** (free tier available)
- **Edge Impulse CLI tools**
- **Arduino Mbed OS Nicla Boards** package

## 🚀 Getting Started

### 1. Set Up Development Environment

```bash
# Install Edge Impulse CLI
npm install -g edge-impulse-cli

# Install Arduino IDE and add Nicla Vision board support
# Go to Tools > Board > Board Manager > Search "Arduino Mbed OS Nicla Boards"
```

### 2. Create Edge Impulse Project

1. Visit [edgeimpulse.com](https://edgeimpulse.com) and create an account
2. Create a new project, select "Audio" type
3. Choose "Classification" as the machine learning task

### 3. Data Collection

**Training Data Collected:**
- **"hello_charfa"** class: 75+ samples of the target phrase
- **"noise"** class: 100+ samples of background noise, music, and other speech

**Recording Guidelines:**
- Sample length: 2-3 seconds
- Frequency: 16kHz
- Various pronunciations, volumes, and distances
- Multiple recording sessions for diversity

### 4. Model Training

**Signal Processing:**
- **Processing Block:** Audio (MFCC)
- **Window Size:** 3000ms
- **Window Increase:** 1000ms
- **MFCC Coefficients:** 13

**Neural Network:**
- **Architecture:** Keras Classification
- **Training Cycles:** 100-200 epochs
- **Achieved Accuracy:** >90%

### 5. Deploy to Arduino

1. In Edge Impulse, go to "Deployment"
2. Select "Arduino library"
3. Choose "EON Compiler" optimization
4. Download the generated library ZIP file

## 💻 Installation

1. **Install the Edge Impulse Library:**
   ```
   Arduino IDE > Sketch > Include Library > Add .ZIP Library
   ```

2. **Upload the Code:**
   - Copy the provided Arduino code
   - Replace the include statement with your project name
   - Upload to your Nicla Vision board

## 📋 Code Structure

```cpp
// Key Components:
- PDM microphone initialization and data handling
- Continuous audio buffer management
- Real-time inference processing
- Confidence threshold detection (70%)
- LED feedback for wake word detection
```

## 🔧 Configuration

### Adjustable Parameters

```cpp
#define CONFIDENCE_LEVEL 0.70    // Detection threshold (0.0 - 1.0)
#define SER_INT_VERBOSE 1        // Enable detailed logging
```

### Performance Tuning

- **Lower threshold (0.5-0.6):** More sensitive, may have false positives
- **Higher threshold (0.8-0.9):** Less sensitive, fewer false positives
- **Microphone gain:** Adjustable via `PDM.setGain()` (default: 24)

## 📊 Expected Output

```
Edge Impulse Inferencing Demo
Inferencing settings:
	Interval: 62.5 ms.
	Frame size: 1000
	Sample length: 3000 ms.
	No. of classes: 2

Predictions (DSP: 15 ms., Classification: 12 ms., Anomaly: 0 ms.)
    hello_charfa: 0.92341
    noise: 0.07659

Hey Charfa!!!
```

## 🎯 Features

- ✅ **Real-time Processing:** Continuous audio monitoring with minimal latency
- ✅ **High Accuracy:** >90% classification accuracy on test data
- ✅ **Low Power:** Optimized for embedded deployment
- ✅ **Customizable:** Easy to modify wake word and add new actions
- ✅ **Debug Output:** Detailed inference timing and confidence scores
- ✅ **Visual Feedback:** Built-in LED indicates detection

## 🔍 Troubleshooting

### Common Issues

**Low Detection Accuracy:**
- Collect more training samples
- Ensure diverse recording conditions
- Check microphone positioning

**False Positives:**
- Increase confidence threshold
- Add more "noise" training samples
- Include similar-sounding phrases in noise class

**PDM Initialization Failed:**
- Check board connection
- Verify correct board selection in Arduino IDE
- Restart the board

### Debug Tips

```cpp
// Enable verbose logging
#define SER_INT_VERBOSE 1

// Check inference timing
Serial.print("DSP: "); Serial.print(result.timing.dsp);
Serial.print(" ms, Classification: "); Serial.println(result.timing.classification);
```

## 📈 Model Performance

| Metric | Value |
|--------|--------|
| Training Accuracy | >90% |
| Validation Accuracy | >85% |
| Inference Time | ~27ms |
| Memory Usage | ~32KB RAM |
| Model Size | <100KB Flash |

## 🔄 Extending the Project

### Add New Wake Words
1. Collect training data for new phrases
2. Retrain the model in Edge Impulse
3. Update Arduino code with new labels
4. Deploy updated library

### Add Custom Actions
```cpp
void triggerWakeWordAction() {
    // Add your custom functionality:
    // - Send wireless commands
    // - Control external devices  
    // - Activate other sensors
    // - Log detection events
}
```

## 📄 License

This project is based on Edge Impulse SDK components licensed under the Apache License 2.0.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test with your hardware
5. Submit a pull request

## 📞 Support

- **Edge Impulse Documentation:** [docs.edgeimpulse.com](https://docs.edgeimpulse.com)
- **Arduino Documentation:** [docs.arduino.cc](https://docs.arduino.cc)
- **Hardware Issues:** Check Arduino Nicla Vision documentation

## 🏆 Acknowledgments

- Edge Impulse for the machine learning platform
- Arduino for the Nicla Vision hardware
- Community contributors and testers

---

**Built with ❤️ using Edge Impulse and Arduino**
