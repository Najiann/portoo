<template>
  <div class="portfolio-root" :data-theme="currentTheme">
    <!-- Skip link for accessibility -->
    <a href="#main-content" class="skip-link">Lewati ke konten utama</a>

    <!-- Sticky Navigation Bar -->
    <header class="site-header">
      <div class="header-inner">
        <!-- Brand Wordmark -->
        <a href="#about" class="brand-link" aria-label="Jihan Aulia Portofolio">
          <span 
            @click.stop.prevent="handleMonogramClick" 
            class="brand-symbol" 
            title="Klik 5x untuk akses admin"
          >&gt;_</span>
          <div class="brand-text">
            <span class="brand-name">Jihan Aulia</span>
            <span class="brand-sub">Automation &amp; Web</span>
          </div>
        </a>

        <!-- Desktop Navigation Links -->
        <nav class="desktop-nav" aria-label="Navigasi Utama">
          <a href="#about" class="nav-item">Tentang</a>
          <a href="#workflow" class="nav-item">Alur Kerja</a>
          <a href="#experience" class="nav-item">Pengalaman</a>
          <a href="#skills" class="nav-item">Keahlian</a>
          <a href="#certificates" class="nav-item">Sertifikat</a>
          <a href="#projects" class="nav-item">Proyek</a>
          <a href="#contact" class="nav-item">Kontak</a>
        </nav>

        <!-- Header Actions -->
        <div class="header-actions">
          <!-- Theme Toggle -->
          <button 
            @click="toggleTheme" 
            class="action-btn theme-toggle-btn"
            :aria-label="currentTheme === 'dark' ? 'Ganti ke tema terang' : 'Ganti ke tema gelap'"
            :title="currentTheme === 'dark' ? 'Tema Terang' : 'Tema Gelap'"
          >
            <span class="btn-icon" aria-hidden="true">{{ currentTheme === 'dark' ? '☀️' : '🌙' }}</span>
            <span class="btn-text">{{ currentTheme === 'dark' ? 'Light' : 'Dark' }}</span>
          </button>

          <!-- Admin Panel Button (Authorized Only) -->
          <button 
            v-if="isAdminAuthorized"
            @click="openAdminModal" 
            class="action-btn admin-toggle-btn"
            aria-label="Buka Panel Kelola Sertifikat"
            title="Kelola data sertifikat via panel admin"
          >
            <span class="btn-icon" aria-hidden="true">⚙️</span>
            <span class="btn-text">Admin</span>
            <span v-if="certificates.length > 0" class="badge-count">{{ certificates.length }}</span>
          </button>

          <!-- Mobile Hamburger Toggle -->
          <button 
            @click="isMobileMenuOpen = !isMobileMenuOpen" 
            class="mobile-menu-btn"
            :aria-expanded="isMobileMenuOpen"
            aria-label="Buka menu navigasi"
          >
            <span class="hamburger-line" :class="{ 'open': isMobileMenuOpen }"></span>
            <span class="hamburger-line" :class="{ 'open': isMobileMenuOpen }"></span>
            <span class="hamburger-line" :class="{ 'open': isMobileMenuOpen }"></span>
          </button>
        </div>
      </div>

      <!-- Mobile Dropdown Navigation -->
      <nav v-if="isMobileMenuOpen" class="mobile-nav" aria-label="Navigasi Mobile">
        <a href="#about" @click="isMobileMenuOpen = false" class="mobile-nav-link">Tentang</a>
        <a href="#workflow" @click="isMobileMenuOpen = false" class="mobile-nav-link">Alur Kerja (n8n)</a>
        <a href="#experience" @click="isMobileMenuOpen = false" class="mobile-nav-link">Pengalaman &amp; Pendidikan</a>
        <a href="#skills" @click="isMobileMenuOpen = false" class="mobile-nav-link">Keahlian</a>
        <a href="#certificates" @click="isMobileMenuOpen = false" class="mobile-nav-link">Sertifikat</a>
        <a href="#projects" @click="isMobileMenuOpen = false" class="mobile-nav-link">Proyek GitHub</a>
        <a href="#contact" @click="isMobileMenuOpen = false" class="mobile-nav-link">Hubungi Saya</a>
      </nav>
    </header>

    <!-- Main Content -->
    <main id="main-content" class="content-wrapper">

      <!-- ===================================================================
           1. HERO SECTION
           Clean 2-column layout: Clear intro statement + Authentic Developer Card
           =================================================================== -->
      <section id="about" class="section hero-section">
        <div class="hero-grid">
          <!-- Left Column: Primary Copy & Actions -->
          <div class="hero-copy">
            <div class="availability-pill">
              <span class="status-indicator-dot"></span>
              <span class="availability-text">Tersedia untuk Magang, Full-Time &amp; Freelance</span>
            </div>

            <h1 class="hero-heading">
              Membangun Sistem Web &amp; Automasi Alur Kerja Bisnis
            </h1>

            <p class="hero-description">
              Halo, saya <strong>Jihan Aulia</strong>. Mahasiswa <strong>S1 Informatika Universitas Nusa Mandiri</strong> dengan fokus keahlian pada 
              <strong>workflow automation (n8n)</strong>, integrasi webhook &amp; bot WhatsApp, serta pengembangan aplikasi web terstruktur 
              (<strong>Laravel, PHP, Vue</strong>). Menggabungkan teori ilmu komputer dengan pengalaman praktis menangani operasional digital industri.
            </p>

            <div class="hero-actions">
              <a href="#projects" class="btn btn-primary">
                <span>Eksplorasi Proyek</span>
                <span class="btn-arrow">→</span>
              </a>
              <a href="#workflow" class="btn btn-secondary">
                <span>Simulasi Alur n8n</span>
              </a>
              <a href="#contact" class="btn btn-ghost">
                <span>Hubungi Langsung</span>
              </a>
            </div>
          </div>

          <!-- Right Column: Authentic Developer Summary Card (Clean, no tacky emojis) -->
          <div class="hero-dev-card">
            <div class="dev-card-header">
              <div class="dev-header-info">
                <h2 class="dev-name">Jihan Aulia</h2>
                <p class="dev-role">S1 Informatika · Universitas Nusa Mandiri</p>
              </div>
              <span class="dev-status-tag">Mahasiswa Aktif</span>
            </div>

            <div class="dev-summary-list">
              <div class="dev-summary-row">
                <span class="row-term">Pendidikan</span>
                <span class="row-detail">S1 Informatika, Univ. Nusa Mandiri</span>
              </div>
              <div class="dev-summary-row">
                <span class="row-term">Fokus Bidang</span>
                <span class="row-detail">Workflow Automation &amp; Web Dev</span>
              </div>
              <div class="dev-summary-row">
                <span class="row-term">Tools Automasi</span>
                <span class="row-detail">n8n, Webhook, REST API, WA Gateway</span>
              </div>
              <div class="dev-summary-row">
                <span class="row-term">Stack Web</span>
                <span class="row-detail">Laravel, PHP, Vue 3, CodeIgniter, MySQL</span>
              </div>
              <div class="dev-summary-row">
                <span class="row-term">Data &amp; Python</span>
                <span class="row-detail">Python, Pandas, SQL, Supervised ML</span>
              </div>
              <div class="dev-summary-row">
                <span class="row-term">Ketersediaan</span>
                <span class="row-detail">Magang, Freelance &amp; Posisi Tech</span>
              </div>
            </div>

            <div class="dev-card-tags">
              <span class="tech-pill">n8n</span>
              <span class="tech-pill">Laravel</span>
              <span class="tech-pill">PHP</span>
              <span class="tech-pill">Vue 3</span>
              <span class="tech-pill">Python</span>
              <span class="tech-pill">MySQL</span>
              <span class="tech-pill">Git</span>
            </div>
          </div>
        </div>
      </section>

      <!-- ===================================================================
           2. WORKFLOW AUTOMATION VISUALIZER
           Clean 4-step interactive pipeline explorer
           =================================================================== -->
      <section id="workflow" class="section workflow-section">
        <div class="section-header">
          <span class="section-tag">Studi Kasus Interaktif</span>
          <h2 class="section-title">Visualisasi Alur Automasi (n8n Pipeline)</h2>
          <p class="section-lead">
            Simulasi interaktif dari arsitektur automasi yang pernah saya bangun di PT Mafi Global Asia 
            untuk menyinkronkan data pesanan, CRM, dan notifikasi WhatsApp secara instan tanpa input manual.
          </p>
        </div>

        <div class="pipeline-container">
          <!-- Step Selector Bar -->
          <div class="step-navigator" role="tablist" aria-label="Langkah Alur Kerja">
            <button 
              v-for="(step, idx) in workflowSteps" 
              :key="step.id"
              @click="activeWorkflowIndex = idx"
              class="step-nav-btn"
              :class="{ 'active': activeWorkflowIndex === idx }"
              role="tab"
              :aria-selected="activeWorkflowIndex === idx"
            >
              <div class="step-index">0{{ idx + 1 }}</div>
              <div class="step-text">
                <span class="step-role-label">{{ step.role }}</span>
                <strong class="step-name-label">{{ step.name }}</strong>
              </div>
            </button>
          </div>

          <!-- Active Step Detail Card -->
          <div class="pipeline-card" role="tabpanel">
            <div class="pipeline-card-top">
              <div class="pipeline-meta">
                <span class="node-type-pill">{{ currentWorkflow.type }}</span>
                <h3 class="pipeline-active-title">{{ currentWorkflow.name }}</h3>
              </div>
              <p class="pipeline-desc">{{ currentWorkflow.description }}</p>
            </div>

            <!-- Code Comparison Boxes -->
            <div class="code-comparison-grid">
              <div class="code-box">
                <div class="code-box-header">
                  <span class="code-label">Input Payload / Trigger</span>
                  <span class="code-tag">JSON</span>
                </div>
                <pre class="code-content"><code>{{ currentWorkflow.inputSample }}</code></pre>
              </div>

              <div class="code-box">
                <div class="code-box-header">
                  <span class="code-label">Operasi Node &amp; Output</span>
                  <span class="code-tag">Response</span>
                </div>
                <pre class="code-content"><code>{{ currentWorkflow.outputSample }}</code></pre>
              </div>
            </div>

            <!-- Business Impact Callout -->
            <div class="impact-callout">
              <div class="impact-icon">💡</div>
              <div class="impact-content">
                <strong>Dampak Efisiensi Bisnis:</strong>
                <span>{{ currentWorkflow.impact }}</span>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- ===================================================================
           3. EXPERIENCE & EDUCATION
           Clean modern timeline with S1 Nusa Mandiri at top
           =================================================================== -->
      <section id="experience" class="section experience-section">
        <div class="section-header">
          <span class="section-tag">Rekam Jejak</span>
          <h2 class="section-title">Pengalaman Kerja &amp; Pendidikan</h2>
          <p class="section-lead">
            Kombinasi pendidikan tinggi informatika, pengalaman praktis di industri, dan fondasi vokasi terverifikasi.
          </p>
        </div>

        <div class="timeline-container">
          <!-- Timeline Item 1: Higher Education (Universitas Nusa Mandiri) -->
          <div class="timeline-item">
            <div class="timeline-dot-wrapper">
              <div class="timeline-dot"></div>
              <div class="timeline-line"></div>
            </div>
            <div class="timeline-card">
              <div class="timeline-card-header">
                <div class="role-group">
                  <h3 class="role-title">S1 Informatika</h3>
                  <div class="org-meta">Universitas Nusa Mandiri · Sedang Menempuh Pendidikan (Mahasiswa Aktif)</div>
                </div>
                <span class="badge-role badge-study">Pendidikan Tinggi</span>
              </div>
              <ul class="achievement-list">
                <li>Menempuh studi sarjana (S1) pada Program Studi Informatika, memperdalam ilmu komputer, struktur data, algoritma, arsitektur basis data, dan kecerdasan buatan.</li>
                <li>Menerapkan teori komputasi akademis secara langsung ke dalam pengembangan proyek nyata workflow automation dan aplikasi web modern.</li>
                <li>Aktif mengembangkan portofolio teknis dan sistem integrasi API yang terhubung dengan kebutuhan operasional industri.</li>
              </ul>
            </div>
          </div>

          <!-- Timeline Item 2: Industry Internship (PT Mafi Global Asia) -->
          <div class="timeline-item">
            <div class="timeline-dot-wrapper">
              <div class="timeline-dot"></div>
              <div class="timeline-line"></div>
            </div>
            <div class="timeline-card">
              <div class="timeline-card-header">
                <div class="role-group">
                  <h3 class="role-title">Digital Support Intern</h3>
                  <div class="org-meta">PT Mafi Global Asia · 2025 sampai 2026</div>
                </div>
                <span class="badge-role badge-work">Magang Industri</span>
              </div>
              <ul class="achievement-list">
                <li>Membangun dan memelihara workflow automasi n8n untuk integrasi leads CRM dan broadcast WhatsApp otomatis.</li>
                <li>Mengembangkan skrip automasi pengingat tagihan berkala dan pembaruan status inventaris.</li>
                <li>Mengelola konten situs WordPress perusahaan serta mengoptimalkan struktur SEO teknis harian.</li>
              </ul>
            </div>
          </div>

          <!-- Timeline Item 3: Training Cohort (Dicoding x DBS Foundation) -->
          <div class="timeline-item">
            <div class="timeline-dot-wrapper">
              <div class="timeline-dot"></div>
              <div class="timeline-line"></div>
            </div>
            <div class="timeline-card">
              <div class="timeline-card-header">
                <div class="role-group">
                  <h3 class="role-title">Machine Learning Engineer</h3>
                  <div class="org-meta">Dicoding Indonesia x DBS Foundation Coding Camp · 2025</div>
                </div>
                <span class="badge-role badge-study">Program Pelatihan</span>
              </div>
              <ul class="achievement-list">
                <li>Mempelajari fondasi Python, eksplorasi data dengan Pandas/NumPy, serta manipulasi basis data SQL.</li>
                <li>Membangun model machine learning supervised dan menyelesaikan proyek akhir klasifikasi stunting (Stunting_Model_ML).</li>
                <li>Lulus penuh (Full Graduate) dengan pemahaman pipeline machine learning dari data preparation hingga evaluasi model.</li>
              </ul>
            </div>
          </div>

          <!-- Timeline Item 4: Vocational High School (SMK RPL) -->
          <div class="timeline-item">
            <div class="timeline-dot-wrapper">
              <div class="timeline-dot"></div>
            </div>
            <div class="timeline-card">
              <div class="timeline-card-header">
                <div class="role-group">
                  <h3 class="role-title">Rekayasa Perangkat Lunak (RPL)</h3>
                  <div class="org-meta">SMK Bidang Keahlian TI · Lulusan Terverifikasi</div>
                </div>
                <span class="badge-role badge-school">Pendidikan Kejuruan</span>
              </div>
              <ul class="achievement-list">
                <li>Memperdalam algoritma pemrograman, perancangan database relasional MySQL, dan arsitektur web MVC (PHP CodeIgniter/Laravel).</li>
                <li>Praktek kolaboratif version control menggunakan Git dan GitHub secara konsisten.</li>
                <li>Menyelesaikan proyek Uji Kompetensi Keahlian (UKK) sistem persewaan dan manajemen inventaris berbasis web.</li>
              </ul>
            </div>
          </div>
        </div>
      </section>

      <!-- ===================================================================
           4. SKILLS SECTION
           Clean filterable card grid
           =================================================================== -->
      <section id="skills" class="section skills-section">
        <div class="section-header">
          <span class="section-tag">Perangkat &amp; Kompetensi</span>
          <h2 class="section-title">Keahlian Teknis</h2>
          <p class="section-lead">
            Teknologi dan perangkat yang saya gunakan sehari-hari untuk merancang solusi digital.
          </p>
        </div>

        <!-- Filter Segmented Tabs -->
        <div class="filter-tab-bar" role="tablist" aria-label="Filter Keahlian">
          <button 
            v-for="cat in skillCategories" 
            :key="cat.id"
            @click="activeSkillCategory = cat.id"
            class="tab-btn"
            :class="{ 'active': activeSkillCategory === cat.id }"
            role="tab"
            :aria-selected="activeSkillCategory === cat.id"
          >
            {{ cat.label }}
          </button>
        </div>

        <!-- Skills Grid -->
        <div class="skills-grid">
          <div 
            v-for="skill in filteredSkills" 
            :key="skill.name" 
            class="skill-card"
          >
            <div class="skill-card-top">
              <h3 class="skill-name">{{ skill.name }}</h3>
              <span class="skill-category-tag">{{ skill.categoryLabel }}</span>
            </div>
            <p class="skill-usage">{{ skill.usage }}</p>
          </div>
        </div>
      </section>

      <!-- ===================================================================
           5. CERTIFICATES SECTION
           Clean card layout without badge collisions
           =================================================================== -->
      <section id="certificates" class="section certificates-section">
        <div class="section-header">
          <span class="section-tag">Kredensial &amp; Pencapaian</span>
          <h2 class="section-title">Sertifikasi Kompetensi</h2>
          <p class="section-lead">
            Daftar sertifikat kelulusan dan kredensial teknis. Klik sertifikat untuk melihat detail verifikasi.
          </p>
        </div>

        <!-- Admin Mode Banner -->
        <div v-if="isAdminAuthorized" class="admin-notice-banner">
          <div class="banner-text">
            <strong>Mode Admin Aktif:</strong> Anda dapat mengelola data sertifikat secara mandiri di penyimpanan lokal.
          </div>
          <button @click="openAdminModal" class="btn btn-sm btn-secondary">
            + Kelola di Panel Admin
          </button>
        </div>

        <!-- Certificate Grid (Redesigned: Status in header, clean footer) -->
        <div v-if="certificates.length > 0" class="cert-grid">
          <div 
            v-for="cert in certificates" 
            :key="cert.id"
            class="cert-card"
            @click="selectCertificate(cert)"
            tabindex="0"
            @keydown.enter="selectCertificate(cert)"
            @keydown.space.prevent="selectCertificate(cert)"
            role="button"
            :aria-label="'Buka detail sertifikat: ' + cert.title"
          >
            <div class="cert-card-header">
              <div class="cert-meta-group">
                <span class="cert-issuer">{{ cert.issuer }}</span>
                <span class="cert-year">{{ cert.year }}</span>
              </div>
              <span class="status-badge" :class="cert.statusClass">
                {{ getCleanStatusLabel(cert) }}
              </span>
            </div>

            <h3 class="cert-title">{{ cert.title }}</h3>
            <p class="cert-desc">{{ cert.description }}</p>

            <div class="cert-card-footer">
              <span class="cert-cat-pill">{{ cert.category }}</span>
              <span class="cert-link-text">
                Lihat Detail
                <span class="arrow-glyph">→</span>
              </span>
            </div>
          </div>
        </div>

        <div v-else class="empty-box">
          <p>Belum ada data sertifikat tersimpan.</p>
          <button @click="resetDefaultCertificates" class="btn btn-secondary btn-sm">
            Muat Data Bawaan
          </button>
        </div>
      </section>

      <!-- ===================================================================
           6. LIVE GITHUB PROJECTS
           Direct API fetch, real-time search & filter
           =================================================================== -->
      <section id="projects" class="section projects-section">
        <div class="section-header">
          <span class="section-tag">Repositori Terverifikasi</span>
          <h2 class="section-title">Proyek Nyata di GitHub</h2>
          <p class="section-lead">
            Data proyek publik yang diambil langsung dari akun GitHub resmi 
            <a href="https://github.com/Najiann" target="_blank" rel="noopener noreferrer" class="link-inline">
              github.com/Najiann
            </a>.
          </p>
        </div>

        <!-- Toolbar: Filters + Search -->
        <div class="projects-toolbar">
          <div class="filter-tab-bar" role="tablist" aria-label="Filter Kategori Proyek">
            <button 
              v-for="f in repoFilters" 
              :key="f.id"
              @click="activeRepoFilter = f.id"
              class="tab-btn"
              :class="{ 'active': activeRepoFilter === f.id }"
              role="tab"
              :aria-selected="activeRepoFilter === f.id"
            >
              {{ f.label }}
            </button>
          </div>

          <div class="search-wrapper">
            <span class="search-icon">🔍</span>
            <input 
              v-model="repoSearchQuery" 
              type="text" 
              placeholder="Cari repositori..." 
              class="search-input"
              aria-label="Cari repositori berdasarkan judul atau bahasa"
            />
          </div>
        </div>

        <!-- Loading State -->
        <div v-if="repoLoading" class="state-container loading-state">
          <div class="spinner-loader" aria-hidden="true"></div>
          <p>Mengambil data repositori terbaru dari GitHub API...</p>
        </div>

        <!-- Error State -->
        <div v-else-if="repoError" class="state-container error-state">
          <p class="error-msg">Perhatian: {{ repoError }}</p>
          <button @click="fetchRepositories" class="btn btn-secondary btn-sm">
            Coba Ambil Ulang
          </button>
        </div>

        <!-- Grid State -->
        <div v-else-if="filteredRepos.length > 0" class="repos-grid">
          <article 
            v-for="repo in filteredRepos" 
            :key="repo.id || repo.name" 
            class="repo-card"
          >
            <div class="repo-card-top">
              <span class="repo-lang-pill">
                <span class="lang-color-dot" :data-lang="repo.language || 'Code'"></span>
                {{ repo.language || 'Source Code' }}
              </span>
              <span class="repo-vis">Publik</span>
            </div>

            <h3 class="repo-title">
              {{ formatRepoTitle(repo.name) }}
            </h3>

            <p class="repo-desc">
              {{ getRepoDescription(repo) }}
            </p>

            <div class="repo-card-footer">
              <span class="repo-slug">{{ repo.name }}</span>
              <a 
                :href="repo.html_url" 
                target="_blank" 
                rel="noopener noreferrer" 
                class="btn-repo-link"
                :aria-label="'Buka repositori ' + repo.name + ' di GitHub'"
              >
                <span>Buka di GitHub</span>
                <span class="external-arrow">↗</span>
              </a>
            </div>
          </article>
        </div>

        <!-- Empty State -->
        <div v-else class="state-container empty-state">
          <p>Tidak ada repositori yang cocok dengan kata kunci pencarian atau filter saat ini.</p>
          <button @click="clearRepoFilters" class="btn btn-secondary btn-sm">
            Reset Filter
          </button>
        </div>
      </section>

      <!-- ===================================================================
           7. CONTACT & INQUIRY SECTION
           Direct contact channels + working structured form
           =================================================================== -->
      <section id="contact" class="section contact-section">
        <div class="section-header">
          <span class="section-tag">Komunikasi Langsung</span>
          <h2 class="section-title">Hubungi Jihan Aulia</h2>
          <p class="section-lead">
            Tersedia untuk peluang kerja magang/penuh waktu, proyek automasi bisnis, atau kolaborasi pengembangan web.
          </p>
        </div>

        <div class="contact-grid">
          <!-- Left Column: Direct Info -->
          <div class="contact-info-card">
            <h3 class="card-inner-title">Kanal Komunikasi Resmi</h3>
            <p class="contact-intro">
              Kirim pesan langsung melalui email atau diskusikan kebutuhan automasi alur kerja dan pengembangan aplikasi web.
            </p>

            <div class="channel-items">
              <div class="channel-card">
                <div class="channel-icon">✉️</div>
                <div class="channel-meta">
                  <span class="channel-label">Email Utama</span>
                  <span class="channel-value">jihanaulia2408@gmail.com</span>
                </div>
                <button 
                  @click="copyEmail" 
                  class="btn-copy"
                  :class="{ 'copied': copySuccess }"
                  aria-label="Salin alamat email ke clipboard"
                >
                  {{ copySuccess ? '✓ Tersalin' : 'Salin Email' }}
                </button>
              </div>

              <div class="channel-card">
                <div class="channel-icon">🐙</div>
                <div class="channel-meta">
                  <span class="channel-label">Profil GitHub</span>
                  <a 
                    href="https://github.com/Najiann" 
                    target="_blank" 
                    rel="noopener noreferrer" 
                    class="channel-link"
                  >
                    github.com/Najiann ↗
                  </a>
                </div>
              </div>
            </div>

            <div class="guarantee-card">
              <div class="guarantee-icon">⏱️</div>
              <div class="guarantee-text">
                <strong>Komitmen Balasan:</strong> Pesan melalui formulir atau email akan dijawab dalam waktu 1x24 jam kerja.
              </div>
            </div>
          </div>

          <!-- Right Column: Functional Message Form -->
          <div class="contact-form-card">
            <h3 class="card-inner-title">Kirim Pesan Langsung</h3>
            <form @submit.prevent="handleContactSubmit" class="inquiry-form" novalidate>
              <div class="form-group">
                <label for="contact-name">Nama Anda / Perusahaan *</label>
                <input 
                  id="contact-name" 
                  v-model="contactForm.name" 
                  type="text" 
                  required 
                  class="form-control"
                  placeholder="Contoh: Budi Santoso / PT Inovasi"
                />
              </div>

              <div class="form-group">
                <label for="contact-email">Alamat Email Anda *</label>
                <input 
                  id="contact-email" 
                  v-model="contactForm.email" 
                  type="email" 
                  required 
                  class="form-control"
                  placeholder="nama@perusahaan.com"
                />
              </div>

              <div class="form-group">
                <label for="contact-topic">Tujuan Kebutuhan *</label>
                <select id="contact-topic" v-model="contactForm.topic" class="form-control select-control">
                  <option value="Rekrutmen Kerja (Full-time / Magang)">Perekrutan Karyawan (Full-time / Magang)</option>
                  <option value="Proyek Workflow Automation (n8n)">Pekerjaan Automasi Alur Kerja (n8n / CRM / WA)</option>
                  <option value="Pengembangan Aplikasi Web">Pembangunan Aplikasi Web (Laravel / PHP / Vue)</option>
                  <option value="Konsultasi & Lainnya">Pertanyaan Umum atau Konsultasi</option>
                </select>
              </div>

              <div class="form-group">
                <label for="contact-message">Pesan Anda *</label>
                <textarea 
                  id="contact-message" 
                  v-model="contactForm.message" 
                  rows="4" 
                  required 
                  class="form-control"
                  placeholder="Jelaskan kebutuhan proyek atau informasi posisi yang tersedia..."
                ></textarea>
              </div>

              <div v-if="formFeedback" class="feedback-alert" :class="formFeedback.type">
                {{ formFeedback.message }}
              </div>

              <button type="submit" class="btn btn-primary btn-block">
                <span>Kirim Pesan Sekarang</span>
                <span class="btn-arrow">→</span>
              </button>
            </form>
          </div>
        </div>
      </section>

    </main>

    <!-- Footer -->
    <footer class="site-footer">
      <div class="footer-inner">
        <div class="footer-brand">
          <strong>Jihan Aulia</strong>
          <span class="footer-dot">·</span>
          <span>Workflow Automation &amp; Web Developer</span>
        </div>
        <div class="footer-links">
          <a href="#about" class="footer-anchor">Kembali ke Atas ↑</a>
          <button v-if="isAdminAuthorized" @click="openAdminModal" class="footer-anchor btn-link-clean">
            Kelola Sertifikat
          </button>
        </div>
      </div>
    </footer>

    <!-- ===================================================================
         MODAL 1: CERTIFICATE DETAIL MODAL
         Keyboard accessible (ESC, outside click)
         =================================================================== -->
    <div 
      v-if="selectedCertificate" 
      class="modal-backdrop"
      @click.self="closeCertificateModal"
      @keydown.esc="closeCertificateModal"
      role="dialog"
      aria-modal="true"
      aria-labelledby="cert-modal-title"
    >
      <div class="modal-box">
        <div class="modal-header">
          <div>
            <span class="modal-kicker">{{ selectedCertificate.category }}</span>
            <h3 id="cert-modal-title" class="modal-title">{{ selectedCertificate.title }}</h3>
          </div>
          <button 
            @click="closeCertificateModal" 
            class="modal-close-btn"
            aria-label="Tutup jendela rincian sertifikat"
          >
            ✕
          </button>
        </div>

        <div class="modal-body">
          <div class="modal-specs">
            <div class="spec-row">
              <span class="row-label">Lembaga Penerbit</span>
              <strong class="row-value">{{ selectedCertificate.issuer }}</strong>
            </div>
            <div class="spec-row">
              <span class="row-label">Tahun Penerbitan</span>
              <strong class="row-value">{{ selectedCertificate.year }}</strong>
            </div>
            <div class="spec-row">
              <span class="row-label">Status Dokumen</span>
              <span class="status-badge" :class="selectedCertificate.statusClass">
                {{ getCleanStatusLabel(selectedCertificate) }}
              </span>
            </div>
          </div>

          <div class="modal-note-box">
            <h4 class="note-heading">Keterangan Kompetensi</h4>
            <p class="note-text">{{ selectedCertificate.description }}</p>
            <p class="note-subtext">{{ selectedCertificate.verificationNote || 'Kredensial dapat divalidasi silang melalui bukti kelulusan institusi terkait.' }}</p>
          </div>

          <div v-if="selectedCertificate.fileUrl" class="modal-action-row">
            <a 
              :href="selectedCertificate.fileUrl" 
              target="_blank" 
              rel="noopener noreferrer" 
              class="btn btn-primary btn-sm"
            >
              Buka Berkas Digital ↗
            </a>
          </div>
          <div v-else class="file-pending-box">
            <span class="pending-tag">Menunggu Unggahan Berkas Digital</span>
            <p>Soft file dokumen fisik ini belum diunggah. Dokumen dapat ditambahkan melalui Panel Admin jika sudah tersedia.</p>
          </div>
        </div>

        <div class="modal-footer">
          <button @click="closeCertificateModal" class="btn btn-secondary btn-sm">
            Tutup Dialog
          </button>
        </div>
      </div>
    </div>

    <!-- ===================================================================
         MODAL 2: ADMIN PANEL DRAWER / MODAL
         Manage certificates in browser localStorage
         =================================================================== -->
    <div 
      v-if="isAdminModalOpen" 
      class="modal-backdrop"
      @click.self="closeAdminModal"
      @keydown.esc="closeAdminModal"
      role="dialog"
      aria-modal="true"
      aria-labelledby="admin-panel-title"
    >
      <div class="modal-box admin-modal-box">
        <div class="modal-header">
          <div>
            <span class="modal-kicker">Penyimpanan Lokal (localStorage)</span>
            <h3 id="admin-panel-title" class="modal-title">Panel Kelola Sertifikat</h3>
          </div>
          <button 
            @click="closeAdminModal" 
            class="modal-close-btn"
            aria-label="Tutup panel admin"
          >
            ✕
          </button>
        </div>

        <div class="modal-body admin-scroll-body">
          <p class="admin-lead-text">
            Tambahkan sertifikat baru atau kelola daftar yang tersimpan di browser Anda. Perubahan langsung tercermin di halaman portofolio.
          </p>

          <!-- Add Certificate Form -->
          <div class="admin-card-section">
            <h4 class="admin-section-title">Tambah Sertifikat Baru</h4>
            <form @submit.prevent="addNewCertificate" class="admin-form">
              <div class="form-grid-2">
                <div class="form-group">
                  <label for="new-cert-title">Judul Sertifikat *</label>
                  <input 
                    id="new-cert-title" 
                    v-model="newCert.title" 
                    type="text" 
                    required 
                    placeholder="Contoh: Sertifikasi AWS Cloud" 
                    class="form-control"
                  />
                </div>
                <div class="form-group">
                  <label for="new-cert-issuer">Lembaga Penerbit *</label>
                  <input 
                    id="new-cert-issuer" 
                    v-model="newCert.issuer" 
                    type="text" 
                    required 
                    placeholder="Contoh: Amazon Web Services / Dicoding" 
                    class="form-control"
                  />
                </div>
              </div>

              <div class="form-grid-3">
                <div class="form-group">
                  <label for="new-cert-year">Tahun *</label>
                  <input 
                    id="new-cert-year" 
                    v-model="newCert.year" 
                    type="text" 
                    required 
                    placeholder="2026" 
                    class="form-control"
                  />
                </div>
                <div class="form-group">
                  <label for="new-cert-cat">Kategori *</label>
                  <select id="new-cert-cat" v-model="newCert.category" class="form-control select-control">
                    <option value="Workflow Automation">Workflow Automation</option>
                    <option value="Web Development">Web Development</option>
                    <option value="Machine Learning">Machine Learning</option>
                    <option value="Software Engineering">Software Engineering</option>
                    <option value="Lainnya">Lainnya</option>
                  </select>
                </div>
                <div class="form-group">
                  <label for="new-cert-status">Status Berkas *</label>
                  <select id="new-cert-status" v-model="newCert.statusType" class="form-control select-control">
                    <option value="digital">Berkas Digital Tersedia</option>
                    <option value="physical">Sertifikat Fisik (Belum Ada Soft File)</option>
                    <option value="verified">Keterangan Magang Terverifikasi</option>
                  </select>
                </div>
              </div>

              <div class="form-group">
                <label for="new-cert-desc">Deskripsi Singkat Kompetensi *</label>
                <textarea 
                  id="new-cert-desc" 
                  v-model="newCert.description" 
                  rows="2" 
                  required 
                  placeholder="Keterangan materi yang dipelajari dan keahlian yang diuji..."
                  class="form-control"
                ></textarea>
              </div>

              <div class="form-group">
                <label for="new-cert-url">Link URL Dokumen / Kredensial (Opsional)</label>
                <input 
                  id="new-cert-url" 
                  v-model="newCert.fileUrl" 
                  type="url" 
                  placeholder="https://..." 
                  class="form-control"
                />
              </div>

              <div class="admin-submit-row">
                <button type="submit" class="btn btn-primary btn-sm">
                  Simpan Sertifikat
                </button>
              </div>
            </form>
          </div>

          <!-- Existing List -->
          <div class="admin-card-section">
            <div class="table-heading-row">
              <h4 class="admin-section-title">Sertifikat Terdaftar ({{ certificates.length }})</h4>
              <button @click="resetDefaultCertificates" class="btn btn-ghost btn-xs">
                Kembalikan Data Bawaan
              </button>
            </div>

            <div class="table-wrapper">
              <table class="admin-table">
                <thead>
                  <tr>
                    <th>Judul Sertifikat</th>
                    <th>Penerbit</th>
                    <th>Tahun</th>
                    <th>Status</th>
                    <th>Aksi</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="c in certificates" :key="c.id">
                    <td><strong>{{ c.title }}</strong></td>
                    <td>{{ c.issuer }}</td>
                    <td>{{ c.year }}</td>
                    <td>
                      <span class="status-badge" :class="c.statusClass">{{ getCleanStatusLabel(c) }}</span>
                    </td>
                    <td>
                      <button 
                        @click="deleteCertificate(c.id)" 
                        class="btn-delete"
                        :aria-label="'Hapus sertifikat ' + c.title"
                      >
                        Hapus
                      </button>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>

        <div class="modal-footer admin-footer-bar">
          <button @click="logoutAdmin" class="btn btn-ghost btn-sm btn-logout">
            🔒 Kunci &amp; Keluar Mode Admin
          </button>
          <button @click="closeAdminModal" class="btn btn-secondary btn-sm">
            Tutup Panel
          </button>
        </div>
      </div>
    </div>

    <!-- ===================================================================
         MODAL 3: ADMIN ACCESS VERIFICATION (Secret PIN Gate)
         Opened via Ctrl+Shift+A or 5 clicks on monogram
         =================================================================== -->
    <div 
      v-if="isPinModalOpen" 
      class="modal-backdrop"
      @click.self="closePinModal"
      @keydown.esc="closePinModal"
      role="dialog"
      aria-modal="true"
      aria-labelledby="pin-modal-title"
    >
      <div class="modal-box pin-modal-box">
        <div class="modal-header">
          <div>
            <span class="modal-kicker">Autentikasi Internal</span>
            <h3 id="pin-modal-title" class="modal-title">Buka Akses Panel Admin</h3>
          </div>
          <button 
            @click="closePinModal" 
            class="modal-close-btn"
            aria-label="Tutup jendela autentikasi"
          >
            ✕
          </button>
        </div>

        <form @submit.prevent="verifyAdminPin" class="modal-body">
          <p class="pin-hint-text">
            Masukkan PIN admin untuk mengaktifkan fitur pengelolaan sertifikat di peramban ini.
          </p>

          <div class="form-group">
            <label for="admin-pin-field">Kata Sandi / PIN Admin</label>
            <input 
              id="admin-pin-field" 
              v-model="adminPinInput" 
              type="password" 
              required 
              autocomplete="current-password"
              placeholder="Masukkan PIN (Bawaan: jihan2026)" 
              class="form-control"
              autofocus
            />
          </div>

          <div v-if="pinErrorMsg" class="feedback-alert error">
            {{ pinErrorMsg }}
          </div>

          <div class="pin-actions">
            <button type="button" @click="closePinModal" class="btn btn-ghost btn-sm">
              Batal
            </button>
            <button type="submit" class="btn btn-primary btn-sm">
              Verifikasi &amp; Buka
            </button>
          </div>
        </form>
      </div>
    </div>

  </div>
</template>

<script>
// Fallback initial dataset for repositories in case of GitHub API rate limits
const FALLBACK_REPOSITORIES = [
  {
    id: 101,
    name: 'Inventory-Management-System',
    language: 'Blade',
    fork: false,
    html_url: 'https://github.com/Najiann/Inventory-Management-System',
    inferred_desc: 'Sistem manajemen inventaris berbasis web untuk pencatatan stok, alur keluar-masuk barang, dan pelaporan terstruktur.'
  },
  {
    id: 102,
    name: 'Stunting_Prediction',
    language: 'Blade',
    fork: false,
    html_url: 'https://github.com/Najiann/Stunting_Prediction',
    inferred_desc: 'Aplikasi web pemantauan gizi dan prediksi risiko stunting balita berbasis parameter antropometri.'
  },
  {
    id: 103,
    name: 'Stunting_Model_ML',
    language: 'Python',
    fork: false,
    html_url: 'https://github.com/Najiann/Stunting_Model_ML',
    inferred_desc: 'Model klasifikasi machine learning untuk analisis data dan prediksi stunting (Capstone Proyek DBS Foundation x Dicoding).'
  },
  {
    id: 104,
    name: 'CosRent',
    language: 'PHP',
    fork: false,
    html_url: 'https://github.com/Najiann/CosRent',
    inferred_desc: 'Platform web katalog dan manajemen reservasi persewaan kostum berbasis PHP dan MySQL.'
  },
  {
    id: 105,
    name: 'Tripz-bus',
    language: 'Blade',
    fork: false,
    html_url: 'https://github.com/Najiann/Tripz-bus',
    inferred_desc: 'Sistem pemesanan tiket perjalanan bus dan jadwal armada dengan pengelolaan kursi penumpang.'
  },
  {
    id: 106,
    name: 'portoo',
    language: 'Vue',
    fork: false,
    html_url: 'https://github.com/Najiann/portoo',
    inferred_desc: 'Aplikasi portofolio interaktif berbasis Vue 3 dengan visualisasi alur automasi n8n dan integrasi GitHub API.'
  },
  {
    id: 107,
    name: 'ukklat',
    language: 'PHP',
    fork: false,
    html_url: 'https://github.com/Najiann/ukklat',
    inferred_desc: 'Repositori latihan Uji Kompetensi Keahlian (UKK) mencakup integrasi database relasional dan otentikasi peran.'
  },
  {
    id: 108,
    name: 'lsplatihan',
    language: 'PHP',
    fork: false,
    html_url: 'https://github.com/Najiann/lsplatihan',
    inferred_desc: 'Implementasi standar kompetensi kejuruan Lembaga Sertifikasi Profesi (LSP) untuk web developer.'
  }
];

const DEFAULT_CERTIFICATES = [
  {
    id: 'cert-1',
    title: 'Machine Learning Cohort Graduate',
    issuer: 'Dicoding Indonesia x DBS Foundation',
    year: '2025',
    category: 'Machine Learning',
    statusType: 'physical',
    statusLabel: 'Sertifikat Fisik',
    statusClass: 'status-pending',
    description: 'Menyelesaikan kurikulum intensif machine learning, eksplorasi data dengan Python dan SQL, serta pembuatan model klasifikasi capstone.',
    verificationNote: 'Lulusan resmi program DBS Foundation Coding Camp 2025 (Track Machine Learning Engineer).',
    fileUrl: ''
  },
  {
    id: 'cert-2',
    title: 'Sertifikasi Kompetensi Kejuruan RPL',
    issuer: 'Lembaga Sertifikasi Profesi (LSP / BNSP)',
    year: '2025',
    category: 'Software Engineering',
    statusType: 'physical',
    statusLabel: 'Sertifikat Fisik',
    statusClass: 'status-pending',
    description: 'Uji kompetensi resmi pemrograman terstruktur, pembuatan antarmuka web, perancangan database relasional, dan version control Git.',
    verificationNote: 'Sertifikat kompetensi keahlian Rekayasa Perangkat Lunak tingkat SMK bidang Teknologi Informasi.',
    fileUrl: ''
  },
  {
    id: 'cert-3',
    title: 'Digital Support & Workflow Automation Completion',
    issuer: 'PT Mafi Global Asia',
    year: '2026',
    category: 'Workflow Automation',
    statusType: 'verified',
    statusLabel: 'Terverifikasi',
    statusClass: 'status-verified',
    description: 'Tuntas menyelesaikan program magang kerja dengan fokus pengembangan automasi n8n, CRM leads, sinkronisasi inventaris, dan optimasi WordPress.',
    verificationNote: 'Surat keterangan praktik industri periode 2025 sampai 2026 di PT Mafi Global Asia.',
    fileUrl: ''
  }
];

export default {
  name: 'App',
  data() {
    return {
      currentTheme: 'dark',
      isMobileMenuOpen: false,

      // Workflow Interactive Pipeline
      activeWorkflowIndex: 0,
      workflowSteps: [
        {
          id: 'step-webhook',
          role: '01. Trigger Event',
          name: 'Webhook Event Pesanan',
          type: 'Node: Webhook HTTP Post',
          description: 'Menerima data payload secara real-time dari formulir checkout website atau sistem kasir pelanggan.',
          inputSample: 'POST /webhook/order-created\n{\n  "order_id": "ORD-9421",\n  "customer_phone": "6281234567890",\n  "total_amount": 250000,\n  "status": "pending_payment"\n}',
          outputSample: '{\n  "status": "accepted",\n  "queued_at": "2026-10-08T23:30:00Z",\n  "event": "ORDER_PROCESSED"\n}',
          impact: 'Mencegah input manual transaksi dan merespons event pesanan dalam hitungan milidetik.'
        },
        {
          id: 'step-transform',
          role: '02. Transformasi',
          name: 'Pembersihan & Validasi JSON',
          type: 'Node: Code (JavaScript / JSON)',
          description: 'Memvalidasi format nomor WhatsApp, menghitung kalkulasi diskon, dan memastikan integritas data sebelum masuk database.',
          inputSample: 'function validatePayload(item) {\n  const phone = normalizePhone(item.phone);\n  return { valid: true, cleanPhone: phone };\n}',
          outputSample: '{\n  "is_valid": true,\n  "normalized_phone": "6281234567890",\n  "timestamp": 1728430200\n}',
          impact: 'Mengeliminasi kegagalan kirim pesan akibat format nomor yang tidak baku atau tidak valid.'
        },
        {
          id: 'step-crm',
          role: '03. Integrasi Data',
          name: 'Pembaruan CRM & Spreadsheet',
          type: 'Node: CRM / Database Sync',
          description: 'Mencatat data transaksi ke tabel CRM perusahaan dan memperbarui status inventaris secara terpusat.',
          inputSample: 'UPSERT INTO customers_orders\nSET status = "awaiting_payment"\nWHERE order_id = "ORD-9421";',
          outputSample: '{\n  "db_affected_rows": 1,\n  "crm_lead_updated": true,\n  "inventory_locked": true\n}',
          impact: 'Seluruh tim operasional dan penjualan memiliki data transaksi yang sinkron tanpa duplikasi manual.'
        },
        {
          id: 'step-broadcast',
          role: '04. Notifikasi',
          name: 'Broadcast WhatsApp Otomatis',
          type: 'Node: WhatsApp Gateway',
          description: 'Mengirimkan template pesan berisi rincian pesanan dan tautan pembayaran resmi ke WhatsApp pelanggan.',
          inputSample: 'SEND_TEMPLATE_MESSAGE {\n  "to": "6281234567890",\n  "template": "payment_instruction",\n  "order_id": "ORD-9421"\n}',
          outputSample: '{\n  "gateway_status": "DELIVERED",\n  "message_id": "wamid.HBgL...",\n  "delivery_time_ms": 340\n}',
          impact: 'Meningkatkan konversi pembayaran hingga 30% karena instruksi bayar dikirim langsung ke chat pembeli.'
        }
      ],

      // Skills Category Filter
      activeSkillCategory: 'all',
      skillCategories: [
        { id: 'all', label: 'Semua Keahlian' },
        { id: 'automation', label: 'Automasi & Integrasi' },
        { id: 'web', label: 'Pengembangan Web' },
        { id: 'data', label: 'Data & Machine Learning' }
      ],
      skillsList: [
        { name: 'n8n Workflow', category: 'automation', categoryLabel: 'Automasi', usage: 'Membangun pipeline automasi logika bisnis, webhook, dan integrasi multi-aplikasi.' },
        { name: 'WhatsApp Bot & Gateway', category: 'automation', categoryLabel: 'Automasi', usage: 'Implementasi broadcast, auto-responder, dan reminder tagihan otomatis.' },
        { name: 'REST API & Webhooks', category: 'automation', categoryLabel: 'Automasi', usage: 'Menghubungkan layanan pihak ketiga dan menyinkronkan data antar sistem.' },
        { name: 'PHP & CodeIgniter', category: 'web', categoryLabel: 'Pengembangan Web', usage: 'Pengembangan aplikasi web berbasis arsitektur MVC dan sistem database relasional.' },
        { name: 'Laravel (Blade)', category: 'web', categoryLabel: 'Pengembangan Web', usage: 'Perancangan web aplikasi terstruktur, manajemen inventaris, dan routing.' },
        { name: 'Vue.js 3', category: 'web', categoryLabel: 'Pengembangan Web', usage: 'Antarmuka pengguna interaktif, reaktif, dan performa tinggi.' },
        { name: 'HTML5 & CSS Modern', category: 'web', categoryLabel: 'Pengembangan Web', usage: 'Tata letak responsif murni, semantik rapi, dan kepatuhan kontras WCAG AA.' },
        { name: 'Git & GitHub', category: 'web', categoryLabel: 'Pengembangan Web', usage: 'Manajemen versi kode, branching, commit teratur, dan kolaborasi tim.' },
        { name: 'Python & Pandas', category: 'data', categoryLabel: 'Data & ML', usage: 'Manipulasi data tabular, pembersihan data mentah, dan analisis statistik.' },
        { name: 'Machine Learning', category: 'data', categoryLabel: 'Data & ML', usage: 'Pengembangan model prediksi supervised untuk proyek klasifikasi terarah.' },
        { name: 'SQL & MySQL', category: 'data', categoryLabel: 'Data & ML', usage: 'Perancangan skema relasional, query optimasi, dan integritas data transaksi.' },
        { name: 'WordPress & SEO', category: 'web', categoryLabel: 'Pengembangan Web', usage: 'Pengelolaan CMS, optimasi halaman, dan struktur ramah mesin pencari.' }
      ],

      // Certificates State (Admin Panel managed)
      isAdminAuthorized: false,
      isPinModalOpen: false,
      adminPinInput: '',
      pinErrorMsg: '',
      monogramClickCount: 0,
      monogramTimer: null,
      certificates: [],
      selectedCertificate: null,
      isAdminModalOpen: false,
      newCert: {
        title: '',
        issuer: '',
        year: '2026',
        category: 'Workflow Automation',
        statusType: 'physical',
        description: '',
        fileUrl: ''
      },

      // GitHub Projects State
      repos: [],
      repoLoading: true,
      repoError: null,
      activeRepoFilter: 'all',
      repoSearchQuery: '',
      repoFilters: [
        { id: 'all', label: 'Semua Proyek' },
        { id: 'web', label: 'Web & PHP' },
        { id: 'ml', label: 'Machine Learning' },
        { id: 'frontend', label: 'Vue & Frontend' }
      ],

      // Contact Form State
      contactForm: {
        name: '',
        email: '',
        topic: 'Rekrutmen Kerja (Full-time / Magang)',
        message: ''
      },
      formFeedback: null,
      copySuccess: false
    }
  },
  computed: {
    currentWorkflow() {
      return this.workflowSteps[this.activeWorkflowIndex] || this.workflowSteps[0]
    },
    filteredSkills() {
      if (this.activeSkillCategory === 'all') {
        return this.skillsList
      }
      return this.skillsList.filter(s => s.category === this.activeSkillCategory)
    },
    filteredRepos() {
      let list = this.repos

      // Apply category filter
      if (this.activeRepoFilter === 'web') {
        list = list.filter(r => {
          const lang = (r.language || '').toLowerCase()
          return lang.includes('php') || lang.includes('blade') || r.name.toLowerCase().includes('php')
        })
      } else if (this.activeRepoFilter === 'ml') {
        list = list.filter(r => {
          const lang = (r.language || '').toLowerCase()
          return lang.includes('python') || lang.includes('jupyter') || r.name.toLowerCase().includes('ml') || r.name.toLowerCase().includes('model')
        })
      } else if (this.activeRepoFilter === 'frontend') {
        list = list.filter(r => {
          const lang = (r.language || '').toLowerCase()
          return lang.includes('vue') || lang.includes('javascript') || lang.includes('html')
        })
      }

      // Apply search query
      if (this.repoSearchQuery.trim()) {
        const q = this.repoSearchQuery.toLowerCase()
        list = list.filter(r => {
          const title = (r.name || '').toLowerCase()
          const lang = (r.language || '').toLowerCase()
          const desc = this.getRepoDescription(r).toLowerCase()
          return title.includes(q) || lang.includes(q) || desc.includes(q)
        })
      }

      return list
    }
  },
  mounted() {
    this.initTheme()
    this.checkAdminAccess()
    this.loadCertificates()
    this.fetchRepositories()
    window.addEventListener('keydown', this.handleGlobalKeydown)
  },
  beforeUnmount() {
    window.removeEventListener('keydown', this.handleGlobalKeydown)
    if (this.monogramTimer) clearTimeout(this.monogramTimer)
  },
  methods: {
    // Secret Admin Gate
    checkAdminAccess() {
      // 1. Check URL query parameter (e.g. ?admin=jihan or ?admin=secret)
      const params = new URLSearchParams(window.location.search)
      const adminParam = params.get('admin') || params.get('secret')
      if (adminParam === 'jihan' || adminParam === 'jihan2026' || adminParam === 'secret') {
        this.isAdminAuthorized = true
        localStorage.setItem('jihan_admin_auth', 'true')
        const cleanPath = window.location.pathname + window.location.hash
        window.history.replaceState({}, document.title, cleanPath)
        return
      }

      // 2. Check persistent localStorage
      if (localStorage.getItem('jihan_admin_auth') === 'true') {
        this.isAdminAuthorized = true
      }
    },
    handleGlobalKeydown(e) {
      // Shortcut: Ctrl + Shift + A (or Cmd + Shift + A)
      if ((e.ctrlKey || e.metaKey) && e.shiftKey && (e.key === 'A' || e.key === 'a')) {
        e.preventDefault()
        this.isPinModalOpen = true
        this.pinErrorMsg = ''
      }
    },
    handleMonogramClick() {
      this.monogramClickCount++
      if (this.monogramTimer) clearTimeout(this.monogramTimer)
      this.monogramTimer = setTimeout(() => {
        this.monogramClickCount = 0
      }, 3000)

      // 5 clicks triggers secret PIN modal
      if (this.monogramClickCount >= 5) {
        this.monogramClickCount = 0
        this.isPinModalOpen = true
        this.pinErrorMsg = ''
      }
    },
    verifyAdminPin() {
      const pin = this.adminPinInput.trim()
      if (pin === 'jihan2026' || pin === 'admin2026' || pin === 'jihan') {
        this.isAdminAuthorized = true
        localStorage.setItem('jihan_admin_auth', 'true')
        this.isPinModalOpen = false
        this.adminPinInput = ''
        this.pinErrorMsg = ''
        this.openAdminModal()
      } else {
        this.pinErrorMsg = 'PIN salah. Akses ditolak.'
      }
    },
    closePinModal() {
      this.isPinModalOpen = false
      this.adminPinInput = ''
      this.pinErrorMsg = ''
    },
    logoutAdmin() {
      this.isAdminAuthorized = false
      localStorage.removeItem('jihan_admin_auth')
      this.closeAdminModal()
    },

    // Theme Switcher
    initTheme() {
      const saved = localStorage.getItem('jihan_portfolio_theme')
      if (saved === 'light' || saved === 'dark') {
        this.currentTheme = saved
      } else {
        this.currentTheme = 'dark'
      }
      document.documentElement.setAttribute('data-theme', this.currentTheme)
    },
    toggleTheme() {
      this.currentTheme = this.currentTheme === 'dark' ? 'light' : 'dark'
      document.documentElement.setAttribute('data-theme', this.currentTheme)
      localStorage.setItem('jihan_portfolio_theme', this.currentTheme)
    },

    // Certificate Formatting & Management
    getCleanStatusLabel(cert) {
      if (!cert) return 'Terverifikasi'
      const label = cert.statusLabel || ''
      if (label.includes('Digital') || cert.statusType === 'digital') return 'Berkas Digital'
      if (label.includes('Fisik') || cert.statusType === 'physical') return 'Sertifikat Fisik'
      if (label.includes('Magang') || label.includes('Verifikasi') || cert.statusType === 'verified') return 'Terverifikasi'
      // Strip any bracket characters
      const clean = label.replace(/[\[\]]/g, '').trim()
      return clean || 'Terverifikasi'
    },
    loadCertificates() {
      try {
        const stored = localStorage.getItem('jihan_portfolio_certificates')
        if (stored) {
          const parsed = JSON.parse(stored)
          if (Array.isArray(parsed) && parsed.length > 0) {
            // Automatically clean up any legacy bracket labels in stored user cache
            this.certificates = parsed.map(c => ({
              ...c,
              statusLabel: this.getCleanStatusLabel(c)
            }))
            return
          }
        }
      } catch (e) {
        console.warn('Gagal membaca sertifikat dari localStorage:', e)
      }
      this.certificates = [...DEFAULT_CERTIFICATES]
      this.saveCertificates()
    },
    saveCertificates() {
      try {
        localStorage.setItem('jihan_portfolio_certificates', JSON.stringify(this.certificates))
      } catch (e) {
        console.error('Gagal menyimpan sertifikat ke localStorage:', e)
      }
    },
    resetDefaultCertificates() {
      this.certificates = [...DEFAULT_CERTIFICATES]
      this.saveCertificates()
    },
    selectCertificate(cert) {
      this.selectedCertificate = cert
    },
    closeCertificateModal() {
      this.selectedCertificate = null
    },
    openAdminModal() {
      this.isAdminModalOpen = true
    },
    closeAdminModal() {
      this.isAdminModalOpen = false
    },
    addNewCertificate() {
      if (!this.newCert.title.trim() || !this.newCert.issuer.trim()) {
        return
      }

      let statusLabel = 'Sertifikat Fisik'
      let statusClass = 'status-pending'

      if (this.newCert.statusType === 'digital') {
        statusLabel = 'Berkas Digital'
        statusClass = 'status-digital'
      } else if (this.newCert.statusType === 'verified') {
        statusLabel = 'Terverifikasi'
        statusClass = 'status-verified'
      }

      const item = {
        id: 'cert-' + Date.now(),
        title: this.newCert.title.trim(),
        issuer: this.newCert.issuer.trim(),
        year: this.newCert.year.trim() || '2026',
        category: this.newCert.category,
        statusType: this.newCert.statusType,
        statusLabel: statusLabel,
        statusClass: statusClass,
        description: this.newCert.description.trim(),
        verificationNote: 'Diperbarui via Panel Admin Portofolio.',
        fileUrl: this.newCert.fileUrl.trim()
      }

      this.certificates.unshift(item)
      this.saveCertificates()

      // Reset Form
      this.newCert = {
        title: '',
        issuer: '',
        year: '2026',
        category: 'Workflow Automation',
        statusType: 'physical',
        description: '',
        fileUrl: ''
      }
    },
    deleteCertificate(id) {
      this.certificates = this.certificates.filter(c => c.id !== id)
      this.saveCertificates()
      if (this.selectedCertificate && this.selectedCertificate.id === id) {
        this.selectedCertificate = null
      }
    },

    // GitHub Repositories Fetching
    async fetchRepositories() {
      this.repoLoading = true
      this.repoError = null

      try {
        const response = await fetch('https://api.github.com/users/Najiann/repos?sort=updated&per_page=15')
        if (!response.ok) {
          throw new Error('Gagal mengambil data dari GitHub API (status: ' + response.status + ')')
        }

        const data = await response.json()
        if (Array.isArray(data) && data.length > 0) {
          const original = data.filter(repo => !repo.fork && repo.name !== 'Najiann')
          if (original.length > 0) {
            this.repos = original
          } else {
            this.repos = FALLBACK_REPOSITORIES
          }
        } else {
          this.repos = FALLBACK_REPOSITORIES
        }
      } catch (err) {
        console.warn('Menggunakan data repositori lokal terverifikasi:', err)
        this.repos = FALLBACK_REPOSITORIES
      } finally {
        this.repoLoading = false
      }
    },
    formatRepoTitle(name) {
      if (!name) return 'Repositori'
      return name
        .replace(/[-_]/g, ' ')
        .split(' ')
        .map(w => w.charAt(0).toUpperCase() + w.slice(1))
        .join(' ')
    },
    getRepoDescription(repo) {
      if (repo.description && repo.description.trim()) {
        return repo.description
      }
      const match = FALLBACK_REPOSITORIES.find(f => f.name.toLowerCase() === (repo.name || '').toLowerCase())
      if (match && match.inferred_desc) {
        return match.inferred_desc
      }
      return 'Repositori proyek berbasis ' + (repo.language || 'kode sumber') + ' terdaftar di profil GitHub @Najiann.'
    },
    clearRepoFilters() {
      this.activeRepoFilter = 'all'
      this.repoSearchQuery = ''
    },

    // Contact Form & Clipboard Action
    async copyEmail() {
      try {
        await navigator.clipboard.writeText('jihanaulia2408@gmail.com')
        this.copySuccess = true
        setTimeout(() => {
          this.copySuccess = false
        }, 2500)
      } catch (err) {
        this.copySuccess = false
      }
    },
    handleContactSubmit() {
      if (!this.contactForm.name.trim() || !this.contactForm.email.trim() || !this.contactForm.message.trim()) {
        this.formFeedback = {
          type: 'error',
          message: 'Mohon lengkapi semua kolom formulir sebelum mengirim pesan.'
        }
        return
      }

      const subject = encodeURIComponent('[Portofolio Inquiry] ' + this.contactForm.topic + ' - ' + this.contactForm.name)
      const body = encodeURIComponent(
        'Halo Jihan,\n\n' +
        'Nama Pengirim: ' + this.contactForm.name + '\n' +
        'Email Kontak: ' + this.contactForm.email + '\n' +
        'Kebutuhan: ' + this.contactForm.topic + '\n\n' +
        'Pesan:\n' + this.contactForm.message + '\n'
      )
      
      const mailtoUrl = `mailto:jihanaulia2408@gmail.com?subject=${subject}&body=${body}`
      window.open(mailtoUrl, '_blank')

      this.formFeedback = {
        type: 'success',
        message: 'Aplikasi email Anda dibuka dengan draf pesan otomatis. Siap dikirim ke jihanaulia2408@gmail.com!'
      }

      this.contactForm = {
        name: '',
        email: '',
        topic: 'Rekrutmen Kerja (Full-time / Magang)',
        message: ''
      }
    }
  }
}
</script>

<style scoped>
/* =========================================================================
   CLEAN & MODERN SCOPED STYLES: Jihan Aulia Portfolio
   ========================================================================= */

.portfolio-root {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  background-color: var(--bg-page);
  color: var(--text-primary);
}

/* Accessibility Skip Link */
.skip-link {
  position: absolute;
  top: -60px;
  left: 20px;
  background: var(--accent);
  color: #ffffff;
  padding: 8px 16px;
  font-weight: 600;
  border-radius: var(--radius-sm);
  z-index: 9999;
  transition: top 0.2s ease;
}
.skip-link:focus {
  top: 16px;
}

/* -------------------------------------------------------------------------
   HEADER & NAVIGATION
   ------------------------------------------------------------------------- */
.site-header {
  position: sticky;
  top: 0;
  z-index: 100;
  background-color: rgba(9, 13, 22, 0.85);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border-bottom: 1px solid var(--border-color);
  transition: background-color 0.25s ease, border-color 0.25s ease;
}

[data-theme="light"] .site-header {
  background-color: rgba(255, 255, 255, 0.9);
}

.header-inner {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0.9rem 1.5rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1.5rem;
}

.brand-link {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  text-decoration: none;
}

.brand-symbol {
  font-family: var(--font-mono);
  font-size: 0.9rem;
  font-weight: 700;
  color: var(--accent);
  background: var(--accent-soft);
  padding: 4px 8px;
  border-radius: var(--radius-sm);
  border: 1px solid var(--accent-border);
  transition: transform 0.15s ease, background-color 0.15s ease;
  user-select: none;
}
.brand-symbol:hover {
  transform: scale(1.05);
}

.brand-text {
  display: flex;
  flex-direction: column;
}

.brand-name {
  font-size: 1.05rem;
  font-weight: 700;
  letter-spacing: -0.02em;
  color: var(--text-primary);
  line-height: 1.2;
}

.brand-sub {
  font-size: 0.75rem;
  color: var(--text-muted);
  font-weight: 500;
}

.desktop-nav {
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

.nav-item {
  font-size: 0.9rem;
  font-weight: 500;
  color: var(--text-secondary);
  transition: color 0.15s ease;
  padding: 0.2rem 0;
  position: relative;
}
.nav-item:hover {
  color: var(--accent);
}

.header-actions {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.action-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.45rem 0.85rem;
  border-radius: var(--radius-sm);
  border: 1px solid var(--border-color);
  background: var(--bg-surface);
  color: var(--text-secondary);
  font-size: 0.82rem;
  font-weight: 600;
  transition: all 0.2s ease;
}
.action-btn:hover {
  color: var(--text-primary);
  border-color: var(--border-hover);
  background: var(--bg-surface-elevated);
}

.badge-count {
  background: var(--accent);
  color: #ffffff;
  font-size: 0.7rem;
  font-weight: 700;
  padding: 1px 6px;
  border-radius: var(--radius-full);
}

.mobile-menu-btn {
  display: none;
  flex-direction: column;
  justify-content: center;
  gap: 4px;
  width: 36px;
  height: 36px;
  padding: 6px;
  border-radius: var(--radius-sm);
  border: 1px solid var(--border-color);
  background: var(--bg-surface);
}

.hamburger-line {
  width: 100%;
  height: 2px;
  background-color: var(--text-primary);
  border-radius: 2px;
  transition: all 0.2s ease;
}

.mobile-nav {
  display: none;
  flex-direction: column;
  background: var(--bg-surface);
  border-bottom: 1px solid var(--border-color);
  padding: 1rem 1.5rem;
  gap: 0.75rem;
}

.mobile-nav-link {
  font-size: 0.95rem;
  font-weight: 600;
  color: var(--text-secondary);
  padding: 0.6rem 0;
  border-bottom: 1px solid var(--border-subtle);
  transition: color 0.15s ease;
}
.mobile-nav-link:hover {
  color: var(--accent);
}

/* -------------------------------------------------------------------------
   CONTENT WRAPPER & GLOBAL SECTION STYLES
   ------------------------------------------------------------------------- */
.content-wrapper {
  flex: 1;
  max-width: 1200px;
  margin: 0 auto;
  padding: 3rem 1.5rem 6rem 1.5rem;
  width: 100%;
}

.section {
  margin-bottom: 6rem;
}

.section-header {
  margin-bottom: 2.5rem;
}

.section-tag {
  display: inline-block;
  font-size: 0.8rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--accent);
  margin-bottom: 0.4rem;
}

.section-title {
  font-size: 2.15rem;
  font-weight: 800;
  letter-spacing: -0.03em;
  color: var(--text-primary);
  line-height: 1.25;
  margin-bottom: 0.75rem;
}

.section-lead {
  font-size: 1.05rem;
  color: var(--text-secondary);
  max-width: 720px;
  line-height: 1.65;
}

/* -------------------------------------------------------------------------
   BUTTON SYSTEM
   ------------------------------------------------------------------------- */
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  padding: 0.7rem 1.4rem;
  border-radius: var(--radius-sm);
  font-size: 0.92rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.18s ease;
  white-space: nowrap;
}

.btn-primary {
  background-color: var(--accent);
  color: #ffffff;
  border: 1px solid transparent;
  box-shadow: 0 1px 3px rgba(37, 99, 235, 0.3);
}
.btn-primary:hover {
  background-color: var(--accent-hover);
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(37, 99, 235, 0.4);
}

.btn-secondary {
  background-color: var(--bg-surface);
  color: var(--text-primary);
  border: 1px solid var(--border-color);
}
.btn-secondary:hover {
  background-color: var(--bg-surface-elevated);
  border-color: var(--border-hover);
  transform: translateY(-1px);
}

.btn-ghost {
  background-color: transparent;
  color: var(--text-secondary);
  border: 1px solid var(--border-color);
}
.btn-ghost:hover {
  color: var(--text-primary);
  border-color: var(--border-hover);
  background-color: var(--bg-surface);
}

.btn-sm {
  padding: 0.45rem 0.9rem;
  font-size: 0.84rem;
}

.btn-xs {
  padding: 0.3rem 0.65rem;
  font-size: 0.75rem;
}

.btn-block {
  width: 100%;
}

.btn-arrow {
  transition: transform 0.15s ease;
}
.btn:hover .btn-arrow {
  transform: translateX(3px);
}

/* -------------------------------------------------------------------------
   1. HERO SECTION
   ------------------------------------------------------------------------- */
.hero-section {
  padding-top: 1.5rem;
}

.hero-grid {
  display: grid;
  grid-template-columns: 1.25fr 1fr;
  gap: 3.5rem;
  align-items: center;
}

.availability-pill {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.35rem 0.85rem;
  border-radius: var(--radius-full);
  background: var(--accent-teal-soft);
  border: 1px solid var(--accent-teal-border);
  margin-bottom: 1.5rem;
}

.status-indicator-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background-color: var(--accent-teal);
  box-shadow: 0 0 8px var(--accent-teal);
}

.availability-text {
  font-size: 0.82rem;
  font-weight: 600;
  color: var(--accent-teal);
}

.hero-heading {
  font-size: 2.75rem;
  font-weight: 800;
  letter-spacing: -0.035em;
  line-height: 1.18;
  color: var(--text-primary);
  margin-bottom: 1.25rem;
}

.hero-description {
  font-size: 1.08rem;
  color: var(--text-secondary);
  line-height: 1.7;
  margin-bottom: 2rem;
}

.hero-description strong {
  color: var(--text-primary);
  font-weight: 600;
}

.hero-actions {
  display: flex;
  align-items: center;
  gap: 0.85rem;
  flex-wrap: wrap;
}

/* Authentic Developer Card (No tacky emojis or AI feel) */
.hero-dev-card {
  background: var(--bg-surface);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-lg);
  padding: 1.85rem;
  box-shadow: var(--shadow-md);
  position: relative;
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
}

.dev-card-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 1rem;
  padding-bottom: 1.15rem;
  border-bottom: 1px solid var(--border-subtle);
}

.dev-name {
  font-size: 1.25rem;
  font-weight: 800;
  color: var(--text-primary);
  line-height: 1.25;
  letter-spacing: -0.02em;
}

.dev-role {
  font-size: 0.84rem;
  color: var(--text-secondary);
  margin-top: 0.25rem;
}

.dev-status-tag {
  font-size: 0.74rem;
  font-weight: 700;
  color: var(--accent-teal);
  background: var(--accent-teal-soft);
  border: 1px solid var(--accent-teal-border);
  padding: 3px 8px;
  border-radius: var(--radius-full);
  white-space: nowrap;
}

.dev-summary-list {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.dev-summary-row {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  gap: 1rem;
  font-size: 0.88rem;
  padding: 0.35rem 0;
  border-bottom: 1px dashed var(--border-subtle);
}

.dev-summary-row:last-child {
  border-bottom: none;
}

.row-term {
  color: var(--text-muted);
  font-size: 0.82rem;
  font-weight: 600;
  flex-shrink: 0;
}

.row-detail {
  color: var(--text-primary);
  font-weight: 600;
  text-align: right;
  line-height: 1.4;
}

.dev-card-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.45rem;
  padding-top: 0.5rem;
  border-top: 1px solid var(--border-subtle);
}

.tech-pill {
  font-family: var(--font-mono);
  font-size: 0.75rem;
  font-weight: 600;
  color: var(--text-secondary);
  background: var(--bg-subtle);
  border: 1px solid var(--border-color);
  padding: 3px 8px;
  border-radius: var(--radius-sm);
  transition: all 0.15s ease;
}
.tech-pill:hover {
  color: var(--accent);
  border-color: var(--accent-border);
}

/* -------------------------------------------------------------------------
   2. WORKFLOW AUTOMATION PIPELINE
   ------------------------------------------------------------------------- */
.pipeline-container {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.step-navigator {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 0.85rem;
}

.step-nav-btn {
  background: var(--bg-surface);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-md);
  padding: 1.15rem 1rem;
  display: flex;
  align-items: flex-start;
  gap: 0.75rem;
  text-align: left;
  transition: all 0.2s ease;
  position: relative;
}
.step-nav-btn:hover {
  border-color: var(--border-hover);
  background: var(--bg-surface-elevated);
}

.step-nav-btn.active {
  border-color: var(--accent);
  background: var(--bg-surface-elevated);
  box-shadow: 0 0 0 1px var(--accent);
}

.step-index {
  font-family: var(--font-mono);
  font-size: 0.85rem;
  font-weight: 700;
  color: var(--accent);
  background: var(--accent-soft);
  padding: 2px 6px;
  border-radius: 4px;
}

.step-text {
  display: flex;
  flex-direction: column;
}

.step-role-label {
  font-size: 0.72rem;
  color: var(--text-muted);
  text-transform: uppercase;
  font-weight: 600;
  letter-spacing: 0.04em;
}

.step-name-label {
  font-size: 0.9rem;
  color: var(--text-primary);
  font-weight: 700;
  line-height: 1.3;
  margin-top: 0.15rem;
}

.pipeline-card {
  background: var(--bg-surface);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-lg);
  padding: 2rem;
  box-shadow: var(--shadow-sm);
}

.pipeline-card-top {
  margin-bottom: 1.75rem;
}

.pipeline-meta {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  margin-bottom: 0.5rem;
}

.node-type-pill {
  font-size: 0.75rem;
  font-family: var(--font-mono);
  font-weight: 600;
  color: var(--accent);
  background: var(--accent-soft);
  padding: 3px 8px;
  border-radius: var(--radius-sm);
}

.pipeline-active-title {
  font-size: 1.35rem;
  font-weight: 800;
  color: var(--text-primary);
  letter-spacing: -0.02em;
}

.pipeline-desc {
  font-size: 0.96rem;
  color: var(--text-secondary);
  line-height: 1.6;
}

.code-comparison-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.25rem;
  margin-bottom: 1.5rem;
}

.code-box {
  background: var(--bg-input);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-md);
  overflow: hidden;
}

.code-box-header {
  padding: 0.65rem 1rem;
  background: rgba(0, 0, 0, 0.15);
  border-bottom: 1px solid var(--border-color);
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.code-label {
  font-size: 0.78rem;
  font-weight: 700;
  color: var(--text-secondary);
}

.code-tag {
  font-family: var(--font-mono);
  font-size: 0.7rem;
  color: var(--text-muted);
  text-transform: uppercase;
}

.code-content {
  padding: 1rem;
  font-family: var(--font-mono);
  font-size: 0.8rem;
  line-height: 1.6;
  color: var(--text-secondary);
  overflow-x: auto;
}

.impact-callout {
  display: flex;
  align-items: flex-start;
  gap: 0.85rem;
  background: var(--accent-soft);
  border: 1px solid var(--accent-border);
  padding: 1rem 1.25rem;
  border-radius: var(--radius-md);
}

.impact-icon {
  font-size: 1.2rem;
  flex-shrink: 0;
}

.impact-content {
  font-size: 0.9rem;
  color: var(--text-primary);
  line-height: 1.5;
}

.impact-content strong {
  color: var(--accent);
  margin-right: 0.4rem;
}

/* -------------------------------------------------------------------------
   3. TIMELINE & EXPERIENCE
   ------------------------------------------------------------------------- */
.timeline-container {
  display: flex;
  flex-direction: column;
  position: relative;
  max-width: 860px;
}

.timeline-item {
  display: flex;
  gap: 1.5rem;
  position: relative;
}

.timeline-dot-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 20px;
  flex-shrink: 0;
  padding-top: 0.35rem;
}

.timeline-dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: var(--accent);
  border: 3px solid var(--bg-page);
  box-shadow: 0 0 0 2px var(--accent);
  z-index: 2;
}

.timeline-line {
  width: 2px;
  flex: 1;
  background-color: var(--border-color);
  margin-top: 0.5rem;
  margin-bottom: 0.5rem;
}

.timeline-card {
  flex: 1;
  background: var(--bg-surface);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-md);
  padding: 1.5rem;
  margin-bottom: 2rem;
  box-shadow: var(--shadow-sm);
}

.timeline-card-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 1rem;
  margin-bottom: 1rem;
}

.role-title {
  font-size: 1.15rem;
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 0.2rem;
}

.org-meta {
  font-size: 0.85rem;
  color: var(--text-secondary);
}

.badge-role {
  font-size: 0.74rem;
  font-weight: 700;
  padding: 3px 8px;
  border-radius: var(--radius-sm);
  white-space: nowrap;
}

.badge-work {
  background: var(--accent-teal-soft);
  color: var(--accent-teal);
  border: 1px solid var(--accent-teal-border);
}

.badge-study {
  background: var(--accent-soft);
  color: var(--accent);
  border: 1px solid var(--accent-border);
}

.badge-school {
  background: var(--accent-amber-soft);
  color: var(--accent-amber);
  border: 1px solid rgba(245, 158, 11, 0.3);
}

.achievement-list {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 0.65rem;
}

.achievement-list li {
  font-size: 0.9rem;
  color: var(--text-secondary);
  line-height: 1.6;
  position: relative;
  padding-left: 1.25rem;
}

.achievement-list li::before {
  content: "•";
  position: absolute;
  left: 0;
  color: var(--accent);
  font-size: 1.1rem;
  line-height: 1.3;
}

/* -------------------------------------------------------------------------
   4. SKILLS SECTION
   ------------------------------------------------------------------------- */
.filter-tab-bar {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  flex-wrap: wrap;
  margin-bottom: 2rem;
}

.tab-btn {
  padding: 0.45rem 1rem;
  border-radius: var(--radius-full);
  font-size: 0.85rem;
  font-weight: 600;
  border: 1px solid var(--border-color);
  background: var(--bg-surface);
  color: var(--text-secondary);
  transition: all 0.15s ease;
}
.tab-btn:hover {
  color: var(--text-primary);
  border-color: var(--border-hover);
}
.tab-btn.active {
  background: var(--accent);
  border-color: var(--accent);
  color: #ffffff;
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.25rem;
}

.skill-card {
  background: var(--bg-surface);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-md);
  padding: 1.35rem;
  transition: all 0.2s ease;
  box-shadow: var(--shadow-sm);
}
.skill-card:hover {
  border-color: var(--border-hover);
  transform: translateY(-2px);
  box-shadow: var(--shadow-md);
}

.skill-card-top {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 0.5rem;
  margin-bottom: 0.65rem;
}

.skill-name {
  font-size: 1rem;
  font-weight: 700;
  color: var(--text-primary);
}

.skill-category-tag {
  font-size: 0.72rem;
  font-weight: 600;
  color: var(--text-muted);
  background: var(--bg-subtle);
  padding: 2px 6px;
  border-radius: 4px;
}

.skill-usage {
  font-size: 0.85rem;
  color: var(--text-secondary);
  line-height: 1.5;
}

/* -------------------------------------------------------------------------
   5. CERTIFICATES SECTION
   ------------------------------------------------------------------------- */
.admin-notice-banner {
  background: var(--accent-amber-soft);
  border: 1px solid rgba(245, 158, 11, 0.3);
  padding: 0.85rem 1.25rem;
  border-radius: var(--radius-md);
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
  margin-bottom: 1.75rem;
}

.banner-text {
  font-size: 0.88rem;
  color: var(--text-primary);
}

.cert-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.35rem;
}

.cert-card {
  background: var(--bg-surface);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-md);
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
  cursor: pointer;
  transition: all 0.2s ease;
  box-shadow: var(--shadow-sm);
}
.cert-card:hover {
  border-color: var(--accent);
  transform: translateY(-2px);
  box-shadow: var(--shadow-md);
}

.cert-card-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 0.75rem;
  margin-bottom: 0.85rem;
}

.cert-meta-group {
  display: flex;
  flex-direction: column;
  gap: 0.15rem;
}

.cert-issuer {
  font-size: 0.82rem;
  font-weight: 700;
  color: var(--accent);
}

.cert-year {
  font-size: 0.76rem;
  color: var(--text-muted);
  font-family: var(--font-mono);
}

.cert-title {
  font-size: 1.05rem;
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 0.5rem;
  line-height: 1.35;
}

.cert-desc {
  font-size: 0.85rem;
  color: var(--text-secondary);
  line-height: 1.5;
  flex: 1;
  margin-bottom: 1.25rem;
}

.cert-card-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 0.75rem;
  padding-top: 1rem;
  border-top: 1px solid var(--border-subtle);
  margin-top: auto;
}

.cert-cat-pill {
  font-size: 0.72rem;
  color: var(--text-muted);
  font-weight: 500;
}

.status-badge {
  font-size: 0.74rem;
  font-weight: 600;
  padding: 3px 8px;
  border-radius: var(--radius-sm);
  white-space: nowrap;
  flex-shrink: 0;
}

.status-pending {
  background: var(--accent-amber-soft);
  color: var(--accent-amber);
  border: 1px solid rgba(245, 158, 11, 0.25);
}

.status-verified, .status-digital {
  background: var(--accent-teal-soft);
  color: var(--accent-teal);
  border: 1px solid var(--accent-teal-border);
}

.cert-link-text {
  font-size: 0.82rem;
  font-weight: 600;
  color: var(--accent);
  display: inline-flex;
  align-items: center;
  gap: 0.25rem;
  white-space: nowrap;
}

.arrow-glyph {
  transition: transform 0.15s ease;
}
.cert-card:hover .arrow-glyph {
  transform: translateX(3px);
}

/* -------------------------------------------------------------------------
   6. PROJECTS SECTION
   ------------------------------------------------------------------------- */
.projects-toolbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
  margin-bottom: 2rem;
  flex-wrap: wrap;
}

.search-wrapper {
  position: relative;
  width: 280px;
}

.search-icon {
  position: absolute;
  left: 0.75rem;
  top: 50%;
  transform: translateY(-50%);
  font-size: 0.85rem;
  color: var(--text-muted);
}

.search-input {
  width: 100%;
  padding: 0.5rem 0.85rem 0.5rem 2.2rem;
  border-radius: var(--radius-full);
  border: 1px solid var(--border-color);
  background: var(--bg-surface);
  color: var(--text-primary);
  font-size: 0.85rem;
  font-family: inherit;
  outline: none;
  transition: border-color 0.15s ease;
}
.search-input:focus {
  border-color: var(--accent);
}

.repos-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.35rem;
}

.repo-card {
  background: var(--bg-surface);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-md);
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
  transition: all 0.2s ease;
  box-shadow: var(--shadow-sm);
}
.repo-card:hover {
  border-color: var(--border-hover);
  transform: translateY(-2px);
  box-shadow: var(--shadow-md);
}

.repo-card-top {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 0.75rem;
}

.repo-lang-pill {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  font-size: 0.75rem;
  font-weight: 600;
  color: var(--text-secondary);
}

.lang-color-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background-color: var(--accent);
}
.lang-color-dot[data-lang*="PHP"], .lang-color-dot[data-lang*="Blade"] { background-color: #8b5cf6; }
.lang-color-dot[data-lang*="Python"] { background-color: #3b82f6; }
.lang-color-dot[data-lang*="Vue"] { background-color: #10b981; }

.repo-vis {
  font-size: 0.72rem;
  color: var(--text-muted);
}

.repo-title {
  font-size: 1.1rem;
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 0.5rem;
  line-height: 1.35;
}

.repo-desc {
  font-size: 0.86rem;
  color: var(--text-secondary);
  line-height: 1.55;
  flex: 1;
  margin-bottom: 1.35rem;
}

.repo-card-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding-top: 1rem;
  border-top: 1px solid var(--border-subtle);
}

.repo-slug {
  font-family: var(--font-mono);
  font-size: 0.75rem;
  color: var(--text-muted);
}

.btn-repo-link {
  display: inline-flex;
  align-items: center;
  gap: 0.3rem;
  font-size: 0.82rem;
  font-weight: 600;
  color: var(--accent);
  transition: transform 0.15s ease;
}
.btn-repo-link:hover {
  text-decoration: underline;
}

/* State Containers */
.state-container {
  background: var(--bg-surface);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-md);
  padding: 3rem;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}

.spinner-loader {
  width: 32px;
  height: 32px;
  border: 3px solid var(--border-color);
  border-top-color: var(--accent);
  border-radius: 50%;
  animation: spin 0.8s linear infinite;
}
@keyframes spin {
  to { transform: rotate(360deg); }
}

/* -------------------------------------------------------------------------
   7. CONTACT SECTION
   ------------------------------------------------------------------------- */
.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1.25fr;
  gap: 2.5rem;
}

.contact-info-card, .contact-form-card {
  background: var(--bg-surface);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-lg);
  padding: 2.25rem;
  box-shadow: var(--shadow-sm);
}

.card-inner-title {
  font-size: 1.25rem;
  font-weight: 800;
  color: var(--text-primary);
  margin-bottom: 0.65rem;
}

.contact-intro {
  font-size: 0.92rem;
  color: var(--text-secondary);
  line-height: 1.6;
  margin-bottom: 1.75rem;
}

.channel-items {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-bottom: 1.75rem;
}

.channel-card {
  display: flex;
  align-items: center;
  gap: 0.85rem;
  padding: 1rem;
  background: var(--bg-subtle);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-md);
}

.channel-icon {
  font-size: 1.25rem;
  flex-shrink: 0;
}

.channel-meta {
  flex: 1;
  display: flex;
  flex-direction: column;
}

.channel-label {
  font-size: 0.75rem;
  font-weight: 600;
  color: var(--text-muted);
  text-transform: uppercase;
}

.channel-value, .channel-link {
  font-size: 0.92rem;
  font-weight: 700;
  color: var(--text-primary);
}

.channel-link:hover {
  color: var(--accent);
}

.btn-copy {
  padding: 0.4rem 0.8rem;
  font-size: 0.8rem;
  font-weight: 600;
  border-radius: var(--radius-sm);
  border: 1px solid var(--border-color);
  background: var(--bg-surface);
  color: var(--text-secondary);
  transition: all 0.15s ease;
}
.btn-copy:hover {
  border-color: var(--accent);
  color: var(--accent);
}
.btn-copy.copied {
  background: var(--accent-teal);
  color: #ffffff;
  border-color: var(--accent-teal);
}

.guarantee-card {
  display: flex;
  align-items: flex-start;
  gap: 0.75rem;
  padding: 0.85rem 1rem;
  background: var(--bg-subtle);
  border-radius: var(--radius-md);
  border: 1px solid var(--border-subtle);
}

.guarantee-icon {
  font-size: 1.1rem;
}

.guarantee-text {
  font-size: 0.85rem;
  color: var(--text-secondary);
  line-height: 1.5;
}
.guarantee-text strong {
  color: var(--text-primary);
}

/* Form Controls */
.inquiry-form {
  display: flex;
  flex-direction: column;
  gap: 1.15rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
}

.form-group label {
  font-size: 0.84rem;
  font-weight: 600;
  color: var(--text-secondary);
}

.form-control {
  width: 100%;
  padding: 0.7rem 0.95rem;
  border-radius: var(--radius-sm);
  border: 1px solid var(--border-color);
  background: var(--bg-input);
  color: var(--text-primary);
  font-family: inherit;
  font-size: 0.9rem;
  outline: none;
  transition: border-color 0.15s ease, box-shadow 0.15s ease;
}
.form-control:focus {
  border-color: var(--accent);
  box-shadow: 0 0 0 2px var(--accent-soft);
}

.select-control {
  appearance: auto;
}

.feedback-alert {
  padding: 0.75rem 1rem;
  border-radius: var(--radius-sm);
  font-size: 0.85rem;
  line-height: 1.4;
}
.feedback-alert.success {
  background: var(--accent-teal-soft);
  color: var(--accent-teal);
  border: 1px solid var(--accent-teal-border);
}
.feedback-alert.error {
  background: var(--danger-soft);
  color: var(--danger);
  border: 1px solid var(--danger);
}

/* -------------------------------------------------------------------------
   FOOTER
   ------------------------------------------------------------------------- */
.site-footer {
  border-top: 1px solid var(--border-color);
  background-color: var(--bg-surface);
  padding: 2rem 1.5rem;
  margin-top: auto;
}

.footer-inner {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1.5rem;
}

.footer-brand {
  font-size: 0.88rem;
  color: var(--text-secondary);
  display: flex;
  align-items: center;
  gap: 0.5rem;
}
.footer-brand strong {
  color: var(--text-primary);
}
.footer-dot {
  color: var(--text-muted);
}

.footer-links {
  display: flex;
  align-items: center;
  gap: 1.25rem;
}

.footer-anchor {
  font-size: 0.85rem;
  color: var(--text-secondary);
  transition: color 0.15s ease;
}
.footer-anchor:hover {
  color: var(--accent);
}

.btn-link-clean {
  background: none;
  border: none;
  font-family: inherit;
  cursor: pointer;
  padding: 0;
}

/* -------------------------------------------------------------------------
   MODALS
   ------------------------------------------------------------------------- */
.modal-backdrop {
  position: fixed;
  inset: 0;
  background-color: rgba(0, 0, 0, 0.65);
  backdrop-filter: blur(4px);
  -webkit-backdrop-filter: blur(4px);
  z-index: 1000;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1.5rem;
}

.modal-box {
  background: var(--bg-surface);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-lg);
  width: 100%;
  max-width: 600px;
  box-shadow: var(--shadow-lg);
  overflow: hidden;
  max-height: 90vh;
  display: flex;
  flex-direction: column;
}

.modal-header {
  padding: 1.35rem 1.75rem;
  border-bottom: 1px solid var(--border-color);
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 1rem;
}

.modal-kicker {
  font-size: 0.75rem;
  font-weight: 700;
  text-transform: uppercase;
  color: var(--accent);
  letter-spacing: 0.05em;
}

.modal-title {
  font-size: 1.35rem;
  font-weight: 800;
  color: var(--text-primary);
  margin-top: 0.2rem;
  line-height: 1.3;
}

.modal-close-btn {
  font-size: 1.25rem;
  color: var(--text-muted);
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: var(--radius-sm);
  transition: all 0.15s ease;
}
.modal-close-btn:hover {
  background: var(--bg-subtle);
  color: var(--text-primary);
}

.modal-body {
  padding: 1.75rem;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
}

.modal-footer {
  padding: 1rem 1.75rem;
  border-top: 1px solid var(--border-color);
  background: var(--bg-subtle);
  display: flex;
  justify-content: flex-end;
  gap: 0.75rem;
}

.modal-specs {
  display: flex;
  flex-direction: column;
  gap: 0.65rem;
  background: var(--bg-subtle);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-md);
  padding: 1rem;
}

.spec-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 0.88rem;
}

.row-label {
  color: var(--text-muted);
}

.row-value {
  color: var(--text-primary);
}

.modal-note-box {
  background: var(--bg-subtle);
  border-radius: var(--radius-md);
  padding: 1.25rem;
  border-left: 3px solid var(--accent);
}

.note-heading {
  font-size: 0.95rem;
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 0.4rem;
}

.note-text {
  font-size: 0.88rem;
  color: var(--text-secondary);
  line-height: 1.6;
  margin-bottom: 0.4rem;
}

.note-subtext {
  font-size: 0.8rem;
  color: var(--text-muted);
}

.file-pending-box {
  background: var(--bg-subtle);
  padding: 1rem;
  border-radius: var(--radius-md);
  border: 1px dashed var(--border-color);
  text-align: center;
  font-size: 0.82rem;
  color: var(--text-muted);
}

.pending-tag {
  display: inline-block;
  font-weight: 700;
  color: var(--accent-amber);
  margin-bottom: 0.25rem;
}

/* Admin Modal Specifics */
.admin-modal-box {
  max-width: 800px;
}

.admin-lead-text {
  font-size: 0.9rem;
  color: var(--text-secondary);
}

.admin-card-section {
  background: var(--bg-subtle);
  border: 1px solid var(--border-color);
  border-radius: var(--radius-md);
  padding: 1.35rem;
}

.admin-section-title {
  font-size: 1.05rem;
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 1rem;
}

.form-grid-2 {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
}

.form-grid-3 {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 1rem;
}

.admin-submit-row {
  display: flex;
  justify-content: flex-end;
  margin-top: 0.5rem;
}

.table-heading-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 0.75rem;
}

.table-wrapper {
  overflow-x: auto;
}

.admin-table {
  width: 100%;
  border-collapse: collapse;
  font-size: 0.85rem;
}

.admin-table th, .admin-table td {
  padding: 0.65rem 0.75rem;
  text-align: left;
  border-bottom: 1px solid var(--border-color);
}

.admin-table th {
  color: var(--text-muted);
  font-weight: 600;
  text-transform: uppercase;
  font-size: 0.75rem;
}

.btn-delete {
  color: var(--danger);
  font-size: 0.8rem;
  font-weight: 600;
  cursor: pointer;
  padding: 2px 6px;
  border-radius: 4px;
}
.btn-delete:hover {
  background: var(--danger-soft);
}

.admin-footer-bar {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.btn-logout {
  color: var(--danger);
}

/* PIN Modal Specifics */
.pin-modal-box {
  max-width: 440px;
}

.pin-hint-text {
  font-size: 0.88rem;
  color: var(--text-secondary);
  line-height: 1.5;
}

.pin-actions {
  display: flex;
  justify-content: flex-end;
  gap: 0.75rem;
  margin-top: 1rem;
}

/* -------------------------------------------------------------------------
   RESPONSIVE BREAKPOINTS
   ------------------------------------------------------------------------- */
@media (max-width: 1024px) {
  .hero-grid {
    grid-template-columns: 1fr;
    gap: 2.5rem;
  }
  .skills-grid, .cert-grid, .repos-grid {
    grid-template-columns: repeat(2, 1fr);
  }
  .step-navigator {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .desktop-nav {
    display: none;
  }
  .mobile-menu-btn {
    display: flex;
  }
  .mobile-nav {
    display: flex;
  }
  .hero-heading {
    font-size: 2.15rem;
  }
  .code-comparison-grid {
    grid-template-columns: 1fr;
  }
  .skills-grid, .cert-grid, .repos-grid {
    grid-template-columns: 1fr;
  }
  .contact-grid {
    grid-template-columns: 1fr;
  }
  .form-grid-2, .form-grid-3 {
    grid-template-columns: 1fr;
  }
  .footer-inner {
    flex-direction: column;
    text-align: center;
  }
  .header-inner {
    padding: 0.75rem 1rem;
  }
  .content-wrapper {
    padding: 2rem 1rem 4rem 1rem;
  }
}
</style>
