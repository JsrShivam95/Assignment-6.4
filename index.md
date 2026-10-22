<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Assignment 6.4 — CSS Positioning Practice</title>
  <meta name="description" content="Demonstrating sticky navigation, fixed floating buttons, absolute badges with relative parents, and z-index layering.">
  <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>📌</text></svg>">
  <link rel="stylesheet" href="positioning.css">
</head>
<body>

  <!-- Top Announcement Bar (Scrolls away with the document) -->
  <div class="top-banner">
    🚀 Spring 2027 Registration opens next Monday! Browse updated courses below.
  </div>

  <!-- Step 2 & 6: Sticky Navbar with z-index: 100 -->
  <nav class="sticky-nav">
    <div class="nav-container">
      <a href="#hero" class="nav-brand">DevCampus</a>
      <ul class="nav-links">
        <li><a href="#overview">Overview</a></li>
        <li><a href="#courses">Courses</a></li>
        <li><a href="#faculty">Faculty</a></li>
        <li><a href="#faq">FAQ</a></li>
      </ul>
    </div>
  </nav>

  <!-- Step 3 & 6: Floating Action Button with position: fixed and z-index: 999 -->
  <a href="#help" class="fab-help" title="Need Help? Chat with us">
    <span class="fab-icon">💬</span>
    <span class="fab-label">Help</span>
  </a>

  <!-- Step 1: Multiple Scrollable Sections -->
  <main class="content-wrapper">

    <!-- Section 1: Overview -->
    <section id="overview" class="content-section">
      <span class="section-tag">Section 01</span>
      <h1>CSS Positioning in Practice</h1>
      <p class="lead-text">
        Scroll down through the page to observe how <code>position: sticky</code> locks the navigation bar at the top boundary, while the floating action button remains anchored at the bottom-right via <code>position: fixed</code>.
      </p>
      <p>
        CSS layout positioning provides fine-grained control over how elements behave relative to the standard document flow, parent containers, and the browser viewport.
      </p>
    </section>

    <!-- Section 2: Courses with Absolute-Positioned Badges (Steps 4 & 5) -->
    <section id="courses" class="content-section">
      <span class="section-tag">Section 02</span>
      <h2>Featured Academic Tracks</h2>
      <p>Notice the badges pinned to the top-right corner of each card using <code>position: absolute</code> inside a <code>position: relative</code> parent.</p>

      <div class="card-grid">

        <!-- Card 1: Relative parent + Absolute Badge -->
        <article class="course-card">
          <!-- Step 4: Absolute positioned badge -->
          <span class="badge badge-popular">Most Popular</span>
          <h3>Full-Stack Web Systems</h3>
          <p>Master modern responsive front-end architecture, API design, and server-side engineering with Node and PostgreSQL.</p>
          <div class="card-meta">12 Weeks &middot; Intermediate</div>
        </article>

        <!-- Card 2: Relative parent + Absolute Badge -->
        <article class="course-card">
          <span class="badge badge-new">New Track</span>
          <h3>Applied AI Engineering</h3>
          <p>Learn to integrate local LLMs, vector databases, and semantic search pipelines into commercial web applications.</p>
          <div class="card-meta">10 Weeks &middot; Advanced</div>
        </article>

        <!-- Card 3: Relative parent + Absolute Badge -->
        <article class="course-card">
          <span class="badge badge-limited">Filling Fast</span>
          <h3>Cloud Native DevOps</h3>
          <p>Deploy scalable infrastructure, CI/CD pipelines, container orchestration with Kubernetes, and automated monitoring.</p>
          <div class="card-meta">8 Weeks &middot; Beginner-Friendly</div>
        </article>

      </div>
    </section>

    <!-- Section 3: Faculty -->
    <section id="faculty" class="content-section">
      <span class="section-tag">Section 03</span>
      <h2>Industry Faculty Mentors</h2>
      <p>
        Courses are taught by senior engineers and research fellows with hands-on production experience. Mentorship sessions are scheduled weekly in one-on-one and small group formats.
      </p>
      <p>
        Each mentor provides continuous code review, architectural critiques, and guidance through technical career milestones.
      </p>
    </section>

    <!-- Section 4: FAQ (Generates enough scroll height) -->
    <section id="faq" class="content-section">
      <span class="section-tag">Section 04</span>
      <h2>Frequently Asked Questions</h2>
      <div class="faq-item">
        <h4>How does <code>position: sticky</code> differ from <code>position: fixed</code>?</h4>
        <p>A sticky element behaves like a normal relative element until its scroll threshold (e.g., <code>top: 0</code>) is reached, at which point it sticks within its parent container. A fixed element is removed from normal flow entirely and stays anchored relative to the viewport window.</p>
      </div>
      <div class="faq-item">
        <h4>Why do we set <code>position: relative</code> on the card parent?</h4>
        <p>Without <code>position: relative</code> on <code>.course-card</code>, an <code>absolute</code> child badge would search upward through ancestor elements until it reached the <code>&lt;body&gt;</code>, pinning itself to the edge of the entire webpage instead of the card corner.</p>
      </div>
    </section>

  </main>

  <footer class="page-footer">
    <p>&copy; 2026 DevCampus &middot; CSS Positioning Lab</p>
  </footer>

</body>
</html>


CSS

/* ==========================================================================
   Base Reset & Layout Setup
   ========================================================================== */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  background-color: #f8fafc;
  color: #1e293b;
  line-height: 1.65;
  min-height: 200vh; /* Ensures ample scroll height to test sticky/fixed */
}

/* ==========================================================================
   Top Announcement Bar (Normal document flow)
   ========================================================================== */
.top-banner {
  background-color: #0f172a;
  color: #e2e8f0;
  font-size: 0.88rem;
  text-align: center;
  padding: 10px 16px;
}

/* ==========================================================================
   Step 2 & 6: Sticky Navigation Bar
   - Sticks to viewport top once user scrolls past the top banner
   - z-index: 100 keeps it elevated above scrolling page content
   ========================================================================== */
.sticky-nav {
  position: -webkit-sticky; /* Vendor prefix for Safari */
  position: sticky;
  top: 0;
  z-index: 100; /* Keeps navbar above standard cards & text */
  background-color: #ffffff;
  border-bottom: 1px solid #e2e8f0;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
}

.nav-container {
  max-width: 1080px;
  margin: 0 auto;
  padding: 14px 24px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-brand {
  font-size: 1.3rem;
  font-weight: 800;
  color: #2563eb;
  text-decoration: none;
  letter-spacing: -0.02em;
}

.nav-links {
  list-style: none;
  display: flex;
  gap: 20px;
}

.nav-links a {
  text-decoration: none;
  color: #475569;
  font-size: 0.95rem;
  font-weight: 500;
  padding: 6px 10px;
  border-radius: 6px;
  transition: color 0.2s, background-color 0.2s;
}

.nav-links a:hover {
  color: #2563eb;
  background-color: #eff6ff;
}

/* ==========================================================================
   Step 3 & 6: Floating Action Button (FAB)
   - Anchored to bottom-right of viewport at all times
   - Highest z-index (999) to never be obscured by other elements
   ========================================================================== */
.fab-help {
  position: fixed;
  bottom: 28px;
  right: 28px;
  z-index: 999; /* Highest priority stacking context */
  display: flex;
  align-items: center;
  gap: 8px;
  background-color: #2563eb;
  color: #ffffff;
  text-decoration: none;
  font-weight: 600;
  font-size: 0.95rem;
  padding: 12px 20px;
  border-radius: 999px; /* Pill shape */
  box-shadow: 0 8px 24px rgba(37, 99, 235, 0.35);
  transition: transform 0.2s ease, background-color 0.2s ease, box-shadow 0.2s ease;
}

.fab-help:hover {
  background-color: #1d4ed8;
  transform: translateY(-3px);
  box-shadow: 0 12px 28px rgba(37, 99, 235, 0.45);
}

.fab-icon {
  font-size: 1.15rem;
}

/* ==========================================================================
   Main Content & Multi-Section Layout (Step 1)
   ========================================================================== */
.content-wrapper {
  max-width: 1080px;
  margin: 0 auto;
  padding: 40px 24px;
}

.content-section {
  background-color: #ffffff;
  border: 1px solid #e2e8f0;
  border-radius: 12px;
  padding: 36px 32px;
  margin-bottom: 36px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.03);
}

.section-tag {
  display: inline-block;
  font-size: 0.75rem;
  font-weight: 700;
  text-transform: uppercase;
  color: #2563eb;
  background-color: #eff6ff;
  padding: 4px 10px;
  border-radius: 4px;
  margin-bottom: 12px;
  letter-spacing: 0.05em;
}

h1 {
  font-size: 2.25rem;
  color: #0f172a;
  margin-bottom: 12px;
  letter-spacing: -0.02em;
}

h2 {
  font-size: 1.6rem;
  color: #0f172a;
  margin-bottom: 10px;
}

p {
  color: #475569;
  margin-bottom: 14px;
}

.lead-text {
  font-size: 1.15rem;
  color: #334155;
}

/* ==========================================================================
   Steps 4, 5 & 6: Card with Relative Parent & Absolute Badge
   ========================================================================== */
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 24px;
  margin-top: 24px;
}

/* Step 5: Appropriate position: relative on the parent container */
.course-card {
  position: relative; /* Crucial: Establishes coordinate reference point for badge */
  background-color: #ffffff;
  border: 1px solid #cbd5e1;
  border-radius: 10px;
  padding: 32px 24px 24px 24px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.04);
  transition: border-color 0.2s, box-shadow 0.2s;
}

.course-card:hover {
  border-color: #93c5fd;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.08);
}

.course-card h3 {
  font-size: 1.25rem;
  color: #0f172a;
  margin-bottom: 10px;
  padding-right: 60px; /* Space so text doesn't overlap absolute badge */
}

.course-card p {
  font-size: 0.92rem;
  color: #64748b;
  margin-bottom: 16px;
}

.card-meta {
  font-size: 0.8rem;
  font-weight: 600;
  color: #2563eb;
}

/* Step 4: position: absolute on the badge */
.badge {
  position: absolute;
  top: 14px;
  right: 14px;
  z-index: 10; /* Keeps badge cleanly resting above card border */
  font-size: 0.72rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  padding: 4px 10px;
  border-radius: 999px;
}

.badge-popular {
  background-color: #dbeafe;
  color: #1e40af;
}

.badge-new {
  background-color: #dcfce7;
  color: #166534;
}

.badge-limited {
  background-color: #fef3c7;
  color: #92400e;
}

/* FAQ items */
.faq-item {
  border-top: 1px solid #f1f5f9;
  padding: 16px 0;
}

.faq-item h4 {
  font-size: 1.05rem;
  color: #0f172a;
  margin-bottom: 6px;
}

.faq-item p {
  margin-bottom: 0;
  font-size: 0.95rem;
}

/* Footer */
.page-footer {
  text-align: center;
  padding: 32px;
  color: #94a3b8;
  font-size: 0.88rem;
  border-top: 1px solid #e2e8f0;
  background-color: #ffffff;
}