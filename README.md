# Resume-Scanner

A web application to automatically predict the job category of a resume using machine learning. Upload a resume in PDF, DOCX, or TXT format and the app will analyze its content and predict the most likely job category.

## Features

- **Resume Category Prediction:** Upload a resume and get a machine learning-based prediction of its job category.
- **Multiple File Formats Supported:** Accepts PDF, DOCX, and TXT files.
- **Automatic Text Extraction:** Extracts and processes text from uploaded resumes.
- **Clean & Preprocess Text:** Removes URLs, special characters, and unicode for accurate predictions.
- **Interactive Web Interface:** Built with Streamlit for an easy-to-use interface.

## Demo

![Resume Scanner Demo](demo.gif) <!-- Add demo gif/image if available -->

## Getting Started

### Prerequisites

Install the following Python packages:

```bash
pip install streamlit scikit-learn python-docx PyPDF2
```

Make sure the following model files are present in the root or specified directory:
- `clf.pkl` (trained classifier model)
- `tfidf.pkl` (TF-IDF vectorizer)
- `encoder.pkl` (LabelEncoder for categories)

### Running the App

```bash
streamlit run src/app.py
```

Open the provided URL in your browser to access the app.

## Usage

1. **Upload Resume:** Click 'Browse files' and upload a resume in PDF, DOCX, or TXT format.
2. **Extracted Text:** Optionally, view the extracted text before prediction.
3. **Get Prediction:** The app will display the predicted job category for the uploaded resume.

## Project Structure

```
Resume-Scanner/
├── src/
│   └── app.py
├── clf.pkl
├── tfidf.pkl
├── encoder.pkl
└── README.md
```

- `src/app.py` - Main Streamlit application.
- `clf.pkl`, `tfidf.pkl`, `encoder.pkl` - Pre-trained model and supporting files.

## How It Works

1. **Upload & Extraction:** The app handles file uploads and extracts text using:
   - PyPDF2 for PDFs
   - python-docx for DOCX files
   - UTF-8/latin-1 decoding for TXT files

2. **Cleaning:** Text is cleaned (removing URLs, special characters, etc.).

3. **Prediction Pipeline:**
   - Cleaned text is vectorized using the pre-trained TF-IDF vectorizer.
   - The vector is fed into the SVM classifier (`clf.pkl`).
   - The predicted category is decoded using the LabelEncoder.

4. **Display Result:** The user is shown the predicted category.

## Code Example

```python
# Example: Predict category from resume text
resume_text = "Experienced Python developer..."
cleaned = cleanResume(resume_text)
vectorized = tfidf.transform([cleaned]).toarray()
category = svc_model.predict(vectorized)
result = le.inverse_transform(category)
print("Predicted category:", result[0])
```

## Dependencies

- [streamlit](https://streamlit.io/)
- [scikit-learn](https://scikit-learn.org/)
- [python-docx](https://python-docx.readthedocs.io/en/latest/)
- [PyPDF2](https://pypdf2.readthedocs.io/en/latest/)

## Notes

- Ensure the model files (`clf.pkl`, `tfidf.pkl`, `encoder.pkl`) are present and were trained using the same preprocessing pipeline.
- For best results, use clear and complete resumes.

## License

MIT License. See [LICENSE](LICENSE).

## Author

Created by [eshPra](https://github.com/eshPra).
