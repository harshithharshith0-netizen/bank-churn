import streamlit as st
import pickle
import numpy as np

model = pickle.load(open("churn_model.pkl","rb"))

st.title("Bank Customer Churn Prediction")

credit_score = st.number_input("Credit Score")
age = st.number_input("Age")
balance = st.number_input("Balance")
products = st.number_input("Number of Products")

if st.button("Predict"):

    data = np.array([[credit_score, age, balance, products]])
    prediction = model.predict(data)

    if prediction == 1:
        st.error("Customer likely to churn")
    else:
        st.success("Customer likely to stay")