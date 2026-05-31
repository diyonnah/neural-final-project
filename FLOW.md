# App Flow and Status

## Flow (Current App)
1. User uploads a mango leaf image in the UI (drag/drop or file picker).
2. Frontend sends the file as FormData to POST /predict (field name: image).
3. Flask backend loads the model and pre-processes the image:
   - convert to grayscale
   - resize to 50x50
   - flatten to 1D array
4. Model predicts Healthy or Unhealthy and returns JSON with result and confidence.
5. Frontend shows the label, emoji, and confidence bar.

## Model Integration Status
- The backend now searches for model files in model/ first, then in the project root.
- MANGO_LEAF_Classifier.sav in the root will load correctly.

## Upload Flow Details
- The browser collects the selected image and stores it in selectedFile.
- On "Classify Leaf", the UI sends FormData with the file under key image.
- The backend accepts image or file as the field name.

## Deployment Readiness
- Not ready for Vercel as-is because Flask is a long-running server.
- A typical fix is to move the Flask API to a server that supports Python services (Render/Railway/Fly) and keep the UI on Vercel.
- Alternative: convert /predict into a Vercel Python serverless function.

## Option 1 Deployment (Render backend + Vercel frontend)
1. Deploy Flask backend to Render (Web Service).
   - Build command: pip install -r requirements.txt
   - Start command: gunicorn app:app
2. Render provides a backend URL (example: https://your-app-name.onrender.com).
3. Update frontend fetch URL to use the backend URL:
   - fetch('https://your-app-name.onrender.com/predict')
4. Deploy the static frontend (index.html) to Vercel.
5. Confirm uploads and predictions work from the Vercel site.

## Updates Mentioned
- Model loading now checks model/ and project root.
- Frontend and backend upload flow is already connected.
