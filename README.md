# sustainability-profiler
import streamlit as st
import pandas as pd
import numpy as np

st.set_page_config(page_title="Carbon Emission Cluster Predictor", layout="centered")
st.title("🌍 Carbon Emission Cluster Predictor")
st.markdown("Enter your company's environmental metrics to predict the sustainability cluster.")

# Input fields
co2_emission = st.slider("CO2 Emissions (tons/year)", 0.0, 50000.0, 5000.0)
energy_use = st.slider("Energy Use (MWh/year)", 0.0, 100000.0, 10000.0)
supply_chain_emission = st.slider("Supply Chain Emissions (%)", 0.0, 100.0, 50.0)
water_consumption = st.number_input("Water Consumption (litres/year)", 0)
air_quality_index = st.slider("Air Quality Index", 0, 500, 100)
green_certified = st.radio("Green Certification", ["Certified", "Not certified"])
regulatory_compliance = st.radio("Regulatory Compliance", ["Compliant", "Not compliant"])

# Dummy prediction logic (replace with real model later)
def dummy_predict(co2, energy, supply_chain, water, air, certified, compliance):
    score = co2 * 0.3 + energy * 0.2 + supply_chain * 10 + water * 0.0001 + air
    if certified == "Not certified":
        score += 500
    if compliance == "Not compliant":
        score += 500

    if score < 3000:
        return "Cluster 1 - Low Emission"
    elif score < 7000:
        return "Cluster 2 - Moderate Emission"
    else:
        return "Cluster 3 - High Emission"

# Predict button
if st.button("Predict Cluster"):
    cluster = dummy_predict(
        co2_emission,
        energy_use,
        supply_chain_emission,
        water_consumption,
        air_quality_index,
        green_certified,
        regulatory_compliance
    )
    st.success(f"🏷️ Predicted Sustainability Cluster: {cluster}")

    if "High Emission" in cluster:
        st.warning("Consider adopting stricter sustainability measures and obtaining certifications.")
    elif "Moderate" in cluster:
        st.info("You're on the right path. Enhancing compliance and certifications will help.")
    else:
        st.balloons()
        st.success("Great job! You're in the sustainable zone.")
