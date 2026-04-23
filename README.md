<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Winpro Architects | CRM Portal</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        :root {
            --primary: #d4af37; /* Metallic Gold */
            --bg: #0f1113;
            --sidebar-bg: #1a1d21;
            --card-bg: rgba(30, 34, 39, 0.9);
            --text-main: #ffffff;
            --text-dim: #a0a0a0;
        }

        body {
            font-family: 'Segoe UI', Roboto, sans-serif;
            background-color: var(--bg);
            /* Architectural Grid Background */
            background-image: 
                linear-gradient(rgba(212, 175, 55, 0.05) 1px, transparent 1px),
                linear-gradient(90deg, rgba(212, 175, 55, 0.05) 1px, transparent 1px);
            background-size: 30px 30px;
            color: var(--text-main);
            margin: 0;
            display: flex;
            min-height: 100vh;
        }

        /* Sidebar Design */
        .sidebar {
            width: 260px;
            background: var(--sidebar-bg);
            padding: 30px 20px;
            border-right: 1px solid #333;
            position: fixed;
            height: 100vh;
        }

        .brand {
            font-size: 28px;
            font-weight: 800;
            color: var(--primary);
            letter-spacing: 2px;
            margin-bottom: 5px;
        }
        .tagline { font-size: 10px; color: var(--text-dim); margin-bottom: 40px; text-transform: uppercase; }

        .nav-item { padding: 12px 0; color: var(--text-dim); cursor: pointer; display: flex; align-items: center; gap: 10px; transition: 0.3s; }
        .nav-item:hover { color: var(--primary); }

        /* Content Area */
        .main-content { margin-left: 300px; padding: 40px; width: calc(100% - 340px); }

        .header-section { margin-bottom: 40px; border-left: 4px solid var(--primary); padding-left: 20px; }
        .header-section h1 { margin: 0; font-size: 24px; }

        /* Professional Form */
        .glass-form {
            background: var(--card-bg);
            padding: 25px;
            border-radius: 15px;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 15px;
            margin-bottom: 40px;
            backdrop-filter: blur(10px);
            border: 1px solid #333;
        }

        input, select, textarea {
            padding: 12px;
            background: #2a2e35;
            border: 1px solid #444;
            color: white;
            border-radius: 6px;
            outline: none;
        }

        textarea { grid-column: span 2; height: 42px; resize: none; }

        .add-btn {
            background: var(--primary);
            color: #000;
            font-weight: bold;
            border: none;
            padding: 12px;
            border-radius: 6px;
            cursor: pointer;
            transition: 0.4s;
        }
        .add-btn:hover { transform: translateY(-2px); box-shadow: 0 5px 15px rgba(212, 175, 55, 0.3); }

        /* Project Cards */
        .grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 25px; }

        .project-card {
            background: var(--card-bg);
            border-radius: 12px;
            padding: 20px;
            border: 1px solid #333;
            transition: 0.3s;
            position: relative;
            overflow: hidden;
        }
        .project-card:hover { border-color: var(--primary); }
        .project-card::before {
            content: "PROJECT"; position: absolute; top: 10px; right: -20px;
            background: var(--primary); color: #000; font-size: 10px; font-weight: bold;
            padding: 2px 30px; transform: rotate(45deg);
        }

        .client-name { color: var(--primary); font-size: 18px; font-weight: bold; margin-bottom: 10px; }
        .details { font-size: 14px; margin-bottom: 8px; color: var(--text-dim); }
        .remark-box { 
            margin-top: 15px; padding-top: 10px; border-top: 1px solid #333; 
            font-style: italic; font-size: 13px; color: #8bc34a; 
        }

        .status-badge {
            display: inline-block; padding: 4px 12px; border-radius: 20px; font-size: 11px;
            background: rgba(212, 175, 55, 0.1); color: var(--primary); border: 1px solid var(--primary);
        }

        .del-icon { position: absolute; bottom: 20px; right: 20px; color: #ff5252; cursor: pointer; opacity: 0.5; }
        .del-icon:hover { opacity: 1; }
    </style>
</head>
<body>

    <div class="sidebar">
        <div class="brand">WINPRO</div>
        <div class="tagline">Architectural Solutions</div>
        <div class="nav-item"><i class="fas fa-layer-group"></i> Active Projects</div>
        <div class="nav-item"><i class="fas fa-user-tie"></i> Asian Clients</div>
        <div class="nav-item"><i class="fas fa-map-marker-alt"></i> Dubai Sites</div>
        <div class="nav-item"><i class="fas fa-cog"></i> Settings</div>
    </div>

    <div class="main-content">
        <div class="header-section">
            <h1>Narmeen Amjad | Lead Architect</h1>
            <p style="color: var(--text-dim);">Project Tracking & Client Management Dashboard</p>
        </div>

        <div class="glass-form">
            <input id="client" placeholder="Client Name (e.g. Rahul Sharma)">
            <input id="project" placeholder="Project (e.g. Dubai Marina Studio)">
            <select id="status">
                <option value="Initial Blueprint">Initial Blueprint</option>
                <option value="Structure Work">Structure Work</option>
                <option value="Final Finishing">Final Finishing</option>
            </select>
            <textarea id="remark" placeholder="Project Remark/Notes..."></textarea>
            <button class="add-btn" onclick="addProject()">+ Add Project</button>
        </div>

        <div class="grid" id="projectGrid"></div>
    </div>

    <script>
        // Real-world Asian Clients in Dubai Demo
        const asianDubaiProjects = [
            { client: "Mr. Rajan Mehta", project: "Villa Extension - Emirates Hills", status: "Structure Work", remark: "Checking MEP drawings for the pool area." },
            { client: "Chen Wei", project: "Retail Fit-out - Dragon Mart 2", status: "Final Finishing", remark: "Cabinet installation in progress." },
            { client: "Dr. Sameer Alvi", project: "Clinic Design - Bur Dubai", status: "Initial Blueprint", remark: "Waiting for DHA approval on floor plan." }
        ];

        let projects = JSON.parse(localStorage.getItem("winpro_crm_data")) || asianDubaiProjects;

        function render() {
            const grid = document.getElementById("projectGrid");
            grid.innerHTML = "";
            projects.forEach((item, index) => {
                grid.innerHTML += `
                    <div class="project-card">
                        <div class="client-name">${item.client}</div>
                        <div class="details"><b>Project:</b> ${item.project}</div>
                        <div class="details"><b>Location:</b> Dubai, UAE</div>
                        <div class="status-badge">${item.status}</div>
                        <div class="remark-box"><b>Remark:</b> ${item.remark || 'No remarks added.'}</div>
                        <i class="fas fa-trash-alt del-icon" onclick="deleteProject(${index})"></i>
                    </div>
                `;
            });
        }

        function addProject() {
            const client = document.getElementById("client").value;
            const project = document.getElementById("project").value;
            const status = document.getElementById("status").value;
            const remark = document.getElementById("remark").value;

            if(client && project) {
                projects.unshift({ client, project, status, remark });
                localStorage.setItem("winpro_crm_data", JSON.stringify(projects));
                render();
                // Clear inputs
                document.getElementById("client").value = "";
                document.getElementById("project").value = "";
                document.getElementById("remark").value = "";
            } else {
                alert("Please enter Client and Project name.");
            }
        }

        function deleteProject(index) {
            if(confirm("Delete this project?")) {
                projects.splice(index, 1);
                localStorage.setItem("winpro_crm_data", JSON.stringify(projects));
                render();
            }
        }

        render();
    </script>
</body>
</html>
