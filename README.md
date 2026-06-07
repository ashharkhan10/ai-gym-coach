# 🏋️‍♂️ AI Real-time GYM Coach
 
An AI-powered gym coaching web app that uses your camera to detect exercise form in real time, counts reps and sets, and delivers live voice feedback via an LLM-powered coach.
 
**Live Demo:** [personal-ai-gym-coach.streamlit.app](https://personal-ai-gym-coach.streamlit.app)
 
---
 
<!-- Add screenshot here -->
 
---
 
## Features
 
- **Real-time pose detection** using MediaPipe via webcam
- **5 supported exercises:** Squats, Push-ups, Bicep Curls, Shoulder Press, Lunges
- **Automatic rep and set counting** with per-exercise form metrics
- **AI voice coaching** powered by Groq (LLaMA 3.3 70B) and gTTS — speaks corrections and motivation aloud
- **Form analysis** with exercise-specific feedback (e.g. knee angle, back arch, hip position)
- **Workout history** stored locally in SQLite and displayed per session
- **User login** via unique username — no password required
- **CI pipeline** via GitHub Actions (linting on every push)
---
 
## Tech Stack
 
| Layer | Technology |
|---|---|
| Frontend & App | Streamlit |
| Pose Detection | MediaPipe Pose Landmarker |
| Camera Streaming | streamlit-webrtc + WebRTC |
| LLM Coaching | Groq API (LLaMA 3.3 70B) |
| Text-to-Speech | gTTS |
| Video Processing | OpenCV |
| Database | SQLite |
| Deployment | Streamlit Cloud |
 
---
 
## Project Structure
 
```
ai-gym-coach/
├── app.py                        # Main Streamlit app
├── core/
│   └── base_exercise.py          # Abstract base class for exercise detectors
├── detectors/                    # Per-exercise pose logic
│   ├── squat.py
│   ├── pushup.py
│   ├── biceps_curl.py
│   ├── shoulder_press.py
│   └── lunges.py
├── services/
│   ├── auth/                     # Username-based login
│   ├── coaching/                 # LLM, TTS, and voice pipeline
│   ├── config/                   # Exercise options and LLM prompt
│   ├── persistence/              # SQLite repository
│   ├── state/                    # Streamlit session defaults
│   ├── tracking/                 # Metrics sync logic
│   ├── ui/                       # CSS and font loader
│   └── vision/                   # WebRTC video processor
├── ml_models/
│   └── pose_landmarker_full.task # MediaPipe model file
├── static/
│   └── style.css                 # Custom dark theme styles
├── requirements.txt
├── packages.txt
└── .github/workflows/ci.yml      # GitHub Actions CI
```
 
---
 
## Running Locally
 
**1. Clone the repo**
```bash
git clone https://github.com/ashharkhan10/ai-gym-coach
cd ai-gym-coach
```
 
**2. Install dependencies**
```bash
pip install -r requirements.txt
```
 
**3. Add your Groq API key**
 
Create a `.env` file in the root:
```
GROQ_API_KEY=your_groq_api_key_here
```
 
Or add it to `.streamlit/secrets.toml`:
```toml
GROQ_API_KEY = "your_groq_api_key_here"
```
 
**4. Run the app**
```bash
streamlit run app.py
```
 
---
 
## Deployment
 
Deployed on **Streamlit Cloud** with auto-redeploy on every push to `main`.
 
The `GROQ_API_KEY` is stored in Streamlit Cloud's secrets manager.
 
System dependencies (OpenCV, MediaPipe) are declared in `packages.txt`.
 
---
 
## CI/CD
 
GitHub Actions runs on every push and pull request to `main`:
- Lints the codebase using `ruff`
- Fails the pipeline if any unused variables or import errors are found
---
 
## Exercises & Metrics
 
| Exercise | Metrics Tracked |
|---|---|
| Squats | Knee angle, back angle, depth status |
| Push-ups | Elbow angle, body alignment, hip position |
| Bicep Curls | Elbow angle, shoulder stability, swing detection |
| Shoulder Press | Elbow angle, arm extension, back arch |
| Lunges | Front knee angle, torso angle, balance status |
 
---
 
## Author
 
Built by [@ashharkhan10](https://github.com/ashharkhan10)
 