# KakekKuKaku — Diabetes Risk Discord Bot

A Discord bot that estimates diabetes risk from a machine-learning model and presents the result as a clean interactive embed.

## How it works

```
Discord user
   │  button-based questionnaire
   ▼
Node.js bot (bot.js, discord.js)
   │  HTTP POST /predict
   ▼
Python inference API (api.py, http.server)
   │  XGBoost model + scaler (joblib)
   ▼
Risk prediction → embed response
```

## Model

- **Algorithm:** XGBoost classifier
- **Features:** age, hypertension, heart disease, BMI, HbA1c level, blood glucose level, gender, smoking status
- **Artifacts:** `train_result/diabetes_xgboost.pkl`, `train_result/diabetes_scaler.pkl`
- Training and evaluation live in `train_model/`

## Project structure

```
api.py            inference HTTP server (/predict)
bot.js            Discord bot (discord.js, buttons, embeds)
train_model/      training notebook / scripts
train_result/     serialized model and scaler
photos/           screenshots
```

## Screenshots

| Training result | Discord bot |
|---|---|
| ![Training](photos/image.png) | ![Bot](photos/image2.png) |

## Running locally

1. **Start the inference API**

   ```bash
   pip install pandas scikit-learn xgboost joblib
   python api.py
   ```

   The API listens for `POST /predict` with the feature payload.

2. **Configure the bot**

   ```bash
   npm install discord.js
   # set your bot token / API URL in bot.js
   node bot.js
   ```

3. Use the bot in Discord and answer the questionnaire via buttons.

## Disclaimer

This project is for academic exploration only. It is **not** a medical device and must not be used for real diagnosis or treatment decisions.
