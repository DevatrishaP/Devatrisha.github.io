<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Devatrisha Purkayastha - Interactive Resume</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            padding: 20px;
            min-height: 100vh;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 40px;
            text-align: center;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        .header p {
            font-size: 1.1em;
            opacity: 0.95;
            margin: 5px 0;
        }

        .controls {
            background: #f8f9fa;
            padding: 15px 40px;
            border-bottom: 2px solid #e9ecef;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .edit-btn, .add-section-btn, .export-btn {
            padding: 10px 20px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s;
        }

        .edit-btn {
            background: #667eea;
            color: white;
        }

        .edit-btn:hover {
            background: #5568d3;
            transform: translateY(-2px);
        }

        .add-section-btn {
            background: #10b981;
            color: white;
        }

        .add-section-btn:hover {
            background: #059669;
            transform: translateY(-2px);
        }

        .export-btn {
            background: #f59e0b;
            color: white;
        }

        .export-btn:hover {
            background: #d97706;
            transform: translateY(-2px);
        }

        .content {
            padding: 40px;
        }

        .section {
            margin-bottom: 40px;
            position: relative;
            padding: 20px;
            border-radius: 10px;
            transition: all 0.3s;
        }

        .section:hover {
            background: #f8f9fa;
        }

        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .section h2 {
            color: #667eea;
            font-size: 1.8em;
            border-bottom: 3px solid #667eea;
            padding-bottom: 10px;
            display: inline-block;
        }

        .section-controls {
            display: none;
            gap: 10px;
        }

        .section:hover .section-controls {
            display: flex;
        }

        .icon-btn {
            background: none;
            border: none;
            cursor: pointer;
            font-size: 1.2em;
            padding: 5px 10px;
            border-radius: 5px;
            transition: all 0.3s;
        }

        .icon-btn:hover {
            background: #e9ecef;
        }

        .editable {
            outline: none;
            padding: 5px;
            border-radius: 5px;
            transition: all 0.3s;
        }

        .editable:focus {
            background: #fff3cd;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.2);
        }

        .skills-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
        }

        .skill-category {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 10px;
            border-left: 4px solid #667eea;
        }

        .skill-category h3 {
            color: #667eea;
            margin-bottom: 10px;
        }

        .experience-item, .education-item {
            margin-bottom: 25px;
            padding: 20px;
            background: #f8f9fa;
            border-radius: 10px;
            border-left: 4px solid #764ba2;
        }

        .experience-item h3, .education-item h3 {
            color: #764ba2;
            margin-bottom: 5px;
        }

        .experience-item h4, .education-item h4 {
            color: #6c757d;
            font-weight: normal;
            margin-bottom: 10px;
        }

        .experience-item ul, .education-item ul {
            margin-left: 20px;
            margin-top: 10px;
        }

        .experience-item li {
            margin-bottom: 8px;
            line-height: 1.6;
        }

        .publications {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 10px;
            border-left: 4px solid #10b981;
        }

        .publications a {
            color: #667eea;
            text-decoration: none;
            font-weight: 600;
        }

        .publications a:hover {
            text-decoration: underline;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }

        .modal-content {
            background: white;
            padding: 30px;
            border-radius: 15px;
            max-width: 500px;
            width: 90%;
        }

        .modal-content h3 {
            margin-bottom: 20px;
            color: #667eea;
        }

        .modal-content input, .modal-content textarea {
            width: 100%;
            padding: 10px;
            margin-bottom: 15px;
            border: 2px solid #e9ecef;
            border-radius: 5px;
            font-family: inherit;
        }

        .modal-content textarea {
            min-height: 100px;
            resize: vertical;
        }

        .modal-buttons {
            display: flex;
            gap: 10px;
            justify-content: flex-end;
        }

        .modal-buttons button {
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: 600;
        }

        .modal-buttons .save {
            background: #10b981;
            color: white;
        }

        .modal-buttons .cancel {
            background: #6c757d;
            color: white;
        }

        @media print {
            body {
                background: white;
                padding: 0;
            }
            .controls, .section-controls, .icon-btn {
                display: none !important;
            }
            .container {
                box-shadow: none;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1 contenteditable="true" class="editable" id="name">Devatrisha Purkayastha</h1>
            <p contenteditable="true" class="editable" id="title">Integrated MS-PhD, IISER Pune, India</p>
            <p contenteditable="true" class="editable" id="contact">📞 +91 93667 58373 | 📧 devatrisha13@gmail.com | 🔗 <a href="https://www.linkedin.com/in/devatrisha-p-513427118/" style="color: white;">LinkedIn</a></p>
        </div>

        <div class="controls">
            <button class="edit-btn" onclick="toggleEdit()">🖊️ Edit Mode: OFF</button>
            <button class="add-section-btn" onclick="showAddSection()">➕ Add Section</button>
            <button class="export-btn" onclick="exportResume()">💾 Export HTML</button>
        </div>

        <div class="content" id="content">
            <div class="section" id="summary">
                <div class="section-header">
                    <h2>Professional Summary</h2>
                    <div class="section-controls">
                        <button class="icon-btn" onclick="deleteSection('summary')">🗑️</button>
                    </div>
                </div>
                <p contenteditable="true" class="editable">Highly motivated PhD Candidate (expected 2026) specializing in Next-Generation Sequencing (NGS) workflows and advanced regulatory biology. I possess expertise in how <strong>RNAs regulate 3D structure of the genome and control gene expression</strong> in a eukaryotic pathogen model, requiring the design of end-to-end wet and dry lab methodologies. I crave opportunities for scientific puzzle-solving at the frontier of genomics technology and seek a challenging scientist role to contribute directly to industry R&D excellence and explore the translational pathways enabled by a leading platform.</p>
            </div>

            <div class="section" id="skills">
                <div class="section-header">
                    <h2>Core Technical & Translational Skills</h2>
                    <div class="section-controls">
                        <button class="icon-btn" onclick="deleteSection('skills')">🗑️</button>
                    </div>
                </div>
                <div class="skills-grid">
                    <div class="skill-category">
                        <h3 contenteditable="true" class="editable">Genomics & Wet Lab</h3>
                        <p contenteditable="true" class="editable">Basic Molecular Biology techniques, NGS Workflow Design, 3D Genome Mapping (Hi-C), Epigenetics (ChIP-seq), Transcription Kinetics, CRISPR/Cas9, Proteomics, in-vitro assays, Cell culture.</p>
                    </div>
                    <div class="skill-category">
                        <h3 contenteditable="true" class="editable">Microscopy & Imaging</h3>
                        <p contenteditable="true" class="editable">Brightfield, Epifluorescence, Confocal, Multi-color Immunofluorescence (IFA), FRAP (Fluorescence Recovery After Photobleaching), Live Imaging, Z-stack Acquisition, Image Analysis (ImageJ)</p>
                    </div>
                    <div class="skill-category">
                        <h3 contenteditable="true" class="editable">Data & Bioinformatics</h3>
                        <p contenteditable="true" class="editable">NGS data QC and pipeline optimization, Statistical Modeling (R), Python (Pandas/NumPy), Juicer, Complex Data Visualization, Data-Driven Insight Generation.</p>
                    </div>
                    <div class="skill-category">
                        <h3 contenteditable="true" class="editable">Translational Innovation</h3>
                        <p contenteditable="true" class="editable">Market Research, Pre-seed Business Modeling, Intellectual Property Strategy, Tech Transfer Readiness, Investor Proposal Generation</p>
                    </div>
                    <div class="skill-category">
                        <h3 contenteditable="true" class="editable">Laboratory Operations</h3>
                        <p contenteditable="true" class="editable">Procurement & Inventory Management (Vendor Relations, Budget Comparison), Workflow Scheduling and Active Scientific Discussion Leadership.</p>
                    </div>
                    <div class="skill-category">
                        <h3 contenteditable="true" class="editable">Teaching & Mentorship</h3>
                        <p contenteditable="true" class="editable">Mentored 5+ trainees, guided Gold Medal winning iGEM 2021 team, coordinated outreach teaching for underprivileged high school students, and served as institute TA.</p>
                    </div>
                </div>
            </div>

            <div class="section" id="experience">
                <div class="section-header">
                    <h2>Professional Experience</h2>
                    <div class="section-controls">
                        <button class="icon-btn" onclick="deleteSection('experience')">🗑️</button>
                    </div>
                </div>
                <div class="experience-item">
                    <h3 contenteditable="true" class="editable">Integrated PhD Scholar</h3>
                    <h4 contenteditable="true" class="editable">Plasmodium Epigenetics Lab, IISER Pune, India | 2019 - Present</h4>
                    <ul>
                        <li contenteditable="true" class="editable"><strong>Disease Mechanism Discovery:</strong> Led the effort to uncover how non-coding RNAs regulate genome structure to control virulence genes, crucial in understanding malaria pathogenesis (Currently ongoing & unpublished work).</li>
                        <li contenteditable="true" class="editable"><strong>End-to-End Wet Lab Platform Execution:</strong> Developed and implemented an integrated multi-omic platform (ChIP-seq, Hi-C, RNA-seq) from sample preparation, final library construction and data analysis and pipeline designs, demonstrating expertise in complex bench-to-data workflows.</li>
                        <li contenteditable="true" class="editable"><strong>Methodology & Quality Control:</strong> Mastered advanced, non-standard techniques like 3D genome mapping and nascent RNA sequencing, successfully overcoming challenges inherent to a non-canonical eukaryotic genome such as Plasmodium falciparum.</li>
                    </ul>
                </div>
                <div class="experience-item">
                    <h3 contenteditable="true" class="editable">AIC-SEED Student Entrepreneur-in-Residence Program</h3>
                    <h4 contenteditable="true" class="editable">Translational Innovation Exposure | 2023 - 2024</h4>
                    <ul>
                        <li contenteditable="true" class="editable"><strong>Entrepreneurship:</strong> Co-founded a deep tech startup "Still-Silk", a futuristic endeavor to produce spider silk fibers of high tensile strength through recombinant biotechnology.</li>
                        <li contenteditable="true" class="editable"><strong>Technical Scaling & Strategic Funding:</strong> Developed the pre-seed business model, led the translational strategy, including collaborating with textile scientists to formulate recombinant yarn spinning methods and conducting research and authored multiple competitive biotech grants (e.g., BIRAC), demonstrating the ability to secure strategic resources and communicate technical milestones to investors/funders.</li>
                    </ul>
                </div>
            </div>

            <div class="section" id="publications">
                <div class="section-header">
                    <h2>Research Contributions</h2>
                    <div class="section-controls">
                        <button class="icon-btn" onclick="deleteSection('publications')">🗑️</button>
                    </div>
                </div>
                <div class="publications">
                    <p contenteditable="true" class="editable">• Mamatharani, D. V., Purkayastha, D., et al. (2025). <a href="https://www.biorxiv.org/content/10.1101/2025.09.23.678141v1.full">The regulation of virulence gene expression...</a> (bioRxiv).</p>
                    <p contenteditable="true" class="editable">• Purkayastha, D., & Karmodiya, K. (2023). <a href="https://www.sciencedirect.com/science/article/pii/S156713482300103X">RNA Polymerase II evolution and adaptations...</a> Infection, Genetics and Evolution, 115, 105505.</p>
                </div>
            </div>

            <div class="section" id="education">
                <div class="section-header">
                    <h2>Education & Credentials</h2>
                    <div class="section-controls">
                        <button class="icon-btn" onclick="deleteSection('education')">🗑️</button>
                    </div>
                </div>
                <div class="education-item">
                    <h3 contenteditable="true" class="editable">Integrated PhD (MSc + PhD), Biology</h3>
                    <h4 contenteditable="true" class="editable">Expected 2026 | IISER Pune | Supervisor: Dr. Krishanpal Karmodiya | MS-CGPA: 8.4</h4>
                </div>
                <div class="education-item">
                    <h3 contenteditable="true" class="editable">BSc (Hons), Biotechnology</h3>
                    <h4 contenteditable="true" class="editable">2016-2019 | St. Edmund's College, North Eastern Hill University, Shillong | University Rank 2</h4>
                </div>
                <div class="education-item">
                    <h3 contenteditable="true" class="editable">Credentials</h3>
                    <p contenteditable="true" class="editable">CSIR-NET (AIR 61) | JGEEBILS Qualifier | AIC-SEED-StEP Fellow | Ishaan Uday Scholar | HBCSE Biology Olympiad - State Topper</p>
                </div>
            </div>
        </div>
    </div>

    <div class="modal" id="addSectionModal">
        <div class="modal-content">
            <h3>Add New Section</h3>
            <input type="text" id="sectionTitle" placeholder="Section Title (e.g., Hobbies, Awards)">
            <textarea id="sectionContent" placeholder="Section content..."></textarea>
            <div class="modal-buttons">
                <button class="cancel" onclick="closeModal()">Cancel</button>
                <button class="save" onclick="addNewSection()">Add Section</button>
            </div>
        </div>
    </div>

    <script>
        let editMode = false;

        function toggleEdit() {
            editMode = !editMode;
            const btn = document.querySelector('.edit-btn');
            const editables = document.querySelectorAll('.editable');
            
            if (editMode) {
                btn.textContent = '🖊️ Edit Mode: ON';
                btn.style.background = '#10b981';
                editables.forEach(el => el.setAttribute('contenteditable', 'true'));
            } else {
                btn.textContent = '🖊️ Edit Mode: OFF';
                btn.style.background = '#667eea';
                editables.forEach(el => el.setAttribute('contenteditable', 'false'));
                saveToStorage();
            }
        }

        function showAddSection() {
            document.getElementById('addSectionModal').style.display = 'flex';
        }

        function closeModal() {
            document.getElementById('addSectionModal').style.display = 'none';
            document.getElementById('sectionTitle').value = '';
            document.getElementById('sectionContent').value = '';
        }

        function addNewSection() {
            const title = document.getElementById('sectionTitle').value;
            const content = document.getElementById('sectionContent').value;
            
            if (!title || !content) {
                alert('Please fill in both title and content');
                return;
            }

            const sectionId = 'section_' + Date.now();
            const newSection = document.createElement('div');
            newSection.className = 'section';
            newSection.id = sectionId;
            newSection.innerHTML = `
                <div class="section-header">
                    <h2>${title}</h2>
                    <div class="section-controls">
                        <button class="icon-btn" onclick="deleteSection('${sectionId}')">🗑️</button>
                    </div>
                </div>
                <p contenteditable="true" class="editable">${content}</p>
            `;

            document.getElementById('content').appendChild(newSection);
            closeModal();
            saveToStorage();
        }

        function deleteSection(sectionId) {
            if (confirm('Are you sure you want to delete this section?')) {
                document.getElementById(sectionId).remove();
                saveToStorage();
            }
        }

        function exportResume() {
            const content = document.documentElement.outerHTML;
            const blob = new Blob([content], { type: 'text/html' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'devatrisha_resume.html';
            a.click();
            URL.revokeObjectURL(url);
        }

        function saveToStorage() {
            const content = document.getElementById('content').innerHTML;
            const header = document.querySelector('.header').innerHTML;
            const data = { content, header };
            // Data stored in memory for this session
            window.resumeData = data;
        }

        function loadFromStorage() {
            if (window.resumeData) {
                document.getElementById('content').innerHTML = window.resumeData.content;
                document.querySelector('.header').innerHTML = window.resumeData.header;
            }
        }

        window.addEventListener('load', loadFromStorage);
    </script>
</body>
</html>
