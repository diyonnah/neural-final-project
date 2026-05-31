# App Flow and Status

## Flow (Current App)
1. User uploads a mango leaf image in the UI (drag/drop or file picker).
2. Frontend sends the file as FormData to POST /api/predict (field name: image).
3. Vercel serverless backend loads the model and pre-processes the image:
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

## Deployment Readiness (Vercel Only)
- The backend is now a Vercel serverless function at /api/predict.
- No separate backend host is required.

## Vercel-Only Deployment Steps
1. Push the project to GitHub.
2. Import the repo into Vercel.
3. Vercel will deploy the static frontend and the /api/predict serverless function.
4. Confirm uploads and predictions work from the Vercel site.

## Updates Mentioned
- Model loading now checks model/ and project root.
- Frontend now calls /api/predict for Vercel serverless.
