# DeepShield

DeepShield is a deepfake detection project with a Python + FastAPI backend and a Flutter mobile app frontend. This README explains the folder structure and how to make the project functional for development.

## Table of Contents
- [Project Structure](#project-structure)  
- [Backend Setup](#backend-setup)  
- [Flutter Frontend Setup](#flutter-frontend-setup)  
- [Running the Project](#running-the-project)  
- [Notes & Tips](#notes--tips)

## Project Structure
Root layout:
```
DeepShield/
│
├── deepshield-backend/      # Python + FastAPI + ML
├── deepshield-app/          # Flutter mobile app
└── docs/                    # Diagrams, notes, sample data (optional)
```

Backend layout (deepshield-backend/):
```
deepshield-backend/
├── app/
│   ├── main.py              # FastAPI app entrypoint
│   ├── api/routes/          # HTTP routes
│   │   ├── classify.py      # /api/classify  (deepfake detection)
│   │   ├── reports.py       # /api/report    (forensic report generation)
│   │   └── blockchain.py    # /api/anchor    (Polygon integration)
│   ├── ml/                  # ML logic
│   │   ├── model_loader.py
│   │   ├── preprocess.py
│   │   ├── inference.py
│   │   └── gradcam.py
│   ├── reports/             # PDF + QR report generation
│   ├── blockchain/          # Smart contract interaction & hashing
│   ├── core/                # Settings and logging
│   ├── utils/               # Helper functions (file validation, etc.)
│   └── models/              # Stored pretrained models (.h5 placeholders)
├── tests/                   # Unit tests & evaluation scripts
└── requirements.txt
```

Frontend layout (deepshield-app/):
```
deepshield-app/
├── lib/
│   ├── main.dart
│   ├── screens/             # Splash, Home, Result screens
│   ├── services/            # API calls to backend
│   ├── widgets/             # Reusable UI widgets
│   ├── utils/               # Constants, config (API URLs, timeouts)
│   └── models/              # Dart classes for JSON responses
├── assets/                  # Images and icons
├── pubspec.yaml
└── README.md
```

## Backend Setup
1. Create and activate a virtual environment:
```bash
# Create venv
python -m venv venv

# Activate (Linux/macOS)
source venv/bin/activate

# Activate (Windows PowerShell)
venv\Scripts\Activate.ps1

# Activate (Windows cmd)
venv\Scripts\activate
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Run FastAPI:
```bash
uvicorn app.main:app --reload
```
API base: http://127.0.0.1:8000  
Key route: POST /api/classify (expects image upload, returns JSON prediction).

Notes:
- Place pretrained .h5 models in `app/models/`.
- Routes under `app/api/routes/` are modular and expandable.
- Use `tests/` to validate endpoints and model behavior.

## Flutter Frontend Setup
1. Install Flutter SDK: https://docs.flutter.dev/get-started/install

2. Get dependencies:
```bash
cd deepshield-app
flutter pub get
```

3. (Optional) Generate platform folders if missing:
```bash
# Run in deepshield-app/
flutter create .
```

4. Configure API base URL:
- Edit `lib/utils/api_constants.dart` to point to the backend (e.g., http://127.0.0.1:8000).

5. Run the app:
```bash
flutter run
```
Ensure backend is running when testing API calls.

## Running the Project
- Start backend first (uvicorn).  
- Start Flutter app (flutter run).  
- Use sample images in `deepshield-backend/tests/` for evaluation.

## Notes & Tips
- Platform folders (android/, ios/, web/) are intentionally omitted to keep the repo lightweight; generate them with `flutter create .` when needed.
- Replace placeholder models in `deepshield-backend/app/models/` with trained `.h5` files.
- Use `deepshield-backend/tests/` to automate verification of predictions and endpoints.
- Add diagrams and sample data to `docs/` for collaborators.

This README should allow a developer to clone the repo, set up backend & frontend, and begin development quickly.