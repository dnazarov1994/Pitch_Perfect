# Pitch Perfect
The Pitch Perfect app allows users to record their voice and then modulate the recorded audio to sound in a different frequency. This app also lets the user speed up or slow down the rate of playback, and experience fun echo and reverb effects.


<img width="400" alt="Screen Shot 2019-08-18 at 12 01 28 AM" src="https://user-images.githubusercontent.com/46335329/63219975-2e4d3d80-c14c-11e9-809e-8ff3e3ee734d.png">

<img width="401" alt="Screen Shot 2019-08-18 at 12 01 53 AM" src="https://user-images.githubusercontent.com/46335329/63219982-5177ed00-c14c-11e9-9e09-0861bff94472.png">

## App Implementation
The app has two view controller scenes:
- Record Sounds View Controller: Allows the user to record the voice.

```
@IBAction func recordAudio(_ sender: Any) {
        recordingLabel.text = "Recording in Progress"
        toggleControlButtons(state: false)
        
        let dirPath = NSSearchPathForDirectoriesInDomains(.documentDirectory,.userDomainMask, true)[0] as String
        let recordingName = "recordedVoice.wav"
        let pathArray = [dirPath, recordingName]
        let filePath = URL(string: pathArray.joined(separator: "/"))
        
        let session = AVAudioSession.sharedInstance()
        try! session.setCategory(AVAudioSession.Category.playAndRecord, mode: AVAudioSession.Mode.default, options: AVAudioSession.CategoryOptions.defaultToSpeaker)
        
        try! audioRecorder = AVAudioRecorder(url: filePath!, settings: [:])
        audioRecorder.delegate = self
        audioRecorder.isMeteringEnabled = true
        audioRecorder.prepareToRecord()
        audioRecorder.record()
    }
```
- Play Sounds View Controller: Allow the user to play recorded audio in a different frequency. 

```
@IBAction func playSoundForButton(_ sender: UIButton) {
        switch(ButtonType(rawValue: sender.tag)!) {
        case .slow:
            playSound(rate: 0.5)
        case .fast:
            playSound(rate: 1.5)
        case .chipmunk:
            playSound(pitch: 1000)
        case .vader:
            playSound(pitch: -1000)
        case .echo:
            playSound(echo: true)
        case .reverb:
            playSound(reverb: true)
        }
        
        configureUI(.playing)
    }
```
## Alerts
```
 struct Alerts {
        static let DismissAlert = "Dismiss"
        static let RecordingDisabledTitle = "Recording Disabled"
        static let RecordingDisabledMessage = "You've disabled this app from recording your microphone. Check Settings."
        static let RecordingFailedTitle = "Recording Failed"
        static let RecordingFailedMessage = "Something went wrong with your recording."
        static let AudioRecorderError = "Audio Recorder Error"
        static let AudioSessionError = "Audio Session Error"
        static let AudioRecordingError = "Audio Recording Error"
        static let AudioFileError = "Audio File Error"
        static let AudioEngineError = "Audio Engine Error"
    }
```
## Requirements
- Xcode 9.2
- Swift 4.0




