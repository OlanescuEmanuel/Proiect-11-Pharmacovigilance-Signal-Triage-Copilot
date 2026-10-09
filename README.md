# Proiect-11-Pharmacovigilance-Signal-Triage-Copilot

## 1. Flow-ul de bază și funcționalitățile aplicației
Aplicația va funcționa ca un asistent inteligent (Copilot) cu o interfață simplă (Dashboard) adresată experților în siguranța medicamentelor.
* **Conectarea surselor de date:** Utilizatorul poate vizualiza un set de date încărcat (ex. extrase din baza openFDA FAERS).
* **Lista de semnale prioritizată:** Aplicația afișează o listă de asocieri „Medicament - Reacție Adversă” (semnale), ordonate descrescător în funcție de un **Scor de Prioritate AI**.
* **Signal Packet (Detaliere):** La un click pe un semnal, se deschide un ecran detaliat care conține evoluția temporală a raportărilor (grafice), statistici, exemple de cazuri și **explicația generată de AI** pentru acel scor (ex. „Acest semnal necesită atenție imediată datorită unei creșteri de 300% a raportărilor în ultimele două luni pentru grupul demografic X”).
* **Stadiul actual (MVP):** Pentru demonstrarea flow-ului de bază, predicțiile AI-ului (scorul de prioritate și explicația text aferentă) pentru 3-4 medicamente sunt **hard-codate manual**, urmând ca la finalul dezvoltării să fie conectate la endpoint-ul celui mai bun model antrenat.

---

## 2. Descrierea problemei rezolvate cu AI

**Descrierea plastică (intuitivă):**
Experții în farmacovigilență trebuie, practic, să găsească „un ac într-un car de fân de dimensiunea unui munte”. În mod normal, ei sunt bombardați de milioane de rapoarte medicale aglomerate, care conțin texte dezordonate, date duplicate, sau nume de medicamente scrise în zeci de feluri. În loc să investigheze clinic o reacție adversă potențial mortală, ei pierd enorm de mult timp „făcând curățenie” prin tabele. AI-ul nostru preia rolul unui super-asistent care citește tot, sortează, elimină zgomotul și le pune pe birou doar dosarele urgente, zicând: „Atenție la acest medicament, iată de ce!”.

**Descrierea formală:**
Problema formulată este una de **clasificare și ranking (Information Retrieval)** combinată cu Procesarea Limbajului Natural (NLP).
* **De ce e important:** Reduce timpul de triaj manual, permițând experților să valideze clinic mai rapid problemele reale de siguranță, salvând astfel pacienții de efecte adverse severe.
* **Cine sunt utilizatorii:** Experții în farmacovigilență din cadrul companiilor farmaceutice, analiștii de date medicale și autoritățile de reglementare (ex: FDA, EMA, ANMDMR).
* **Date de intrare:** Structurate (ID-uri baze de date RxNorm, DrugCentral) și Nestructurate (Text liber din formularele de raportare a efectelor adverse, furnizate prin openFDA FAERS API).
* **Date de ieșire:** Un indicator numeric continuu (Scor de risc/prioritate) pentru fiecare semnal detectat, acompaniat de metadate structurate (Signal Packet) și XAI (Explainable AI - text argumentativ privind factorii deciziei).
* **Măsurarea performanței AI:** Se vor utiliza metrici specifice de Machine Learning: 
  - **Recall (Sensibilitatea):** Cea mai importantă metrică; este vital să nu ratăm un efect advers real (False Negatives trebuie minimizate).
  - **Precision și F1-Score:** Pentru a măsura acuratețea semnalelor marcate ca urgente și a nu copleși experții cu alarme false.
  - **AUC-ROC:** Pentru performanța generală de clasificare și separare a semnalelor relevante de cele nerelevante.

---

## 3. Related work & useful tools and technologies

În dezvoltarea proiectului ne raportăm la următoarele lucrări și soluții din domeniu (minim 4 studii/proiecte, având în vedere echipa de 2 membri):

**1. A Natural Language Processing Framework for Detecting Adverse Drug Reactions (IJDRC, 2024)**
* **Date folosite:** Date textuale nestructurate (ex. dataset-ul PsyTAR și review-uri clinice). 
* **Algoritmi AI:** Named Entity Recognition (NER), Analiza sentimentului și framework-uri NLP pe bază de reguli. 
* **Performanțe:** Cercetări similare citate în studiu au atins 75% Precision și 59% Recall, demonstrând un avantaj net față de identificarea manuală. 
* **Tehnologii/Git:** Python (Pandas, Numpy, Ipywidgets, Seaborn); autorii oferă un repository public GitHub numit `ADRD-an-ADR_Detection_NLP-framework`. 

**2. Deep Learning Prediction of Adverse Drug Reactions Using Open Data (arXiv, 2020)**
* **Date folosite:** Seturi de date deschise și asocieri chimice între medicamente. 
* **Algoritmi AI:** Deep Neural Networks (DNN) folosiți pentru predicția diferitelor clase de efecte adverse. 
* **Performanțe:** Modelele au obținut o acuratețe medie ridicată în testele de validare pentru predicția reacțiilor (ADR).
* **Tehnologii/Git:** PyTorch și TensorFlow (tool-urile standard folosite în dezvoltarea rețelelor DNN prezentate).

**3. FAERS-Based Machine Learning for Predicting Severe Outcomes (Zenodo, 2026)**
* **Date folosite:** Date extrase din openFDA FAERS, informații demografice și planuri de tratament ale pacienților. 
* **Algoritmi AI:** Algoritmi clasici de Machine Learning aplicați pe date tabulare complexe pentru detectarea tiparelor de risc. 
* **Performanțe:** Extragerea și detectarea cu succes a cazurilor de mare risc  și a predictorilor subtili care depășesc instrumentele tradiționale de raportare.
* **Tehnologii:** Python Data Science Stack și integrarea directă cu API-urile FAERS Open Data.

**4. Drug Adverse Event Detection Using Text-Based Convolutional Neural Networks (MDPI, 2022)**
* **Date folosite:** Date textuale cu limbaj natural din comentarii și rapoarte medicale nesistematizate. 
* **Algoritmi AI:** Rețele Neurale Convoluționale adaptate pentru procesarea de text (Text-CNN).
* **Performanțe:** Evaluarea modelului s-a realizat prin Accuracy, Precision și Recall bazate pe matrici de confuzie clare, dovedind eficiența rețelelor CNN pe textul cu terminologie farmaceutică.
* **Tehnologii:** Librării NLP pentru preprocesare text (Tokenizare, curățare) și framework-uri de Deep Learning.
