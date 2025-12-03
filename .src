<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>CyberWatch INDIA - Cybercrime Intelligence Dashboard</title>

    <!-- Leaflet CSS -->
    <link
      rel="stylesheet"
      href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
    />

    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.js"></script>

    <!-- Leaflet JS -->
    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

    <style>
      * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
      }

      :root {
        --slate-900: #0f172a;
        --slate-800: #1e293b;
        --slate-700: #334155;
        --slate-600: #475569;
        --slate-500: #64748b;
        --slate-400: #94a3b8;
        --slate-300: #cbd5e1;
        --slate-200: #e2e8f0;
        --slate-100: #f1f5f9;
        --blue-600: #2563eb;
        --blue-500: #3b82f6;
        --blue-400: #60a5fa;
        --cyan-600: #0891b2;
        --cyan-500: #06b6d4;
        --green-500: #22c55e;
        --yellow-500: #eab308;
        --red-500: #ef4444;
        --orange-500: #f97316;
      }

      body {
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto",
          "Oxygen", "Ubuntu", "Cantarell", sans-serif;
        background: linear-gradient(
          135deg,
          var(--slate-900) 0%,
          var(--slate-800) 100%
        );
        color: #f1f5f9;
        min-height: 100vh;
        line-height: 1.6;
      }

      .hidden {
        display: none !important;
      }

      /* Animations */
      @keyframes fadeInUp {
        from {
          opacity: 0;
          transform: translateY(20px);
        }
        to {
          opacity: 1;
          transform: translateY(0);
        }
      }

      @keyframes pulse-glow {
        0%,
        100% {
          box-shadow: 0 0 20px rgba(59, 130, 246, 0.3);
        }
        50% {
          box-shadow: 0 0 30px rgba(59, 130, 246, 0.5);
        }
      }

      @keyframes gradient-shift {
        0% {
          background-position: 0% 50%;
        }
        50% {
          background-position: 100% 50%;
        }
        100% {
          background-position: 0% 50%;
        }
      }

      .animate-fade-in-up {
        animation: fadeInUp 0.6s ease-out;
      }

      .gradient-animate {
        background-size: 200% 200%;
        animation: gradient-shift 8s ease infinite;
      }

      /* Navbar */
      .navbar {
        background: linear-gradient(
          135deg,
          rgba(15, 23, 42, 0.95) 0%,
          rgba(30, 41, 59, 0.95) 100%
        );
        backdrop-filter: blur(10px);
        border-bottom: 1px solid rgba(148, 163, 184, 0.2);
        padding: 1rem 2rem;
        display: flex;
        justify-content: space-between;
        align-items: center;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      }

      .navbar-brand {
        display: flex;
        align-items: center;
        gap: 0.75rem;
        font-size: 1.5rem;
        font-weight: 700;
        background: linear-gradient(135deg, #60a5fa, #06b6d4);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        background-clip: text;
      }

      .logo {
        width: 40px;
        height: 40px;
        border-radius: 8px;
        display: flex;
        align-items: center;
        justify-content: center;
        box-shadow: 0 4px 12px rgba(59, 130, 246, 0.4);
        overflow: hidden;
      }
      .logo img {
        width: 100%;
        height: 100%;
        object-fit: contain;
      }

      .navbar-user {
        display: flex;
        align-items: center;
        gap: 1rem;
      }

      .user-info {
        text-align: right;
      }

      .user-name {
        font-weight: 600;
        color: #f1f5f9;
      }

      .user-role {
        font-size: 0.875rem;
        color: var(--slate-400);
      }

      .btn {
        padding: 0.5rem 1.25rem;
        border-radius: 0.5rem;
        border: none;
        font-weight: 500;
        cursor: pointer;
        transition: all 0.3s ease;
        font-size: 0.95rem;
      }

      .btn-primary {
        background: linear-gradient(135deg, var(--blue-600), var(--cyan-600));
        color: white;
        box-shadow: 0 4px 12px rgba(59, 130, 246, 0.3);
      }

      .btn-primary:hover {
        transform: translateY(-2px);
        box-shadow: 0 6px 16px rgba(59, 130, 246, 0.4);
      }

      .btn-secondary {
        background: rgba(100, 116, 139, 0.2);
        color: #f1f5f9;
        border: 1px solid rgba(148, 163, 184, 0.3);
      }

      .btn-secondary:hover {
        background: rgba(100, 116, 139, 0.3);
      }

      .btn-danger {
        background: linear-gradient(135deg, #dc2626, #b91c1c);
        color: white;
      }

      .btn-danger:hover {
        transform: translateY(-2px);
        box-shadow: 0 6px 16px rgba(220, 38, 38, 0.4);
      }

      /* Navigation Menu */
      .nav-menu {
        background: linear-gradient(
          90deg,
          var(--slate-900),
          var(--slate-800),
          var(--slate-900)
        );
        border-bottom: 1px solid rgba(59, 130, 246, 0.2);
        padding: 0.75rem 2rem;
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
      }

      .nav-menu-items {
        display: flex;
        gap: 0.5rem;
        max-width: 1280px;
        margin: 0 auto;
      }

      .nav-btn {
        padding: 0.625rem 1.25rem;
        background: transparent;
        color: var(--slate-300);
        border: none;
        border-radius: 0.5rem;
        cursor: pointer;
        transition: all 0.3s ease;
        display: flex;
        align-items: center;
        gap: 0.5rem;
        font-size: 0.95rem;
        font-weight: 500;
      }

      .nav-btn:hover {
        background: rgba(71, 85, 105, 0.5);
      }

      .nav-btn.active {
        background: linear-gradient(135deg, var(--blue-600), var(--cyan-600));
        color: white;
        box-shadow: 0 4px 12px rgba(59, 130, 246, 0.3);
      }

      /* Container */
      .container {
        max-width: 1280px;
        margin: 0 auto;
        padding: 2rem;
      }

      /* Login Page */
      .login-container {
        min-height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
        background: linear-gradient(
          135deg,
          var(--slate-900) 0%,
          var(--slate-800) 50%,
          var(--slate-900) 100%
        );
        padding: 2rem;
      }

      .login-card {
        background: rgba(30, 41, 59, 0.7);
        backdrop-filter: blur(10px);
        border: 1px solid rgba(148, 163, 184, 0.1);
        border-radius: 1rem;
        padding: 3rem;
        width: 100%;
        max-width: 450px;
        box-shadow: 0 20px 60px rgba(0, 0, 0, 0.5);
      }

      .login-header {
        text-align: center;
        margin-bottom: 2rem;
      }

      .login-title {
        font-size: 2rem;
        font-weight: 700;
        background: linear-gradient(135deg, #60a5fa, #06b6d4);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        background-clip: text;
        margin-bottom: 0.5rem;
      }

      .login-subtitle {
        color: var(--slate-400);
        font-size: 0.95rem;
      }

      .form-group {
        margin-bottom: 1.5rem;
      }

      .form-label {
        display: block;
        margin-bottom: 0.5rem;
        color: var(--slate-300);
        font-weight: 500;
        font-size: 0.95rem;
      }

      .form-input,
      .form-select {
        width: 100%;
        padding: 0.75rem 1rem;
        background: rgba(15, 23, 42, 0.5);
        border: 1px solid rgba(148, 163, 184, 0.2);
        border-radius: 0.5rem;
        color: #f1f5f9;
        font-size: 0.95rem;
        transition: all 0.3s ease;
      }

      .form-input:focus,
      .form-select:focus {
        outline: none;
        border-color: var(--blue-500);
        box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
      }

      .form-select option {
        background: var(--slate-800);
        color: #f1f5f9;
      }

      /* Hero Section */
      .hero {
        text-align: center;
        padding: 4rem 2rem;
        background: linear-gradient(
          135deg,
          rgba(15, 23, 42, 0.8),
          rgba(30, 41, 59, 0.8)
        );
        border-radius: 1rem;
        margin-bottom: 3rem;
        animation: fadeInUp 0.6s ease-out;
      }

      .hero-title {
        font-size: 3rem;
        font-weight: 700;
        background: linear-gradient(135deg, #60a5fa, #06b6d4);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        background-clip: text;
        margin-bottom: 1rem;
      }

      .hero-subtitle {
        font-size: 1.25rem;
        color: var(--slate-300);
        margin-bottom: 2rem;
        max-width: 800px;
        margin-left: auto;
        margin-right: auto;
      }

      /* Stats Grid */
      .stats-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
        gap: 1.5rem;
        margin-bottom: 3rem;
      }

      .stat-card {
        background: rgba(30, 41, 59, 0.7);
        backdrop-filter: blur(10px);
        border: 1px solid rgba(148, 163, 184, 0.1);
        border-radius: 1rem;
        padding: 1.5rem;
        transition: all 0.3s ease;
      }

      .stat-card:hover {
        transform: translateY(-4px);
        box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
      }

      .stat-header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 1rem;
      }

      .stat-title {
        color: var(--slate-400);
        font-size: 0.875rem;
        font-weight: 500;
      }

      .stat-icon {
        width: 40px;
        height: 40px;
        border-radius: 0.5rem;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 1.25rem;
      }

      .stat-value {
        font-size: 2rem;
        font-weight: 700;
        color: #f1f5f9;
        margin-bottom: 0.5rem;
      }

      .stat-change {
        font-size: 0.875rem;
        display: flex;
        align-items: center;
        gap: 0.25rem;
      }

      .stat-change.positive {
        color: var(--green-500);
      }

      .stat-change.negative {
        color: var(--red-500);
      }

      /* Cards */
      .card {
        background: rgba(30, 41, 59, 0.7);
        backdrop-filter: blur(10px);
        border: 1px solid rgba(148, 163, 184, 0.1);
        border-radius: 1rem;
        padding: 1.5rem;
        margin-bottom: 2rem;
      }

      .card-header {
        margin-bottom: 1.5rem;
      }

      .card-title {
        font-size: 1.5rem;
        font-weight: 600;
        color: #f1f5f9;
        margin-bottom: 0.5rem;
      }

      .card-description {
        color: var(--slate-400);
        font-size: 0.95rem;
      }

      /* Map Container */
      #map {
        height: 500px;
        border-radius: 0.75rem;
        overflow: hidden;
        box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
      }

      /* Filter Sidebar */
      .dashboard-layout {
        display: grid;
        grid-template-columns: 280px 1fr;
        gap: 2rem;
        margin-bottom: 2rem;
      }

      .filter-sidebar {
        background: rgba(30, 41, 59, 0.7);
        backdrop-filter: blur(10px);
        border: 1px solid rgba(148, 163, 184, 0.1);
        border-radius: 1rem;
        padding: 1.5rem;
        height: fit-content;
        position: sticky;
        top: 1rem;
      }

      .filter-title {
        font-size: 1.125rem;
        font-weight: 600;
        margin-bottom: 1.5rem;
        color: #f1f5f9;
      }

      .filter-group {
        margin-bottom: 1.5rem;
      }

      .filter-label {
        display: block;
        margin-bottom: 0.5rem;
        color: var(--slate-300);
        font-size: 0.875rem;
        font-weight: 500;
      }

      .checkbox-group {
        display: flex;
        flex-direction: column;
        gap: 0.5rem;
      }

      .checkbox-label {
        display: flex;
        align-items: center;
        gap: 0.5rem;
        color: var(--slate-300);
        font-size: 0.875rem;
        cursor: pointer;
      }

      .checkbox-label input[type="checkbox"] {
        width: 16px;
        height: 16px;
        cursor: pointer;
      }

      /* Table */
      .table-container {
        overflow-x: auto;
        border-radius: 0.75rem;
        background: rgba(15, 23, 42, 0.5);
      }

      .table {
        width: 100%;
        border-collapse: collapse;
      }

      .table thead {
        background: rgba(30, 41, 59, 0.8);
      }

      .table th {
        padding: 1rem;
        text-align: left;
        color: var(--slate-300);
        font-weight: 600;
        font-size: 0.875rem;
        border-bottom: 1px solid rgba(148, 163, 184, 0.2);
      }

      .table td {
        padding: 1rem;
        color: var(--slate-200);
        font-size: 0.875rem;
        border-bottom: 1px solid rgba(148, 163, 184, 0.1);
      }

      .table tbody tr:hover {
        background: rgba(30, 41, 59, 0.4);
      }

      .badge {
        padding: 0.25rem 0.75rem;
        border-radius: 9999px;
        font-size: 0.75rem;
        font-weight: 600;
        display: inline-block;
      }

      .badge-critical {
        background: rgba(239, 68, 68, 0.2);
        color: #fca5a5;
        border: 1px solid rgba(239, 68, 68, 0.3);
      }

      .badge-high {
        background: rgba(249, 115, 22, 0.2);
        color: #fdba74;
        border: 1px solid rgba(249, 115, 22, 0.3);
      }

      .badge-medium {
        background: rgba(234, 179, 8, 0.2);
        color: #fde047;
        border: 1px solid rgba(234, 179, 8, 0.3);
      }

      .badge-low {
        background: rgba(34, 197, 94, 0.2);
        color: #86efac;
        border: 1px solid rgba(34, 197, 94, 0.3);
      }

      /* Charts */
      .charts-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
        gap: 2rem;
        margin-bottom: 2rem;
      }

      .chart-container {
        position: relative;
        height: 300px;
      }

      /* Toast Notifications */
      .toast-container {
        position: fixed;
        top: 1rem;
        right: 1rem;
        z-index: 9999;
        display: flex;
        flex-direction: column;
        gap: 0.5rem;
      }

      .toast {
        background: rgba(30, 41, 59, 0.95);
        backdrop-filter: blur(10px);
        border: 1px solid rgba(148, 163, 184, 0.2);
        border-radius: 0.5rem;
        padding: 1rem 1.5rem;
        min-width: 300px;
        box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        animation: fadeInUp 0.3s ease-out;
        display: flex;
        align-items: center;
        gap: 0.75rem;
      }

      .toast-success {
        border-left: 4px solid var(--green-500);
      }

      .toast-error {
        border-left: 4px solid var(--red-500);
      }

      .toast-info {
        border-left: 4px solid var(--blue-500);
      }

      .toast-message {
        flex: 1;
        color: #f1f5f9;
        font-size: 0.95rem;
      }

      /* Simulation Page */
      .simulation-controls {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
        gap: 1rem;
        margin-bottom: 2rem;
      }

      .prediction-card {
        background: rgba(30, 41, 59, 0.7);
        backdrop-filter: blur(10px);
        border: 1px solid rgba(148, 163, 184, 0.1);
        border-radius: 1rem;
        padding: 1.5rem;
        margin-bottom: 1rem;
        transition: all 0.3s ease;
      }

      .prediction-card:hover {
        transform: translateY(-2px);
        box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
      }

      .prediction-header {
        display: flex;
        justify-content: space-between;
        align-items: start;
        margin-bottom: 1rem;
      }

      .prediction-location {
        font-size: 1.125rem;
        font-weight: 600;
        color: #f1f5f9;
      }

      .prediction-type {
        font-size: 0.875rem;
        color: var(--slate-400);
      }

      .prediction-details {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        gap: 0.75rem;
        margin-top: 1rem;
      }

      .prediction-detail {
        display: flex;
        flex-direction: column;
      }

      .prediction-detail-label {
        font-size: 0.75rem;
        color: var(--slate-400);
        margin-bottom: 0.25rem;
      }

      .prediction-detail-value {
        font-size: 0.95rem;
        color: #f1f5f9;
        font-weight: 500;
      }

      /* Responsive */
      @media (max-width: 768px) {
        .navbar {
          padding: 1rem;
          flex-direction: column;
          gap: 1rem;
        }

        .nav-menu {
          padding: 0.75rem 1rem;
        }

        .nav-menu-items {
          flex-wrap: wrap;
        }

        .container {
          padding: 1rem;
        }

        .dashboard-layout {
          grid-template-columns: 1fr;
        }

        .filter-sidebar {
          position: static;
        }

        .hero-title {
          font-size: 2rem;
        }

        .hero-subtitle {
          font-size: 1rem;
        }

        .charts-grid {
          grid-template-columns: 1fr;
        }

        .simulation-controls {
          grid-template-columns: 1fr;
        }

        #map {
          height: 400px;
        }
      }

      /* Loading Spinner */
      .spinner {
        border: 3px solid rgba(148, 163, 184, 0.2);
        border-top: 3px solid var(--blue-500);
        border-radius: 50%;
        width: 40px;
        height: 40px;
        animation: spin 1s linear infinite;
        margin: 2rem auto;
      }

      @keyframes spin {
        0% {
          transform: rotate(0deg);
        }
        100% {
          transform: rotate(360deg);
        }
      }

      /* Icons (Using Unicode symbols) */
      .icon {
        display: inline-flex;
        align-items: center;
        justify-content: center;
      }
    </style>
  </head>
  <body>
    <!-- Toast Container -->
    <div id="toastContainer" class="toast-container"></div>

    <!-- Navbar (Hidden on login page) -->
    <div id="navbar" class="navbar hidden">
      <div class="navbar-brand">
        <div class="logo">
          <img
            src="https://i.postimg.cc/Jz2XXwkp/download-logo-ps.png"
            alt="CyberWatch INDIA Logo"
          />
        </div>
        <span>CyberWatch INDIA</span>
      </div>
      <div class="navbar-user">
        <div class="user-info">
          <div class="user-name" id="userName"></div>
          <div class="user-role" id="userRole"></div>
        </div>
        <button class="btn btn-danger" onclick="logout()">Logout</button>
      </div>
    </div>

    <!-- Navigation Menu (Hidden on login page) -->
    <div id="navMenu" class="nav-menu hidden">
      <div class="nav-menu-items">
        <button class="nav-btn" data-page="home" onclick="navigateTo('home')">
          <span class="icon">🏠</span> Home
        </button>
        <button
          class="nav-btn"
          data-page="dashboard"
          onclick="navigateTo('dashboard')"
        >
          <span class="icon">📊</span> Dashboard
        </button>
        <button
          class="nav-btn"
          data-page="analytics"
          onclick="navigateTo('analytics')"
        >
          <span class="icon">📈</span> Analytics
        </button>
        <button
          class="nav-btn"
          data-page="simulation"
          onclick="navigateTo('simulation')"
        >
          <span class="icon">⚡</span> Simulation
        </button>
      </div>
    </div>

    <!-- Login Page -->
    <div id="loginPage" class="login-container">
      <div class="login-card animate-fade-in-up">
        <div class="login-header">
          <div
            class="logo"
            style="margin: 0 auto 1rem; width: 80px; height: 80px"
          >
            <img
              src="https://i.postimg.cc/Jz2XXwkp/download-logo-ps.png"
              alt="CyberWatch INDIA Logo"
            />
          </div>
          <h1 class="login-title">CyberWatch INDIA</h1>
          <p class="login-subtitle">Cybercrime Intelligence Dashboard</p>
        </div>
        <form id="loginForm" onsubmit="handleLogin(event)">
          <div class="form-group">
            <label class="form-label" for="username">Username</label>
            <input
              type="text"
              id="username"
              class="form-input"
              placeholder="Enter username"
              required
            />
          </div>
          <div class="form-group">
            <label class="form-label" for="password">Password</label>
            <input
              type="password"
              id="password"
              class="form-input"
              placeholder="Enter password"
              required
            />
          </div>
          <div class="form-group">
            <label class="form-label" for="role">Role</label>
            <select id="role" class="form-select" required>
              <option value="">Select your role</option>
              <option value="LEA Officer">LEA Officer</option>
              <option value="Analyst">Analyst</option>
            </select>
          </div>
          <button
            type="submit"
            class="btn btn-primary"
            style="width: 100%; margin-top: 1rem"
          >
            Login to Dashboard
          </button>
        </form>
      </div>
    </div>

    <!-- Home Page -->
    <div id="homePage" class="hidden">
      <div class="container">
        <div class="hero">
          <h1 class="hero-title">CyberWatch INDIA</h1>
          <p class="hero-subtitle">
            Advanced Cybercrime Intelligence & Predictive Analytics Platform
          </p>
          <div
            style="
              display: flex;
              gap: 1rem;
              justify-content: center;
              margin-top: 2rem;
            "
          >
            <button class="btn btn-primary" onclick="navigateTo('dashboard')">
              View Dashboard →
            </button>
            <button
              class="btn btn-secondary"
              onclick="navigateTo('simulation')"
            >
              Run Simulation
            </button>
          </div>
        </div>

        <div class="stats-grid">
          <div class="stat-card">
            <div class="stat-header">
              <span class="stat-title">Total Alerts</span>
              <div
                class="stat-icon"
                style="background: linear-gradient(135deg, #3b82f6, #06b6d4)"
              >
                🔔
              </div>
            </div>
            <div class="stat-value">1,248</div>
            <div class="stat-change positive">
              <span>↑ 12%</span>
              <span style="color: var(--slate-400)">vs last month</span>
            </div>
          </div>

          <div class="stat-card">
            <div class="stat-header">
              <span class="stat-title">Critical Threats</span>
              <div
                class="stat-icon"
                style="background: linear-gradient(135deg, #ef4444, #dc2626)"
              >
                ⚠️
              </div>
            </div>
            <div class="stat-value">38</div>
            <div class="stat-change negative">
              <span>↑ 8%</span>
              <span style="color: var(--slate-400)">vs last month</span>
            </div>
          </div>

          <div class="stat-card">
            <div class="stat-header">
              <span class="stat-title">States Monitored</span>
              <div
                class="stat-icon"
                style="background: linear-gradient(135deg, #22c55e, #16a34a)"
              >
                🗺️
              </div>
            </div>
            <div class="stat-value">28</div>
            <div class="stat-change positive">
              <span>100%</span>
              <span style="color: var(--slate-400)">coverage</span>
            </div>
          </div>

          <div class="stat-card">
            <div class="stat-header">
              <span class="stat-title">Predictions Made</span>
              <div
                class="stat-icon"
                style="background: linear-gradient(135deg, #f59e0b, #d97706)"
              >
                🎯
              </div>
            </div>
            <div class="stat-value">892</div>
            <div class="stat-change positive">
              <span>↑ 15%</span>
              <span style="color: var(--slate-400)">vs last month</span>
            </div>
          </div>
        </div>

        <div class="card">
          <div class="card-header">
            <h2 class="card-title">About CyberWatch INDIA</h2>
            <p class="card-description">
              An advanced platform for monitoring, analyzing, and predicting
              cybercrime threats across India.
            </p>
          </div>
          <div
            style="
              display: grid;
              grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
              gap: 1.5rem;
            "
          >
            <div>
              <h3
                style="
                  font-size: 1.125rem;
                  margin-bottom: 0.5rem;
                  color: var(--blue-400);
                "
              >
                🗺️ Interactive Maps
              </h3>
              <p style="color: var(--slate-400); font-size: 0.95rem">
                Visualize cybercrime data across all Indian states and cities
                with real-time updates.
              </p>
            </div>
            <div>
              <h3
                style="
                  font-size: 1.125rem;
                  margin-bottom: 0.5rem;
                  color: var(--cyan-400);
                "
              >
                📊 Analytics
              </h3>
              <p style="color: var(--slate-400); font-size: 0.95rem">
                Comprehensive charts and graphs showing trends, patterns, and
                insights.
              </p>
            </div>
            <div>
              <h3
                style="
                  font-size: 1.125rem;
                  margin-bottom: 0.5rem;
                  color: var(--green-500);
                "
              >
                ⚡ Predictions
              </h3>
              <p style="color: var(--slate-400); font-size: 0.95rem">
                AI-powered predictive analytics to identify potential cybercrime
                hotspots.
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Dashboard Page -->
    <div id="dashboardPage" class="hidden">
      <div class="container">
        <h1
          style="
            font-size: 2rem;
            margin-bottom: 2rem;
            background: linear-gradient(135deg, #60a5fa, #06b6d4);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
          "
        >
          Interactive Dashboard
        </h1>

        <div class="dashboard-layout">
          <aside class="filter-sidebar">
            <h3 class="filter-title">Filters</h3>

            <div class="filter-group">
              <label class="filter-label">Time Range</label>
              <select
                class="form-select"
                id="timeRange"
                onchange="updateDashboard()"
              >
                <option value="24h">Last 24 Hours</option>
                <option value="7d">Last 7 Days</option>
                <option value="30d" selected>Last 30 Days</option>
                <option value="90d">Last 90 Days</option>
              </select>
            </div>

            <div class="filter-group">
              <label class="filter-label">Threat Level</label>
              <div class="checkbox-group">
                <label class="checkbox-label">
                  <input type="checkbox" checked onchange="updateDashboard()" />
                  Critical
                </label>
                <label class="checkbox-label">
                  <input type="checkbox" checked onchange="updateDashboard()" />
                  High
                </label>
                <label class="checkbox-label">
                  <input type="checkbox" checked onchange="updateDashboard()" />
                  Medium
                </label>
                <label class="checkbox-label">
                  <input type="checkbox" checked onchange="updateDashboard()" />
                  Low
                </label>
              </div>
            </div>

            <div class="filter-group">
              <label class="filter-label">Crime Type</label>
              <div class="checkbox-group">
                <label class="checkbox-label">
                  <input type="checkbox" checked onchange="updateDashboard()" />
                  Phishing
                </label>
                <label class="checkbox-label">
                  <input type="checkbox" checked onchange="updateDashboard()" />
                  Ransomware
                </label>
                <label class="checkbox-label">
                  <input type="checkbox" checked onchange="updateDashboard()" />
                  Data Breach
                </label>
                <label class="checkbox-label">
                  <input type="checkbox" checked onchange="updateDashboard()" />
                  Identity Theft
                </label>
                <label class="checkbox-label">
                  <input type="checkbox" checked onchange="updateDashboard()" />
                  Financial Fraud
                </label>
              </div>
            </div>

            <button
              class="btn btn-primary"
              style="width: 100%"
              onclick="resetFilters()"
            >
              Reset Filters
            </button>
          </aside>

          <div>
            <div class="card">
              <div class="card-header">
                <h2 class="card-title">Cybercrime Heatmap - India</h2>
                <p class="card-description">
                  Interactive map showing cybercrime incidents across Indian
                  states
                </p>
              </div>
              <div id="map"></div>
            </div>

            <div class="card">
              <div class="card-header">
                <h2 class="card-title">Recent Alerts</h2>
                <p class="card-description">
                  Latest cybercrime alerts and incidents
                </p>
              </div>
              <div class="table-container">
                <table class="table" id="alertsTable">
                  <thead>
                    <tr>
                      <th>Time</th>
                      <th>Location</th>
                      <th>Type</th>
                      <th>Severity</th>
                      <th>Status</th>
                    </tr>
                  </thead>
                  <tbody>
                    <!-- Populated by JavaScript -->
                  </tbody>
                </table>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Analytics Page -->
    <div id="analyticsPage" class="hidden">
      <div class="container">
        <h1
          style="
            font-size: 2rem;
            margin-bottom: 2rem;
            background: linear-gradient(135deg, #60a5fa, #06b6d4);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
          "
        >
          Analytics & Insights
        </h1>

        <div class="stats-grid">
          <div class="stat-card">
            <div class="stat-header">
              <span class="stat-title">Total Incidents</span>
              <div
                class="stat-icon"
                style="background: linear-gradient(135deg, #3b82f6, #06b6d4)"
              >
                📊
              </div>
            </div>
            <div class="stat-value">3,847</div>
            <div class="stat-change positive">
              <span>↑ 23%</span>
              <span style="color: var(--slate-400)">from last period</span>
            </div>
          </div>

          <div class="stat-card">
            <div class="stat-header">
              <span class="stat-title">Avg Response Time</span>
              <div
                class="stat-icon"
                style="background: linear-gradient(135deg, #22c55e, #16a34a)"
              >
                ⏱️
              </div>
            </div>
            <div class="stat-value">2.4h</div>
            <div class="stat-change positive">
              <span>↓ 15%</span>
              <span style="color: var(--slate-400)">improvement</span>
            </div>
          </div>

          <div class="stat-card">
            <div class="stat-header">
              <span class="stat-title">Resolution Rate</span>
              <div
                class="stat-icon"
                style="background: linear-gradient(135deg, #f59e0b, #d97706)"
              >
                ✅
              </div>
            </div>
            <div class="stat-value">87%</div>
            <div class="stat-change positive">
              <span>↑ 5%</span>
              <span style="color: var(--slate-400)">from last period</span>
            </div>
          </div>

          <div class="stat-card">
            <div class="stat-header">
              <span class="stat-title">Active Cases</span>
              <div
                class="stat-icon"
                style="background: linear-gradient(135deg, #ef4444, #dc2626)"
              >
                🔴
              </div>
            </div>
            <div class="stat-value">142</div>
            <div class="stat-change negative">
              <span>↑ 8%</span>
              <span style="color: var(--slate-400)">from last period</span>
            </div>
          </div>
        </div>

        <div class="charts-grid">
          <div class="card">
            <div class="card-header">
              <h3 class="card-title" style="font-size: 1.25rem">
                Crime Types Distribution
              </h3>
            </div>
            <div class="chart-container">
              <canvas id="crimeTypesChart"></canvas>
            </div>
          </div>

          <div class="card">
            <div class="card-header">
              <h3 class="card-title" style="font-size: 1.25rem">
                Monthly Trend
              </h3>
            </div>
            <div class="chart-container">
              <canvas id="monthlyTrendChart"></canvas>
            </div>
          </div>
        </div>

        <div class="card">
          <div class="card-header">
            <h2 class="card-title">Severity Level Trends</h2>
            <p class="card-description">
              Distribution of incidents by severity over time
            </p>
          </div>
          <div class="chart-container" style="height: 350px">
            <canvas id="severityTrendChart"></canvas>
          </div>
        </div>

        <div class="card">
          <div class="card-header">
            <h2 class="card-title">Top Affected States</h2>
            <p class="card-description">
              States with highest cybercrime incidents
            </p>
          </div>
          <div class="chart-container" style="height: 350px">
            <canvas id="statesChart"></canvas>
          </div>
        </div>
      </div>
    </div>

    <!-- Simulation Page -->
    <div id="simulationPage" class="hidden">
      <div class="container">
        <h1
          style="
            font-size: 2rem;
            margin-bottom: 2rem;
            background: linear-gradient(135deg, #60a5fa, #06b6d4);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
          "
        >
          Predictive Simulation
        </h1>

        <div class="card">
          <div class="card-header">
            <h2 class="card-title">Generate Predictions</h2>
            <p class="card-description">
              Simulate cybercrime predictions based on historical data and
              trends
            </p>
          </div>

          <div class="simulation-controls">
            <div class="form-group">
              <label class="form-label">State</label>
              <select class="form-select" id="simState">
                <option value="all">All States</option>
                <option value="Maharashtra">Maharashtra</option>
                <option value="Delhi">Delhi</option>
                <option value="Karnataka">Karnataka</option>
                <option value="Tamil Nadu">Tamil Nadu</option>
                <option value="Uttar Pradesh">Uttar Pradesh</option>
                <option value="West Bengal">West Bengal</option>
              </select>
            </div>

            <div class="form-group">
              <label class="form-label">Crime Type</label>
              <select class="form-select" id="simCrimeType">
                <option value="all">All Types</option>
                <option value="Phishing">Phishing</option>
                <option value="Ransomware">Ransomware</option>
                <option value="Data Breach">Data Breach</option>
                <option value="Identity Theft">Identity Theft</option>
                <option value="Financial Fraud">Financial Fraud</option>
              </select>
            </div>

            <div class="form-group">
              <label class="form-label">Time Period</label>
              <select class="form-select" id="simPeriod">
                <option value="7">Next 7 Days</option>
                <option value="14">Next 14 Days</option>
                <option value="30" selected>Next 30 Days</option>
                <option value="90">Next 90 Days</option>
              </select>
            </div>

            <div class="form-group">
              <label class="form-label">Number of Predictions</label>
              <input
                type="number"
                class="form-input"
                id="simCount"
                value="5"
                min="1"
                max="20"
              />
            </div>
          </div>

          <button
            class="btn btn-primary"
            onclick="runSimulation()"
            style="width: 100%"
          >
            ⚡ Run Simulation
          </button>
        </div>

        <div id="simulationResults" class="hidden">
          <div class="card">
            <div class="card-header">
              <h2 class="card-title">Prediction Results</h2>
              <p class="card-description">
                AI-generated cybercrime predictions
              </p>
            </div>
            <div id="predictionsContainer">
              <!-- Populated by JavaScript -->
            </div>
          </div>
        </div>
      </div>
    </div>

    <script>
      // Global State
      let currentUser = null;
      let currentPage = "login";
      let map = null;
      let charts = {};

      // Indian States Data with coordinates
      const indianStates = [
        { name: "Maharashtra", lat: 19.7515, lng: 75.7139, incidents: 245 },
        { name: "Delhi", lat: 28.7041, lng: 77.1025, incidents: 198 },
        { name: "Karnataka", lat: 15.3173, lng: 75.7139, incidents: 176 },
        { name: "Tamil Nadu", lat: 11.1271, lng: 78.6569, incidents: 164 },
        { name: "Uttar Pradesh", lat: 26.8467, lng: 80.9462, incidents: 152 },
        { name: "West Bengal", lat: 22.9868, lng: 87.855, incidents: 143 },
        { name: "Gujarat", lat: 22.2587, lng: 71.1924, incidents: 128 },
        { name: "Rajasthan", lat: 27.0238, lng: 74.2179, incidents: 115 },
        { name: "Telangana", lat: 18.1124, lng: 79.0193, incidents: 108 },
        { name: "Andhra Pradesh", lat: 15.9129, lng: 79.74, incidents: 97 },
      ];

      // Crime Types
      const crimeTypes = [
        "Phishing",
        "Ransomware",
        "Data Breach",
        "Identity Theft",
        "Financial Fraud",
      ];
      const severityLevels = ["Critical", "High", "Medium", "Low"];

      // Toast Notification System
      function showToast(message, type = "info") {
        const toast = document.createElement("div");
        toast.className = `toast toast-${type}`;
        toast.innerHTML = `
                <span class="icon">${
                  type === "success" ? "✓" : type === "error" ? "✕" : "ℹ"
                }</span>
                <div class="toast-message">${message}</div>
            `;

        document.getElementById("toastContainer").appendChild(toast);

        setTimeout(() => {
          toast.style.opacity = "0";
          setTimeout(() => toast.remove(), 300);
        }, 3000);
      }

      // Authentication
      function handleLogin(event) {
        event.preventDefault();
        const username = document.getElementById("username").value;
        const password = document.getElementById("password").value;
        const role = document.getElementById("role").value;

        if (username && password && role) {
          currentUser = { name: username, role: role };
          showToast(`Welcome, ${username}!`, "success");
          navigateTo("home");
        } else {
          showToast("Please fill in all fields", "error");
        }
      }

      function logout() {
        currentUser = null;
        showToast("Logged out successfully", "success");
        navigateTo("login");
      }

      // Navigation
      function navigateTo(page) {
        currentPage = page;

        // Hide all pages
        document.getElementById("loginPage").classList.add("hidden");
        document.getElementById("homePage").classList.add("hidden");
        document.getElementById("dashboardPage").classList.add("hidden");
        document.getElementById("analyticsPage").classList.add("hidden");
        document.getElementById("simulationPage").classList.add("hidden");

        // Update nav buttons
        document.querySelectorAll(".nav-btn").forEach((btn) => {
          btn.classList.remove("active");
        });

        if (page === "login") {
          document.getElementById("navbar").classList.add("hidden");
          document.getElementById("navMenu").classList.add("hidden");
          document.getElementById("loginPage").classList.remove("hidden");
        } else {
          if (!currentUser) {
            navigateTo("login");
            return;
          }

          document.getElementById("navbar").classList.remove("hidden");
          document.getElementById("navMenu").classList.remove("hidden");
          document.getElementById("userName").textContent = currentUser.name;
          document.getElementById("userRole").textContent = currentUser.role;

          document.getElementById(`${page}Page`).classList.remove("hidden");
          const navBtn = document.querySelector(`[data-page="${page}"]`);
          if (navBtn) navBtn.classList.add("active");

          // Initialize page-specific content
          if (page === "dashboard") {
            initDashboard();
          } else if (page === "analytics") {
            initAnalytics();
          }
        }
      }

      // Dashboard Functions
      function initDashboard() {
        if (!map) {
          // Initialize Leaflet map centered on India
          setTimeout(() => {
            map = L.map("map").setView([20.5937, 78.9629], 5);

            L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
              attribution: "© OpenStreetMap contributors",
              maxZoom: 18,
            }).addTo(map);

            // Add markers for Indian states
            indianStates.forEach((state) => {
              const severity =
                state.incidents > 180
                  ? "critical"
                  : state.incidents > 140
                  ? "high"
                  : state.incidents > 120
                  ? "medium"
                  : "low";

              const color =
                severity === "critical"
                  ? "#ef4444"
                  : severity === "high"
                  ? "#f97316"
                  : severity === "medium"
                  ? "#eab308"
                  : "#22c55e";

              const circle = L.circleMarker([state.lat, state.lng], {
                radius: Math.sqrt(state.incidents) * 2,
                fillColor: color,
                color: "#fff",
                weight: 2,
                opacity: 1,
                fillOpacity: 0.6,
              }).addTo(map);

              circle.bindPopup(`
                            <div style="color: #1e293b; font-family: system-ui;">
                                <strong style="font-size: 1.1em;">${
                                  state.name
                                }</strong><br>
                                <span style="color: #64748b;">Incidents: ${
                                  state.incidents
                                }</span><br>
                                <span style="color: ${color}; font-weight: 600;">Severity: ${severity.toUpperCase()}</span>
                            </div>
                        `);
            });

            showToast("Map loaded successfully", "success");
          }, 100);
        }

        // Populate alerts table
        populateAlertsTable();
      }

      function populateAlertsTable() {
        const tbody = document.querySelector("#alertsTable tbody");
        tbody.innerHTML = "";

        const alerts = generateAlerts(15);
        alerts.forEach((alert) => {
          const row = tbody.insertRow();
          row.innerHTML = `
                    <td>${alert.time}</td>
                    <td>${alert.location}</td>
                    <td>${alert.type}</td>
                    <td><span class="badge badge-${alert.severity.toLowerCase()}">${
            alert.severity
          }</span></td>
                    <td>${alert.status}</td>
                `;
        });
      }

      function generateAlerts(count) {
        const alerts = [];
        const statuses = ["Active", "Investigating", "Resolved", "Pending"];

        for (let i = 0; i < count; i++) {
          const state =
            indianStates[Math.floor(Math.random() * indianStates.length)];
          const crimeType =
            crimeTypes[Math.floor(Math.random() * crimeTypes.length)];
          const severity =
            severityLevels[Math.floor(Math.random() * severityLevels.length)];
          const status = statuses[Math.floor(Math.random() * statuses.length)];

          const hoursAgo = Math.floor(Math.random() * 48);
          const time = `${hoursAgo}h ago`;

          alerts.push({
            time,
            location: state.name,
            type: crimeType,
            severity,
            status,
          });
        }

        return alerts;
      }

      function updateDashboard() {
        populateAlertsTable();
        showToast("Dashboard updated", "info");
      }

      function resetFilters() {
        document
          .querySelectorAll('.filter-sidebar input[type="checkbox"]')
          .forEach((cb) => {
            cb.checked = true;
          });
        document.getElementById("timeRange").value = "30d";
        updateDashboard();
        showToast("Filters reset", "info");
      }

      // Analytics Functions
      function initAnalytics() {
        if (!charts.crimeTypes) {
          createCrimeTypesChart();
          createMonthlyTrendChart();
          createSeverityTrendChart();
          createStatesChart();
        }
      }

      function createCrimeTypesChart() {
        const ctx = document.getElementById("crimeTypesChart").getContext("2d");
        charts.crimeTypes = new Chart(ctx, {
          type: "doughnut",
          data: {
            labels: crimeTypes,
            datasets: [
              {
                data: [324, 287, 256, 198, 165],
                backgroundColor: [
                  "rgba(59, 130, 246, 0.8)",
                  "rgba(6, 182, 212, 0.8)",
                  "rgba(34, 197, 94, 0.8)",
                  "rgba(234, 179, 8, 0.8)",
                  "rgba(239, 68, 68, 0.8)",
                ],
                borderColor: "#1e293b",
                borderWidth: 2,
              },
            ],
          },
          options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
              legend: {
                position: "bottom",
                labels: {
                  color: "#cbd5e1",
                  padding: 15,
                  font: { size: 12 },
                },
              },
            },
          },
        });
      }

      function createMonthlyTrendChart() {
        const ctx = document
          .getElementById("monthlyTrendChart")
          .getContext("2d");
        charts.monthlyTrend = new Chart(ctx, {
          type: "line",
          data: {
            labels: ["Jan", "Feb", "Mar", "Apr", "May", "Jun"],
            datasets: [
              {
                label: "Incidents",
                data: [520, 580, 640, 610, 720, 780],
                borderColor: "rgba(59, 130, 246, 1)",
                backgroundColor: "rgba(59, 130, 246, 0.1)",
                tension: 0.4,
                fill: true,
                borderWidth: 3,
              },
            ],
          },
          options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
              legend: {
                labels: {
                  color: "#cbd5e1",
                  font: { size: 12 },
                },
              },
            },
            scales: {
              y: {
                beginAtZero: true,
                ticks: { color: "#94a3b8" },
                grid: { color: "rgba(148, 163, 184, 0.1)" },
              },
              x: {
                ticks: { color: "#94a3b8" },
                grid: { color: "rgba(148, 163, 184, 0.1)" },
              },
            },
          },
        });
      }

      function createSeverityTrendChart() {
        const ctx = document
          .getElementById("severityTrendChart")
          .getContext("2d");
        charts.severityTrend = new Chart(ctx, {
          type: "bar",
          data: {
            labels: ["Week 1", "Week 2", "Week 3", "Week 4"],
            datasets: [
              {
                label: "Critical",
                data: [45, 52, 48, 55],
                backgroundColor: "rgba(239, 68, 68, 0.8)",
              },
              {
                label: "High",
                data: [68, 72, 65, 78],
                backgroundColor: "rgba(249, 115, 22, 0.8)",
              },
              {
                label: "Medium",
                data: [92, 88, 95, 90],
                backgroundColor: "rgba(234, 179, 8, 0.8)",
              },
              {
                label: "Low",
                data: [125, 130, 128, 135],
                backgroundColor: "rgba(34, 197, 94, 0.8)",
              },
            ],
          },
          options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
              legend: {
                position: "top",
                labels: {
                  color: "#cbd5e1",
                  padding: 15,
                  font: { size: 12 },
                },
              },
            },
            scales: {
              y: {
                stacked: true,
                beginAtZero: true,
                ticks: { color: "#94a3b8" },
                grid: { color: "rgba(148, 163, 184, 0.1)" },
              },
              x: {
                stacked: true,
                ticks: { color: "#94a3b8" },
                grid: { color: "rgba(148, 163, 184, 0.1)" },
              },
            },
          },
        });
      }

      function createStatesChart() {
        const ctx = document.getElementById("statesChart").getContext("2d");
        const topStates = indianStates.slice(0, 8);

        charts.states = new Chart(ctx, {
          type: "bar",
          data: {
            labels: topStates.map((s) => s.name),
            datasets: [
              {
                label: "Incidents",
                data: topStates.map((s) => s.incidents),
                backgroundColor: "rgba(6, 182, 212, 0.8)",
                borderColor: "rgba(6, 182, 212, 1)",
                borderWidth: 2,
              },
            ],
          },
          options: {
            responsive: true,
            maintainAspectRatio: false,
            indexAxis: "y",
            plugins: {
              legend: {
                display: false,
              },
            },
            scales: {
              x: {
                beginAtZero: true,
                ticks: { color: "#94a3b8" },
                grid: { color: "rgba(148, 163, 184, 0.1)" },
              },
              y: {
                ticks: { color: "#94a3b8" },
                grid: { color: "rgba(148, 163, 184, 0.1)" },
              },
            },
          },
        });
      }

      // Simulation Functions
      function runSimulation() {
        const state = document.getElementById("simState").value;
        const crimeType = document.getElementById("simCrimeType").value;
        const period = document.getElementById("simPeriod").value;
        const count = parseInt(document.getElementById("simCount").value);

        showToast("Running simulation...", "info");

        setTimeout(() => {
          const predictions = generatePredictions(
            count,
            state,
            crimeType,
            period
          );
          displayPredictions(predictions);
          showToast("Simulation completed successfully!", "success");
        }, 1500);
      }

      function generatePredictions(
        count,
        stateFilter,
        crimeTypeFilter,
        period
      ) {
        const predictions = [];

        for (let i = 0; i < count; i++) {
          const state =
            stateFilter === "all"
              ? indianStates[Math.floor(Math.random() * indianStates.length)]
                  .name
              : stateFilter;

          const type =
            crimeTypeFilter === "all"
              ? crimeTypes[Math.floor(Math.random() * crimeTypes.length)]
              : crimeTypeFilter;

          const severity =
            severityLevels[Math.floor(Math.random() * severityLevels.length)];
          const confidence = (75 + Math.random() * 20).toFixed(1);
          const daysAhead = Math.floor(Math.random() * parseInt(period)) + 1;
          const probability = (60 + Math.random() * 35).toFixed(1);

          predictions.push({
            state,
            type,
            severity,
            confidence,
            daysAhead,
            probability,
            targetCount: Math.floor(50 + Math.random() * 200),
          });
        }

        return predictions;
      }

      function displayPredictions(predictions) {
        const container = document.getElementById("predictionsContainer");
        const resultsSection = document.getElementById("simulationResults");

        container.innerHTML = predictions
          .map(
            (pred, index) => `
                <div class="prediction-card" style="animation-delay: ${
                  index * 0.1
                }s;">
                    <div class="prediction-header">
                        <div>
                            <div class="prediction-location">${pred.state}</div>
                            <div class="prediction-type">${pred.type}</div>
                        </div>
                        <span class="badge badge-${pred.severity.toLowerCase()}">${
              pred.severity
            }</span>
                    </div>
                    <div class="prediction-details">
                        <div class="prediction-detail">
                            <span class="prediction-detail-label">Confidence</span>
                            <span class="prediction-detail-value">${
                              pred.confidence
                            }%</span>
                        </div>
                        <div class="prediction-detail">
                            <span class="prediction-detail-label">Probability</span>
                            <span class="prediction-detail-value">${
                              pred.probability
                            }%</span>
                        </div>
                        <div class="prediction-detail">
                            <span class="prediction-detail-label">Time Frame</span>
                            <span class="prediction-detail-value">${
                              pred.daysAhead
                            } days</span>
                        </div>
                        <div class="prediction-detail">
                            <span class="prediction-detail-label">Est. Targets</span>
                            <span class="prediction-detail-value">${
                              pred.targetCount
                            }</span>
                        </div>
                    </div>
                </div>
            `
          )
          .join("");

        resultsSection.classList.remove("hidden");
        resultsSection.scrollIntoView({ behavior: "smooth", block: "nearest" });
      }

      // Initialize app
      navigateTo("login");
    </script>
  </body>
</html>
//This update includes minor documentation improvements for better project clarity
