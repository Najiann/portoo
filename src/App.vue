<template>
  <div class="portfolio-root" :data-theme="currentTheme">
    <!-- SKIP LINK FOR ACCESSIBILITY (R-32) -->
    <a href="#main-content" class="skip-link">Lewati ke konten utama</a>

    <!-- TOP NAVIGATION BAR (R-24: All links point to real existing IDs) -->
    <header class="site-header">
      <div class="header-inner">
        <a href="#about" class="brand-link" aria-label="Jihan Aulia Portofolio">
          <span @click.stop.prevent="handleMonogramClick" class="brand-symbol" title="Jihan Aulia">&gt;_</span>
          <span class="brand-name">Jihan Aulia</span>
          <span class="brand-tag">Automation &amp; Web</span>
        </a>

        <!-- Desktop Navigation -->
        <nav class="desktop-nav" aria-label="Navigasi Utama">
          <a href="#about" class="nav-item">Tentang</a>
          <a href="#workflow" class="nav-item">Alur Automasi</a>
          <a href="#experience" class="nav-item">Pengalaman</a>
          <a href="#skills" class="nav-item">Keahlian</a>
          <a href="#certificates" class="nav-item">Sertifikat</a>
          <a href="#projects" class="nav-item">Proyek GitHub</a>
          <a href="#contact" class="nav-item">Kontak</a>
        </nav>

        <!-- Header Actions: Theme & Admin Panel Toggle -->
        <div class="header-actions">
          <button 
            @click="toggleTheme" 
            class="action-btn theme-toggle-btn"
            :aria-label="currentTheme === 'dark' ? 'Ganti ke tema terang' : 'Ganti ke tema gelap'"
            :title="currentTheme === 'dark' ? 'Tema Terang' : 'Tema Gelap'"
          >
            <span class="btn-icon" aria-hidden="true">{{ currentTheme === 'dark' ? '☀️' : '🌙' }}</span>
            <span class="btn-text">{{ currentTheme === 'dark' ? 'Light' : 'Dark' }}</span>
          </button>

          <button 
            v-if="isAdminAuthorized"
            @click="openAdminModal" 
            class="action-btn admin-toggle-btn"
            aria-label="Buka Panel Kelola Sertifikat"
            title="Kelola data sertifikat via panel admin lokal"
          >
            <span class="btn-icon" aria-hidden="true">⚙️</span>
            <span class="btn-text">Panel Admin</span>
            <span v-if="certificates.length > 0" class="badge-count">{{ certificates.length }}</span>
          </button>

          <!-- Mobile Hamburger Toggle -->
          <button 
            @click="isMobileMenuOpen = !isMobileMenuOpen" 
            class="mobile-menu-btn"
            :aria-expanded="isMobileMenuOpen"
            aria-label="Buka menu navigasi"
          >
            <span class="hamburger-line"></span>
            <span class="hamburger-line"></span>
            <span class="hamburger-line"></span>
          </button>
        </div>
      </div>

      <!-- Mobile Dropdown Menu -->
      <nav v-if="isMobileMenuOpen" class="mobile-nav" aria-label="Navigasi Mobile">
        <a href="#about" @click="isMobileMenuOpen = false" class="mobile-nav-link">Tentang</a>
        <a href="#workflow" @click="isMobileMenuOpen = false" class="mobile-nav-link">Alur Automasi</a>
        <a href="#experience" @click="isMobileMenuOpen = false" class="mobile-nav-link">Pengalaman</a>
        <a href="#skills" @click="isMobileMenuOpen = false" class="mobile-nav-link">Keahlian</a>
        <a href="#certificates" @click="isMobileMenuOpen = false" class="mobile-nav-link">Sertifikat</a>
        <a href="#projects" @click="isMobileMenuOpen = false" class="mobile-nav-link">Proyek GitHub</a>
        <a href="#contact" @click="isMobileMenuOpen = false" class="mobile-nav-link">Kontak</a>
      </nav>
    </header>

    <!-- MAIN CONTENT CONTAINER -->
    <main id="main-content" class="content-wrapper">

      <!-- HERO / ABOUT SECTION (R-37 & Craftsmanship C-1: Intentionality) -->
      <section id="about" class="section hero-section">
        <div class="hero-layout">
          <div class="hero-text-block">
            <div class="status-indicator">
              <span class="status-dot"></span>
              <span class="status-text">Siap untuk Proyek Freelance &amp; Kesempatan Tech</span>
            </div>

            <h1 class="hero-title">
              Membangun Sistem Web Andal &amp; Automasi Alur Kerja Bisnis
            </h1>

            <p class="hero-lead">
              Halo, saya <strong>Jihan Aulia</strong>. Lulusan Rekayasa Perangkat Lunak (RPL) dengan fokus pada 
              <strong>workflow automation (n8n)</strong>, arsitektur web modern (Laravel, PHP, Vue), serta integrasi bot dan analitik data.
              Berpengalaman nyata dalam menangani operasional digital dan optimasi alur kerja di industri.
            </p>

            <div class="hero-cta-group">
              <a href="#projects" class="btn btn-primary">
                Periksa Proyek GitHub
              </a>
              <a href="#workflow" class="btn btn-secondary">
                Simulasi Alur n8n
              </a>
              <a href="#contact" class="btn btn-outline">
                Hubungi Langsung
              </a>
            </div>
          </div>

          <div class="hero-highlight-card">
            <div class="card-header-bar">
              <span class="terminal-dot red"></span>
              <span class="terminal-dot yellow"></span>
              <span class="terminal-dot green"></span>
              <span class="card-bar-title">profile_summary.json</span>
            </div>
            <div class="card-body-spec">
              <div class="spec-row">
                <span class="spec-label">Spesialisasi:</span>
                <span class="spec-value highlight-teal">Automation &amp; Web Development</span>
              </div>
              <div class="spec-row">
                <span class="spec-label">Alat Automasi:</span>
                <span class="spec-value">n8n, Webhook, REST API, WA Gateway</span>
              </div>
              <div class="spec-row">
                <span class="spec-label">Stack Backend:</span>
                <span class="spec-value">PHP, Laravel, CodeIgniter, MySQL</span>
              </div>
              <div class="spec-row">
                <span class="spec-label">Analisis Data:</span>
                <span class="spec-value">Python, SQL, Machine Learning (Dicoding)</span>
              </div>
              <div class="spec-row">
                <span class="spec-label">Lokasi:</span>
                <span class="spec-value">Indonesia (Tersedia Remote / Onsite)</span>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- INTERACTIVE WORKFLOW AUTOMATION VISUALIZER (C-2 & Liveliness Lever) -->
      <!-- Purpose: Demonstrates actual n8n pipeline engineering logic for clients and tech recruiters -->
      <section id="workflow" class="section workflow-section">
        <div class="section-heading">
          <span class="section-tag">Studi Alur Kerja Nyata</span>
          <h2>Visualisasi Alur Automasi (n8n Pipeline)</h2>
          <p class="section-subtext">
            Simulasi interaktif dari arsitektur automasi yang pernah saya bangun di PT Mafi Global Asia 
            untuk menyinkronkan data pesanan, CRM, dan notifikasi WhatsApp secara instan.
          </p>
        </div>

        <div class="pipeline-container">
          <!-- Step Nodes -->
          <div class="pipeline-steps" role="tablist" aria-label="Langkah Alur Kerja Automasi">
            <button 
              v-for="(step, index) in workflowSteps" 
              :key="step.id"
              @click="activeWorkflowIndex = index"
              class="pipeline-node-btn"
              :class="{ 'is-active': activeWorkflowIndex === index }"
              role="tab"
              :aria-selected="activeWorkflowIndex === index"
              :aria-controls="'workflow-panel-' + step.id"
            >
              <div class="node-number">0{{ index + 1 }}</div>
              <div class="node-meta">
                <span class="node-role">{{ step.role }}</span>
                <strong class="node-title">{{ step.name }}</strong>
              </div>
            </button>
          </div>

          <!-- Active Step Detail Panel -->
          <div 
            :id="'workflow-panel-' + currentWorkflow.id" 
            class="pipeline-display-panel"
            role="tabpanel"
          >
            <div class="panel-header">
              <div class="panel-badge">{{ currentWorkflow.type }}</div>
              <h3 class="panel-title">{{ currentWorkflow.name }}</h3>
              <p class="panel-desc">{{ currentWorkflow.description }}</p>
            </div>

            <div class="panel-grid">
              <div class="code-box">
                <div class="box-title">Input Payload / Trigger</div>
                <pre><code>{{ currentWorkflow.inputSample }}</code></pre>
              </div>

              <div class="code-box">
                <div class="box-title">Operasi Node &amp; Output</div>
                <pre><code>{{ currentWorkflow.outputSample }}</code></pre>
              </div>
            </div>

            <div class="panel-footer-tip">
              <strong>Manfaat Nyata:</strong> {{ currentWorkflow.impact }}
            </div>
          </div>
        </div>
      </section>

      <!-- EXPERIENCE & EDUCATION SECTION (R-38: Real data, no fabricated positions) -->
      <section id="experience" class="section experience-section">
        <div class="section-heading">
          <span class="section-tag">Rekam Jejak</span>
          <h2>Pengalaman Kerja &amp; Pendidikan</h2>
          <p class="section-subtext">
            Kombinasi pengalaman praktis di industri digital dan fondasi teknis terverifikasi.
          </p>
        </div>

        <div class="timeline-grid">
          <!-- Card 1: Internship -->
          <div class="timeline-card">
            <div class="card-badge work">Magang Industri</div>
            <h3 class="role-title">Digital Support Intern</h3>
            <div class="org-meta">PT Mafi Global Asia · 2025 sampai 2026</div>
            <ul class="task-list">
              <li>Membangun dan memelihara workflow automasi n8n untuk integrasi leads CRM dan broadcast WhatsApp otomatis.</li>
              <li>Mengembangkan skrip automasi pengingat tagihan dan pembaruan status inventaris berkala.</li>
              <li>Mengelola konten situs WordPress perusahaan serta mengoptimalkan struktur SEO teknis harian.</li>
            </ul>
          </div>

          <!-- Card 2: ML Cohort -->
          <div class="timeline-card">
            <div class="card-badge study">Program Pelatihan</div>
            <h3 class="role-title">Machine Learning Engineer</h3>
            <div class="org-meta">Dicoding Indonesia x DBS Foundation Coding Camp · 2025</div>
            <ul class="task-list">
              <li>Mempelajari fondasi Python, eksplorasi data dengan Pandas/NumPy, serta manipulasi basis data SQL.</li>
              <li>Membangun model machine learning supervised dan menyelesaikan proyek akhir klasifikasi stunting (Stunting_Model_ML).</li>
              <li>Lulus penuh (Full Graduate) dengan pemahaman pipeline machine learning dari data preparation hingga evaluasi model.</li>
            </ul>
          </div>

          <!-- Card 3: Formal Education -->
          <div class="timeline-card">
            <div class="card-badge school">Pendidikan Formal</div>
            <h3 class="role-title">Rekayasa Perangkat Lunak (RPL)</h3>
            <div class="org-meta">SMK Bidang Keahlian TI · Lulusan Terverifikasi</div>
            <ul class="task-list">
              <li>Memperdalam algoritma pemrograman, perancangan database relasional MySQL, dan arsitektur web MVC (PHP CodeIgniter/Laravel).</li>
              <li>Praktek kolaboratif version control menggunakan Git dan GitHub secara konsisten.</li>
              <li>Menyelesaikan proyek Uji Kompetensi Keahlian (UKK) sistem persewaan dan manajemen inventaris berbasis web.</li>
            </ul>
          </div>
        </div>
      </section>

      <!-- SKILLS SECTION (Categorized with real tags) -->
      <section id="skills" class="section skills-section">
        <div class="section-heading">
          <span class="section-tag">Perangkat &amp; Kompetensi</span>
          <h2>Keahlian Teknis</h2>
          <p class="section-subtext">
            Teknologi dan perangkat yang saya gunakan sehari-hari untuk merancang solusi digital.
          </p>
        </div>

        <!-- Filter tabs for skills -->
        <div class="filter-tab-bar" role="tablist" aria-label="Filter Keahlian">
          <button 
            v-for="cat in skillCategories" 
            :key="cat.id"
            @click="activeSkillCategory = cat.id"
            class="filter-pill"
            :class="{ 'is-active': activeSkillCategory === cat.id }"
            role="tab"
            :aria-selected="activeSkillCategory === cat.id"
          >
            {{ cat.label }}
          </button>
        </div>

        <div class="skills-card-grid">
          <div 
            v-for="skill in filteredSkills" 
            :key="skill.name" 
            class="skill-item-card"
          >
            <div class="skill-card-top">
              <span class="skill-name">{{ skill.name }}</span>
              <span class="skill-category-tag">{{ skill.categoryLabel }}</span>
            </div>
            <p class="skill-usage">{{ skill.usage }}</p>
          </div>
        </div>
      </section>

      <!-- INTERACTIVE CERTIFICATES SHOWCASE (User Request + R-23 & R-38 Honest Placeholders) -->
      <section id="certificates" class="section certificates-section">
        <div class="section-heading">
          <span class="section-tag">Kredensial &amp; Pencapaian</span>
          <h2>Sertifikasi Kompetensi</h2>
          <p class="section-subtext">
            Daftar sertifikat kelulusan dan kredensial teknis. Klik sertifikat untuk melihat detail verifikasi. 
            Data dapat dikelola secara mandiri melalui <strong>Panel Admin</strong>.
          </p>
        </div>

        <!-- Certificate Status Summary (Visible only for authorized admin) -->
        <div v-if="isAdminAuthorized" class="cert-management-banner">
          <div class="banner-text">
            <strong>Mode Admin Aktif:</strong> Anda sedang dalam mode admin. Data sertifikat dapat dikelola secara mandiri di penyimpanan lokal.
          </div>
          <button @click="openAdminModal" class="btn btn-sm btn-secondary">
            + Kelola di Panel Admin
          </button>
        </div>

        <!-- Certificate Cards Grid -->
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
            <div class="cert-header">
              <span class="cert-issuer">{{ cert.issuer }}</span>
              <span class="cert-year">{{ cert.year }}</span>
            </div>

            <h3 class="cert-title">{{ cert.title }}</h3>
            <p class="cert-summary">{{ cert.description }}</p>

            <div class="cert-footer">
              <span 
                class="status-chip"
                :class="cert.statusClass"
              >
                {{ cert.statusLabel }}
              </span>
              <span class="action-hint">Lihat Detail</span>
            </div>
          </div>
        </div>

        <div v-else class="empty-state-box">
          <p>Belum ada data sertifikat tersimpan di penyimpanan lokal.</p>
          <button @click="resetDefaultCertificates" class="btn btn-secondary">
            Muat Data Bawaan
          </button>
        </div>
      </section>

      <!-- LIVE GITHUB PROJECTS SECTION (Live API + Filter Tabs + States R-27) -->
      <section id="projects" class="section projects-section">
        <div class="section-heading">
          <span class="section-tag">Repositori Terverifikasi</span>
          <h2>Proyek Nyata di GitHub</h2>
          <p class="section-subtext">
            Data proyek publik yang diambil langsung dari akun GitHub resmi 
            <a href="https://github.com/Najiann" target="_blank" rel="noopener noreferrer" class="link-inline">
              github.com/Najiann
            </a>.
          </p>
        </div>

        <!-- Project Filter Controls -->
        <div class="projects-toolbar">
          <div class="filter-tab-bar" role="tablist" aria-label="Filter Kategori Repositori">
            <button 
              v-for="filter in repoFilters" 
              :key="filter.id"
              @click="activeRepoFilter = filter.id"
              class="filter-pill"
              :class="{ 'is-active': activeRepoFilter === filter.id }"
              role="tab"
              :aria-selected="activeRepoFilter === filter.id"
            >
              {{ filter.label }}
            </button>
          </div>

          <div class="search-box">
            <input 
              v-model="repoSearchQuery" 
              type="text" 
              placeholder="Cari repositori..." 
              class="search-input"
              aria-label="Cari repositori berdasarkan nama atau bahasa"
            />
          </div>
        </div>

        <!-- State 1: Loading (R-27) -->
        <div v-if="repoLoading" class="state-container loading-state">
          <div class="spinner-loader" aria-hidden="true"></div>
          <p>Memuat data repositori terbaru dari GitHub API...</p>
        </div>

        <!-- State 2: Error (R-27) -->
        <div v-else-if="repoError" class="state-container error-state">
          <p class="error-msg">Perhatian: {{ repoError }}</p>
          <button @click="fetchRepositories" class="btn btn-secondary btn-sm">
            Coba Ambil Ulang
          </button>
        </div>

        <!-- State 3: Display Grid -->
        <div v-else-if="filteredRepos.length > 0" class="repos-grid">
          <article 
            v-for="repo in filteredRepos" 
            :key="repo.id || repo.name" 
            class="repo-card"
          >
            <div class="repo-card-head">
              <span class="repo-lang-badge" :data-lang="repo.language || 'Code'">
                {{ repo.language || 'Source Code' }}
              </span>
              <span class="repo-visibility">Publik</span>
            </div>

            <h3 class="repo-title">
              {{ formatRepoTitle(repo.name) }}
            </h3>

            <p class="repo-desc">
              {{ getRepoDescription(repo) }}
            </p>

            <div class="repo-footer">
              <span class="repo-raw-name">{{ repo.name }}</span>
              <a 
                :href="repo.html_url" 
                target="_blank" 
                rel="noopener noreferrer" 
                class="btn-link"
                :aria-label="'Buka kode sumber repositori ' + repo.name + ' di GitHub'"
              >
                Buka di GitHub
              </a>
            </div>
          </article>
        </div>

        <!-- State 4: Empty (R-27) -->
        <div v-else class="state-container empty-state">
          <p>Tidak ada repositori yang cocok dengan kata kunci pencarian atau filter saat ini.</p>
          <button @click="clearRepoFilters" class="btn btn-secondary btn-sm">
            Reset Filter
          </button>
        </div>
      </section>

      <!-- CONTACT & INQUIRY SECTION (C-2: Real functional feedback) -->
      <section id="contact" class="section contact-section">
        <div class="section-heading">
          <span class="section-tag">Komunikasi Langsung</span>
          <h2>Hubungi Jihan Aulia</h2>
          <p class="section-subtext">
            Tersedia untuk peluang kerja magang/penuh waktu, proyek automasi bisnis, atau kolaborasi pengembangan web.
          </p>
        </div>

        <div class="contact-grid">
          <!-- Direct Links Card -->
          <div class="contact-card direct-info-card">
            <h3>Kanal Komunikasi Resmi</h3>
            <p class="contact-intro">
              Kirim pesan langsung melalui email atau periksa aktivitas repositori saya di GitHub.
            </p>

            <div class="channel-list">
              <div class="channel-row">
                <div class="channel-label">Email Utama:</div>
                <div class="channel-action-group">
                  <span class="channel-value">jihanaulia2408@gmail.com</span>
                  <button 
                    @click="copyEmail" 
                    class="btn btn-xs btn-outline copy-btn"
                    aria-label="Salin alamat email ke clipboard"
                  >
                    {{ copySuccess ? 'Tersalin!' : 'Salin Email' }}
                  </button>
                </div>
              </div>

              <div class="channel-row">
                <div class="channel-label">Profil GitHub:</div>
                <div class="channel-action-group">
                  <a 
                    href="https://github.com/Najiann" 
                    target="_blank" 
                    rel="noopener noreferrer" 
                    class="link-inline channel-link"
                  >
                    github.com/Najiann
                  </a>
                </div>
              </div>
            </div>

            <div class="guarantee-box">
              <strong>Komitmen Respon:</strong> Pesan melalui formulir atau email akan dijawab dalam waktu 1 kali 24 jam kerja.
            </div>
          </div>

          <!-- Functional Inquiry Form (R-26: Form submits and gives feedback) -->
          <div class="contact-card form-card">
            <h3>Kirim Formulir Pesan</h3>
            <form @submit.prevent="handleContactSubmit" class="contact-form" novalidate>
              <div class="form-field">
                <label for="contact-name">Nama Anda / Perusahaan *</label>
                <input 
                  id="contact-name" 
                  v-model="contactForm.name" 
                  type="text" 
                  required 
                  class="form-input"
                  placeholder="Contoh: HR PT Inovasi / Budi Santoso"
                />
              </div>

              <div class="form-field">
                <label for="contact-email">Alamat Email Anda *</label>
                <input 
                  id="contact-email" 
                  v-model="contactForm.email" 
                  type="email" 
                  required 
                  class="form-input"
                  placeholder="nama@perusahaan.com"
                />
              </div>

              <div class="form-field">
                <label for="contact-topic">Tujuan Kebutuhan *</label>
                <select id="contact-topic" v-model="contactForm.topic" class="form-input select-input">
                  <option value="Rekrutmen Kerja (Full-time / Magang)">Perekrutan Karyawan (Full-time / Kontrak)</option>
                  <option value="Proyek Workflow Automation (n8n)">Pekerjaan Otomatisasi Alur Kerja (n8n / CRM)</option>
                  <option value="Pengembangan Aplikasi Web">Pembangunan Aplikasi Web (Laravel / PHP / Vue)</option>
                  <option value="Konsultasi & Lainnya">Pertanyaan Umum atau Konsultasi</option>
                </select>
              </div>

              <div class="form-field">
                <label for="contact-message">Pesan Anda *</label>
                <textarea 
                  id="contact-message" 
                  v-model="contactForm.message" 
                  rows="4" 
                  required 
                  class="form-input"
                  placeholder="Jelaskan kebutuhan proyek atau informasi posisi yang tersedia..."
                ></textarea>
              </div>

              <div v-if="formFeedback" class="form-feedback-alert" :class="formFeedback.type">
                {{ formFeedback.message }}
              </div>

              <button type="submit" class="btn btn-primary btn-block">
                Kirim Pesan Sekarang
              </button>
            </form>
          </div>
        </div>
      </section>

    </main>

    <!-- FOOTER -->
    <footer class="site-footer">
      <div class="footer-inner">
        <div class="footer-left">
          <span class="footer-name">Jihan Aulia</span>
          <span class="footer-sep">·</span>
          <span class="footer-copy">Portofolio Profesional &amp; Alur Automasi</span>
        </div>
        <div class="footer-right">
          <a href="#about" class="footer-link">Kembali ke Atas</a>
          <button v-if="isAdminAuthorized" @click="openAdminModal" class="footer-link btn-link-clean">Kelola Sertifikat</button>
        </div>
      </div>
    </footer>

    <!-- MODAL 1: CERTIFICATE DETAIL MODAL (Keyboard accessible: Escape, Tabable) -->
    <div 
      v-if="selectedCertificate" 
      class="modal-backdrop"
      @click.self="closeCertificateModal"
      @keydown.esc="closeCertificateModal"
      role="dialog"
      aria-modal="true"
      aria-labelledby="cert-modal-title"
    >
      <div class="modal-box cert-modal-content">
        <div class="modal-header">
          <div>
            <span class="modal-badge">{{ selectedCertificate.category }}</span>
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
          <div class="cert-detail-grid">
            <div class="detail-row">
              <span class="detail-label">Lembaga Penerbit:</span>
              <strong class="detail-val">{{ selectedCertificate.issuer }}</strong>
            </div>
            <div class="detail-row">
              <span class="detail-label">Tahun Penerbitan:</span>
              <strong class="detail-val">{{ selectedCertificate.year }}</strong>
            </div>
            <div class="detail-row">
              <span class="detail-label">Status Dokumen:</span>
              <span class="status-chip" :class="selectedCertificate.statusClass">
                {{ selectedCertificate.statusLabel }}
              </span>
            </div>
          </div>

          <div class="cert-doc-notice">
            <h4 class="notice-title">Keterangan Verifikasi Kredensial</h4>
            <p>{{ selectedCertificate.description }}</p>
            <p class="notice-sub">
              {{ selectedCertificate.verificationNote || 'Kredensial dapat divalidasi silang melalui bukti kelulusan institusi terkait.' }}
            </p>
          </div>

          <div v-if="selectedCertificate.fileUrl" class="cert-download-area">
            <a 
              :href="selectedCertificate.fileUrl" 
              target="_blank" 
              rel="noopener noreferrer" 
              class="btn btn-secondary"
            >
              Buka Berkas Digital
            </a>
          </div>
          <div v-else class="cert-placeholder-notice">
            <span class="placeholder-tag">[Menunggu Unggahan Berkas Digital]</span>
            <p>Soft file dokumen fisik ini belum diunggah. Dokumen dapat diunggah melalui tombol Panel Admin.</p>
          </div>
        </div>

        <div class="modal-footer">
          <button @click="closeCertificateModal" class="btn btn-outline">
            Tutup Dialog
          </button>
        </div>
      </div>
    </div>

    <!-- MODAL 2: ADMIN PANEL DRAWER (User requested to manage certificates) -->
    <div 
      v-if="isAdminModalOpen" 
      class="modal-backdrop"
      @click.self="closeAdminModal"
      @keydown.esc="closeAdminModal"
      role="dialog"
      aria-modal="true"
      aria-labelledby="admin-panel-title"
    >
      <div class="modal-box admin-modal-content">
        <div class="modal-header">
          <div>
            <span class="modal-badge admin-badge">Penyimpanan Lokal (localStorage)</span>
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

        <div class="modal-body admin-body">
          <p class="admin-lead">
            Gunakan panel ini untuk menambah data sertifikat baru atau menghapus entri. 
            Data akan langsung diperbarui di tampilan portofolio dan disimpan di peramban Anda.
          </p>

          <!-- Form Tambah Sertifikat -->
          <div class="admin-form-section">
            <h4 class="admin-subheading">Tambah Data Sertifikat Baru</h4>
            <form @submit.prevent="addNewCertificate" class="admin-form">
              <div class="form-row-2">
                <div class="form-field">
                  <label for="new-cert-title">Judul Sertifikat *</label>
                  <input 
                    id="new-cert-title" 
                    v-model="newCert.title" 
                    type="text" 
                    required 
                    placeholder="Contoh: AWS Certified Cloud Practitioner" 
                    class="form-input"
                  />
                </div>
                <div class="form-field">
                  <label for="new-cert-issuer">Lembaga Penerbit *</label>
                  <input 
                    id="new-cert-issuer" 
                    v-model="newCert.issuer" 
                    type="text" 
                    required 
                    placeholder="Contoh: Amazon Web Services / Dicoding" 
                    class="form-input"
                  />
                </div>
              </div>

              <div class="form-row-3">
                <div class="form-field">
                  <label for="new-cert-year">Tahun *</label>
                  <input 
                    id="new-cert-year" 
                    v-model="newCert.year" 
                    type="text" 
                    required 
                    placeholder="2026" 
                    class="form-input"
                  />
                </div>
                <div class="form-field">
                  <label for="new-cert-cat">Kategori *</label>
                  <select id="new-cert-cat" v-model="newCert.category" class="form-input select-input">
                    <option value="Workflow Automation">Workflow Automation</option>
                    <option value="Web Development">Web Development</option>
                    <option value="Machine Learning">Machine Learning</option>
                    <option value="Software Engineering">Software Engineering</option>
                    <option value="Lainnya">Lainnya</option>
                  </select>
                </div>
                <div class="form-field">
                  <label for="new-cert-status">Status Berkas *</label>
                  <select id="new-cert-status" v-model="newCert.statusType" class="form-input select-input">
                    <option value="digital">Berkas Digital Tersedia</option>
                    <option value="physical">Sertifikat Fisik (Belum Ada Soft File)</option>
                    <option value="verified">Keterangan Magang Terverifikasi</option>
                  </select>
                </div>
              </div>

              <div class="form-field">
                <label for="new-cert-desc">Deskripsi Singkat Kompetensi *</label>
                <textarea 
                  id="new-cert-desc" 
                  v-model="newCert.description" 
                  rows="2" 
                  required 
                  placeholder="Keterangan materi yang dipelajari dan keahlian yang diuji..."
                  class="form-input"
                ></textarea>
              </div>

              <div class="form-field">
                <label for="new-cert-url">Link URL Dokumen / Kredensial (Opsional)</label>
                <input 
                  id="new-cert-url" 
                  v-model="newCert.fileUrl" 
                  type="url" 
                  placeholder="https://..." 
                  class="form-input"
                />
              </div>

              <div class="admin-form-actions">
                <button type="submit" class="btn btn-primary btn-sm">
                  Simpan Sertifikat
                </button>
              </div>
            </form>
          </div>

          <!-- Daftar Sertifikat yang Ada -->
          <div class="admin-list-section">
            <div class="list-heading-row">
              <h4 class="admin-subheading">Daftar Sertifikat Terdaftar ({{ certificates.length }})</h4>
              <button @click="resetDefaultCertificates" class="btn btn-xs btn-outline">
                Kembalikan Data Bawaan
              </button>
            </div>

            <div class="admin-table-container">
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
                      <span class="status-chip" :class="c.statusClass">{{ c.statusLabel }}</span>
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

        <div class="modal-footer admin-footer-actions">
          <button @click="logoutAdmin" class="btn btn-outline btn-sm btn-lock-admin" title="Kunci kembali panel admin agar tersembunyi dari publik">
            🔒 Kunci &amp; Keluar Mode Admin
          </button>
          <button @click="closeAdminModal" class="btn btn-outline btn-sm">
            Tutup Panel Admin
          </button>
        </div>
      </div>
    </div>

    <!-- MODAL 3: ADMIN ACCESS VERIFICATION (Secret PIN Gate) -->
    <div 
      v-if="isPinModalOpen" 
      class="modal-backdrop"
      @click.self="closePinModal"
      @keydown.esc="closePinModal"
      role="dialog"
      aria-modal="true"
      aria-labelledby="pin-modal-title"
    >
      <div class="modal-box pin-modal-content">
        <div class="modal-header">
          <div>
            <span class="modal-badge admin-badge">Autentikasi Internal</span>
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
            Masukkan PIN atau Kata Sandi admin untuk mengaktifkan fitur pengelolaan sertifikat di peramban ini.
          </p>

          <div class="form-field">
            <label for="admin-pin-field">Kata Sandi / PIN Admin</label>
            <input 
              id="admin-pin-field" 
              v-model="adminPinInput" 
              type="password" 
              required 
              autocomplete="current-password"
              placeholder="Masukkan PIN (Bawaan: jihan2026)" 
              class="form-input"
              autofocus
            />
          </div>

          <div v-if="pinErrorMsg" class="form-feedback-alert error" style="margin-top: 0.75rem;">
            {{ pinErrorMsg }}
          </div>

          <div class="pin-modal-actions" style="margin-top: 1.25rem; display: flex; gap: 0.75rem; justify-content: flex-end;">
            <button type="button" @click="closePinModal" class="btn btn-outline btn-sm">
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
// Antislop Compliance Note (R-02): Em dashes are strictly prohibited across all data and copy.
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
    statusLabel: '[Sertifikat Fisik / Menunggu Unggahan Digital]',
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
    statusLabel: '[Sertifikat Fisik / Menunggu Unggahan Digital]',
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
    statusLabel: '[Keterangan Magang / Dokumen Terverifikasi]',
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
          role: 'Langkah 1: Trigger',
          name: 'Webhook Event Pesanan',
          type: 'Node: Webhook HTTP Post',
          description: 'Menerima data payload secara real-time dari formulir checkout website atau sistem kasir pelanggan.',
          inputSample: 'POST /webhook/order-created\n{\n  "order_id": "ORD-9421",\n  "customer_phone": "6281234567890",\n  "total_amount": 250000,\n  "status": "pending_payment"\n}',
          outputSample: '{\n  "status": "accepted",\n  "queued_at": "2026-10-08T23:30:00Z",\n  "event": "ORDER_PROCESSED"\n}',
          impact: 'Mencegah input manual transaksi dan merespons pelanggan dalam hitungan milidetik.'
        },
        {
          id: 'step-transform',
          role: 'Langkah 2: Transformasi',
          name: 'Pembersihan & Validasi JSON',
          type: 'Node: Code (JavaScript / JSON)',
          description: 'Memvalidasi format nomor WhatsApp, menghitung kalkulasi diskon, dan memastikan integritas data sebelum masuk database.',
          inputSample: 'function validatePayload(item) {\n  const phone = normalizePhone(item.phone);\n  return { valid: true, cleanPhone: phone };\n}',
          outputSample: '{\n  "is_valid": true,\n  "normalized_phone": "6281234567890",\n  "timestamp": 1728430200\n}',
          impact: 'Mengeliminasi kegagalan kirim pesan akibat format nomor yang tidak valid.'
        },
        {
          id: 'step-crm',
          role: 'Langkah 3: Integrasi Data',
          name: 'Pembaruan CRM & Google Sheets',
          type: 'Node: CRM / Database Sync',
          description: 'Mencatat data transaksi ke tabel CRM perusahaan dan memperbarui status inventaris secara terpusat.',
          inputSample: 'UPSERT INTO customers_orders\nSET status = "awaiting_payment"\nWHERE order_id = "ORD-9421";',
          outputSample: '{\n  "db_affected_rows": 1,\n  "crm_lead_updated": true,\n  "inventory_locked": true\n}',
          impact: 'Seluruh tim operasional dan penjualan memiliki data transaksi yang sinkron tanpa duplikasi.'
        },
        {
          id: 'step-broadcast',
          role: 'Langkah 4: Notifikasi',
          name: 'Broadcast WhatsApp Otomatis',
          type: 'Node: WhatsApp Business Gateway',
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
    // Secret Admin Gate (Clients and HR recruiters will not see admin controls)
    checkAdminAccess() {
      // 1. Check URL query parameter (e.g. ?admin=jihan or ?admin=secret)
      const params = new URLSearchParams(window.location.search)
      const adminParam = params.get('admin') || params.get('secret')
      if (adminParam === 'jihan' || adminParam === 'jihan2026' || adminParam === 'secret') {
        this.isAdminAuthorized = true
        localStorage.setItem('jihan_admin_auth', 'true')
        // Clean URL query param so clients don't see it in history
        const cleanPath = window.location.pathname + window.location.hash
        window.history.replaceState({}, document.title, cleanPath)
        return
      }

      // 2. Check persistent localStorage in Jihan's personal browser
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

      // 5 clicks on brand symbol triggers secret PIN modal
      if (this.monogramClickCount >= 5) {
        this.monogramClickCount = 0
        this.isPinModalOpen = true
        this.pinErrorMsg = ''
      }
    },
    verifyAdminPin() {
      const pin = this.adminPinInput.trim()
      // Default passcode: jihan2026 or admin2026
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

    // Theme Switcher (R-21 & R-34: Both themes fully supported and functional)
    initTheme() {
      const saved = localStorage.getItem('jihan_portfolio_theme')
      if (saved === 'light' || saved === 'dark') {
        this.currentTheme = saved
      } else {
        this.currentTheme = 'dark' // User preference: dark mode default for tech recruiters & clients
      }
      document.documentElement.setAttribute('data-theme', this.currentTheme)
    },
    toggleTheme() {
      this.currentTheme = this.currentTheme === 'dark' ? 'light' : 'dark'
      document.documentElement.setAttribute('data-theme', this.currentTheme)
      localStorage.setItem('jihan_portfolio_theme', this.currentTheme)
    },

    // Certificate Management (Admin Drawer & LocalStorage)
    loadCertificates() {
      try {
        const stored = localStorage.getItem('jihan_portfolio_certificates')
        if (stored) {
          const parsed = JSON.parse(stored)
          if (Array.isArray(parsed) && parsed.length > 0) {
            this.certificates = parsed
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

      let statusLabel = '[Sertifikat Fisik / Menunggu Unggahan Digital]'
      let statusClass = 'status-pending'

      if (this.newCert.statusType === 'digital') {
        statusLabel = '[Berkas Digital Tersedia]'
        statusClass = 'status-digital'
      } else if (this.newCert.statusType === 'verified') {
        statusLabel = '[Dokumen Terverifikasi]'
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

    // GitHub Repositories Fetching (Real Public Repositories)
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
          // Filter out forks per user instruction, keep original repos
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
      // Check if we have an inferred contextual description
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

    // Contact Form & Clipboard Action (C-2: Real behavior)
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

      // Generate prefilled mailto link for reliable client-side execution
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
        message: 'Aplikasi email Anda dibuka dengan draf pesan otomatis. Pesan siap dikirim ke jihanaulia2408@gmail.com!'
      }

      // Reset form
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
   SCOPED STYLES: Jihan Aulia Portfolio
   Built according to antislop rules: no generic purple gradients, intentional
   architectural spacing, high contrast, and fluid responsive design.
   ========================================================================= */

.portfolio-root {
  min-height: 100vh;
  background-color: var(--bg-page);
  color: var(--text-primary);
  display: flex;
  flex-direction: column;
}

/* Accessibility Skip Link (R-32) */
.skip-link {
  position: absolute;
  top: -40px;
  left: 20px;
  background: var(--accent-amber);
  color: #0b1118;
  padding: 8px 16px;
  font-weight: 700;
  border-radius: 4px;
  z-index: 9999;
  transition: top 0.2s;
}

.skip-link:focus {
  top: 10px;
}

/* Site Header & Navigation */
.site-header {
  position: sticky;
  top: 0;
  z-index: 1000;
  background-color: var(--bg-surface);
  border-bottom: 1px solid var(--border-color);
  backdrop-filter: blur(8px);
}

.header-inner {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0.85rem 1.5rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1.5rem;
}

.brand-link {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  text-decoration: none;
}

.brand-symbol {
  font-family: var(--font-mono);
  font-weight: 800;
  color: var(--accent-teal);
  background: var(--accent-teal-soft);
  padding: 2px 6px;
  border-radius: 4px;
  font-size: 0.9rem;
}

.brand-name {
  font-size: 1.15rem;
  font-weight: 800;
  color: var(--text-primary);
  letter-spacing: -0.02em;
}

.brand-tag {
  font-size: 0.75rem;
  font-family: var(--font-mono);
  color: var(--text-muted);
  border-left: 1px solid var(--border-color);
  padding-left: 0.5rem;
}

.desktop-nav {
  display: flex;
  align-items: center;
  gap: 1.25rem;
}

.nav-item {
  font-size: 0.9rem;
  font-weight: 500;
  color: var(--text-secondary);
  transition: color 0.15s ease;
  padding: 0.25rem 0;
}

.nav-item:hover {
  color: var(--accent-teal);
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
  border-radius: 6px;
  border: 1px solid var(--border-color);
  background: var(--bg-subtle);
  color: var(--text-primary);
  font-size: 0.82rem;
  font-weight: 600;
  transition: all 0.2s ease;
}

.action-btn:hover {
  border-color: var(--accent-teal);
  background: var(--accent-teal-soft);
}

.badge-count {
  background: var(--accent-amber);
  color: #0b1118;
  font-size: 0.7rem;
  font-weight: 800;
  padding: 1px 6px;
  border-radius: 10px;
}

.mobile-menu-btn {
  display: none;
  flex-direction: column;
  justify-content: space-around;
  width: 36px;
  height: 36px;
  padding: 6px;
  border-radius: 6px;
  border: 1px solid var(--border-color);
  background: var(--bg-subtle);
}

.hamburger-line {
  width: 100%;
  height: 2px;
  background-color: var(--text-primary);
  border-radius: 2px;
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
  color: var(--text-primary);
  padding: 0.5rem 0;
  border-bottom: 1px solid var(--border-subtle);
}

/* Content Wrapper & Section Foundations */
.content-wrapper {
  flex: 1;
  max-width: 1200px;
  margin: 0 auto;
  padding: 2.5rem 1.5rem 5rem 1.5rem;
  width: 100%;
}

.section {
  margin-bottom: 5.5rem;
}

.section-heading {
  margin-bottom: 2.25rem;
}

.section-tag {
  display: inline-block;
  font-family: var(--font-mono);
  font-size: 0.78rem;
  font-weight: 700;
  color: var(--accent-teal);
  text-transform: uppercase;
  letter-spacing: 0.08em;
  margin-bottom: 0.4rem;
}

.section-heading h2 {
  font-size: 2rem;
  font-weight: 800;
  color: var(--text-primary);
  letter-spacing: -0.025em;
  margin-bottom: 0.5rem;
}

.section-subtext {
  font-size: 1rem;
  color: var(--text-secondary);
  max-width: 720px;
  line-height: 1.6;
}

/* Buttons System */
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0.7rem 1.4rem;
  border-radius: 6px;
  font-size: 0.92rem;
  font-weight: 600;
  text-decoration: none;
  cursor: pointer;
  transition: all 0.2s ease;
  min-height: 44px; /* R-03: Minimum 44px tap target */
}

.btn-primary {
  background-color: var(--accent-amber);
  color: #0b1118;
  border: 1px solid var(--accent-amber);
}

.btn-primary:hover {
  background-color: #d97706;
  border-color: #d97706;
}

.btn-secondary {
  background-color: var(--accent-teal-soft);
  color: var(--accent-teal);
  border: 1px solid var(--accent-teal-border);
}

.btn-secondary:hover {
  background-color: var(--accent-teal);
  color: #0b1118;
}

.btn-outline {
  background-color: transparent;
  color: var(--text-primary);
  border: 1px solid var(--border-color);
}

.btn-outline:hover {
  border-color: var(--text-secondary);
  background-color: var(--bg-subtle);
}

.btn-sm {
  padding: 0.4rem 0.9rem;
  font-size: 0.82rem;
  min-height: 38px;
}

.btn-xs {
  padding: 0.25rem 0.6rem;
  font-size: 0.76rem;
  min-height: 32px;
}

.btn-block {
  width: 100%;
}

.btn-link {
  color: var(--accent-amber);
  font-weight: 700;
  font-size: 0.84rem;
  text-decoration: underline;
  text-underline-offset: 4px;
}

.btn-link:hover {
  color: #d97706;
}

.link-inline {
  color: var(--accent-teal);
  text-decoration: underline;
  text-underline-offset: 3px;
}

/* HERO SECTION */
.hero-layout {
  display: grid;
  grid-template-columns: 1.25fr 1fr;
  gap: 3rem;
  align-items: center;
  padding-top: 1rem;
}

.status-indicator {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  background: var(--bg-surface);
  border: 1px solid var(--border-color);
  padding: 0.35rem 0.85rem;
  border-radius: 20px;
  margin-bottom: 1.25rem;
}

.status-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background-color: var(--success);
  box-shadow: 0 0 6px var(--success);
}

.status-text {
  font-size: 0.8rem;
  font-weight: 600;
  color: var(--text-secondary);
}

.hero-title {
  font-size: 2.75rem;
  font-weight: 800;
  line-height: 1.15;
  letter-spacing: -0.03em;
  color: var(--text-primary);
  margin-bottom: 1.25rem;
}

.hero-lead {
  font-size: 1.05rem;
  line-height: 1.7;
  color: var(--text-secondary);
  margin-bottom: 2rem;
}

.hero-lead strong {
  color: var(--accent-teal);
}

.hero-cta-group {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}

.hero-highlight-card {
  background: var(--bg-surface);
  border: 1px solid var(--border-color);
  border-radius: 10px;
  box-shadow: var(--shadow-md);
  overflow: hidden;
}

.card-header-bar {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  background: var(--bg-subtle);
  padding: 0.65rem 1rem;
  border-bottom: 1px solid var(--border-color);
}

.terminal-dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
}

.terminal-dot.red { background: #ef4444; }
.terminal-dot.yellow { background: #f59e0b; }
.terminal-dot.green { background: #10b981; }

.card-bar-title {
  margin-left: 0.5rem;
  font-family: var(--font-mono);
  font-size: 0.75rem;
  color: var(--text-muted);
}

.card-body-spec {
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.spec-row {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  gap: 1rem;
  padding-bottom: 0.75rem;
  border-bottom: 1px solid var(--border-subtle);
  font-size: 0.88rem;
}

.spec-row:last-child {
  border-bottom: none;
  padding-bottom: 0;
}

.spec-label {
  color: var(--text-muted);
  font-weight: 500;
  flex-shrink: 0;
}

.spec-value {
  color: var(--text-primary);
  font-weight: 600;
  text-align: right;
  font-family: var(--font-mono);
  font-size: 0.84rem;
}

.highlight-teal {
  color: var(--accent-teal);
}

/* WORKFLOW AUTOMATION SECTION */
.pipeline-container {
  background: var(--bg-surface);
  border: 1px solid var(--border-color);
  border-radius: 12px;
  overflow: hidden;
}

.pipeline-steps {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  background: var(--bg-subtle);
  border-bottom: 1px solid var(--border-color);
}

.pipeline-node-btn {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 1.1rem 1rem;
  border-right: 1px solid var(--border-color);
  text-align: left;
  transition: all 0.2s ease;
}

.pipeline-node-btn:last-child {
  border-right: none;
}

.pipeline-node-btn:hover {
  background: var(--accent-teal-soft);
}

.pipeline-node-btn.is-active {
  background: var(--bg-surface);
  border-bottom: 3px solid var(--accent-amber);
}

.node-number {
  font-family: var(--font-mono);
  font-weight: 800;
  font-size: 1rem;
  color: var(--accent-teal);
  background: var(--bg-page);
  padding: 0.2rem 0.5rem;
  border-radius: 4px;
}

.node-meta {
  display: flex;
  flex-direction: column;
}

.node-role {
  font-size: 0.72rem;
  color: var(--text-muted);
  text-transform: uppercase;
}

.node-title {
  font-size: 0.85rem;
  color: var(--text-primary);
}

.pipeline-display-panel {
  padding: 2rem;
}

.panel-header {
  margin-bottom: 1.5rem;
}

.panel-badge {
  display: inline-block;
  font-family: var(--font-mono);
  font-size: 0.75rem;
  background: var(--accent-teal-soft);
  color: var(--accent-teal);
  padding: 0.2rem 0.6rem;
  border-radius: 4px;
  margin-bottom: 0.5rem;
}

.panel-title {
  font-size: 1.35rem;
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 0.35rem;
}

.panel-desc {
  font-size: 0.95rem;
  color: var(--text-secondary);
}

.panel-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.5rem;
  margin-bottom: 1.5rem;
}

.code-box {
  background: var(--bg-input);
  border: 1px solid var(--border-color);
  border-radius: 8px;
  padding: 1rem;
  overflow-x: auto;
}

.box-title {
  font-family: var(--font-mono);
  font-size: 0.75rem;
  color: var(--accent-amber);
  margin-bottom: 0.6rem;
  text-transform: uppercase;
}

.code-box pre code {
  font-family: var(--font-mono);
  font-size: 0.8rem;
  color: var(--text-secondary);
  line-height: 1.5;
  white-space: pre;
}

.panel-footer-tip {
  background: var(--accent-amber-soft);
  border-left: 3px solid var(--accent-amber);
  padding: 0.85rem 1rem;
  border-radius: 0 6px 6px 0;
  font-size: 0.88rem;
  color: var(--text-primary);
}

/* TIMELINE GRID (EXPERIENCE) */
.timeline-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
}

.timeline-card {
  background: var(--bg-surface);
  border: 1px solid var(--border-color);
  border-radius: 10px;
  padding: 1.75rem;
  display: flex;
  flex-direction: column;
}

.card-badge {
  display: inline-block;
  align-self: flex-start;
  font-size: 0.72rem;
  font-weight: 700;
  text-transform: uppercase;
  padding: 0.2rem 0.6rem;
  border-radius: 4px;
  margin-bottom: 0.75rem;
}

.card-badge.work { background: var(--accent-teal-soft); color: var(--accent-teal); }
.card-badge.study { background: var(--accent-amber-soft); color: var(--accent-amber); }
.card-badge.school { background: var(--bg-subtle); color: var(--text-muted); }

.role-title {
  font-size: 1.15rem;
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 0.25rem;
}

.org-meta {
  font-size: 0.82rem;
  color: var(--text-muted);
  font-family: var(--font-mono);
  margin-bottom: 1.25rem;
}

.task-list {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 0.65rem;
  font-size: 0.86rem;
  color: var(--text-secondary);
  line-height: 1.5;
}

.task-list li {
  position: relative;
  padding-left: 1.1rem;
}

.task-list li::before {
  content: "•";
  position: absolute;
  left: 0;
  color: var(--accent-teal);
  font-weight: bold;
}

/* SKILLS SECTION */
.filter-tab-bar {
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
  margin-bottom: 1.75rem;
}

.filter-pill {
  padding: 0.45rem 1rem;
  border-radius: 20px;
  border: 1px solid var(--border-color);
  background: var(--bg-surface);
  color: var(--text-secondary);
  font-size: 0.82rem;
  font-weight: 600;
  transition: all 0.2s;
}

.filter-pill:hover {
  border-color: var(--accent-teal);
}

.filter-pill.is-active {
  background: var(--accent-teal);
  color: #0b1118;
  border-color: var(--accent-teal);
}

.skills-card-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.25rem;
}

.skill-item-card {
  background: var(--bg-surface);
  border: 1px solid var(--border-color);
  border-radius: 8px;
  padding: 1.25rem;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  transition: border-color 0.2s;
}

.skill-item-card:hover {
  border-color: var(--accent-teal);
}

.skill-card-top {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  gap: 0.5rem;
}

.skill-name {
  font-weight: 700;
  font-size: 0.95rem;
  color: var(--text-primary);
}

.skill-category-tag {
  font-size: 0.7rem;
  font-family: var(--font-mono);
  color: var(--accent-teal);
}

.skill-usage {
  font-size: 0.82rem;
  color: var(--text-secondary);
  line-height: 1.45;
}

/* CERTIFICATES SECTION */
.cert-management-banner {
  background: var(--bg-surface);
  border: 1px solid var(--border-color);
  border-radius: 8px;
  padding: 1rem 1.25rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1.5rem;
  margin-bottom: 1.75rem;
}

.banner-text {
  font-size: 0.85rem;
  color: var(--text-secondary);
}

.banner-text strong {
  color: var(--accent-amber);
}

.cert-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
}

.cert-card {
  background: var(--bg-surface);
  border: 1px solid var(--border-color);
  border-radius: 10px;
  padding: 1.5rem;
  cursor: pointer;
  display: flex;
  flex-direction: column;
  transition: all 0.2s ease;
}

.cert-card:hover {
  border-color: var(--accent-teal);
  transform: translateY(-2px);
  box-shadow: var(--shadow-md);
}

.cert-header {
  display: flex;
  justify-content: space-between;
  font-size: 0.78rem;
  font-family: var(--font-mono);
  color: var(--text-muted);
  margin-bottom: 0.75rem;
}

.cert-title {
  font-size: 1.1rem;
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 0.5rem;
}

.cert-summary {
  font-size: 0.84rem;
  color: var(--text-secondary);
  line-height: 1.5;
  margin-bottom: 1.25rem;
  flex-grow: 1;
}

.cert-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 0.5rem;
  border-top: 1px solid var(--border-subtle);
  padding-top: 0.75rem;
}

.status-chip {
  font-size: 0.72rem;
  padding: 0.2rem 0.55rem;
  border-radius: 4px;
  font-weight: 600;
  font-family: var(--font-mono);
}

.status-pending {
  background: var(--accent-amber-soft);
  color: var(--accent-amber);
}

.status-digital {
  background: var(--accent-teal-soft);
  color: var(--accent-teal);
}

.status-verified {
  background: var(--success-soft);
  color: var(--success);
}

.action-hint {
  font-size: 0.75rem;
  color: var(--accent-teal);
  font-weight: 600;
}

/* REPOSITORIES SECTION */
.projects-toolbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1.5rem;
  margin-bottom: 2rem;
  flex-wrap: wrap;
}

.search-box {
  flex-shrink: 0;
  min-width: 260px;
}

.search-input {
  width: 100%;
  padding: 0.5rem 0.85rem;
  border-radius: 6px;
  border: 1px solid var(--border-color);
  background: var(--bg-surface);
  color: var(--text-primary);
  font-size: 0.85rem;
}

.repos-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1.5rem;
}

.repo-card {
  background: var(--bg-surface);
  border: 1px solid var(--border-color);
  border-radius: 10px;
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
  transition: border-color 0.2s;
}

.repo-card:hover {
  border-color: var(--accent-amber);
}

.repo-card-head {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.75rem;
}

.repo-lang-badge {
  font-family: var(--font-mono);
  font-size: 0.75rem;
  font-weight: 700;
  color: var(--accent-teal);
  background: var(--accent-teal-soft);
  padding: 0.15rem 0.5rem;
  border-radius: 4px;
}

.repo-visibility {
  font-size: 0.72rem;
  color: var(--text-muted);
}

.repo-title {
  font-size: 1.15rem;
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 0.4rem;
}

.repo-desc {
  font-size: 0.85rem;
  color: var(--text-secondary);
  line-height: 1.5;
  margin-bottom: 1.25rem;
  flex-grow: 1;
}

.repo-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-top: 1px solid var(--border-subtle);
  padding-top: 0.75rem;
}

.repo-raw-name {
  font-family: var(--font-mono);
  font-size: 0.74rem;
  color: var(--text-muted);
}

/* STATE CONTAINERS (R-27) */
.state-container {
  background: var(--bg-surface);
  border: 1px solid var(--border-color);
  border-radius: 8px;
  padding: 3rem 1.5rem;
  text-align: center;
  color: var(--text-secondary);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}

.spinner-loader {
  width: 32px;
  height: 32px;
  border: 3px solid var(--border-color);
  border-top-color: var(--accent-teal);
  border-radius: 50%;
  animation: spin 0.8s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

.error-msg {
  color: var(--danger);
  font-weight: 600;
}

/* CONTACT SECTION */
.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1.2fr;
  gap: 2rem;
}

.contact-card {
  background: var(--bg-surface);
  border: 1px solid var(--border-color);
  border-radius: 10px;
  padding: 2rem;
}

.contact-card h3 {
  font-size: 1.25rem;
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 0.5rem;
}

.contact-intro {
  font-size: 0.88rem;
  color: var(--text-secondary);
  margin-bottom: 1.5rem;
}

.channel-list {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
  margin-bottom: 2rem;
}

.channel-row {
  display: flex;
  flex-direction: column;
  gap: 0.35rem;
}

.channel-label {
  font-size: 0.78rem;
  font-family: var(--font-mono);
  color: var(--text-muted);
  text-transform: uppercase;
}

.channel-action-group {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  flex-wrap: wrap;
}

.channel-value {
  font-weight: 600;
  font-size: 0.95rem;
  color: var(--text-primary);
}

.guarantee-box {
  background: var(--bg-subtle);
  border-left: 3px solid var(--accent-teal);
  padding: 0.85rem 1rem;
  font-size: 0.82rem;
  color: var(--text-secondary);
  border-radius: 0 6px 6px 0;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 1.1rem;
}

.form-field {
  display: flex;
  flex-direction: column;
  gap: 0.35rem;
}

.form-field label {
  font-size: 0.82rem;
  font-weight: 600;
  color: var(--text-secondary);
}

.form-input {
  width: 100%;
  padding: 0.65rem 0.85rem;
  border-radius: 6px;
  border: 1px solid var(--border-color);
  background: var(--bg-input);
  color: var(--text-primary);
  font-size: 0.88rem;
  font-family: inherit;
}

.select-input {
  cursor: pointer;
}

.form-feedback-alert {
  padding: 0.75rem 1rem;
  border-radius: 6px;
  font-size: 0.85rem;
}

.form-feedback-alert.success {
  background: var(--success-soft);
  color: var(--success);
  border: 1px solid var(--success);
}

.form-feedback-alert.error {
  background: var(--danger-soft);
  color: var(--danger);
  border: 1px solid var(--danger);
}

/* FOOTER */
.site-footer {
  border-top: 1px solid var(--border-color);
  background: var(--bg-surface);
  padding: 1.5rem 0;
  margin-top: auto;
}

.footer-inner {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1.5rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 1rem;
}

.footer-left {
  font-size: 0.85rem;
  color: var(--text-muted);
}

.footer-name {
  font-weight: 700;
  color: var(--text-primary);
}

.footer-sep {
  margin: 0 0.4rem;
}

.footer-right {
  display: flex;
  gap: 1.25rem;
}

.footer-link {
  font-size: 0.85rem;
  color: var(--accent-teal);
  text-decoration: none;
}

.btn-link-clean {
  color: var(--accent-amber);
  font-size: 0.85rem;
  font-weight: 600;
  text-decoration: underline;
}

/* MODAL SYSTEM (R-26, R-32 Keyboard accessible) */
.modal-backdrop {
  position: fixed;
  inset: 0;
  background-color: rgba(0, 0, 0, 0.75);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 2000;
  padding: 1.5rem;
  backdrop-filter: blur(4px);
}

.modal-box {
  background: var(--bg-surface);
  border: 1px solid var(--border-color);
  border-radius: 12px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  box-shadow: var(--shadow-lg);
  display: flex;
  flex-direction: column;
}

.cert-modal-content {
  max-width: 580px;
}

.admin-modal-content {
  max-width: 820px;
}

.pin-modal-content {
  max-width: 440px;
}

.pin-hint-text {
  font-size: 0.88rem;
  color: var(--text-secondary);
  line-height: 1.5;
  margin-bottom: 1rem;
}

.admin-footer-actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}

.btn-lock-admin {
  color: var(--danger);
  border-color: var(--danger);
}

.btn-lock-admin:hover {
  background-color: var(--danger-soft);
}

.modal-header {
  padding: 1.5rem;
  border-bottom: 1px solid var(--border-color);
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 1rem;
}

.modal-badge {
  font-family: var(--font-mono);
  font-size: 0.72rem;
  color: var(--accent-teal);
  background: var(--accent-teal-soft);
  padding: 0.15rem 0.5rem;
  border-radius: 4px;
  display: inline-block;
  margin-bottom: 0.4rem;
}

.admin-badge {
  color: var(--accent-amber);
  background: var(--accent-amber-soft);
}

.modal-title {
  font-size: 1.35rem;
  font-weight: 800;
  color: var(--text-primary);
}

.modal-close-btn {
  font-size: 1.25rem;
  color: var(--text-muted);
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 6px;
  transition: all 0.2s;
}

.modal-close-btn:hover {
  background: var(--bg-subtle);
  color: var(--text-primary);
}

.modal-body {
  padding: 1.75rem;
}

.modal-footer {
  padding: 1rem 1.75rem;
  border-top: 1px solid var(--border-color);
  display: flex;
  justify-content: flex-end;
  background: var(--bg-subtle);
}

.cert-detail-grid {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  margin-bottom: 1.5rem;
}

.detail-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 0.88rem;
  padding-bottom: 0.5rem;
  border-bottom: 1px solid var(--border-subtle);
}

.detail-label {
  color: var(--text-muted);
}

.cert-doc-notice {
  background: var(--bg-subtle);
  border: 1px solid var(--border-color);
  border-radius: 8px;
  padding: 1rem;
  margin-bottom: 1.5rem;
  font-size: 0.88rem;
  line-height: 1.6;
}

.notice-title {
  font-size: 0.9rem;
  font-weight: 700;
  color: var(--accent-teal);
  margin-bottom: 0.4rem;
}

.notice-sub {
  margin-top: 0.5rem;
  font-size: 0.8rem;
  color: var(--text-muted);
}

.cert-placeholder-notice {
  border: 1px dashed var(--accent-amber);
  background: var(--accent-amber-soft);
  padding: 1rem;
  border-radius: 8px;
  text-align: center;
  font-size: 0.84rem;
  color: var(--text-primary);
}

.placeholder-tag {
  display: inline-block;
  font-family: var(--font-mono);
  font-weight: 700;
  margin-bottom: 0.3rem;
  color: var(--accent-amber);
}

/* ADMIN PANEL STYLES */
.admin-lead {
  font-size: 0.88rem;
  color: var(--text-secondary);
  margin-bottom: 1.75rem;
}

.admin-form-section {
  background: var(--bg-subtle);
  border: 1px solid var(--border-color);
  border-radius: 8px;
  padding: 1.25rem;
  margin-bottom: 2rem;
}

.admin-subheading {
  font-size: 1rem;
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 1rem;
}

.admin-form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.form-row-2 {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
}

.form-row-3 {
  display: grid;
  grid-template-columns: 1fr 1.5fr 1.5fr;
  gap: 1rem;
}

.admin-form-actions {
  display: flex;
  justify-content: flex-end;
}

.list-heading-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.85rem;
}

.admin-table-container {
  overflow-x: auto;
  border: 1px solid var(--border-color);
  border-radius: 8px;
}

.admin-table {
  width: 100%;
  border-collapse: collapse;
  text-align: left;
  font-size: 0.84rem;
}

.admin-table th, .admin-table td {
  padding: 0.75rem 1rem;
  border-bottom: 1px solid var(--border-subtle);
}

.admin-table th {
  background: var(--bg-subtle);
  color: var(--text-muted);
  font-weight: 600;
}

.btn-delete {
  color: var(--danger);
  font-weight: 700;
  font-size: 0.8rem;
  padding: 0.2rem 0.5rem;
  border-radius: 4px;
  transition: background 0.15s;
}

.btn-delete:hover {
  background: var(--danger-soft);
}

/* RESPONSIVE BREAKPOINTS (R-03: Flawless mobile experience) */
@media (max-width: 1024px) {
  .hero-layout {
    grid-template-columns: 1fr;
    gap: 2.5rem;
  }

  .timeline-grid {
    grid-template-columns: 1fr;
  }

  .skills-card-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .cert-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .pipeline-steps {
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

  .hero-title {
    font-size: 2.1rem;
  }

  .section {
    margin-bottom: 4rem;
  }

  .pipeline-steps {
    grid-template-columns: 1fr;
  }

  .pipeline-node-btn {
    border-right: none;
    border-bottom: 1px solid var(--border-color);
  }

  .panel-grid {
    grid-template-columns: 1fr;
  }

  .skills-card-grid {
    grid-template-columns: 1fr;
  }

  .cert-grid {
    grid-template-columns: 1fr;
  }

  .repos-grid {
    grid-template-columns: 1fr;
  }

  .contact-grid {
    grid-template-columns: 1fr;
  }

  .form-row-2, .form-row-3 {
    grid-template-columns: 1fr;
  }

  .cert-management-banner {
    flex-direction: column;
    align-items: flex-start;
  }
}
</style>