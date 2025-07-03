import streamlit as st

st.set_page_config(page_title="Burnout Score Calculator", layout="centered")

st.title("🔥 Burnout Score Calculator")
st.write("Rate each statement from 1 (Never) to 5 (Always)")

questions = {
    "Workload & Stress": [
        ("I feel emotionally drained after work.", False),
        ("I find it hard to concentrate lately.", False),
        ("I often work late or skip breaks.", False)
    ],
    "Sleep & Recovery": [
        ("I get at least 7 hours of restful sleep.", True),
        ("I feel refreshed when I wake up.", True),
        ("I take regular screen-free breaks during the day.", True)
    ],
    "Joy & Engagement": [
        ("I still enjoy the work I do.", True),
        ("I feel a sense of purpose in daily life.", True),
        ("I have hobbies or activities I enjoy weekly.", True)
    ],
    "Social Support": [
        ("I talk to friends/family regularly.", True),
        ("I feel supported at work or home.", True),
        ("I’ve laughed with someone in the past 3 days.", True)
    ]
}

total_score = 0
max_score = len(questions) * 3 * 5

for category, qs in questions.items():
    st.subheader(category)
    for q_text, is_positive in qs:
        rating = st.slider(f"• {q_text}", 1, 5, 3)
        total_score += rating if is_positive else (6 - rating)

# 🧠 Show result after all sliders are filled
if st.button("Calculate Burnout Score"):
    st.markdown(f"### ✅ Your Burnout Score: {total_score} / {max_score}")

    if total_score <= 20:
        level = "🚨 SEVERE"
        note = "Hypertension, insomnia, and fatigue are common at this level."
        tips = "- Deep breathing\n- Magnesium-rich foods\n- No caffeine after 2 PM"
    elif total_score <= 35:
        level = "⚠️ MODERATE"
        note = "Linked to lowered immunity and sleep issues."
        tips = "- Gratitude journaling\n- 10-min stretch\n- Guided meditation"
    elif total_score <= 50:
        level = "🌤️ MILD STRESS"
        note = "Can subtly affect mood and focus over time."
        tips = "- Nature walks\n- Herbal tea\n- Fun creative time"
    else:
        level = "🌈 LOW"
        note = "You’re thriving! Keep up the good work."
        tips = "- Protect weekends\n- Try new hobbies\n- Celebrate yourself!"

    st.success(f"**Burnout Level: {level}**\n\n🧠 *{note}*\n\n💡 Tips:\n{tips}")

