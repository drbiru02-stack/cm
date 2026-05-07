# cm
this is my pdf file
from reportlab.lib.pagesizes import A4
from reportlab.platypus import SimpleDocTemplate, Paragraph, Spacer, Table, TableStyle, HRFlowable
from reportlab.lib.styles import getSampleStyleSheet, ParagraphStyle
from reportlab.lib.units import cm
from reportlab.lib import colors
from reportlab.lib.enums import TA_CENTER, TA_LEFT, TA_JUSTIFY

doc = SimpleDocTemplate(
    "/mnt/user-data/outputs/CommMed_Last1Hour_PYQ_Predictions.pdf",
    pagesize=A4,
    rightMargin=1.8*cm, leftMargin=1.8*cm,
    topMargin=1.5*cm, bottomMargin=1.5*cm
)

styles = getSampleStyleSheet()

# Custom styles
title_style = ParagraphStyle('Title', parent=styles['Normal'],
    fontSize=18, fontName='Helvetica-Bold', alignment=TA_CENTER,
    textColor=colors.HexColor('#1a1a2e'), spaceAfter=4)

subtitle_style = ParagraphStyle('Sub', parent=styles['Normal'],
    fontSize=11, fontName='Helvetica', alignment=TA_CENTER,
    textColor=colors.HexColor('#444'), spaceAfter=2)

section_style = ParagraphStyle('Section', parent=styles['Normal'],
    fontSize=13, fontName='Helvetica-Bold',
    textColor=colors.white, spaceAfter=4, spaceBefore=10,
    backColor=colors.HexColor('#16213e'), borderPadding=(6,8,6,8))

q_style = ParagraphStyle('Q', parent=styles['Normal'],
    fontSize=10.5, fontName='Helvetica-Bold',
    textColor=colors.HexColor('#c0392b'), spaceAfter=3, spaceBefore=8,
    leftIndent=0)

a_style = ParagraphStyle('A', parent=styles['Normal'],
    fontSize=10, fontName='Helvetica',
    textColor=colors.HexColor('#1a1a1a'), spaceAfter=4,
    leftIndent=12, leading=15)

bullet_style = ParagraphStyle('Bullet', parent=styles['Normal'],
    fontSize=10, fontName='Helvetica',
    textColor=colors.HexColor('#222'), spaceAfter=2,
    leftIndent=20, leading=14)

tip_style = ParagraphStyle('Tip', parent=styles['Normal'],
    fontSize=9.5, fontName='Helvetica-Oblique',
    textColor=colors.HexColor('#1e6b3c'), spaceAfter=3,
    leftIndent=10, backColor=colors.HexColor('#eafaf1'),
    borderPadding=(4,6,4,6))

tag_style = ParagraphStyle('Tag', parent=styles['Normal'],
    fontSize=8.5, fontName='Helvetica-Bold',
    textColor=colors.HexColor('#6c3483'),
    spaceAfter=2, spaceBefore=2)

story = []

# ── HEADER ──────────────────────────────────────────────────────────────────
story.append(Paragraph("COMMUNITY MEDICINE", title_style))
story.append(Paragraph("Last 1-Hour Exam Survival Guide | Burdwan Medical College", subtitle_style))
story.append(Paragraph("MBBS Phase II (3rd Semester) | Batch 2023-24", subtitle_style))
story.append(HRFlowable(width="100%", thickness=2, color=colors.HexColor('#c0392b'), spaceAfter=6))

# Analysis table
data = [
    ["TOPIC", "FREQUENCY", "EXAM WEIGHT", "PRIORITY"],
    ["Levels of Prevention + Modes of Intervention", "Every exam", "15–20%", "★★★"],
    ["Indicators of Health (DALY, QALY, Sullivan, IMR)", "Every exam", "10–15%", "★★★"],
    ["Epidemiology: Epidemic/Endemic/Sporadic/Pandemic", "Most exams", "10%", "★★★"],
    ["Source vs Reservoir / Relative Risk", "Most exams", "8–10%", "★★★"],
    ["Air & Water Pollution / Safe Water", "Cyclical", "8%", "★★"],
    ["Vitamin A Deficiency / Nutritional deficiencies", "Most exams", "8%", "★★★"],
    ["Screening (criteria, types, examples)", "Every exam", "8%", "★★★"],
    ["Study Designs (Cohort vs Case-Control)", "Every exam", "8%", "★★"],
    ["MCQ topics: RDA, Reference Man, Epidemiological terms", "Every exam", "15%", "★★★"],
]
col_widths = [7.5*cm, 3.2*cm, 3.2*cm, 2.2*cm]
t = Table(data, colWidths=col_widths)
t.setStyle(TableStyle([
    ('BACKGROUND', (0,0), (-1,0), colors.HexColor('#16213e')),
    ('TEXTCOLOR', (0,0), (-1,0), colors.white),
    ('FONTNAME', (0,0), (-1,0), 'Helvetica-Bold'),
    ('FONTSIZE', (0,0), (-1,0), 9),
    ('ROWBACKGROUNDS', (0,1), (-1,-1), [colors.HexColor('#f4f6f7'), colors.white]),
    ('FONTNAME', (0,1), (-1,-1), 'Helvetica'),
    ('FONTSIZE', (0,1), (-1,-1), 8.5),
    ('TEXTCOLOR', (-1,1), (-1,-1), colors.HexColor('#c0392b')),
    ('FONTNAME', (-1,1), (-1,-1), 'Helvetica-Bold'),
    ('GRID', (0,0), (-1,-1), 0.4, colors.grey),
    ('ALIGN', (1,0), (-1,-1), 'CENTER'),
    ('VALIGN', (0,0), (-1,-1), 'MIDDLE'),
    ('TOPPADDING', (0,0), (-1,-1), 4),
    ('BOTTOMPADDING', (0,0), (-1,-1), 4),
]))
story.append(t)
story.append(Spacer(1, 8))

# ── SECTION 1 ───────────────────────────────────────────────────────────────
story.append(Paragraph("SECTION 1: LEVELS OF PREVENTION [STATIC – EVERY EXAM]", section_style))

story.append(Paragraph("Q1. Outline the modes of intervention at primary, secondary and tertiary levels with suitable examples. (15 marks – most repeated)", q_style))
story.append(Paragraph("<b>Answer Framework:</b>", a_style))
story.append(Paragraph("<b>Natural History of Disease concept (Leavell & Clark)</b> — Disease passes through Pre-pathogenesis and Pathogenesis phases. Prevention is applied at different stages.", a_style))

story.append(Paragraph("<b>1. PRIMORDIAL PREVENTION</b>", bullet_style))
story.append(Paragraph("• Prevents emergence of risk factors in a population that has not yet developed them.", bullet_style))
story.append(Paragraph("• Mode: Individual + Mass education. Best for Non-communicable diseases.", bullet_style))

story.append(Paragraph("<b>2. PRIMARY PREVENTION</b> — Removes possibility of disease before it occurs", bullet_style))
story.append(Paragraph("• <b>Health Promotion:</b> Health education, nutritional intervention, environmental modification, lifestyle changes", bullet_style))
story.append(Paragraph("• <b>Specific Protection:</b> Vaccines, contraception, helmets, mosquito nets, iodized salt", bullet_style))
story.append(Paragraph("• Applied in: Pre-pathogenesis phase | Risk factors present but disease not yet occurred", bullet_style))

story.append(Paragraph("<b>3. SECONDARY PREVENTION</b> — Arrests disease at incipient stage", bullet_style))
story.append(Paragraph("• <b>Early Diagnosis:</b> Sputum smear for AFB, P/S for malaria, Pap smear, Blood sugar screening", bullet_style))
story.append(Paragraph("• <b>Prompt Treatment:</b> DOTS for TB, MDT for leprosy, ORS for diarrhoea", bullet_style))
story.append(Paragraph("• Applied in: Early pathogenesis phase | Screening is done here", bullet_style))
story.append(Paragraph("• Govt health programs (TB, Leprosy, STDs) mostly operate at secondary level", bullet_style))

story.append(Paragraph("<b>4. TERTIARY PREVENTION</b> — Reduces impairment and disability in established disease", bullet_style))
story.append(Paragraph("• <b>Disability Limitation:</b> Prevents impairment from becoming handicap — Physiotherapy in polio", bullet_style))
story.append(Paragraph("• <b>Rehabilitation:</b> Medical, vocational, social, psychological — Crutches, hearing aids", bullet_style))
story.append(Paragraph("• Applied in: Late pathogenesis phase", bullet_style))

story.append(Paragraph("★ EXAM TIP: Draw the Natural History & Prevention diagram (Fig 2.6 type). Screening = Secondary Prevention.", tip_style))

story.append(Paragraph("Q2. Explain why: Screening is an example of Secondary Prevention. (MCQ/SAQ)", q_style))
story.append(Paragraph("Screening detects disease in its incipient (early, pre-symptomatic) stage — when biochemical/functional changes are present but manifest signs are absent. This corresponds to the early pathogenesis phase where secondary prevention (early diagnosis + prompt treatment) is applied. Examples: Pap smear for cervical cancer, sputum AFB for TB, P/S for malaria.", a_style))

# ── SECTION 2 ───────────────────────────────────────────────────────────────
story.append(Paragraph("SECTION 2: INDICATORS OF HEALTH [STATIC – EVERY EXAM]", section_style))

story.append(Paragraph("Q3. What do you mean by 'Indicator of Health'? Criteria of ideal indicators? Describe one mortality and one morbidity indicator. (2+3+5+5 = 15 marks)", q_style))

story.append(Paragraph("<b>Health Indicator:</b> A variable that helps measure changes; used when changes cannot be measured directly (WHO). Indicators are used to measure health status, compare countries, allocate resources, and evaluate programs.", a_style))

story.append(Paragraph("<b>Criteria of an Ideal Indicator (VRSSFR):</b>", a_style))
story.append(Paragraph("• Valid — measures what it is supposed to measure", bullet_style))
story.append(Paragraph("• Reliable/Objective — same result when measured by different people", bullet_style))
story.append(Paragraph("• Sensitive — detects changes in the situation", bullet_style))
story.append(Paragraph("• Specific — reflects changes only in that situation", bullet_style))
story.append(Paragraph("• Feasible — data can be obtained easily", bullet_style))
story.append(Paragraph("• Relevant — contributes to understanding of the phenomenon", bullet_style))

story.append(Paragraph("<b>Mortality Indicators:</b> CDR, IMR, MMR, CMR, CFR, YPLL, Under-5 mortality, Proportional mortality", a_style))
story.append(Paragraph("<b>Key Mortality Indicator — Infant Mortality Rate (IMR):</b>", a_style))
story.append(Paragraph("• Number of deaths under 1 year per 1000 live births in a year", bullet_style))
story.append(Paragraph("• <b>Significance:</b> Single most sensitive indicator of health of a community; reflects standard of living, nutrition, sanitation, MCH services", bullet_style))
story.append(Paragraph("• India IMR (2020): ~28/1000 live births", bullet_style))

story.append(Paragraph("<b>Morbidity Indicators:</b> Incidence, Prevalence, Notification rates, Hospital attendance", a_style))
story.append(Paragraph("<b>Key — Incidence vs Prevalence:</b>", a_style))
story.append(Paragraph("• Incidence = New cases / Population at risk × time (measures risk)", bullet_style))
story.append(Paragraph("• Prevalence = All cases (old+new) / Total population (measures burden)", bullet_style))
story.append(Paragraph("• P = I × D (Prevalence = Incidence × Duration)", bullet_style))

story.append(Paragraph("<b>Disability-Adjusted Life Year (DALY):</b> BEST measure of disease burden. 1 DALY = 1 year of healthy life lost. DALY = YLL + YLD (Years Lost to Life + Years Lived with Disability)", a_style))
story.append(Paragraph("<b>QALY:</b> 1 QALY = 1 year in perfect health. Used to assess value of money for medical intervention.", a_style))
story.append(Paragraph("<b>Sullivan's Index:</b> = Life expectancy MINUS duration of disability = 'Disability-Free Life Expectancy (DFLE)'", a_style))

story.append(Paragraph("★ KEY MCQ: DALY is BEST measure of disease burden. QALY = 1 year perfect health. Sullivan's = DFLE.", tip_style))

# ── SECTION 3 ───────────────────────────────────────────────────────────────
story.append(Paragraph("SECTION 3: EPIDEMIOLOGICAL TERMS [HIGH FREQUENCY]", section_style))

story.append(Paragraph("Q4. Source and reservoir are not always synonymous — Justify with example. (3 marks)", q_style))
story.append(Paragraph("<b>Source:</b> The person, animal, object or substance from which an infectious agent passes directly to the host. It is the immediate donor of infection.", a_style))
story.append(Paragraph("<b>Reservoir:</b> Any person, animal, arthropod, plant, soil or substance in which an infectious agent normally lives and multiplies, and from which it can be transmitted.", a_style))
story.append(Paragraph("<b>Why they differ:</b> In tuberculosis — the reservoir is humans (where M. tuberculosis maintains itself) but the source can be a coughing patient (direct) OR contaminated sputum on a surface (indirect). In zoonoses like rabies — the reservoir is the dog/wild animal but the source to humans is the bite wound. A chronic carrier may be a reservoir but not the source of a specific outbreak.", a_style))
story.append(Paragraph("★ Key: Source = immediate donor | Reservoir = long-term habitat. They coincide in person-to-person diseases.", tip_style))

story.append(Paragraph("Q5. Relative Risk cannot be calculated from Case-Control study — Explain. (4 marks)", q_style))
story.append(Paragraph("<b>Relative Risk (RR)</b> = Incidence in exposed / Incidence in non-exposed. To calculate RR, we need incidence rates, which require knowing the total population at risk.", a_style))
story.append(Paragraph("In a <b>Case-Control study</b>, subjects are selected based on disease status (cases vs controls) — not based on exposure. The study starts from disease and looks back. Since the study population is not a representative sample of the original population, we cannot calculate true incidence rates, and therefore cannot calculate true RR.", a_style))
story.append(Paragraph("Instead, <b>Odds Ratio (OR)</b> is used as an approximation of RR in case-control studies. OR = (a×d)/(b×c) from a 2×2 table.", a_style))
story.append(Paragraph("★ Cohort study → calculate RR directly. Case-control → OR approximates RR.", tip_style))

story.append(Paragraph("Q6. Incidence of a disease cannot be measured by cross-sectional studies — Explain. (3 marks)", q_style))
story.append(Paragraph("Cross-sectional (prevalence) studies measure the health status of a population at ONE point in time (a 'snapshot'). Incidence requires following a disease-free population over a period of time to measure NEW cases. Since cross-sectional studies do not follow up over time, they cannot capture new case development — they can only measure prevalence (existing cases). Longitudinal/Cohort studies are needed for incidence.", a_style))

# ── SECTION 4 ───────────────────────────────────────────────────────────────
story.append(Paragraph("SECTION 4: AIR POLLUTION & WATER [CYCLICAL TOPIC]", section_style))

story.append(Paragraph("Q7. Enumerate indicators of Air Pollution. Health effects + control measures. (3+3+4=10)", q_style))
story.append(Paragraph("<b>Indicators of Air Pollution:</b>", a_style))
story.append(Paragraph("Particulate Matter (PM2.5, PM10), SO2, NOx, CO, CO2, Ozone (O3), Lead, Hydrocarbons, SPM (Suspended Particulate Matter), RSPM", bullet_style))

story.append(Paragraph("<b>Health Effects:</b>", a_style))
story.append(Paragraph("• Respiratory: COPD, Asthma, Bronchitis, Lung cancer (SO2, PM, smoking)", bullet_style))
story.append(Paragraph("• CO: Binds Hb 200x more than O2 → CO poisoning, headache, death", bullet_style))
story.append(Paragraph("• Lead: Neurotoxicity, learning disability in children", bullet_style))
story.append(Paragraph("• Ozone: Eye/mucous membrane irritation, lung damage", bullet_style))
story.append(Paragraph("• Global: Greenhouse effect (CO2), Acid rain (SO2, NOx), Ozone depletion (CFCs)", bullet_style))

story.append(Paragraph("<b>Control Measures:</b>", a_style))
story.append(Paragraph("• Source control: Unleaded petrol, CNG, catalytic converters, smokeless chulha", bullet_style))
story.append(Paragraph("• Industry: Electrostatic precipitators, scrubbers, relocation from cities", bullet_style))
story.append(Paragraph("• Planning: Green belts, zoning laws, vehicle emission norms (BS-VI)", bullet_style))
story.append(Paragraph("• Legislation: Air Prevention & Control of Pollution Act 1981, CPCB monitoring", bullet_style))

story.append(Paragraph("Q8. Criteria of safe and wholesome water + health hazards of contaminated water + household purification. (2+4+4=10)", q_style))
story.append(Paragraph("<b>Criteria of Safe Water (WHO):</b> Colorless, odorless, tasteless, free from pathogens, chemical impurities within limits, no radioactivity, pH 6.5–8.5, turbidity <5 NTU, TDS <500 mg/L, No E.coli in 100mL.", a_style))
story.append(Paragraph("<b>Health Hazards of Contaminated Water:</b>", a_style))
story.append(Paragraph("• Waterborne: Cholera, typhoid, hepatitis A, amoebic dysentery, polio", bullet_style))
story.append(Paragraph("• Water-washed: Trachoma, scabies, skin infections (lack of water for hygiene)", bullet_style))
story.append(Paragraph("• Water-based: Guinea worm (Dracunculiasis), Schistosomiasis", bullet_style))
story.append(Paragraph("• Water-related vector: Malaria, dengue, filariasis (stagnant water breeding)", bullet_style))
story.append(Paragraph("• Chemical: Fluorosis (excess F), Methaemoglobinaemia (NO3), Arsenicosis", bullet_style))
story.append(Paragraph("<b>Household Purification:</b> Boiling (most effective for pathogens), Filtration (Candle/Berkefield), Chlorination (0.5 mg/L residual), Solar disinfection (SODIS), Alum flocculation", a_style))

# ── SECTION 5 ───────────────────────────────────────────────────────────────
story.append(Paragraph("SECTION 5: NUTRITION — VIT A, PEM, RDA [STATIC]", section_style))

story.append(Paragraph("Q9. Clinical manifestations of Vitamin A Deficiency. (5 marks)", q_style))
story.append(Paragraph("<b>Xerophthalmia</b> (dry eye) — most common in children 1–3 years:", a_style))

data2 = [
    ["WHO Classification", "Sign"],
    ["X1A", "Conjunctival xerosis — FIRST clinical sign"],
    ["X1B", "Bitot's spots — triangular pearly-white foamy spots on bulbar conjunctiva"],
    ["X2", "Corneal xerosis"],
    ["X3A", "Corneal ulceration (<1/3 cornea)"],
    ["X3B", "Keratomalacia — liquefaction of cornea (GRAVE emergency)"],
    ["XN", "Night blindness — FIRST clinical symptom"],
    ["XF", "Xerophthalmic fundus"],
    ["XS", "Xerophthalmic scarring"],
]
t2 = Table(data2, colWidths=[3*cm, 12*cm])
t2.setStyle(TableStyle([
    ('BACKGROUND', (0,0), (-1,0), colors.HexColor('#e74c3c')),
    ('TEXTCOLOR', (0,0), (-1,0), colors.white),
    ('FONTNAME', (0,0), (-1,0), 'Helvetica-Bold'),
    ('FONTSIZE', (0,0), (-1,-1), 9),
    ('FONTNAME', (0,1), (-1,-1), 'Helvetica'),
    ('ROWBACKGROUNDS', (0,1), (-1,-1), [colors.HexColor('#fdf2f2'), colors.white]),
    ('GRID', (0,0), (-1,-1), 0.4, colors.grey),
    ('TOPPADDING', (0,0), (-1,-1), 3),
    ('BOTTOMPADDING', (0,0), (-1,-1), 3),
]))
story.append(t2)
story.append(Spacer(1,4))
story.append(Paragraph("<b>Extraocular manifestations:</b> Follicular hyperkeratosis (toad skin), anorexia, growth retardation, increased susceptibility to infections", bullet_style))
story.append(Paragraph("<b>Vitamin A Prophylaxis Programme:</b> 6m–1yr → 1 Lakh IU once | >1yr–5yr → 2 Lakh IU every 6 months | Total 9 doses", bullet_style))
story.append(Paragraph("★ Bitot's spots = most common INDICATOR. Serum retinol <10 mcg/dL = deficiency.", tip_style))

story.append(Paragraph("Q10. What is Open Vial Policy? (Short note, 5 marks)", q_style))
story.append(Paragraph("Open Vial Policy (OVP) was introduced by WHO/UNICEF to reduce vaccine wastage. It allows multi-dose vials of certain vaccines (that meet stability criteria) to be kept and used in subsequent immunization sessions (up to 28 days for some vaccines) rather than discarding them after each session.", a_style))
story.append(Paragraph("<b>Vaccines under OVP:</b> OPV, DPT, TT, Hepatitis B, liquid Hib — if stored properly at 2–8°C, VVM has not passed, not expired, aseptic technique maintained.", a_style))
story.append(Paragraph("<b>Vaccines NOT under OVP (must discard after session):</b> BCG, Measles, MMR (lyophilized vaccines reconstituted with diluent)", a_style))
story.append(Paragraph("★ BCG must always be discarded after session — not covered by OVP!", tip_style))

# ── SECTION 6 ───────────────────────────────────────────────────────────────
story.append(Paragraph("SECTION 6: STUDY DESIGNS + EPIDEMIOLOGY [STATIC]", section_style))

story.append(Paragraph("Q11. A study identified typhoid cases from a common well — what type of study? (MCQ)", q_style))
story.append(Paragraph("<b>Answer: Cohort Study.</b> Groups are formed based on exposure (using vs not using the well) and followed for disease outcome (typhoid). Cases and disease-free controls are NOT selected — instead exposed and unexposed are followed. This is the cohort (prospective) design.", a_style))

story.append(Paragraph("Q12. Epidemic vs Endemic vs Pandemic vs Sporadic — Key differences (for MCQs)", q_style))

data3 = [
    ["Term", "Definition", "Key Feature", "Example"],
    ["Epidemic", "Cases clearly in excess of normal expectancy", "No. > Mean + 2SD", "COVID-19 initial outbreak"],
    ["Endemic", "Constant presence at usual/expected frequency", "Baseline never zero", "Malaria in WB"],
    ["Pandemic", "Epidemic over large geographic area (global)", "Crosses international borders", "Swine flu H1N1"],
    ["Sporadic", "Cases scattered in space and time, no pattern", "No recognizable source", "Rabies, snake bite"],
    ["Hyperendemic", "High incidence, affects all age groups equally", "Persistent high level", "Malaria in Africa"],
]
t3 = Table(data3, colWidths=[2.8*cm, 5.2*cm, 4*cm, 3.5*cm])
t3.setStyle(TableStyle([
    ('BACKGROUND', (0,0), (-1,0), colors.HexColor('#16213e')),
    ('TEXTCOLOR', (0,0), (-1,0), colors.white),
    ('FONTNAME', (0,0), (-1,0), 'Helvetica-Bold'),
    ('FONTSIZE', (0,0), (-1,-1), 8.5),
    ('FONTNAME', (0,1), (-1,-1), 'Helvetica'),
    ('ROWBACKGROUNDS', (0,1), (-1,-1), [colors.HexColor('#eaf4fb'), colors.white]),
    ('GRID', (0,0), (-1,-1), 0.4, colors.grey),
    ('TOPPADDING', (0,0), (-1,-1), 3),
    ('BOTTOMPADDING', (0,0), (-1,-1), 3),
    ('VALIGN', (0,0), (-1,-1), 'MIDDLE'),
]))
story.append(t3)
story.append(Spacer(1,4))

# ── SECTION 7 ───────────────────────────────────────────────────────────────
story.append(Paragraph("SECTION 7: MCQ RAPID FIRE FACTS", section_style))

mcq_data = [
    ["MCQ", "Answer", "Why"],
    ["PHC reports 48 cases, normal is 40–50 → called?", "Endemic", "Within normal expected frequency for that area"],
    ["Screening is example of?", "Secondary Prevention", "Early diagnosis in pre-symptomatic stage"],
    ["Case Fatality Rate relates to?", "Pathogenicity / Virulence", "Proportion who die of those who get the disease"],
    ["PQLI consolidates which indicators?", "IMR + Literacy + LE at age 1", "Range 0–100, India value = 65"],
    ["Reference Man criteria?", "19–39 yr, 65 kg, BMI 18.5–22.9", "ICMR/NIN 2020 guidelines"],
    ["Lactation extra calories (0–6 months)?", "+600 kcal/day (sedentary)", "ICMR 2020 RDA"],
    ["Best measure of disease burden?", "DALY", "Measures both mortality + disability"],
    ["Didactic method of communication?", "One-way communication", "Lecture/talk — no feedback"],
    ["Iron status most sensitive tool?", "Serum Ferritin", "Most sensitive single tool"],
    ["ICDS heart = ?", "Anganwadi", "1 per 400–800 rural population"],
    ["World has eradicated only? (globally)", "Smallpox (8 May 1980)", "Only 1 globally eradicated disease"],
    ["India has eliminated?", "Leprosy (Dec 2005)", "Also: Guineaworm 2000, Yaws 2016, Neonatal tetanus 2016"],
    ["Relative Risk used in?", "Cohort study", "Incidence in exposed / unexposed"],
    ["Odds Ratio used as proxy for RR in?", "Case-Control study", "Cannot calculate incidence directly"],
]
t4 = Table(mcq_data, colWidths=[5.5*cm, 3.5*cm, 6.5*cm])
t4.setStyle(TableStyle([
    ('BACKGROUND', (0,0), (-1,0), colors.HexColor('#c0392b')),
    ('TEXTCOLOR', (0,0), (-1,0), colors.white),
    ('FONTNAME', (0,0), (-1,0), 'Helvetica-Bold'),
    ('FONTSIZE', (0,0), (-1,-1), 8.5),
    ('FONTNAME', (0,1), (-1,-1), 'Helvetica'),
    ('ROWBACKGROUNDS', (0,1), (-1,-1), [colors.HexColor('#fef9e7'), colors.white]),
    ('GRID', (0,0), (-1,-1), 0.4, colors.grey),
    ('TOPPADDING', (0,0), (-1,-1), 3),
    ('BOTTOMPADDING', (0,0), (-1,-1), 3),
    ('VALIGN', (0,0), (-1,-1), 'TOP'),
]))
story.append(t4)
story.append(Spacer(1,6))

# ── SECTION 8 ───────────────────────────────────────────────────────────────
story.append(Paragraph("SECTION 8: DISEASE CONTROL, ERADICATION & ELIMINATION TABLE", section_style))

data5 = [
    ["Feature", "Disease Control", "Disease Elimination", "Disease Eradication"],
    ["Definition", "Reduce transmission to low level, ceases as public health problem", "Complete interruption of transmission in defined area", "Complete extermination globally ('all or none')"],
    ["Scope", "Country/region/world", "Country or region (geographical term)", "Global (whole planet)"],
    ["Causative organism", "May persist in environment", "May persist in environment", "Organism wiped out"],
    ["Intervention needed?", "Continued — no time limit", "Continued to prevent re-establishment", "No longer needed after certification"],
    ["India examples", "Tuberculosis", "Leprosy (2005), Guineaworm, Yaws, Neo-Tetanus", "—"],
    ["Global examples", "—", "—", "Smallpox (1980 only)"],
]
t5 = Table(data5, colWidths=[3*cm, 4*cm, 4.3*cm, 4.2*cm])
t5.setStyle(TableStyle([
    ('BACKGROUND', (0,0), (-1,0), colors.HexColor('#1e6b3c')),
    ('TEXTCOLOR', (0,0), (-1,0), colors.white),
    ('FONTNAME', (0,0), (-1,0), 'Helvetica-Bold'),
    ('FONTSIZE', (0,0), (-1,-1), 8),
    ('FONTNAME', (0,1), (-1,-1), 'Helvetica'),
    ('ROWBACKGROUNDS', (0,1), (-1,-1), [colors.HexColor('#eafaf1'), colors.white]),
    ('GRID', (0,0), (-1,-1), 0.4, colors.grey),
    ('TOPPADDING', (0,0), (-1,-1), 3),
    ('BOTTOMPADDING', (0,0), (-1,-1), 3),
    ('VALIGN', (0,0), (-1,-1), 'TOP'),
]))
story.append(t5)
story.append(Spacer(1,6))

# ── FOOTER NOTE ─────────────────────────────────────────────────────────────
story.append(HRFlowable(width="100%", thickness=1.5, color=colors.HexColor('#c0392b'), spaceAfter=4))
story.append(Paragraph("LAST-MINUTE PRIORITY ORDER: (1) Levels of Prevention → (2) Health Indicators + DALY → (3) Source vs Reservoir + RR vs OR → (4) Epidemic types → (5) Vit A deficiency → (6) MCQ facts table", tip_style))
story.append(Paragraph("Good Luck! — Compiled from BMC PYQ Analysis (Batch 2023-24, 3rd Semester)", subtitle_style))

doc.build(story)
print("PDF created successfully!")
