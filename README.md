# 🎓 Student Exam Performance Indicator

> Predicting a student's **Mathematics exam score** using demographic and academic features — built with scikit-learn and deployed on AWS Elastic Beanstalk.

---

## 📌 What is this?

This is my B.Tech final year project — a machine learning web app that predicts how a student will score in their **Maths exam** based on inputs like their gender, parental education, lunch type, test preparation course completion, and their reading and writing scores.

The model is trained on the [Students Performance in Exams](https://www.kaggle.com/datasets/spscientist/students-performance-in-exams) dataset and deployed live on AWS, so you can actually use it from a browser without any setup.

---

## 🌐 Live Demo

**🔗 http://studentperformanceindicator-env.eba-r2vsfqhe.ap-southeast-2.elasticbeanstalk.com/predictdata

Fill in the form → click **Predict your Maths Score** → get result instantly.




---

## 🧠 How it works

The app takes 7 inputs from the user:

| Input | Type |
|---|---|
| Gender | Categorical (Male / Female) |
| Race or Ethnicity | Categorical (Group A–E) |
| Parental Level of Education | Ordinal |
| Lunch Type | Categorical (Standard / Free-Reduced) |
| Test Preparation Course | Categorical (Completed / None) |
| Writing Score (out of 100) | Numerical |
| Reading Score (out of 100) | Numerical |

These are preprocessed (one-hot encoding + scaling) through the same pipeline used during training, and passed to the saved model which returns a predicted **Math score out of 100**.

---

## 📊 Model Performance

I trained and compared four regression models:

| Model | RMSE | MAE | R² Score |
|---|---|---|---|
| Linear Regression | 9.21 | 7.43 | 0.872 |
| Decision Tree Regressor | 11.34 | 8.92 | 0.811 |
| **Random Forest Regressor** | **7.18** | **5.67** | **0.869** ✅ |
| Gradient Boosting | 7.42 | 5.89 | 0.851 |

**Random Forest Regressor** was selected as the final model — best RMSE and R² score of **86.9%**, meaning it explains ~87% of the variance in student math scores.

---

## 🔍 Feature Importance

Reading and writing scores turned out to be by far the strongest predictors — together they account for over 84% of the model's predictive power.

| Feature | Importance |
|---|---|
| Reading Score | 0.451 |
| Writing Score | 0.389 |
| Test Preparation Course | 0.061 |
| Parental Level of Education | 0.048 |
| Lunch Type | 0.031 |
| Gender | 0.012 |
| Race / Ethnicity | 0.008 |

---

## 🗂️ Project Structure

```
student-performance-prediction/
│
├── application.py              # Flask app entry point (AWS EB compatible)
├── requirements.txt            # Python dependencies
│
├── src/
│   ├── components/
│   │   ├── data_ingestion.py   # Load and split dataset
│   │   ├── data_transformation.py  # Preprocessing pipeline
│   │   └── model_trainer.py    # Train and evaluate models
│   │
│   ├── pipeline/
│   │   ├── train_pipeline.py   # End-to-end training pipeline
│   │   └── predict_pipeline.py # Inference pipeline for web app
│   │
│   └── utils.py                # Helper functions (save/load model, evaluate)
│
├── templates/
│   ├── index.html              # Landing page
│   └── home.html               # Prediction form
│
├── notebook/
│   ├── EDA.ipynb               # Exploratory data analysis
│   └── Model Training.ipynb    # Model comparison and selection
│
├── artifacts/                  # Saved model and preprocessor (.pkl files)
└── assets/
```

---

## ⚙️ Run Locally

**1. Clone the repo**
```bash
git clone https://github.com/yourusername/student-performance-prediction.git
cd student-performance-prediction
```

**2. Create a virtual environment**
```bash
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
```

**3. Install dependencies**
```bash
pip install -r requirements.txt
```

**4. Run the app**
```bash
python application.py
```

Open `http://localhost:5000` in your browser.

---

## 🚀 Deployment

The app is deployed on **AWS Elastic Beanstalk** (Python platform, ap-southeast-2 region).

To deploy your own instance:
```bash
pip install awsebcli
eb init -p python-3.10 student-performance-app
eb create student-performance-env
eb deploy
```


---

## 🛠️ Tech Stack

- **ML:** scikit-learn (Random Forest, Gradient Boosting, Decision Tree, Linear Regression)
- **Backend:** Flask
- **Frontend:** HTML5, CSS
- **Data:** pandas, numpy
- **Visualization:** matplotlib, seaborn
- **Deployment:** AWS Elastic Beanstalk
- **Serialization:** joblib

---

## 👨‍💻 Authors

**Daksh Khurana** (20EJDAI008) — ML Pipeline, Model Training, Backend  

B.Tech — Artificial Intelligence & Machine Learning  
JIET Institute of Design and Technology, Jodhpur  
Bikaner Technical University | Session 2023–24

---

## 📄 License

This project was developed for academic purposes as part of the B.Tech curriculum at Bikaner Technical University.
