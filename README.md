 CyberWatch INDIA - Cybercrime Intelligence Dashboard

CyberWatch INDIA is an innovative AI-powered web dashboard that transforms India's fight against financial cyber fraud by integrating data from the National Cybercrime Reporting Portal (NCRP), banking APIs, and telecom sources to predict high-risk cash withdrawal hotspots and deliver actionable intelligence in real time.[1][5][11]
Deployed at https://cyber-watch-india.vercel.app/,
it provides law enforcement agencies (LEAs), banks, telecom operators, and regulators with a unified platform to visualize fraud patterns, monitor trends, and enable proactive interventions like fund blocking and rapid response.[3][5][12]

 Project Purpose and Impact
The dashboard tackles key challenges in cybercrime response, including manual processes, data silos across agencies, and delayed coordination that result in significant financial losses.
By leveraging predictive analytics, it forecasts fraud-prone ATM zones and withdrawal points, empowering stakeholders with geo-specific insights to improve recovery rates, boost digital payment trust, and align with national initiatives like the Indian Cybercrime Coordination Centre (I4C).[11][12][3]

Core Features
- Interactive GIS Hotspot Mapping: Displays high-risk cash withdrawal zones, districts, and emerging trends with time, location, and crime-type filters using Leaflet.js for geospatial analysis.
- Secure Multi-User Dashboards: Customized interfaces for police (alerts, evidence tools), banks (fund-block triggers), and regulators (reports), featuring real-time notifications via SMS/email/API and offline capabilities for remote operations.[15][2][11]
- Predictive Analytics & Visualizations: ML-based risk scoring with dynamic Chart.js charts showing complaint volumes, fraud spikes, and forecasts to support data-driven decisions.

Technical Stack and Architecture
Developed with a scalable stack: Python/Pandas for data handling, PostgreSQL+PostGIS/MongoDB for geospatial storage, Node.js/Flask backend, and HTML/CSS/JavaScript frontend hosted on Vercel for high availability.
The modular architecture supports data ingestion → analytics (GIS mapping, ML prediction) → secure REST APIs → responsive web/mobile access, ensuring performance in low-connectivity areas and easy expansion to more data sources.[21][22][2]

Contributors
Collaboratively developed by:  
- Ankita Roy (Lead Developer)  
- Sneha Jana (UI/UX & Frontend)  
- Nilay Dasgupta (ML & Backend)  
- Niloy Das (Data & GIS Integration)  
- Bikramjit Saha (DevOps & Deployment)[11]

Innovation and Future Scope
This end-to-end platform innovates with GIS risk maps, cross-agency data sharing, and field-ready tools to reduce fraud losses and enhance cyber awareness nationwide.[12][2][11]
Future expansions include AR visualizations, broader bank/telecom integrations, and public-facing apps for comprehensive digital security. Live demo: https://cyber-watch-india.vercel.app/.
