import streamlit as st
from datetime import datetime
import json

# ตั้งค่าหน้า
st.set_page_config(
    page_title="Self-Caring App",
    page_icon="🌿",
    layout="wide",
    initial_sidebar_state="expanded"
)

# ชื่อเรื่อง
st.title("🌿 Self-Caring App")
st.markdown("---")

# Sidebar สำหรับเมนูหลัก
st.sidebar.title("📋 เมนู")
page = st.sidebar.radio(
    "เลือกหมวดหมู่:",
    ["🏠 หน้าแรก", "💧 ดื่มน้ำ", "😴 ชั่วโมงนอน", "🏃 ออกกำลังกาย", "📝 บันทึก", "📊 สถิติ"]
)

# ============================================
# หน้าแรก
# ============================================
if page == "🏠 หน้าแรก":
    col1, col2, col3 = st.columns(3)
    
    with col1:
        st.metric(label="💧 ดื่มน้ำวันนี้", value="6 แก้ว", delta="2 แก้ว")
    
    with col2:
        st.metric(label="😴 นอนเมื่อวาน", value="7 ชั่วโมง", delta="ดี")
    
    with col3:
        st.metric(label="🏃 ออกกำลังวันนี้", value="30 นาที", delta="✓ สำเร็จ")
    
    st.markdown("---")
    
    st.subheader("📌 เคล็ดลับการดูแลตนเอง")
    tips = [
        "🥗 ทานอาหารที่มีสารอาหารครบถ้วน",
        "💤 นอนให้พอเพียง 7-8 ชั่วโมงต่อวัน",
        "🚶 เดินหรือออกกำลังกายอย่างน้อย 30 นาทีต่อวัน",
        "🧘 ทำสมาธิหรือผ่อนคลายใจ 10 นาทีต่อวัน",
        "📱 ลดการใช้โทรศัพท์ก่อนนอน"
    ]
    for tip in tips:
        st.write(tip)

# ============================================
# ดื่มน้ำ
# ============================================
elif page == "💧 ดื่มน้ำ":
    st.subheader("💧 ติดตามการดื่มน้ำ")
    
    col1, col2 = st.columns(2)
    
    with col1:
        st.write("**เป้าหมายวันนี้: 8 แก้ว**")
        water_intake = st.slider("กี่แก้วแล้ว?", 0, 15, 6)
        st.progress(water_intake / 8)
        st.success(f"คุณดื่มไปแล้ว {water_intake} แก้ว")
    
    with col2:
        st.write("**เลือกขนาดแก้ว:**")
        cup_size = st.radio(
            "ขนาด:",
            ["🥤 250 ml", "🥛 350 ml", "🍶 500 ml"],
            horizontal=True
        )
        if st.button("➕ เพิ่มการดื่มน้ำ"):
            st.balloons()
            st.success("บันทึกการดื่มน้ำเรียบร้อย!")

# ============================================
# ชั่วโมงนอน
# ============================================
elif page == "😴 ชั่วโมงนอน":
    st.subheader("😴 ติดตามชั่วโมงนอน")
    
    col1, col2 = st.columns(2)
    
    with col1:
        sleep_hours = st.number_input("นอนกี่ชั่วโมง?", min_value=0.0, max_value=12.0, step=0.5)
        sleep_quality = st.slider("คุณภาพการนอน", 1, 10, 7)
        
        if sleep_hours >= 7:
            st.success("✅ นอนได้พอเพียง!")
        elif sleep_hours >= 6:
            st.warning("⚠️ นอนน้อยกว่าเป้าหมาย")
        else:
            st.error("❌ นอนไม่เพียงพอ")
    
    with col2:
        st.write(f"**คุณภาพการนอน: {sleep_quality}/10**")
        st.bar_chart({"คุณภาพ": [sleep_quality], "เป้าหมาย": [8]})
        
        if st.button("💾 บันทึกการนอน"):
            st.success("บันทึกการนอนเรียบร้อย!")

# ============================================
# ออกกำลังกาย
# ============================================
elif page == "🏃 ออกกำลังกาย":
    st.subheader("🏃 ติดตามการออกกำลังกาย")
    
    exercise_type = st.selectbox(
        "เลือกประเภทการออกกำลัง:",
        ["🚴 ปั่นจักรยาน", "🏃 วิ่ง", "🏊 ว่ายน้ำ", "🧘 โยคะ", "🤸 ยิมนาสติกส์"]
    )
    
    duration = st.number_input("ออกกำลังนานเท่าไหร่ (นาที)?", min_value=5, step=5)
    intensity = st.select_slider(
        "ความเข้มข้น:",
        options=["🟢 ต่ำ", "🟡 ปานกลาง", "🔴 สูง"]
    )
    
    col1, col2 = st.columns(2)
    with col1:
        if st.button("✅ บันทึกการออกกำลัง"):
            st.balloons()
            st.success(f"บันทึก {exercise_type} {duration} นาที ({intensity}) เรียบร้อย!")
    
    with col2:
        st.info(f"🎯 เป้าหมายวันนี้: 30 นาที")

# ============================================
# บันทึก
# ============================================
elif page == "📝 บันทึก":
    st.subheader("📝 บันทึกประจำวัน")
    
    mood = st.select_slider(
        "อารมณ์ของคุณวันนี้:",
        options=["😢", "😕", "😐", "🙂", "😊", "😄"]
    )
    
    journal = st.text_area(
        "เขียนบันทึกประจำวันของคุณ:",
        placeholder="วันนี้ฉูกรูสึกเป็นอย่างไร...",
        height=200
    )
    
    if st.button("💾 บันทึกทั้งหมด"):
        st.success("บันทึกประจำวันเรียบร้อย! 📝")

# ============================================
# สถิติ
# ============================================
elif page == "📊 สถิติ":
    st.subheader("📊 สถิติประจำสัปดาห์")
    
    col1, col2 = st.columns(2)
    
    with col1:
        st.write("**ชั่วโมงนอน**")
        sleep_data = {"จันทร์": 7, "อังคาร": 6.5, "พุธ": 8, "พฤหัส": 7.5, "ศุกร์": 6, "เสาร์": 9, "อาทิตย์": 8.5}
        st.line_chart(sleep_data)
    
    with col2:
        st.write("**การออกกำลังกาย (นาที)**")
        exercise_data = {"จันทร์": 30, "อังคาร": 45, "พุธ": 30, "พฤหัส": 50, "ศุกร์": 0, "เสาร์": 60, "อาทิตย์": 40}
        st.bar_chart(exercise_data)

st.markdown("---")
st.write("💚 ดูแลตัวเอง คือการลงทุนที่ดีที่สุด")
