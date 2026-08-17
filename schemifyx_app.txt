import streamlit as st

# ---------------------------------------------------------
# PAGE CONFIGURATION
# ---------------------------------------------------------
st.set_page_config(
    page_title="Schemifyx",
    page_icon="🎓",
    layout="wide"
)

# ---------------------------------------------------------
# CUSTOM CSS
# ---------------------------------------------------------
st.markdown("""
<style>

.main-title {
    font-size: 42px;
    font-weight: 800;
    color: #4F46E5;
    margin-bottom: 0;
}

.subtitle {
    font-size: 20px;
    color: #555;
    margin-top: 0;
}

.info-box {
    padding: 18px;
    border-radius: 12px;
    background-color: #f5f7ff;
    border: 1px solid #e0e4ff;
}

.result-box {
    padding: 20px;
    border-radius: 15px;
    background-color: #ffffff;
    border: 1px solid #e5e7eb;
    margin-bottom: 15px;
}

.agent-box {
    padding: 20px;
    border-radius: 15px;
    background-color: #f8f9ff;
    border: 1px solid #e1e4ff;
    min-height: 180px;
}

.footer {
    text-align: center;
    color: #777;
    font-size: 13px;
    padding: 20px;
}

</style>
""", unsafe_allow_html=True)


# ---------------------------------------------------------
# HEADER
# ---------------------------------------------------------
st.markdown(
    '<p class="main-title">🎓 Schemifyx</p>',
    unsafe_allow_html=True
)

st.markdown(
    '<p class="subtitle">AI-Powered Government Opportunity Finder</p>',
    unsafe_allow_html=True
)

st.write(
    "Discover government opportunities based on your profile — "
    "including scholarships, internships, fellowships, "
    "skill-development programs and financial assistance."
)

st.divider()


# ---------------------------------------------------------
# SAMPLE OPPORTUNITY DATABASE
# ---------------------------------------------------------
opportunities = [

    {
        "name": "National Scholarship Program",
        "type": "🎓 Scholarship",
        "states": ["All"],
        "education": ["UG", "PG"],
        "income": 500000,
        "min_cgpa": 6.0,
        "min_age": 17,
        "max_age": 30,
        "category": ["All"],
        "skills": [],
        "documents": [
            "Aadhaar",
            "Income Certificate",
            "College ID",
            "Bank Details"
        ],
        "benefit": "Financial support for education",
        "deadline": "Check official portal",
        "description":
            "A sample scholarship opportunity for eligible undergraduate "
            "and postgraduate students."
    },

    {
        "name": "Government Skill Development Program",
        "type": "🧑‍💻 Skill Development",
        "states": ["All"],
        "education": ["UG", "PG", "Diploma"],
        "income": 800000,
        "min_cgpa": 5.0,
        "min_age": 18,
        "max_age": 35,
        "category": ["All"],
        "skills": ["Python", "AI", "Web Development"],
        "documents": [
            "Aadhaar",
            "Education Certificate",
            "College ID"
        ],
        "benefit": "Free skill training and certification",
        "deadline": "Check official portal",
        "description":
            "A sample skill-development opportunity matched using "
            "education and student interests."
    },

    {
        "name": "Student Internship Opportunity",
        "type": "💼 Internship",
        "states": ["All"],
        "education": ["UG", "PG"],
        "income": 1000000,
        "min_cgpa": 6.5,
        "min_age": 18,
        "max_age": 30,
        "category": ["All"],
        "skills": ["Python", "AI", "Machine Learning", "Web Development"],
        "documents": [
            "Resume",
            "College ID",
            "Education Certificate"
        ],
        "benefit": "Internship experience and certificate",
        "deadline": "Check official portal",
        "description":
            "A sample internship opportunity for students with "
            "relevant academic background and skills."
    },

    {
        "name": "Student Research Fellowship",
        "type": "🏆 Fellowship",
        "states": ["All"],
        "education": ["UG", "PG"],
        "income": 600000,
        "min_cgpa": 7.0,
        "min_age": 18,
        "max_age": 30,
        "category": ["All"],
        "skills": ["AI", "Machine Learning", "Research"],
        "documents": [
            "College ID",
            "Academic Records",
            "Resume"
        ],
        "benefit": "Research exposure and fellowship support",
        "deadline": "Check official portal",
        "description":
            "A sample research fellowship matched using academic "
            "performance and interests."
    },

    {
        "name": "Education Financial Support Program",
        "type": "💰 Financial Assistance",
        "states": ["All"],
        "education": ["UG", "PG", "Diploma"],
        "income": 250000,
        "min_cgpa": 5.0,
        "min_age": 17,
        "max_age": 35,
        "category": ["All"],
        "skills": [],
        "documents": [
            "Income Certificate",
            "Aadhaar",
            "College ID"
        ],
        "benefit": "Financial assistance for eligible education expenses",
        "deadline": "Check official portal",
        "description":
            "A sample financial-support opportunity where family income "
            "is an important eligibility factor."
    }
]


# ---------------------------------------------------------
# SIDEBAR - STUDENT PROFILE
# ---------------------------------------------------------
st.sidebar.header("👤 Student Profile")

st.sidebar.write(
    "Enter your details to find suitable opportunities."
)

name = st.sidebar.text_input(
    "Full Name",
    placeholder="Enter your name"
)

age = st.sidebar.number_input(
    "Age",
    min_value=15,
    max_value=60,
    value=20
)

state = st.sidebar.selectbox(
    "State",
    [
        "Tamil Nadu",
        "Kerala",
        "Karnataka",
        "Andhra Pradesh",
        "Telangana",
        "Other"
    ]
)

education = st.sidebar.selectbox(
    "Education Level",
    ["UG", "PG", "Diploma"]
)

course = st.sidebar.text_input(
    "Course",
    placeholder="Eg: B.E CSE"
)

year = st.sidebar.selectbox(
    "Current Year",
    [
        "1st Year",
        "2nd Year",
        "3rd Year",
        "4th Year"
    ]
)

cgpa = st.sidebar.number_input(
    "CGPA",
    min_value=0.0,
    max_value=10.0,
    value=7.5,
    step=0.1
)

income = st.sidebar.number_input(
    "Annual Family Income (₹)",
    min_value=0,
    value=250000,
    step=10000
)

category = st.sidebar.selectbox(
    "Category",
    ["General", "OBC", "SC", "ST", "Other"]
)

skills = st.sidebar.text_input(
    "Skills / Interests",
    placeholder="Eg: Python, AI, ML"
)


# ---------------------------------------------------------
# PROFILE SUMMARY
# ---------------------------------------------------------
st.header("👤 Your Profile")

col1, col2, col3, col4 = st.columns(4)

with col1:
    st.metric("Age", age)

with col2:
    st.metric("CGPA", cgpa)

with col3:
    st.metric("Education", education)

with col4:
    st.metric("Family Income", f"₹{income:,}")


st.info(
    f"📍 **State:** {state}  |  "
    f"🎓 **Course:** {course if course else 'Not provided'}  |  "
    f"📚 **Year:** {year}  |  "
    f"👤 **Category:** {category}"
)


# ---------------------------------------------------------
# FIND OPPORTUNITIES BUTTON
# ---------------------------------------------------------
if st.button(
    "🔎 Find My Opportunities",
    type="primary",
    use_container_width=True
):

    if not name:
        st.warning("Please enter your name in the Student Profile.")
        st.stop()

    # Convert skills into list
    student_skills = [
        skill.strip().lower()
        for skill in skills.split(",")
        if skill.strip()
    ]

    matches = []

    # -----------------------------------------------------
    # ELIGIBILITY MATCHING
    # -----------------------------------------------------
    for opp in opportunities:

        education_match = education in opp["education"]

        income_match = income <= opp["income"]

        age_match = (
            opp["min_age"] <= age <= opp["max_age"]
        )

        cgpa_match = cgpa >= opp["min_cgpa"]

        state_match = (
            "All" in opp["states"]
            or state in opp["states"]
        )

        category_match = (
            "All" in opp["category"]
            or category in opp["category"]
        )

        # Skill matching
        required_skills = [
            skill.lower()
            for skill in opp["skills"]
        ]

        skill_match = True

        if required_skills:
            skill_match = any(
                student_skill in required_skill
                or required_skill in student_skill
                for student_skill in student_skills
                for required_skill in required_skills
            )

        # Overall eligibility
        if (
            education_match
            and income_match
            and age_match
            and cgpa_match
            and state_match
            and category_match
            and skill_match
        ):
            matches.append(opp)

    # -----------------------------------------------------
    # RESULTS
    # -----------------------------------------------------
    st.divider()

    st.header("🎯 Opportunities For You")

    st.success(
        f"Hi {name}! Schemifyx analyzed your profile "
        f"and found **{len(matches)} suitable opportunities**."
    )

    if matches:

        # Category summary
        types = {}

        for opp in matches:
            opportunity_type = opp["type"]
            types[opportunity_type] = (
                types.get(opportunity_type, 0) + 1
            )

        st.subheader("📊 Opportunity Categories")

        category_columns = st.columns(len(types))

        for i, (opp_type, count) in enumerate(types.items()):

            with category_columns[i]:
                st.metric(
                    opp_type,
                    count
                )

        st.divider()

        # -------------------------------------------------
        # DISPLAY MATCHES
        # -------------------------------------------------
        for opp in matches:

            with st.container():

                st.markdown(
                    f"""
                    <div class="result-box">
                    <h3>{opp['type']} &nbsp; {opp['name']}</h3>
                    <p><b>Benefit:</b> {opp['benefit']}</p>
                    <p><b>Eligibility:</b> Your profile matches the
                    sample eligibility criteria.</p>
                    </div>
                    """,
                    unsafe_allow_html=True
                )

                with st.expander("📄 View Opportunity Details"):

                    st.write(
                        f"**About:** {opp['description']}"
                    )

                    st.write(
                        "### ✅ Eligibility Match"
                    )

                    st.write(
                        f"• Education: **{education}** ✓"
                    )

                    st.write(
                        f"• Age: **{age}** ✓"
                    )

                    st.write(
                        f"• CGPA: **{cgpa}** ✓"
                    )

                    st.write(
                        f"• Family Income: **₹{income:,}** ✓"
                    )

                    st.write(
                        f"• Category: **{category}** ✓"
                    )

                    st.write(
                        "### 📄 Required Documents"
                    )

                    for doc in opp["documents"]:
                        st.write(f"• {doc}")

                    st.write(
                        f"### 💰 Benefit\n{opp['benefit']}"
                    )

                    st.write(
                        f"### 📅 Deadline\n{opp['deadline']}"
                    )

                    st.link_button(
                        "🔗 Apply / Verify on Official Portal",
                        "https://www.india.gov.in/"
                    )

    else:

        st.warning(
            "No direct matches were found based on the current "
            "sample criteria. Try updating your profile."
        )


# ---------------------------------------------------------
# AI AGENTS SECTION
# ---------------------------------------------------------
st.divider()

st.header("🤖 Schemifyx AI Agent Workflow")

st.write(
    "The proposed system uses multiple specialized agents "
    "to personalize government opportunity discovery."
)

c1, c2, c3, c4 = st.columns(4)

with c1:
    st.markdown(
        """
        <div class="agent-box">
        <h3>👤 Profile Agent</h3>
        <p>
        Understands the student's education, income,
        interests and other profile details.
        </p>
        </div>
        """,
        unsafe_allow_html=True
    )

with c2:
    st.markdown(
        """
        <div class="agent-box">
        <h3>🔎 Opportunity Agent</h3>
        <p>
        Finds relevant scholarships, internships,
        fellowships and programs.
        </p>
        </div>
        """,
        unsafe_allow_html=True
    )

with c3:
    st.markdown(
        """
        <div class="agent-box">
        <h3>✅ Eligibility Agent</h3>
        <p>
        Compares student details with opportunity
        eligibility requirements.
        </p>
        </div>
        """,
        unsafe_allow_html=True
    )

with c4:
    st.markdown(
        """
        <div class="agent-box">
        <h3>📄 Document Agent</h3>
        <p>
        Identifies required documents and provides
        application guidance.
        </p>
        </div>
        """,
        unsafe_allow_html=True
    )


# ---------------------------------------------------------
# PROCESS FLOW
# ---------------------------------------------------------
st.divider()

st.header("🔄 How Schemifyx Works")

st.markdown(
    """
    **👤 Student Profile**
    &nbsp; → &nbsp;
    **🤖 Profile Analysis**
    &nbsp; → &nbsp;
    **🔎 Opportunity Discovery**
    &nbsp; → &nbsp;
    **✅ Eligibility Matching**
    &nbsp; → &nbsp;
    **📄 Documents & Benefits**
    &nbsp; → &nbsp;
    **🔗 Application Guidance**
    """
)



